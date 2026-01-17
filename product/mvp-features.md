# 🛠️ MVP Özellikler

## Özellik Önceliklendirme Matrisi

### Öncelik 1: Core (MVP Zorunlu)

| Özellik | Açıklama | Effort | Impact |
|---------|----------|--------|--------|
| Fotoğraf Yükleme | Tek/toplu yükleme, galeri erişimi | M | 10 |
| Otomatik Tarih-Yaş | EXIF tarih + çocuk doğum tarihi | S | 9 |
| Çocuk Profili | Ad, doğum tarihi, fotoğraf | S | 9 |
| Timeline Görünümü | Yaşa göre kronolojik liste | M | 9 |
| Hikaye/Not Ekleme | Her fotoğrafa metin alanı | S | 8 |
| Temel Arama | Tarih, yaş filtresi | S | 7 |
| **🎉 Milestone Celebrations** | **İlk adım, ilk diş, doğum günü otomatik vurgulama** | **S** | **10** |
| **💝 Memory Cards** | **"2 yıl öncesine bugün" emoşyonal anımsatıcı** | **S** | **9** |

### Öncelik 2: Essential (V1.0)

| Özellik | Açıklama | Effort | Impact |
|---------|----------|--------|--------|
| Etiketleme | İlkler, aile, okul vb. | M | 8 |
| Aile Paylaşımı | Davet linki, view-only | M | 8 |
| Albüm Preview | Yıl sonu önizleme | L | 9 |
| Favoriler | Yıldızlı anılar | S | 6 |
| Push Notifications | Upload hatırlatma | S | 5 |
| **📸 Açılmaz Anılar (Surprise)** | **Random fotoğraf, "Bugün bu fotoğraf çekildi" push (duygusal)** | **S** | **8** |
| **🎂 Yaş Günü Sayacı** | **"40 gün sonra 3. yaş günü, 50 fotoğraf bekleniyor"** | **S** | **7** |

### Öncelik 3: Enhanced (V1.5)

| Özellik | Açıklama | Effort | Impact |
|---------|----------|--------|--------|
| Video Desteği | 30sn video upload | M | 7 |
| Konum Etiketleme | Harita entegrasyonu | M | 6 |
| Kişi Etiketleme | Yüz tanıma (basit) | L | 6 |
| Gelişmiş Arama | Full-text, etiket kombine | M | 6 |
| Export | JSON/ZIP dışa aktarma | M | 5 |

### Öncelik 4: AI Features (V2.0)

| Özellik | Açıklama | Effort | Impact |
|---------|----------|--------|--------|
| AI Anı Seçimi | Yıllık en iyi fotoğraflar | L | 8 |
| Otomatik Hikaye | AI ile metin üretimi | L | 7 |
| Yüz Gruplandırma | Otomatik person tagging | L | 6 |
| Akıllı Albüm Layout | AI ile sayfa düzeni | L | 7 |

---

## MVP Scope (4 Hafta)

### Hafta 1-2: Core Infrastructure

```
Backend:
├── User authentication (Firebase/Supabase)
├── Child profile CRUD
├── Media upload (S3/Cloudinary)
├── Date/age calculation logic
└── Basic API endpoints

Frontend:
├── Onboarding flow
├── Child creation screen
├── Photo upload interface
└── Basic timeline view
```

### Hafta 3: Essential Features

```
├── Story/note editing
├── Tag system
├── Search/filter
├── Family invite (view-only link)
└── Settings & profile
```

### Hafta 4: Polish & Album Preview

```
├── Album preview mockup
├── UI/UX polish
├── Performance optimization
├── Beta testing prep
└── App Store submission prep
```

---

## Ekran Listesi (MVP)

### 1. Onboarding

| Ekran | İçerik |
|-------|--------|
| Splash | Logo, tagline |
| Welcome | 3 slide value prop |
| Sign Up | E-posta/Google/Apple |
| Child Create | İsim, doğum tarihi, fotoğraf |
| Subscription | Paket seçimi |

### 2. Ana Akış

| Ekran | İçerik |
|-------|--------|
| Home | Timeline, quick upload |
| Upload | Gallery picker, batch select |
| Media Detail | Fotoğraf, hikaye, tarih, tags |
| Edit Story | Text editor |

### 3. Organizasyon

| Ekran | İçerik |
|-------|--------|
| Timeline | Yaşa göre gruplandırılmış |
| Search | Filtreler, sonuçlar |
| Favorites | Yıldızlı liste |
| Tags | Tag listesi ve içerikleri |

### 4. Albüm

| Ekran | İçerik |
|-------|--------|
| Album Preview | Yıllık özet, sayfa preview |
| Album Confirmation | Düzen onayı |

### 5. Ayarlar

| Ekran | İçerik |
|-------|--------|
| Profile | Kullanıcı bilgileri |
| Child Settings | Profil düzenleme |
| Family Sharing | Davet yönetimi |
| Subscription | Plan, ödeme |
| Privacy | Data, güvenlik |

---

## Teknik Stack Önerisi

### Mobile App

```
Framework: React Native (Expo)
├── Neden: Cross-platform, hızlı geliştirme
├── State: Zustand veya Redux Toolkit
├── Navigation: React Navigation
└── UI: NativeBase veya custom

Alternatif: Flutter
├── Neden: Performans, single codebase
├── State: Riverpod
└── UI: Material 3
```

### Backend

```
Option A: Firebase + Cloudinary
├── Auth: Firebase Auth
├── Database: Firestore
├── Storage: Cloudinary (resim işleme)
├── Functions: Cloud Functions
└── Hosting: Firebase Hosting

Option B: Supabase + AWS S3
├── Auth: Supabase Auth
├── Database: PostgreSQL
├── Storage: AWS S3 + CloudFront
├── APIs: Edge Functions
└── Hosting: Vercel
```

### Infrastructure

```
├── CDN: CloudFront veya Bunny.net
├── Image Processing: Cloudinary veya imgix
├── Push: Firebase FCM
├── Analytics: Mixpanel veya Amplitude
├── Error Tracking: Sentry
└── AB Testing: PostHog
```

---

## MVP Success Criteria

### Teknik KPIlar

| Metrik | Hedef |
|--------|-------|
| App Crash Rate | <0.5% |
| Photo Upload Success | >99% |
| Time to Upload (10 foto) | <30 saniye |
| App Launch Time | <2 saniye |
| App Size | <50MB |

### Kullanıcı KPIları

| Metrik | Hedef |
|--------|-------|
| D1 Retention | >50% |
| D7 Retention | >30% |
| Photos per User (Hafta 1) | >10 |
| Story Completion Rate | >40% |
| Family Invite Rate | >20% |
