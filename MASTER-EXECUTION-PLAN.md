# 🚀 VERA - EXECUTION MASTER PLAN

**Status**: Ready for execution  
**Timeline**: 73 days to Q1 deadline (Jan 17 - Mar 31, 2026)  
**Goal**: MVP launch + 50 beta users + validated pricing

---

## PHASE 1: FOUNDATION (Jan 17 - Jan 31, 2 Weeks)

### Week 1: Setup & Planning

#### Technical (Dev Hiring Priority)

- [ ] Tech stack approved (Next.js + Node.js + PostgreSQL) → [TECH-STACK.md](../technical/TECH-STACK.md)
- [ ] Backend developer hired (50% initial, 100% Feb from)
- [ ] Frontend developer hired (React/Next expert)
- [ ] Designer hired (UI/UX)
- [ ] Project management setup (GitHub, Slack, Figma)
- [ ] First sprint planning (2-week sprints)

**Owner**: You (CEO)  
**Deliverable**: Signed contracts, devs start coding

---

#### Printer & Logistics (Offline Priority)

- [ ] Mega Print (İstanbul) - capacity & pricing meeting
- [ ] Ofset Basım A.Ş. (Ankara) - capacity & pricing meeting
- [ ] Request for quote (RFQ) all 3 vendors
- [ ] Sample order planning (100 units, Standart albüm)
- [ ] Aras Kargo bulk discount negotiation
- [ ] Printer contract draft preparation

**Owner**: You (or ops hire)  
**Deliverable**: 2+ printer meetings, RFQ received, sample order scheduled

---

#### Marketing & Beta Waitlist

- [ ] Landing page wireframes design (Figma)
- [ ] Copy writing (emotional hook) → [BETA-WAITLIST-STRATEGY.md](../marketing/BETA-WAITLIST-STRATEGY.md)
- [ ] Influencer list compilation (10-15 targets)
- [ ] Email funnel sequence draft (Mailchimp/GetResponse)
- [ ] Instagram creative assets (3-5 variants)
- [ ] Analytics setup (Google Analytics, Mixpanel)

**Owner**: You or marketing hire  
**Deliverable**: Landing page ready for dev, influencer list + templates

---

### Week 2: Infrastructure & Marketing Launch

#### Technical

- [ ] Repository setup (GitHub)
- [ ] Development environment configured
- [ ] Database schema initialized (PostgreSQL)
- [ ] S3 setup (AWS)
- [ ] Firebase Auth configured
- [ ] First backend skeleton (auth API)
- [ ] First frontend skeleton (Next.js pages)

**Owner**: Dev lead  
**Deliverable**: Deployable repo, CI/CD working

---

#### Printer (Action)

- [ ] Sample order submitted (100 units)
- [ ] Printer contract negotiated & signed
- [ ] Kargo contract negotiated & signed
- [ ] PDF template specification finalized

**Owner**: You or ops  
**Deliverable**: Contracts signed, sample in production

---

#### Marketing (Action)

- [ ] Landing page goes LIVE
- [ ] Instagram ads start (₺5K budget, 3 variants)
- [ ] Influencer outreach emails sent (5-10 targets)
- [ ] Google Analytics tracking live
- [ ] Email list setup (GetResponse)
- [ ] First organic post (TikTok/Instagram)

**Owner**: You or marketing  
**Deliverable**: 30+ waitlist signups, 500+ landing page visitors

---

## PHASE 2: MVP BUILD (Feb 1 - Feb 28, 4 Weeks)

### Week 3-4: Core Infrastructure

#### Backend (Node.js)

```
✅ Endpoints to build:

Auth:
└── POST /api/auth/signup
└── POST /api/auth/login
└── POST /api/auth/logout

Child Profiles:
└── POST /api/children (create)
└── GET /api/children (list)
└── PUT /api/children/{id}
└── DELETE /api/children/{id}

Photos:
└── POST /api/photos/upload (multipart)
└── GET /api/photos (timeline)
└── PUT /api/photos/{id}/story (add note)
└── GET /api/photos/search (filter by date, age)

Subscriptions:
└── POST /api/stripe/checkout
└── POST /api/stripe/webhook (payment confirm)

Database:
└── users, children, photos, stories, subscriptions tables
```

