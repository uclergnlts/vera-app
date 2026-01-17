# 🗄️ Database Schema & Entity Relationship Diagram

## PostgreSQL Schema

```sql
-- ============ USERS & AUTHENTICATION ============

CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  firebase_uid VARCHAR(255) UNIQUE,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  deleted_at TIMESTAMP
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_firebase_uid ON users(firebase_uid);

-- ============ SUBSCRIPTION & BILLING ============

CREATE TABLE subscriptions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  plan VARCHAR(50) NOT NULL, -- 'standard', 'premium', 'vip'
  price_monthly INT, -- cents (999 = ₺9.99)
  price_yearly INT,
  billing_period VARCHAR(10) NOT NULL, -- 'monthly', 'yearly'
  stripe_subscription_id VARCHAR(255) UNIQUE,
  stripe_customer_id VARCHAR(255) UNIQUE,
  status VARCHAR(50) DEFAULT 'active', -- 'active', 'paused', 'cancelled'
  started_at TIMESTAMP NOT NULL,
  renews_at TIMESTAMP NOT NULL,
  cancelled_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_subscriptions_user_id ON subscriptions(user_id);
CREATE INDEX idx_subscriptions_stripe_subscription_id ON subscriptions(stripe_subscription_id);

-- ============ PAYMENT HISTORY ============

CREATE TABLE payments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  subscription_id UUID NOT NULL REFERENCES subscriptions(id),
  amount_cents INT NOT NULL,
  currency VARCHAR(3) DEFAULT 'TRY',
  status VARCHAR(50) DEFAULT 'pending', -- 'pending', 'succeeded', 'failed'
  stripe_payment_intent_id VARCHAR(255) UNIQUE,
  paid_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_payments_subscription_id ON payments(subscription_id);

-- ============ CHILDREN PROFILES ============

CREATE TABLE children (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  name VARCHAR(255) NOT NULL,
  date_of_birth DATE NOT NULL,
  profile_photo_url TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_children_user_id ON children(user_id);

-- ============ PHOTOS & MEDIA ============

CREATE TABLE photos (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  child_id UUID NOT NULL REFERENCES children(id) ON DELETE CASCADE,
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  
  -- File storage
  original_url TEXT NOT NULL, -- S3 URL
  thumbnail_url TEXT NOT NULL, -- 300x300 thumb
  web_url TEXT NOT NULL, -- optimized web version
  file_size_bytes INT,
  mime_type VARCHAR(50),
  
  -- EXIF data
  exif_date_taken TIMESTAMP, -- from EXIF
  exif_camera_model VARCHAR(255),
  exif_gps_lat DECIMAL(10, 8),
  exif_gps_lng DECIMAL(11, 8),
  
  -- Calculated data
  calculated_age_months INT GENERATED ALWAYS AS (
    EXTRACT(EPOCH FROM (uploaded_at - 
      (SELECT date_of_birth FROM children WHERE id = child_id))) / 2592000
  ) STORED,
  
  -- Metadata
  story_text TEXT,
  is_favorite BOOLEAN DEFAULT FALSE,
  uploaded_at TIMESTAMP DEFAULT NOW(),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_photos_child_id ON photos(child_id);
CREATE INDEX idx_photos_user_id ON photos(user_id);
CREATE INDEX idx_photos_exif_date ON photos(exif_date_taken);
CREATE INDEX idx_photos_calculated_age ON photos(calculated_age_months);

-- ============ TAGS & TAGGING ============

CREATE TABLE tag_categories (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) UNIQUE NOT NULL, -- 'milestones', 'locations', 'people'
  description TEXT
);

INSERT INTO tag_categories (name) VALUES 
  ('milestones'),
  ('locations'),
  ('people'),
  ('events'),
  ('emotions');

CREATE TABLE tags (
  id SERIAL PRIMARY KEY,
  category_id INT NOT NULL REFERENCES tag_categories(id),
  name VARCHAR(255) NOT NULL,
  UNIQUE(category_id, name)
);

INSERT INTO tags (category_id, name) VALUES
  (1, 'İlk adım'),
  (1, 'İlk diş'),
  (1, 'Doğum günü'),
  (1, 'Okul başlangıcı'),
  (2, 'Ev'),
  (2, 'Park'),
  (2, 'Plaj'),
  (3, 'Anne'),
  (3, 'Baba'),
  (4, 'Tatil'),
  (4, 'Aile buluşması');

CREATE TABLE photo_tags (
  photo_id UUID NOT NULL REFERENCES photos(id) ON DELETE CASCADE,
  tag_id INT NOT NULL REFERENCES tags(id),
  PRIMARY KEY(photo_id, tag_id)
);

CREATE INDEX idx_photo_tags_tag_id ON photo_tags(tag_id);

-- ============ FAMILY SHARING ============

CREATE TABLE family_shares (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  child_id UUID NOT NULL REFERENCES children(id) ON DELETE CASCADE,
  shared_by_user_id UUID NOT NULL REFERENCES users(id),
  
  -- Share type
  share_type VARCHAR(50) DEFAULT 'view_only', -- 'view_only', 'can_edit'
  
  -- Access method
  invite_token VARCHAR(255) UNIQUE NOT NULL,
  invite_email VARCHAR(255),
  shared_family_member_id UUID REFERENCES users(id),
  
  -- Permissions
  can_view_photos BOOLEAN DEFAULT TRUE,
  can_edit_stories BOOLEAN DEFAULT FALSE,
  can_receive_album BOOLEAN DEFAULT TRUE,
  
  -- Status
  status VARCHAR(50) DEFAULT 'pending', -- 'pending', 'accepted', 'revoked'
  accepted_at TIMESTAMP,
  revoked_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW(),
  expires_at TIMESTAMP -- share link expiry
);

CREATE INDEX idx_family_shares_child_id ON family_shares(child_id);
CREATE INDEX idx_family_shares_invite_token ON family_shares(invite_token);

-- ============ ALBUMS ============

CREATE TABLE albums (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  child_id UUID NOT NULL REFERENCES children(id) ON DELETE CASCADE,
  user_id UUID NOT NULL REFERENCES users(id),
  
  -- Album metadata
  year INT NOT NULL,
  design_variant VARCHAR(50) DEFAULT 'modern', -- template choice
  status VARCHAR(50) DEFAULT 'draft', -- 'draft', 'ready', 'printed', 'shipped', 'delivered'
  
  -- Photo selection
  selected_photo_ids UUID[] DEFAULT '{}'::UUID[], -- JSON array of selected photo IDs
  photo_count INT GENERATED ALWAYS AS (array_length(selected_photo_ids, 1)) STORED,
  cover_photo_id UUID REFERENCES photos(id),
  
  -- Customization
  custom_title VARCHAR(255),
  custom_message TEXT,
  
  -- Dates
  preview_url TEXT, -- PDF preview for user
  print_sent_at TIMESTAMP, -- when sent to printer
  print_completed_at TIMESTAMP,
  shipped_at TIMESTAMP,
  delivered_at TIMESTAMP,
  
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_albums_child_id ON albums(child_id);
CREATE INDEX idx_albums_year ON albums(year);
CREATE INDEX idx_albums_status ON albums(status);

-- ============ NOTIFICATIONS ============

CREATE TABLE notifications (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  child_id UUID REFERENCES children(id),
  
  -- Notification type
  type VARCHAR(50) NOT NULL, -- 'milestone', 'memory_card', 'album_ready', 'album_shipped', etc
  title VARCHAR(255) NOT NULL,
  body TEXT NOT NULL,
  
  -- Data for handling
  data JSONB, -- { photoId, milestoneType, etc }
  
  -- Delivery
  push_token VARCHAR(255), -- Expo push token
  sent_at TIMESTAMP,
  read_at TIMESTAMP,
  
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_notifications_user_id ON notifications(user_id);
CREATE INDEX idx_notifications_read_at ON notifications(read_at);

-- ============ MILESTONES (Pre-defined) ============

CREATE TABLE milestones (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255) NOT NULL UNIQUE, -- 'First step', 'First tooth', etc
  description TEXT,
  emoji VARCHAR(10),
  category VARCHAR(50) -- 'physical', 'development', 'social'
);

INSERT INTO milestones (name, emoji, category) VALUES
  ('İlk adım', '👣', 'physical'),
  ('İlk diş', '🦷', 'physical'),
  ('İlk sözcük', '🗣️', 'development'),
  ('Doğum günü', '🎂', 'event'),
  ('Okul başlangıcı', '🎓', 'event'),
  ('Yüzme öğrenmesi', '🏊', 'physical');

-- ============ ACTIVITY LOG ============

CREATE TABLE activity_logs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id),
  action VARCHAR(100) NOT NULL, -- 'photo_uploaded', 'story_added', 'family_invited'
  resource_type VARCHAR(50), -- 'photo', 'child', 'share'
  resource_id UUID,
  metadata JSONB,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_activity_logs_user_id ON activity_logs(user_id);
CREATE INDEX idx_activity_logs_created_at ON activity_logs(created_at);

-- ============ FEATURE FLAGS ============

CREATE TABLE feature_flags (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255) UNIQUE NOT NULL,
  enabled BOOLEAN DEFAULT FALSE,
  description TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);

INSERT INTO feature_flags (name, enabled, description) VALUES
  ('ai_memory_selection', FALSE, 'AI-powered best photo selection'),
  ('video_support', FALSE, 'Video upload support'),
  ('face_recognition', FALSE, 'Automatic face tagging'),
  ('location_services', FALSE, 'GPS location tagging');
```

