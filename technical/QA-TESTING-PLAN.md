# 🧪 QA & Testing Plan

## Testing Strategy

```
Test Pyramid:
├── Unit Tests (60%)
│   ├── Service functions
│   ├── Store logic
│   └── Utility functions
│
├── Integration Tests (25%)
│   ├── API endpoints
│   ├── Database operations
│   └── Third-party integrations (Stripe, S3)
│
└── E2E Tests (15%)
    ├── Critical user flows
    ├── Mobile app flows
    └── Edge cases
```

---

## Unit Testing (Jest)

### Test Structure

```typescript
// __tests__/services/photo.test.ts

import { photoService } from '../../services/photo';
import { jest } from '@jest/globals';

describe('photoService', () => {
  
  describe('extractEXIF', () => {
    it('should extract EXIF date from image', async () => {
      const mockUri = 'file://test-photo.jpg';
      const exif = await photoService.extractEXIF(mockUri);
      
      expect(exif).toHaveProperty('dateTaken');
      expect(exif.dateTaken).toBeInstanceOf(Date);
    });

    it('should handle images without EXIF', async () => {
      const mockUri = 'file://no-exif.jpg';
      const exif = await photoService.extractEXIF(mockUri);
      
      expect(exif.dateTaken).toBeDefined(); // fallback to upload time
    });
  });

  describe('optimizeImage', () => {
    it('should compress image below 500KB', async () => {
      const result = await photoService.optimizeImage(largeImageUri);
      const size = await getFileSize(result.uri);
      
      expect(size).toBeLessThan(500 * 1024);
    });

    it('should maintain aspect ratio', async () => {
      const result = await photoService.optimizeImage(testImageUri);
      
      expect(result.width / result.height).toBeCloseTo(
        originalWidth / originalHeight,
        1
      );
    });
  });
});
```

### Service Tests

```typescript
// __tests__/services/auth.test.ts

describe('authService', () => {
  
  beforeEach(() => {
    jest.clearAllMocks();
  });

  describe('signup', () => {
    it('should create user and store JWT', async () => {
      const result = await authService.signup('test@vera.app', 'Password123!');
      
      expect(result.user).toBeDefined();
      expect(result.token).toBeDefined();
      
      // Verify token stored securely
      const stored = await SecureStore.getItemAsync('token');
      expect(stored).toBe(result.token);
    });

    it('should reject weak password', async () => {
      await expect(
        authService.signup('test@vera.app', 'weak')
      ).rejects.toThrow('Password must be at least 8 characters');
    });

    it('should reject existing email', async () => {
      await authService.signup('existing@vera.app', 'Password123!');
      
      await expect(
        authService.signup('existing@vera.app', 'Password456!')
      ).rejects.toThrow('Email already registered');
    });
  });
});
```

### Store Tests (Zustand)

```typescript
// __tests__/store/photoStore.test.ts

import { create } from 'zustand';
import { photoStore } from '../../store/photoStore';

describe('photoStore', () => {
  
  it('should add photo to store', () => {
    const { addPhoto, photos } = photoStore.getState();
    const mockPhoto = { id: '1', uri: 'file://photo.jpg' };
    
    addPhoto(mockPhoto);
    
    expect(photoStore.getState().photos).toContain(mockPhoto);
  });

  it('should remove photo from store', () => {
    const { addPhoto, removePhoto } = photoStore.getState();
    const mockPhoto = { id: '1', uri: 'file://photo.jpg' };
    
    addPhoto(mockPhoto);
    removePhoto('1');
    
    expect(photoStore.getState().photos).not.toContain(mockPhoto);
  });
});
```

---

## Integration Testing

### API Endpoint Tests

