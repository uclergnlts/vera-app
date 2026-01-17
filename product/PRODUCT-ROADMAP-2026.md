# 🗺️ Product Roadmap (Q1 2026 - Q4 2026)

## Executive Summary

**Vision:** Build the digital memory archive + physical album platform for families, with intelligent features that celebrate childhood moments.

**Mission:** Help parents preserve and relive their children's growth stories through automatic milestone detection, emotional reminders, and beautiful physical albums.

**Phases:**
- **Q1 (MVP)**: Jan 17 - Mar 31: Core photo archive + 1 album per year
- **Q2 (Early Traction)**: Apr 1 - Jun 30: AI milestones + family sharing
- **Q3 (Product-Market Fit)**: Jul 1 - Sep 30: Multiple albums + subscriptions upgrade
- **Q4 (Scale)**: Oct 1 - Dec 31: Automations + partnerships + international expansion

---

## Q1 2026: MVP Launch (Jan 17 - Mar 31)

### Theme: "Core Memory Archive"

**Objective:** Build the foundational photo storage + 1 yearly album + simple sharing

### Features

#### Phase 1A: Foundation (Jan 17 - Feb 20)

**Photo Upload & Storage**
```
✅ Photo upload (mobile app)
├── JPEG/PNG support
├── EXIF date + GPS extraction
├── Auto-rotation based on device orientation
├── Compression (original + thumbnail + web format)
├── Progress indicator
├── Batch upload (5-10 photos)
└── Success/error feedback

✅ Photo Timeline
├── Chronological grid view
├── Age-based grouping (0-3mo, 3-6mo, 6-9mo, etc)
├── Infinite scroll
├── Search by date range
├── Filter by child
└── Performance optimized (60fps scrolling)

✅ Photo Details Screen
├── Full-size image viewer
├── EXIF metadata display
├── Captured date and calculated age
├── Edit story/notes (max 500 chars)
├── Favorite/unfavorite toggle
├── Share photo (external)
└── Delete option with confirmation

✅ Offline Functionality
├── Download timeline to SQLite (last 30 days)
├── View cached photos without internet
├── Queue uploads when offline
├── Sync when internet returns
├── Sync status indicator
└── Conflict resolution (server wins)

✅ Authentication & Profile
├── Email/password signup
├── Email verification
├── Secure password requirements (12+ chars, mixed case)
├── Profile setup (name, profile photo)
├── Password reset flow
├── Logout functionality
└── Session management (24-hour tokens)
```

**Children Management**
```
✅ Add Children
├── Name input
├── Date of birth picker
├── Profile photo upload
├── Multiple children support (up to plan limit)
└── Edit/delete child

✅ Child Profile
├── Display child name and age
├── Total photo count
├── Last upload date
├── Photo count trends (optional)
└── Edit child details
```

**Subscription & Billing**
```
✅ Subscription Plans
├── Basic (₺999/year): 1 child, no albums
├── Standard (₺1,999/year): 2 children, 1 album/year
├── Premium (₺4,999/year): 5 children, 1 album/year + 50 physical prints
└── Monthly option (₺99/month, auto-convert yearly on day 1)

✅ Checkout Flow
├── Stripe integration
├── İyzico fallback (Turkish payment)
├── Plan selection
├── Secure payment form
├── Receipt generation
├── Auto-renewal setup
└── Plan change support (pro-rata billing)

✅ Subscription Dashboard
├── Current plan display
├── Renewal date
├── Usage stats (children, photos)
├── Plan upgrade/downgrade
├── Billing history
├── Payment method management
└── Cancellation option
```

#### Phase 1B: Albums & Sharing (Feb 21 - Mar 31)