**Owner**: Backend dev (full-time)  
**Deliverable**: All endpoints working, docs updated

---

#### Frontend (Next.js)

```
✅ Screens to build:

Onboarding:
└── /splash
└── /welcome
└── /signup
└── /child-create
└── /subscription-select

Main App:
└── /dashboard (timeline)
└── /upload (photo picker)
└── /photo/{id} (detail + story editor)
└── /search (filters)
└── /settings

Auth:
└── Login/logout flow
└── Protected routes (middleware)
```

**Owner**: Frontend dev (full-time)  
**Deliverable**: All screens functional, mobile responsive

---

#### Product Features

```
✅ Core MVP:

1. Photo Upload
   └── Single & batch upload
   └── Gallery picker integration
   └── EXIF date extraction
   └── Image optimization (Sharp)

2. Child Profile
   └── Create/edit screen
   └── Auto age calculation (from DOB)
   └── Profile photo

3. Timeline View
   └── Age-grouped photos
   └── Chronological order
   └── Tap to detail

4. Story/Note Adding
   └── Text editor per photo
   └── Save to database

5. Milestone Celebrations (NEW)
   └── Auto-detect milestones (1st step, 1st tooth)
   └── Special UI for milestone photos
   └── Notification trigger

6. Memory Cards (NEW)
   └── "N years ago today" logic
   └── Push notification
   └── Card UI display

7. Search & Filter
   └── Date range filter
   └── Age filter
   └── Tag system (basic)

8. Favoriting
   └── Star rating
   └── Favorites view
```

**Owner**: Product lead + both devs  
**Deliverable**: All features working end-to-end

---

### Week 5-6: Essentials & Polish

#### Features (continued)

```
✅ Secondary Features:

1. Family Sharing
   └── Generate share link
   └── View-only access (no edit)
   └── Invite UI

2. Basic Album Preview
   └── Mock-up of yearly album
   └── Show selected photos
   └── Design preview (static)

3. Settings & Account
   └── Profile page
   └── Password change
   └── Subscription manage
   └── Data export (prep for KVKK)

4. Push Notifications
   └── Setup Firebase Cloud Messaging
   └── Milestone notifications
   └── Memory card triggers
   └── Opt-in/opt-out

5. Bug Fixes & Polish
   └── UI consistency
   └── Performance optimization
   └── Mobile testing
   └── Accessibility (a11y)
```

**Owner**: Frontend + backend  
**Deliverable**: Feature-complete MVP

---

#### Beta User Preparation

- [ ] TestFlight build created (iOS)
- [ ] Google Play internal testing setup (Android)
- [ ] Beta testing guide written
- [ ] Feedback form prepared (Google Form)
- [ ] First 20 beta users selected (from waitlist)
- [ ] Onboarding call scripts prepared

**Owner**: You + product  
**Deliverable**: 20 beta testers ready, June 1st start

---

### Week 7: Testing & Submission Prep

#### QA & Testing

- [ ] Functional testing (all features)
- [ ] Device testing (iOS + Android)
- [ ] Edge case handling (empty states, errors)
- [ ] Performance testing (load time, image processing)
- [ ] Security testing (auth, data transmission)

**Owner**: QA person (or dev)  
**Deliverable**: No critical bugs, ready for TestFlight

---

#### App Store Submission

- [ ] App Store Connect setup
- [ ] Screenshots & descriptions written (English + TR)
- [ ] Privacy policy & Terms of Service finalized
- [ ] Build submitted to TestFlight (iOS)
- [ ] Build submitted to Play Console (Android)
- [ ] Expected approval: 5-7 days (iOS), 1-3 hours (Android)

**Owner**: Ops/product  
**Deliverable**: Apps in review

---

#### Marketing Metrics

- [ ] Waitlist size: **Target 100+**
- [ ] Landing page CTR: **Target >2%**
- [ ] Email list: **Target 50+ warm leads**
- [ ] Influencer commits: **Target 3+ partners**
- [ ] Printer sample received: **✅ (from Week 2)**

**Owner**: Marketing  
**Deliverable**: Strong beta user pipeline

---

## PHASE 3: CLOSED BETA & ITERATION (Mar 1 - Mar 31, 4 Weeks)

### Week 8-9: Closed Beta Launch

