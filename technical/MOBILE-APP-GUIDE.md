# 📱 Mobile App Development Guide (React Native Expo)

## Architecture Overview

```
Vera Mobile (iOS + Android via Expo)
│
├── Frontend (React Native Expo)
│   ├── Navigation (React Navigation)
│   ├── UI Components (React Native Paper + custom)
│   ├── State Management (Zustand)
│   └── API Client (Axios + React Query)
│
├── Backend APIs (Node.js - shared)
│   └── All endpoints mobile & web consume
│
└── Local Storage
    ├── SQLite (offline-first sync)
    └── AsyncStorage (user prefs)
```

---

## Development Environment Setup

### Prerequisites

```bash
# Node.js 18+
node --version

# Expo CLI
npm install -g expo-cli

# XCode (Mac) or Android Studio (Windows/Linux)
# For iOS: XCode 14+
# For Android: Android Studio + SDK 32+
```

### Project Initialize

```bash
# Create Expo project
expo init vera-mobile
cd vera-mobile

# Choose: blank (TypeScript)

# Install core dependencies
npm install \
  react-navigation react-native-screens react-native-safe-area-context \
  axios react-query zustand \
  react-native-paper \
  react-native-image-picker react-native-camera \
  react-native-fs react-native-sqlite-storage \
  @react-native-async-storage/async-storage

# Install dev
npm install --save-dev typescript @types/react-native
```

### File Structure

```
vera-mobile/
├── src/
│   ├── screens/
│   │   ├── auth/
│   │   │   ├── LoginScreen.tsx
│   │   │   ├── SignupScreen.tsx
│   │   │   └── ChildCreateScreen.tsx
│   │   ├── main/
│   │   │   ├── DashboardScreen.tsx (timeline)
│   │   │   ├── UploadScreen.tsx
│   │   │   ├── PhotoDetailScreen.tsx
│   │   │   └── SearchScreen.tsx
│   │   ├── family/
│   │   │   ├── FamilySharingScreen.tsx
│   │   │   └── FamilyListScreen.tsx
│   │   └── settings/
│   │       ├── SettingsScreen.tsx
│   │       └── SubscriptionScreen.tsx
│   │
│   ├── components/
│   │   ├── PhotoCard.tsx
│   │   ├── TimelineGroup.tsx
│   │   ├── StoryEditor.tsx
│   │   ├── MilestoneAlert.tsx
│   │   ├── MemoryCard.tsx
│   │   └── CustomTabs.tsx
│   │
│   ├── navigation/
│   │   ├── RootNavigator.tsx
│   │   ├── AuthNavigator.tsx
│   │   └── AppNavigator.tsx
│   │
│   ├── services/
│   │   ├── api.ts (axios instance + interceptors)
│   │   ├── auth.ts (Firebase + JWT)
│   │   ├── photo.ts (upload, EXIF, S3)
│   │   ├── database.ts (local SQLite)
│   │   └── sync.ts (offline-first logic)
│   │
│   ├── store/
│   │   ├── authStore.ts (user, token)
│   │   ├── photoStore.ts (local cache)
│   │   ├── uiStore.ts (loading, errors)
│   │   └── settingsStore.ts (user prefs)
│   │
│   ├── hooks/
│   │   ├── useAuth.ts
│   │   ├── usePhotos.ts
│   │   ├── useUpload.ts
│   │   └── useSync.ts
│   │
│   ├── types/
│   │   └── index.ts (User, Photo, Child, etc.)
│   │
│   └── App.tsx (entry point)
│
├── app.json (Expo config)
├── package.json
└── tsconfig.json
```

---

## Core Features Implementation

### 1. Authentication

```typescript
// services/auth.ts
import * as SecureStore from 'expo-secure-store';
import axios from 'axios';

export const authService = {
  async signup(email: string, password: string) {
    // Firebase Auth
    const { user, idToken } = await firebaseAuth.createUserWithEmailAndPassword(email, password);
    
    // Store JWT
    await SecureStore.setItemAsync('token', idToken);
    
    // Create user profile on backend
    await api.post('/api/users', { uid: user.uid, email });
    
    return { user, token: idToken };
  },

  async login(email: string, password: string) {
    const { idToken, user } = await firebaseAuth.signInWithEmailAndPassword(email, password);
    await SecureStore.setItemAsync('token', idToken);
    return { user, token: idToken };
  },

  async logout() {
    await firebaseAuth.signOut();
    await SecureStore.deleteItemAsync('token');
  }
};
```

### 2. Photo Upload (Mobile-optimized)