**Album Creation (Annual)**
```
✅ Auto-Album Curation
├── Automatic selection of best photos (ML-based, simulated)
├── Photos from Jan 1 - Dec 31 previous year
├── Sort by quality score, diversity, date
├── Default: Top 150-200 photos
└── Manual selection available

✅ Album Customization
├── Design variant selection (5 templates for MVP)
│   ├── Modern (minimalist)
│   ├── Classic (traditional)
│   ├── Warm (emotional, family-focused)
│   ├── Playful (colorful, fun)
│   └── Elegant (premium, serif fonts)
├── Custom title ("Emma's 2025", etc)
├── Custom message (page 1)
├── Photo selection/reordering
├── Photo captions editing
├── Layout options (2-up, 3-up, full-page)
└── Cover customization (color, photo)

✅ Album Preview
├── Full-page PDF preview
├── Mobile swipeable preview
├── Physical dimensions display (A5 = 148×210mm)
├── Page count indication
└── Download preview option

✅ Album Ordering
├── Price display (physical production + shipping)
├── Quantity selection
├── Shipping address entry
├── Estimated delivery date
├── Order tracking
└── Fulfillment via Mega Print

✅ Album Shipping
├── Mega Print integration (API)
├── Order submission automation
├── Tracking number provision
├── Delivery status updates
├── Returns/damaged handling
└── Reorder previous album
```

**Basic Family Sharing**
```
✅ Invite Family Members
├── Enter email address
├── Set permissions (view-only, can-edit)
├── Optional expiration date (30/60/90 days)
├── Invite token generation
├── Email invitation with link
└── Resend invite option

✅ Family Member Access
├── View shared photos via link
├── No account required (public link)
├── Ability to accept invite (create account)
├── Edit permissions if granted
├── Access to current year's album preview
└── Download individual photos (optional)

✅ Family Share Management
├── List of all family shares
├── Active/pending status
├── Revoke access anytime
├── Edit permissions
├── See who viewed what (optional)
└── View last access date
```

**Notifications (Basic)**
```
✅ Push Notifications
├── Notification permission request on first launch
├── Subscription renewal reminder (7 days before)
├── Album ready notification (when design finalized)
├── Album shipped notification (with tracking)
├── Family member joined notification
├── Daily "1 year ago today" notification (opt-in)
└── Notification settings in profile
```

### Success Metrics (Target)

```
Usage Metrics
├── 500+ beta signups
├── 250+ active users (1+ upload/month)
├── 50,000+ photos uploaded
├── 50%+ photos with custom stories
└── 80%+ monthly active rate

Subscription Metrics
├── 200+ paid subscriptions
├── 40% conversion from beta
├── ₺200,000+ MRR (assuming ₺1,000 ARPU)
├── <5% monthly churn
└── 3:1 basic:standard:premium ratio

Album Metrics
├── 150+ albums ordered
├── ₺150,000+ album revenue (₺1,000 per album avg)
├── 90%+ customer satisfaction
├── <2% fulfillment errors
└── <5 day avg delivery time

Sharing Metrics
├── 30%+ users invite family members
├── Avg 2.5 family members per user
└── 20%+ invited users convert to paid

---

## Q2 2026: Early Traction (Apr 1 - Jun 30)

### Theme: "Smart Memory Curation"

**Objective:** Add AI-powered milestone detection and expand sharing features

### Features

#### Milestone Detection (AI)

**Auto-Milestone Recognition**
```
👶 Detected Milestones:
├── First smile
├── Rolling over
├── Sitting up
├── Crawling
├── Standing/cruising
├── First steps
├── First words
├── Teeth eruption
├── Eating solids
├── First hair cut
├── Birthday celebrations
├── Holidays (holidays)
└── Family events (based on calendar integration)

How it works:
├── Machine Learning model (TensorFlow Lite or Firebase ML)
├── Photo analysis on device (privacy-first)
├── Fallback: Manual milestone selection
├── User confirmation for milestones
└── Milestone notification system
```

**Milestone Timeline**
```
✅ Milestone View
├── Timeline filtered by milestones
├── Milestone cards with icon + description
├── Associated photos grid
├── Edit milestone details
├── Add custom milestones
├── Share milestone via social
└── Print milestone page
```

#### Memory Cards (Notifications)

```
✅ Anniversary Notifications
├── "X years ago today" - show photos from this date
├── "1 year ago Emma was only Xmo old" with throwback photo
├── Customizable frequency (daily, weekly, monthly)
├── Notification with memory photo
├── Open to memory timeline
└── Share memory with family
```

#### Advanced Family Sharing

```
✅ Family Collaboration
├── Multiple family members can edit album
├── Add photos from family members
├── Comment on photos
├── Tag people in photos
├── Family contributions tracked
└── Approval workflow for public album