---

## Entity Relationship Diagram (ERD)

```
┌──────────────┐
│    USERS     │
├──────────────┤
│ id (PK)      │
│ email        │
│ password_hash│
│ firebase_uid │
└──────────────┘
       │
       ├─────────────────────────────────────┐
       │                                     │
       ▼                                     ▼
┌──────────────────────┐         ┌──────────────────┐
│ SUBSCRIPTIONS        │         │ CHILDREN         │
├──────────────────────┤         ├──────────────────┤
│ id (PK)              │         │ id (PK)          │
│ user_id (FK)         │         │ user_id (FK)     │
│ plan                 │         │ name             │
│ stripe_subscription_id         │ date_of_birth    │
│ status               │         │ profile_photo_url│
│ renews_at            │         └──────────────────┘
└──────────────────────┘                   │
       │                                   │
       ▼                                   ▼
┌──────────────────────┐         ┌──────────────────┐
│ PAYMENTS             │         │ PHOTOS           │
├──────────────────────┤         ├──────────────────┤
│ id (PK)              │         │ id (PK)          │
│ subscription_id (FK) │         │ child_id (FK)    │
│ amount_cents         │         │ user_id (FK)     │
│ status               │         │ original_url     │
│ stripe_payment_..._id          │ story_text       │
└──────────────────────┘         │ calculated_age_mo│
                                 │ exif_date_taken  │
                                 │ is_favorite      │
                                 └──────────────────┘
                                         │
                                         ▼
                                ┌──────────────────┐
                                │ PHOTO_TAGS       │
                                ├──────────────────┤
                                │ photo_id (FK)    │
                                │ tag_id (FK)      │
                                └──────────────────┘
                                         │
                                         ▼
                                ┌──────────────────┐
                                │ TAGS             │
                                ├──────────────────┤
                                │ id (PK)          │
                                │ category_id (FK) │
                                │ name             │
                                └──────────────────┘

    ┌──────────────────────────────────┐
    │ FAMILY_SHARES                    │
    ├──────────────────────────────────┤
    │ id (PK)                          │
    │ child_id (FK)                    │
    │ shared_by_user_id (FK)           │
    │ shared_family_member_id (FK)     │
    │ invite_token                     │
    │ status                           │
    └──────────────────────────────────┘

    ┌──────────────────────────────────┐
    │ ALBUMS                           │
    ├──────────────────────────────────┤
    │ id (PK)                          │
    │ child_id (FK)                    │
    │ user_id (FK)                     │
    │ year                             │
    │ selected_photo_ids []            │
    │ status                           │
    │ shipped_at                       │
    └──────────────────────────────────┘

    ┌──────────────────────────────────┐
    │ NOTIFICATIONS                    │
    ├──────────────────────────────────┤
    │ id (PK)                          │
    │ user_id (FK)                     │
    │ child_id (FK)                    │
    │ type                             │
    │ title, body                      │
    │ sent_at, read_at                 │
    └──────────────────────────────────┘
```