#### Beta Rollout

- [ ] 20-30 beta users invited (from waitlist)
- [ ] Give them free year + ₺200 albüm credit
- [ ] Daily standups with beta users (feedback)
- [ ] Crash reporting enabled (Sentry)
- [ ] Usage analytics tracked (Mixpanel)

**Owner**: You + product  
**Deliverable**: 20+ active beta users, daily feedback

---

#### Data Collection

```
Metrics to track:

Product:
├── Daily active users (DAU)
├── Photos uploaded per user (avg)
├── Stories added per photo (%)
├── Family shares created
└── Feature usage heat map

Feedback:
├── NPS survey (weekly)
├── Open-ended feedback (Google Form)
├── Bug reports (GitHub issues)
└── Feature requests (voting)

Pricing Validation:
├── WTP survey (Van Westendorp) → [PRICING-VALIDATION.md](../research/PRICING-VALIDATION.md)
├── Intent to pay (Likert scale)
├── Churn predictions (usage analysis)
└── Albüm value perception
```

**Owner**: Product + analytics  
**Deliverable**: Clean data dashboard

---

#### Iteration Loop

**Weekly Process**:
1. Monday: Review user feedback
2. Tuesday: Prioritize fixes (top 3 pain points)
3. Wednesday-Friday: Dev implementation
4. Friday: Deploy to TestFlight/Play
5. Next Monday: Repeat

**Target**: Top 3 pain points fixed by Week 10

---

### Week 10-11: Pricing Validation & Market Test

#### Pricing Validation (See [PRICING-VALIDATION.md](../research/PRICING-VALIDATION.md))

- [ ] A/B test 3 pricing variants (50/50/50 traffic split)
- [ ] Van Westendorp survey (100+ beta users)
- [ ] Willingness to pay analysis
- [ ] Final pricing decision
- [ ] Contingency: If WTP <₺800, prepare freemium model

**Owner**: You + product/research  
**Deliverable**: Validated pricing model

---

#### Printer Reality Check

- [ ] Sample albüm received from printer
- [ ] Quality assessment (compare against spec)
- [ ] Adjustments made if needed
- [ ] Production timeline confirmed for Kasım
- [ ] Full contract finalized

**Owner**: You or ops  
**Deliverable**: Sample albüm approved, ready for scale

---

### Week 12: Pre-Launch Finalization

#### Feature Lock & Polish

- [ ] Feature creep STOPPED (only bugs fixed)
- [ ] Design consistency final pass
- [ ] Copywriting review (tone, clarity)
- [ ] Performance optimization (target <3s load)
- [ ] Accessibility audit (WCAG AA)

**Owner**: Frontend/design  
**Deliverable**: Polished MVP ready for public

---

#### Compliance & Legal

- [ ] KVKK compliance check (data processing)
- [ ] Terms of Service finalized
- [ ] Privacy Policy finalized
- [ ] Data security audit (encryption, backups)
- [ ] Stripe/iyzico compliance verified

**Owner**: You + legal consultant  
**Deliverable**: Signed legal docs

---

#### Public Launch Preparation

- [ ] Press release written (TechCrunch, local media)
- [ ] Blog post: "Vera Launches" (Medium, product website)
- [ ] Influencer schedule (coordinated posts)
- [ ] Launch day timeline (9am server check, 10am go-live)
- [ ] Support team brief (Intercom, Zendesk setup)

**Owner**: Marketing + ops  
**Deliverable**: Launch materials ready

---

#### Final Metrics (Week 12 Status)

| Metric | Target | Current | Status |
|--------|--------|---------|--------|
| Beta users | 50+ | TBD | Track |
| NPS | >40 | TBD | Track |
| Churn rate | <8% | TBD | Track |
| Pricing confidence | >70% intent | TBD | Track |
| App store approval | Both approved | Pending | Await |
| Printer sample | Approved | Week 8 | Ready |
| Waitlist | 100+ | 30+ (target) | Grow |

---

## SUCCESS DEFINITION (Q1 END)

✅ **MVP Feature Complete**
- Upload, timeline, stories, family sharing, notifications all working

✅ **Public Apps Available**
- iOS + Android, both app stores approved

✅ **Validated Product-Market Fit Signals**
- 50+ beta users
- NPS >40
- Intent to pay >60%
- Pricing validated