✅ Family Calendar
├── Integration with Apple Calendar / Google Calendar
├── Birthday and milestone reminders
├── Family events sync
├── Photo tagging by event
└── Event-based photo albums
```

#### Premium Printing Features

```
✅ Multiple Albums Per Year
├── Seasonal albums (Spring, Summer, Fall, Winter)
├── Milestone-based albums (First Year, Second Year, etc)
├── Event-based albums (Holiday, Birthday, Trip)
├── Monthly mini albums (12 pages)
└── Priority printing (2-week vs 4-week)

✅ Premium Materials
├── Hardcover option
├── Dust jacket option
├── Premium matte paper
├── Custom spine text
├── Gift wrapping option
└── Personalized message card
```

#### Integrations

```
✅ Calendar Integrations
├── Apple Calendar sync (iOS)
├── Google Calendar sync
├── iCloud Photos backup (auto-import)
├── Automatic photo tagging by calendar events
└── Inaccessible photos trigger calendar reminder

✅ Social Media Sharing
├── Share photos to Instagram Stories
├── Share milestones to WhatsApp
├── Share memories to Facebook
├── Post album preview to Instagram Feed
└── Pinterest board creation
```

### Timeline (Q2)

```
Apr 1-15: Milestone AI Model
├── TensorFlow Lite setup
├── Milestone classification model
├── On-device inference
├── User validation workflow
└── Notification delivery

Apr 16-30: Memory Cards & Notifications
├── Anniversary detection
├── Memory card design
├── Push notification system
├── Notification scheduling
└── Analytics tracking

May 1-15: Advanced Sharing
├── Family collaboration features
├── Comment system
├── Calendar integration
└── Event-based albums

May 16-31: Premium Printing
├── Multiple album types
├── Premium material selection
├── Seasonal album templates
└── Print API expansion

Jun 1-15: Social Integrations
├── Instagram Stories
├── Facebook sharing
├── WhatsApp integration
├── Calendar sync (Google + Apple)

Jun 16-30: Testing & Launch
├── QA and bug fixes
├── Performance optimization
├── User testing
└── Go-live Q2 features
```

### Success Metrics

```
User Engagement
├── 60%+ users with milestones tagged
├── 50%+ milestone notification open rate
├── 40%+ memory card interaction rate
├── 70%+ family collaboration adoption
└── 30%+ album sharing to social

Content Metrics
├── 300,000+ total photos
├── 2,000+ milestones identified
├── 500+ family members invited
└── 80%+ user-provided milestone confirmation

Business Metrics
├── 400+ paid subscriptions (2x Q1)
├── ₺500,000+ MRR
├── 300+ albums ordered (2x Q1)
├── ₺300,000+ album revenue
└── <3% monthly churn
```

---

## Q3 2026: Product-Market Fit (Jul 1 - Sep 30)

### Theme: "Full Platform Maturity"

**Objective:** Refine core features, improve retention, expand payment options

### Features

#### Advanced Search & Organization

```
✅ Smart Search
├── Full-text search (photo stories + captions)
├── Face recognition (optional, privacy alert)
├── Object detection (animals, toys, etc)
├── Location search (GPS-based)
├── Time-range search
├── Tag-based search
├── Combination filters
└── Saved searches
```

#### Subscription & Monetization Expansion

```
✅ New Subscription Tiers
├── Family Tier (₺7,999/year): 10 children, 3 albums/year
├── Enterprise (Custom): 50+ children for institutions
├── Annual prepay discount (10% off)
├── Gift subscriptions (3/6/12 month)
└── Student discount (20% with .edu email)

✅ Print-on-Demand Expansion
├── Photo prints (4x6, 5x7, 8x10)
├── Calendars (wall, desk)
├── Mugs/t-shirts (basic apparel)
├── Throw pillows (photo cushions)
├── Book marks and cards
└── Mega Print API expansion
```

#### Mobile App Optimization

```
✅ App Performance
├── App size optimization (<150MB)
├── Faster photo upload (parallel uploads)
├── Smarter caching strategy
├── Battery optimization
├── Network optimization (data saving mode)
└── Cold start performance (<2 seconds)

✅ iOS-Specific Features
├── iCloud integration (backup photos)
├── Siri Shortcuts (voice commands)
├── WidgetKit support (quick access)
├── Face ID / Touch ID (quick unlock)
└── Handoff (continue on iPad)