```typescript
// __tests__/api/photos.test.ts

import axios from 'axios';
import { API_BASE_URL } from '../../services/api';

describe('Photo API', () => {
  let token: string;

  beforeAll(async () => {
    // Get auth token
    const loginRes = await axios.post(`${API_BASE_URL}/auth/login`, {
      email: 'test@vera.app',
      password: 'TestPassword123!'
    });
    token = loginRes.data.token;
  });

  describe('POST /api/photos/upload', () => {
    it('should upload single photo with metadata', async () => {
      const formData = new FormData();
      formData.append('photo', photoFile);
      formData.append('childId', 'child-123');
      formData.append('metadata', JSON.stringify({
        exifDate: '2026-01-17T10:00:00Z',
        story: 'First upload'
      }));

      const response = await axios.post(
        `${API_BASE_URL}/api/photos/upload`,
        formData,
        { headers: { Authorization: `Bearer ${token}` } }
      );

      expect(response.status).toBe(200);
      expect(response.data.photoId).toBeDefined();
    });

    it('should reject oversized file', async () => {
      const largeFile = new File(
        [new ArrayBuffer(60 * 1024 * 1024)], // 60MB
        'large.jpg'
      );
      
      const formData = new FormData();
      formData.append('photo', largeFile);

      await expect(
        axios.post(`${API_BASE_URL}/api/photos/upload`, formData)
      ).rejects.toThrow('File too large (max 50MB)');
    });

    it('should extract EXIF and calculate age', async () => {
      const response = await axios.post(
        `${API_BASE_URL}/api/photos/upload`,
        formData,
        { headers: { Authorization: `Bearer ${token}` } }
      );

      expect(response.data.exifDate).toBeDefined();
      expect(response.data.calculatedAgeMonths).toBeDefined();
      expect(response.data.calculatedAgeMonths).toBeGreaterThanOrEqual(0);
    });
  });

  describe('GET /api/photos/timeline', () => {
    it('should fetch photos grouped by age', async () => {
      const response = await axios.get(
        `${API_BASE_URL}/api/photos/timeline?childId=child-123`,
        { headers: { Authorization: `Bearer ${token}` } }
      );

      expect(response.status).toBe(200);
      expect(Array.isArray(response.data.timeline)).toBe(true);
      expect(response.data.timeline[0]).toHaveProperty('ageMonths');
      expect(response.data.timeline[0]).toHaveProperty('photos');
    });

    it('should filter by age range', async () => {
      const response = await axios.get(
        `${API_BASE_URL}/api/photos/timeline?childId=child-123&ageFrom=6&ageTo=12`,
        { headers: { Authorization: `Bearer ${token}` } }
      );

      response.data.timeline.forEach(group => {
        expect(group.ageMonths).toBeGreaterThanOrEqual(6);
        expect(group.ageMonths).toBeLessThanOrEqual(12);
      });
    });
  });
});
```

### Database Tests

```typescript
// __tests__/db/photos.test.ts

import { db } from '../../services/database';

describe('Database - Photos', () => {
  
  beforeEach(async () => {
    // Clean up test data
    await db.query('DELETE FROM photos WHERE user_id = $1', ['test-user-id']);
  });

  it('should insert photo and calculate age', async () => {
    const childId = 'child-123';
    const childDOB = new Date('2023-01-17');
    const uploadDate = new Date('2026-01-17');
    
    const result = await db.query(
      `INSERT INTO photos (child_id, exif_date_taken, user_id)
       VALUES ($1, $2, $3)
       RETURNING *, 
         EXTRACT(EPOCH FROM ($4 - $5)) / 2592000 as calculated_age_months`,
      [childId, uploadDate, 'test-user-id', uploadDate, childDOB]
    );

    expect(result.rows[0].calculated_age_months).toBe(36); // 3 years = 36 months
  });

  it('should prevent unauthorized access', async () => {
    // Insert photo as user A
    await db.query(
      'INSERT INTO photos (id, child_id, user_id) VALUES ($1, $2, $3)',
      ['photo-123', 'child-A', 'user-A']
    );

    // User B tries to access
    const result = await db.query(
      'SELECT * FROM photos WHERE id = $1 AND user_id = $2',
      ['photo-123', 'user-B']
    );

    expect(result.rows).toHaveLength(0);
  });
});
```

---

## E2E Testing (Detox)

### Mobile App E2E Tests