```typescript
// services/photo.ts
import * as ImagePicker from 'expo-image-picker';
import { manipulateAsync, SaveFormat } from 'expo-image-manipulator';
import EXIF from 'react-native-exif';

export const photoService = {
  async pickImages() {
    const result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ImagePicker.MediaTypeOptions.Photos,
      allowsMultipleSelection: true,
      quality: 0.8,
      base64: false,
    });

    return result.assets.map(asset => ({
      uri: asset.uri,
      width: asset.width,
      height: asset.height,
    }));
  },

  async optimizeImage(uri: string) {
    // Compress for mobile
    const result = await manipulateAsync(uri, [
      { resize: { width: 1920, height: 2880 } },
    ], { compress: 0.7, format: SaveFormat.JPEG });

    return result.uri;
  },

  async extractEXIF(uri: string) {
    const exifData = await EXIF.getExif(uri);
    return {
      dateTaken: exifData.DateTime || new Date(),
      cameraModel: exifData.Model,
      gpsLat: exifData.GPSLatitude,
      gpsLng: exifData.GPSLongitude,
    };
  },

  async uploadBatch(photos: Photo[]) {
    const formData = new FormData();
    
    photos.forEach((photo, index) => {
      formData.append(`photos[${index}]`, {
        uri: photo.uri,
        type: 'image/jpeg',
        name: `photo_${Date.now()}.jpg`,
      });
      formData.append(`metadata[${index}]`, JSON.stringify(photo.exif));
    });

    return await api.post('/api/photos/batch-upload', formData, {
      headers: { 'Content-Type': 'multipart/form-data' },
    });
  }
};
```

### 3. Offline-First Sync

```typescript
// services/sync.ts
import SQLite from 'react-native-sqlite-storage';
import { useEffect, useState } from 'react';

const db = SQLite.openDatabase({ name: 'vera.db' });

export const syncService = {
  async initDB() {
    // Local SQLite tables
    db.executeSql(`
      CREATE TABLE IF NOT EXISTS photos (
        id TEXT PRIMARY KEY,
        childId TEXT,
        uri TEXT,
        exifDate TEXT,
        story TEXT,
        tags TEXT,
        isFavorite INTEGER,
        syncStatus TEXT, -- 'pending', 'synced', 'error'
        createdAt TEXT
      )
    `);
  },

  async addPhotoLocal(photo: Photo) {
    db.executeSql(
      `INSERT INTO photos VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)`,
      [photo.id, photo.childId, photo.uri, photo.exifDate, photo.story,
       JSON.stringify(photo.tags), photo.isFavorite ? 1 : 0, 'pending', new Date().toISOString()]
    );
  },

  async syncPending() {
    // When online, upload pending photos
    const [result] = await db.executeSql(
      `SELECT * FROM photos WHERE syncStatus = 'pending'`
    );

    const photos = result.rows.raw();
    
    for (const photo of photos) {
      try {
        await photoService.uploadBatch([photo]);
        await db.executeSql(
          `UPDATE photos SET syncStatus = 'synced' WHERE id = ?`,
          [photo.id]
        );
      } catch (error) {
        await db.executeSql(
          `UPDATE photos SET syncStatus = 'error' WHERE id = ?`,
          [photo.id]
        );
      }
    }
  }
};

// Hook for background sync
export function useSyncOffline() {
  useEffect(() => {
    const subscription = NetInfo.addEventListener(state => {
      if (state.isConnected) {
        syncService.syncPending();
      }
    });

    return () => subscription?.unsubscribe();
  }, []);
}
```

### 4. Timeline Screen (Performance-optimized)

```typescript
// screens/main/DashboardScreen.tsx
import { FlatList, View, Image } from 'react-native';
import { useFocusEffect } from '@react-navigation/native';

export function DashboardScreen() {
  const [timeline, setTimeline] = useState<TimelineGroup[]>([]);
  const [loading, setLoading] = useState(false);

  useFocusEffect(
    useCallback(() => {
      loadTimeline();
    }, [])
  );

  const loadTimeline = async () => {
    setLoading(true);
    // Fetch 30 days of photos, paginated
    const { data } = await api.get('/api/photos/timeline?limit=50&offset=0');
    
    // Group by age
    const grouped = groupByAge(data.photos);
    setTimeline(grouped);
    setLoading(false);
  };

  const renderTimelineGroup = ({ item }: { item: TimelineGroup }) => (
    <View style={{ marginBottom: 24 }}>
      <Text style={styles.ageHeader}>{item.age} yaşında</Text>
      
      <ScrollView horizontal showsHorizontalScrollIndicator={false}>
        {item.photos.map(photo => (
          <TouchableOpacity key={photo.id} onPress={() => navigate('PhotoDetail', { photoId: photo.id })}>
            <Image
              source={{ uri: photo.thumbnailUrl }}
              style={{ width: 120, height: 120, marginRight: 8, borderRadius: 8 }}
            />
          </TouchableOpacity>
        ))}
      </ScrollView>
    </View>
  );

  return (
    <FlatList
      data={timeline}
      renderItem={renderTimelineGroup}
      keyExtractor={(item) => item.ageMonths.toString()}
      onEndReached={loadMore}
      ListEmptyComponent={<EmptyTimeline />}
      removeClippedSubviews={true}
      maxToRenderPerBatch={10}
      updateCellsBatchingPeriod={50}
    />
  );
}
```

### 5. Push Notifications (Milestones + Memory Cards)