---

## Key Design Patterns

### 1. Soft Deletes (GDPR Compliance)
- Users can request data deletion
- `deleted_at` timestamp tracks when deleted
- Queries filter: `WHERE deleted_at IS NULL`

### 2. Calculated Fields (Performance)
- `calculated_age_months` generated from DOB
- Timeline queries filter by age instantly
- No runtime calculations needed

### 3. JSONB for Flexibility
- `notifications.data` = JSON metadata
- `albums.selected_photo_ids` = array of photo IDs
- Easy to add fields without migrations

### 4. Array Storage
- Album photo selection = UUID array
- Fast filtering: `array_contains(selected_photo_ids, $1)`
- Denormalized for performance

### 5. Denormalization Strategy
- `photo.calculated_age_months` = pre-calculated
- `album.photo_count` = generated always
- Avoids expensive JOINs on timeline queries

---

## Indexes Strategy

```sql
-- Hot query paths:

-- Timeline (most common):
SELECT * FROM photos 
WHERE child_id = $1 
ORDER BY exif_date_taken DESC
-- Index: idx_photos_child_id, idx_photos_exif_date

-- Search by age:
SELECT * FROM photos 
WHERE child_id = $1 AND calculated_age_months BETWEEN $2 AND $3
-- Index: idx_photos_calculated_age

-- User subscriptions:
SELECT * FROM subscriptions 
WHERE user_id = $1 AND status = 'active'
-- Index: idx_subscriptions_user_id

-- Photo tags (for search):
SELECT p.* FROM photos p
JOIN photo_tags pt ON p.id = pt.photo_id
WHERE pt.tag_id = $1
-- Index: idx_photo_tags_tag_id
```

---

## Migration Strategy

```typescript
// Using Prisma migrations:

// 1. npx prisma migrate dev --name init
// Creates migration files in prisma/migrations/

// 2. In production:
// npx prisma migrate deploy
// Applies migrations in order

// Schema versioning:
// Schema v1.0 (Jan 2026) = initial schema
// Schema v1.1 (Feb 2026) = add feature flags
// Schema v1.2 (Mar 2026) = add AI fields
```

---

## Backup & Recovery

```
Daily backups:
├── Full backup (1am UTC)
├── Incremental (every 6 hours)
└── Retention: 30 days

Point-in-time recovery:
├── Available for last 7 days
├── Recovery time: <1 minute
└── Data loss: <1 minute

Disaster recovery:
├── 2 database replicas (standby)
├── Auto-failover (if primary down)
└── RTO: 5 minutes, RPO: <1 minute
```

---

**Status**: ✅ Ready for implementation