✅ Android-Specific Features
├── Google Photos integration (backup)
├── Quick Tile support
├── Notification shortcuts
├── Biometric unlock
└── Material You dynamic color support
```

#### Community & Engagement

```
✅ Vera Community
├── User-generated stories (blog)
├── Tips & tricks articles
├── Parenting insights from data
├── User spotlight / featured families
├── Contests and challenges
├── Vera Ambassador program
└── Community guidelines

✅ Gamification (Subtle)
├── Milestone badges (achieved X milestones)
├── Upload streaks (consecutive days)
├── Album completion rewards
├── Referral rewards (₺100 credit)
├── Leaderboards (photos/month - optional)
└── Achievement notifications (celebratory)
```

#### Support & Retention

```
✅ Customer Support Expansion
├── In-app chat support (24/7 via Intercom)
├── Video tutorials (Loom + Wistia)
├── FAQ improvements
├── Community forum (Discourse)
├── Email support tickets
└── NPS tracking and follow-up

✅ Retention Features
├── Win-back campaigns (email automation)
├── Usage-based notifications
├── Personalized recommendations
├── Pause subscription option (temp)
└── Loyalty rewards program
```

### Timeline (Q3)

```
Jul 1-15: Search & Organization
├── Full-text search implementation
├── Face recognition (optional)
├── Advanced filtering
└── Saved searches

Jul 16-31: Mobile Optimization
├── App size reduction
├── Performance improvements
├── Platform-specific features
└── Battery optimization

Aug 1-15: New Subscription Tiers
├── Family tier launch
├── Pricing strategy A/B test
├── Discount structure validation
└── Go-to-market planning

Aug 16-31: Print-on-Demand Expansion
├── New print products
├── Third-party vendor integration
├── Fulfillment automation
└── Quality assurance

Sep 1-15: Community & Engagement
├── Community platform launch
├── Ambassador program
├── Gamification features
└── Content marketing

Sep 16-30: Support & Testing
├── Support infrastructure
├── Testing and optimization
├── Launch readiness
└── Q4 planning
```

### Success Metrics

```
Growth Metrics
├── 800+ paid subscriptions (2x Q2)
├── ₺1,000,000+ MRR run-rate
├── 500,000+ photos stored
├── 1,000+ albums ordered (Q3 only)
├── 50% YoY growth rate

Engagement Metrics
├── 75%+ monthly active rate
├── 50%+ users with searches
├── 60%+ milestone adoption
├── 40%+ family tier signups
└── 5+ photos/week average user

Retention Metrics
├── 3%+ monthly churn
├── 40%+ 6-month retention
├── 70%+ annual renewal rate
├── +2 NPS improvement (vs Q2)
└── 4.8+ app store rating
```

---

## Q4 2026: Scale & Growth (Oct 1 - Dec 31)

### Theme: "Sustainable Scale & International"

**Objective:** Expand to new markets, automation, and long-term retention

### Features

#### Content Automation

```
✅ Auto-Album Creation
├── Annual album automatically created each Dec 31
├── Photos curated by ML model
├── User can customize before printing
├── Auto-submit option (no user action needed)
├── Bulk annual album discounts
└── Gift album to grandparents workflow

✅ Automated Reminders
├── Reminder to add photos if <10/week
├── Reminder to customize annual album
├── Reminder to renew subscription
├── Reminder to download data (GDPR)
├── Smart notification timing (based on user behavior)
└── Opt-out granular control
```

#### International Expansion

```
✅ Localization (Phase 1)
├── Language support: English, Turkish, German
├── Date/time localization
├── Currency localization (EUR, GBP, TRY)
├── Timezone support
└── Locale-specific content

✅ International Printing
├── Germany printing partner (local)
├── UK printing partner (local)
├── EU shipping support
├── Local payment methods (Klarna, Sofort)
├── VAT compliance
└── Multilingual support

✅ Market-Specific Features
├── EU right to deletion (GDPR)
├── UK payment methods
├── German privacy preferences
└── Localized marketing content
```

#### Platform Expansion

```
✅ Web Platform (Minimal)
├── Photo upload to website (not on landing page)
├── Album preview on web
├── Family sharing via web links
├── Photo download
├── Profile settings on web
└── Subscription management on web

Note: Web = Admin/support only, mobile is primary