```typescript
// services/notifications.ts
import * as Notifications from 'expo-notifications';

Notifications.setNotificationHandler({
  handleNotification: async () => ({
    shouldShowAlert: true,
    shouldPlaySound: true,
    shouldSetBadge: true,
  }),
});

export const notificationService = {
  async scheduleMilestoneNotification(child: Child, milestone: string) {
    const message = {
      "İlk adım": `Bugün ${child.name} ilk adımını attı! 🎉`,
      "İlk diş": `Bugün ${child.name} ilk dişini kaybetti 🦷`,
      "Doğum günü": `Bugün ${child.name} ${child.ageYears} yaşında! 🎂`,
    };

    await Notifications.scheduleNotificationAsync({
      content: {
        title: "Özel Anı 💝",
        body: message[milestone],
        data: { type: 'milestone', childId: child.id },
      },
      trigger: { seconds: 60 },
    });
  },

  async scheduleMemoryCard(childId: string, photosFromYearAgo: number) {
    const year = Math.floor(photosFromYearAgo / 365);
    
    await Notifications.scheduleNotificationAsync({
      content: {
        title: `${year} yıl öncesine bugün`,
        body: `Bu fotoğrafı açtır mı?`,
        data: { type: 'memory', childId, photosFromYearAgo },
      },
      trigger: {
        hour: 9,
        minute: 0,
        repeats: false,
      },
    });
  }
};

// Handle notification tap
Notifications.addNotificationResponseReceivedListener(response => {
  const { type, childId } = response.notification.request.content.data;
  
  if (type === 'memory') {
    // Navigate to that photo from year ago
    navigation.navigate('PhotoDetail', { childId, fromYearAgo: true });
  }
});
```

---

## Testing Strategy (Mobile)

### Unit Tests

```typescript
// __tests__/photoService.test.ts
import { photoService } from '../services/photo';

describe('photoService', () => {
  it('should extract EXIF date from photo', async () => {
    const uri = 'file://photo.jpg';
    const exif = await photoService.extractEXIF(uri);
    
    expect(exif.dateTaken).toBeDefined();
  });

  it('should compress image to <500KB', async () => {
    const compressed = await photoService.optimizeImage(largeImageUri);
    const fileSize = await getFileSize(compressed);
    
    expect(fileSize).toBeLessThan(500 * 1024);
  });
});
```

### E2E Tests (Detox)

```typescript
// e2e/firstUpload.e2e.ts
describe('Photo Upload Flow', () => {
  beforeAll(async () => {
    await device.launchApp();
  });

  it('should upload photo with story', async () => {
    await element(by.id('uploadButton')).multiTap();
    await element(by.id('cameraRoll')).tap();
    await element(by.text('Select Photo')).tap();
    
    await element(by.id('storyInput')).typeText('İlk adımı attı! 🎉');
    await element(by.id('submitButton')).tap();
    
    await waitFor(element(by.text('Yükleme başarılı')))
      .toBeVisible()
      .withTimeout(5000);
  });
});
```

---

## Performance Optimization

### Mobile-Specific

```typescript
// Image lazy loading
<Image
  source={{ uri: photo.thumbnailUrl }}
  defaultSource={require('../assets/placeholder.png')}
  progressiveRenderingEnabled={true}
/>

// Memoize components
const PhotoCard = React.memo(({ photo, onPress }) => (
  <TouchableOpacity onPress={onPress}>
    <Image source={{ uri: photo.uri }} style={styles.image} />
  </TouchableOpacity>
));

// FlatList optimization
<FlatList
  data={photos}
  renderItem={renderPhoto}
  keyExtractor={item => item.id}
  initialNumToRender={20}
  maxToRenderPerBatch={10}
  updateCellsBatchingPeriod={50}
  removeClippedSubviews={true}
  getItemLayout={(data, index) => ({
    length: PHOTO_ITEM_HEIGHT,
    offset: PHOTO_ITEM_HEIGHT * index,
    index,
  })}
/>

// Bundle size optimization
// app.json
{
  "expo": {
    "plugins": [
      ["expo-image-picker", { "photosPermission": "..." }]
    ],
    "android": { "package": "com.vera.app" },
    "ios": { "bundleIdentifier": "com.vera.app" }
  }
}
```

---

## App Store Submission

### iOS (TestFlight → App Store)

```
1. XCode build
   └── expo build:ios

2. Upload to TestFlight
   └── Use Transporter app

3. TestFlight testing (beta users)
   └── 2-3 days before App Store

4. App Store submission
   └── Screenshots, description, keywords
   └── Privacy policy link
   └── Category: Lifestyle / Photo
```

### Android (Google Play)

```
1. Android build
   └── expo build:android --type apk

2. Google Play Console
   └── Upload APK
   └── Screenshots, description
   └── Content rating questionnaire

3. Review (24-48 hours)
   └── Usually auto-approved
```

---

## Deployment Checklist

- [ ] All screens working on iOS + Android
- [ ] Offline mode tested (no internet)
- [ ] Photo upload 100+ photos at once
- [ ] Memory card notifications working
- [ ] Milestone celebrations triggered correctly
- [ ] Performance: App opens <2 seconds
- [ ] Battery: <5% drain in 1 hour normal use
- [ ] No console errors or warnings
- [ ] Privacy policy & KVKK compliant
- [ ] Screenshots for app stores
- [ ] Launch sequence documented

---

**Status**: 🚀 Ready for development