✅ **Ready for Q2 Launch**
- Marketing ready (influencers, ads, content)
- Printer ready (production line set)
- Team in place (dev, ops, marketing)

---

## TEAM & HIRING

### Current Needs (Jan)

```
Immediate (Full-time):
├── 1x Backend Engineer (Node.js)
├── 1x Frontend Engineer (Next.js/React)
├── 1x Product Designer (UI/UX)
└── 1x Operations (Printer logistics, fulfillment)

Optional (Contractor):
├── 1x DevOps (CI/CD, Stripe integration)
└── 1x QA (Testing, bug reporting)

You (CEO): Product strategy, fundraising, ops oversight
```

**Budget**: ~₺200K/month × 3 months = ₺600K (MVP phase)

---

## CONTINGENCY PLANS

### If Tech Timeline Slips

**If Week 12 = not ready**:
- Extend beta to April (soft launch, not public)
- Focus on core 3 features only (upload, timeline, stories)
- Skip fancy features (notifications, advanced search)
- Public launch pushed to May 1

---

### If Printer Fails

**If sample quality bad**:
- Switch to Ofset Basım backup
- Delay production timeline by 2-3 weeks
- Still deliver by year-end, but tighter

---

### If Pricing Validation Fails

**If WTP <₺700**:
- Switch to freemium model
- Free: Sınırsız dijital + basic features
- Paid: +₺699/yıl for family sharing + albüm
- Extend free user acquisition 3-4 months

---

## GO/NO-GO DECISION (Mar 28)

### Before Q2 Public Launch, Ask:

1. **Product**: MVP stable, 0 critical bugs?
2. **Team**: Dev, ops, marketing all confident?
3. **Printer**: Sample approved, contracts signed?
4. **Pricing**: Confidence >60%?
5. **Beta**: 50+ users, NPS >35?

**If YES to all 5**: 🟢 GREEN LIGHT, Launch Q2  
**If NO to any**: 🟡 YELLOW FLAG, discuss extension

---

## WHO OWNS WHAT

| Area | Owner | Backup |
|------|-------|--------|
| Product strategy | You | Product manager (hire later) |
| Technical | Backend/Frontend leads | You (code review) |
| Design | Designer | You (final approval) |
| Printer logistics | Ops hire | You (decision-making) |
| Marketing | You initially | Hire marketing lead by Feb |
| Finances | You | Accountant (external) |

---

## SUCCESS METRICS

### Jan End

```
✅ Team hired (3-4 people started)
✅ Printer meetings done (RFQ received)
✅ Landing page live (30+ signups)
✅ Engineering kickoff (sprints begin)
```

### Feb End

```
✅ MVP 80% feature complete
✅ Beta user onboarding begins (Week 8)
✅ Printer sample in production
✅ Waitlist 100+ (marketing success)
✅ No critical blockers
```

### Mar End

```
✅ MVP feature complete
✅ 50+ beta users active
✅ Pricing validated (>60% intent)
✅ Apps submitted (approval expected)
✅ Printer ready for Kasım (sample approved)
✅ Green light for Q2 public launch
```

---

## NEXT IMMEDIATE STEPS (This Week)

### TODAY (Jan 17)

- [ ] Share this plan with any co-founder/advisors
- [ ] Start backend developer search (LinkedIn, AngelList, local networks)
- [ ] Schedule printer meetings (Mega Print, Ofset Basım)
- [ ] GitHub repo creation + initial commit

### TOMORROW (Jan 18)

- [ ] Dev interviews start
- [ ] Landing page designer brief
- [ ] Influencer outreach email template draft

### NEXT 3 DAYS (Jan 19-21)

- [ ] 2-3 dev interviews completed
- [ ] Designer briefing (landing page wireframe)
- [ ] Printer RFQ sent

### END OF WEEK (Jan 24)

- [ ] Dev team hired (ideally)
- [ ] Tech stack architecture doc signed off
- [ ] Landing page live
- [ ] First printer response received

---

**🚀 LET'S BUILD A UNICORN**

**Current status**: Strategy complete, ready for execution  
**Next meeting**: Weekly Monday 10am (progress check-in)  
**Success is non-negotiable**: 50 beta users by end of Q1.
