# 🏗️ Vera Tech Stack

## Frontend (Web + Mobile)

### Stack Choice: **Next.js + React Native Expo**

**Neden:**
- Next.js: SSR, API routes (backend kısaltır), deployment kolay (Vercel)
- React Native Expo: iOS/Android aynı code, app store submit kolay
- Shared component library: Veri tutarlılığı

**Dependencies:**
```
Frontend Core:
├── next.js 14.x (web)
├── react-native-expo 50.x (mobile)
├── typescript
├── tailwind.css (styling)
├── zustand (state management)
└── react-query (server sync)

Upload & Media:
├── react-dropzone
├── react-image-crop
├── sharp (image optimization)
└── ffmpeg (video encoding)

Forms:
├── react-hook-form
└── zod (validation)
```

**Timeline:**
- Prototip: 2 hafta
- 80% feature complete: 4 hafta
- Push to TestFlight/Play Store: 5. hafta

---

## Backend

### Stack Choice: **Node.js + Express + TypeScript**

**Neden:**
- Hızlı (startup için ideal)
- JavaScript shared (frontend'le code reuse)
- Scalable (worker threads, clustering)

**Dependencies:**
```
Runtime:
├── node.js 20.x
├── express 4.x
├── typescript
├── joi (validation)
└── winston (logging)

Auth:
├── firebase-admin (Auth)
├── jsonwebtoken (JWT)
└── bcrypt

Database:
├── prisma (ORM)
└── postgresql 15.x

Storage:
├── aws-sdk (S3)
└── sharp (image resizing)

Payment:
├── stripe (primary)
└── iyzipay (TR backup)

Job Queue:
├── bull (Redis-based)
└── node-schedule (crons)
```

**Architecture:**
```
src/
├── controllers/     (business logic)
├── services/        (external APIs)
├── models/          (database)
├── middleware/      (auth, validation)
├── routes/          (endpoints)
└── utils/           (helpers)
```

**Timeline:**
- Auth setup: 3 gün
- Core APIs (child, photos, tags): 1 hafta
- Search/filter: 3 gün
- Album preview: 3 gün

---

## Database

### PostgreSQL 15 + Prisma ORM

**Schema (Temel):**
```sql
users
├── id, email, password_hash
├── stripe_customer_id
└── subscription_plan

children
├── id, user_id, name, dob
└── photo_count

photos
├── id, child_id, photo_url, uploaded_at
├── exif_date, calculated_age
├── story, tags
└── is_favorite

tags
├── id, name (milestones, locations, people)
└── category

albums
├── id, child_id, year
├── selected_photos (JSON array)
├── design_variant
└── status (draft, printed, shipped)

subscriptions
├── user_id, plan, starts_at, renews_at
└── stripe_subscription_id
```

---

## Storage

### AWS S3 (Primary) + CloudFront (CDN)

**Folder Structure:**
```
s3://vera-app/
├── users/{user_id}/
│   └── photos/{photo_id}/(original, thumb, web)
└── albums/{user_id}/{year}/(proof, final)
```

**Optimization:**
- Originals: JPEG 85%, WebP 75%
- Thumbnails: 300x300 JPG
- CDN cache: 30 gün

---

## Payment

### Stripe (Primary) + İyzico (Fallback)

**Flow:**
```
1. Next.js API route (/api/checkout)
2. Stripe Checkout Session
3. Webhook: payment_intent.succeeded
4. Database: update subscription
5. Email: welcome + first steps
```

**Recurring:**
- Yearly billing (default)
- Renewal 30 gün önce email
- Stripe Portal: self-serve cancel

---

## Deployment

### Infrastructure

```
Frontend:
├── Next.js → Vercel (auto-deploy)
└── React Native → Apple Testflight + Google Play

Backend:
├── Node.js → Railway.app (saat başı 0 gün uptime)
└── PostgreSQL → Railway (auto-backup)

Storage:
└── AWS S3 (already has backup)

Monitoring:
├── Sentry (error tracking)
├── DataDog (performance)
└── LogRocket (frontend replay)
```

**Cost (Yıl 1):**
- Railway: ₺3K/ay
- AWS S3: ₺500/ay (1000 user, 10GB/user = 10TB)
- Stripe: 2.9% + $0.30
- CDN: ₺300/ay
- **Total**: ~₺50K/yıl

---

## Development Workflow

### CI/CD

```yaml
GitHub Actions:
├── Run tests (Jest)
├── Lint (ESLint)
├── Build (Next.js)
├── Deploy (Vercel + Railway)
└── Notify (Slack)

Timeline:
- Main branch = production
- Feature branches = PR review
- Deploy time: ~2 min
```

---

## Security & Compliance

### Authentication

```
Frontend → JWT (localStorage)
Backend → Verify JWT middleware
Session → 30 days (auto-refresh)
```

### Data Security

- **KVKK**: Data processing agreement (DPA)
- **Encryption**: AES-256 at rest (AWS KMS)
- **SSL/TLS**: HTTPS only
- **Backup**: Daily automated (AWS)
- **GDPR Compliance**: User data export, deletion

---

## MVP Timeline (4 Weeks)

```
Week 1:
├── Backend: Auth + DB setup
├── Frontend: Onboarding screens
└── Infra: Deploy skeleton

Week 2:
├── Photo upload API + frontend
├── Child profile CRUD
└── Timeline view (basic)

Week 3:
├── Story/note system
├── Tags + search
└── Family sharing (share link)

Week 4:
├── Album preview mockup
├── Settings + account
├── Polish + bug fixes
└── TestFlight/Play Store prep
```

---

## Team Required (MVP)

```
1 Full-stack engineer (Next.js + Node)
1 React Native engineer (Expo)
1 Designer (UI/UX)
1 PM (you)

Cost: ~₺200K/month × 1 ay = ₺200K
```

---

## Risks & Mitigations

| Risk | Mitigation |
|------|-----------|
| Image processing (EXIF) slow | Use Sharp in queue, presign URLs |
| Stripe integration bugs | Test with Stripe fixtures |
| App store approval delays | Submit Week 3, plan for Week 5 |
| Mobile auth complexity | Firebase + Expo built-in support |
| Database scaling (1000 users) | PostgreSQL handles easily, shard later |

---

**Status**: ✅ APPROVED FOR BUILD