✅ Wearable Integration
├── Apple Watch complications (quick upload)
├── Smartwatch notifications
├── Voice commands (Siri)
└── Handoff support
```

#### Advanced Analytics

```
✅ Parent Insights Dashboard
├── Photo trends (per month)
├── Milestone timeline
├── Family comparison (with consent)
├── Growth charts (per child)
├── Peak activity times
└── Photo quality trends

✅ Business Analytics
├── Cohort analysis
├── Lifetime value modeling
├── Churn prediction
├── Revenue forecasting
├── Geographic analysis
└── Feature usage metrics
```

### Timeline (Q4)

```
Oct 1-15: Auto-Album Creation
├── ML curation algorithm refinement
├── Auto-submit workflow
├── User testing and feedback
└── Launch

Oct 16-31: Automated Reminders
├── Reminder system architecture
├── Behavioral targeting
├── Testing and optimization
└── Launch

Nov 1-15: International Prep
├── Partner onboarding (Germany, UK)
├── Localization work
├── Payment method integration
└── Compliance review

Nov 16-30: International Launch
├── Language release (English, German)
├── New markets go-live (Germany, UK)
├── Marketing campaigns
└── Support scaling

Dec 1-15: Web Platform
├── Basic web features
├── Admin dashboard
├── Testing and QA
└── Launch

Dec 16-31: Refinement & Planning
├── Year-end optimization
├── Analyze Q4 metrics
├── 2027 roadmap planning
└── Holiday campaigns & promotions
```

### Success Metrics

```
Growth Metrics
├── 1,500+ paid subscriptions (1.875x Q3)
├── ₺2,000,000+ MRR run-rate
├── 30% international revenue
├── 2,000+ albums ordered (Q4 only)
├── 1,000,000+ photos stored globally

Market Expansion
├── 500+ German users
├── 300+ UK users
├── 10% of base from international
├── +2 new language support

Retention & Health
├── 2%+ monthly churn
├── 50%+ annual retention
├── 75%+ monthly active rate
├── 4.9+ app store rating

Business Sustainability
├── Break-even operations
├── Positive unit economics
├── +3 NPS
├── Ready for Series A fundraising
```

---

## 2027 & Beyond (Future Vision)

### Potential Features (Post-MVP)

```
AI & Intelligence
├── Emotion-based photo organization
├── Story generation (written + video)
├── Multi-child collaboration features
├── Predictive recommendations
└── Smart photo enhancement

Partnerships
├── Insurance integration (Allianz, Axa)
├── Bank partnerships (for B2B2C)
├── Camera integrations (GoPro, Instant cameras)
├── Cloud backup partners (OneDrive, Dropbox)
└── Family productivity platforms (Google Family Link)

Entertainment
├── Video compilation creator
├── Photo slideshow (with music)
├── Animated storybooks (from photos)
├── Shared family streaming (memories)
└── Virtual birthday album parties

Commercial
├── Professional photographers marketplace
├── Photo editing services
├── Subscription gift marketplace
├── Premium templates (limited releases)
└── White-label solution for daycares
```

---

## Feature Prioritization Matrix

```
P0 (MVP - Q1) - MUST HAVE
├── Photo upload and storage
├── Timeline view
├── Annual album
├── Subscription system
├── Basic sharing
└── Push notifications

P1 (Q2-Q3) - SHOULD HAVE
├── Milestone detection
├── Memory cards
├── Advanced sharing
├── Search functionality
├── Multiple albums
└── Print-on-demand expansion

P2 (Q4+) - NICE TO HAVE
├── International expansion
├── Community features
├── Advanced analytics
├── Web platform
├── API for partners
└── Integrations
```

---

## Success Criteria by Quarter

```
Q1: Product-Market Fit Signals
├── 40%+ conversion from beta
├── 50%+ monthly active rate
├── <10% churn
└── Clear product-market fit in user interviews

Q2: Retention & Engagement
├── 50%+ with milestones
├── 70% of annual cohort still active
├── 4+ NPS improvement
└── Clear retention hooks validated

Q3: Monetization & Scale
├── 50%+ average revenue per user increase
├── $10K+ MRR from albums
├── 3%+ churn or lower
└── Ready for paid marketing scale

Q4: Sustainability & Expansion
├── Profitable operations
├── International market entry
├── 2x user growth YoY
└── Seed funding secured or bootstrapped sustainability
```

---

**Status**: ✅ Complete product roadmap ready for implementation