```typescript
// e2e/uploadFlow.e2e.ts

describe('Photo Upload Flow', () => {
  beforeAll(async () => {
    await device.launchApp({
      newInstance: true,
      permissions: { photos: 'always' }
    });
  });

  it('should complete full upload flow with story', async () => {
    // Login
    await element(by.id('emailInput')).typeText('test@vera.app');
    await element(by.id('passwordInput')).typeText('TestPassword123!');
    await element(by.id('loginButton')).tap();

    // Wait for dashboard
    await waitFor(element(by.id('dashboard')))
      .toBeVisible()
      .withTimeout(5000);

    // Tap upload button
    await element(by.id('uploadButton')).tap();

    // Select photo from gallery
    await element(by.id('selectFromGallery')).tap();
    await waitFor(element(by.text('Select Photo')))
      .toBeVisible()
      .withTimeout(3000);
    await element(by.text('Test Photo 1')).multiTap();

    // Add story
    await element(by.id('storyInput')).typeText('First upload! 🎉');
    
    // Submit
    await element(by.id('submitButton')).tap();

    // Verify success
    await waitFor(element(by.text('Photo uploaded successfully')))
      .toBeVisible()
      .withTimeout(5000);

    // Verify photo appears in timeline
    await waitFor(element(by.id('photoCard-1')))
      .toBeVisible()
      .withTimeout(3000);
  });

  it('should handle offline photo upload', async () => {
    // Simulate offline
    await device.setAirplaneMode(true);

    // Upload photo (should save locally)
    await element(by.id('uploadButton')).tap();
    await element(by.id('selectFromGallery')).tap();
    await element(by.text('Test Photo 2')).multiTap();
    await element(by.id('submitButton')).tap();

    // Should show "Saved offline"
    await waitFor(element(by.text('Saved offline')))
      .toBeVisible()
      .withTimeout(3000);

    // Go back online
    await device.setAirplaneMode(false);

    // Should auto-sync
    await waitFor(element(by.text('Syncing photos...')))
      .toBeVisible()
      .withTimeout(5000);
  });
});
```

---

## Performance Testing

### Load Testing

```bash
# Using Artillery.io

# artillery.yml
config:
  target: https://api.vera.app
  phases:
    - duration: 60
      arrivalRate: 10
      name: "Warm up"
    - duration: 300
      arrivalRate: 50
      name: "Ramp up"
    - duration: 600
      arrivalRate: 100
      name: "Sustained load"

scenarios:
  - name: "Photo Upload"
    flow:
      - post:
          url: "/api/photos/upload"
          formData:
            photo: "@photo.jpg"

# Run: artillery run artillery.yml
```

### Performance Targets

```
API Response Times:
├── GET /api/photos/timeline: <500ms (p95)
├── POST /api/photos/upload: <2s (p95)
├── GET /api/photos/{id}: <300ms (p95)
└── POST /api/auth/login: <1s (p95)

Database:
├── Query time: <100ms (p95)
├── Index hits: >95%
└── Connection pool: <10ms wait

Mobile App:
├── Startup: <3s
├── Timeline scroll: 60fps
├── Image load: <1s (thumbnail)
└── Memory: <150MB

Web (Landing Page):
├── First paint: <1s
├── Time to interactive: <2s
├── Lighthouse score: >95
└── Bundle size: <100KB
```

---

## Test Coverage Targets

```
Coverage by Module:

Auth:           >95%
├── signup
├── login
└── logout

Photo Service:  >90%
├── extractEXIF
├── optimizeImage
└── uploadBatch

Photo Store:    >85%
├── Add/remove photos
├── Filter operations
└── Sync logic

API Endpoints:  >80%
├── Happy paths
├── Error cases
└── Edge cases

Database:       >75%
├── CRUD operations
├── Transactions
└── Constraints

Total:          >85% code coverage (acceptance)
                >80% branch coverage
```

---

## Testing Checklist (Before Q2 Launch)

- [ ] Unit tests: 85%+ coverage
- [ ] Integration tests: All critical APIs tested
- [ ] E2E tests: Main user flows tested (iOS + Android)
- [ ] Performance tests: All targets met
- [ ] Security tests: No OWASP Top 10 issues
- [ ] Accessibility tests: WCAG AA compliant
- [ ] Manual testing: Full product review
- [ ] Beta feedback: Incorporated + retested
- [ ] Regression tests: No new bugs introduced
- [ ] Load testing: Handles 1000 concurrent users

---

**Status**: ✅ Testing framework prepared
