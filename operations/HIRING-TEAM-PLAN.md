# 👥 Hiring & Team Plan

## 1. Team Structure (MVP Phase: Jan 17 - Mar 31)

```
Vera Team Structure
├── Founder/CEO (You)
│   └── Role: Product strategy, operations, fundraising
│
├── Backend Engineer (1 FTE)
│   ├── Role: Node.js API, database, infrastructure
│   ├── Start: Jan 24, 2026
│   └── Urgency: CRITICAL
│
├── Frontend Engineer (1 FTE)
│   ├── Role: React Native mobile app + landing page
│   ├── Start: Jan 24, 2026
│   └── Urgency: CRITICAL
│
├── Designer/UI-UX (1 FTE)
│   ├── Role: Design system, app UI, album templates
│   ├── Start: Jan 22, 2026
│   └── Urgency: HIGH (before dev starts)
│
└── Operations Manager (1 Part-Time / Contractor)
    ├── Role: Marketing, beta coordination, printer liaison
    ├── Start: Feb 1, 2026
    └── Urgency: MEDIUM (can overlap with dev)

Total Team: 4 people
Total Cost (monthly): ₺115,000 - ₺130,000
Break-even (subscribers needed): 115-130 at ₺999/year (annualized)
```

---

## 2. Backend Engineer

### Job Description

**Position:** Full-Stack Backend Engineer (Node.js + TypeScript)

**Location:** Remote (Turkey preferred for timezone)

**Salary:** ₺35,000 - ₺40,000/month

**Contract Type:** Full-time, 3-month initial (renewable)

**Start Date:** January 24, 2026

---

### Responsibilities

**Core Development (70%)**
- Build REST API using Node.js + Express + TypeScript
- Design and implement PostgreSQL database schema
- Implement authentication (Firebase + JWT)
- Integrate payment processing (Stripe + İyzico)
- Setup AWS S3 for photo storage and CloudFront CDN
- Deploy to Railway.app with CI/CD pipeline
- Optimize API performance (target <500ms response time)

**Infrastructure & DevOps (20%)**
- Setup GitHub Actions for automated testing and deployment
- Configure monitoring (Sentry, DataDog, UptimeRobot)
- Implement database backups (daily full + 6-hourly incremental)
- Setup staging environment for testing
- Document API and deployment procedures
- Monitor production health and logs

**Testing & Documentation (10%)**
- Write unit tests (Jest) targeting 85%+ coverage
- Create API documentation (OpenAPI/Swagger)
- Document database schema and migrations
- Write runbooks for common operations

---

### Required Skills

✅ **Required (Must-Have)**
```
├── 3+ years Node.js production experience
├── TypeScript (intermediate+)
├── PostgreSQL (schema design, optimization)
├── RESTful API design
├── JWT authentication & OAuth
├── Docker & containerization basics
├── Git & GitHub workflow
├── Linux/Unix command line
└── Firebase Admin SDK experience
```

✅ **Highly Desired**
```
├── AWS services (S3, CloudFront, RDS)
├── Stripe payment integration
├── React Native backend integration
├── Database optimization & query planning
├── Message queues (Bull, RabbitMQ)
├── GraphQL (bonus)
└── 0-1 scale startup experience
```

---

### Technical Evaluation

**Screening (30 min)**
```
1. Confirm required experience (Node.js, TypeSQL, PostgreSQL)
2. Ask about scaling challenges (database optimization)
3. Ask about payment integration (Stripe)
4. Understanding of mobile backend requirements
5. Availability (can start Jan 24?)
```

**Technical Interview (90 min)**
```
1. Design API endpoint: POST /photos/upload
   ├── Request/response format
   ├── Error handling
   ├── Authentication
   └── Rate limiting

2. Database design: Design photo table
   ├── Columns and types
   ├── Indexes for performance
   ├── EXIF metadata storage
   └── Soft delete strategy

3. Infrastructure: How would you deploy to production?
   ├── CI/CD pipeline (GitHub Actions)
   ├── Environment variables management
   ├── Database migrations
   └── Zero-downtime deployments

4. Optimization: How to optimize timeline endpoint?
   ├── Pagination strategy
   ├── Query optimization
   ├── Caching strategy
   └── Response time target (<500ms)
```

**Take-Home Assignment (4-6 hours)**
```
Build a simple Node.js API with:
├── Authentication (JWT)
├── PostgreSQL database
├── CRUD endpoints for photos
├── Error handling
├── Unit tests (Jest)
└── API documentation

Evaluation criteria:
├── Code quality and organization
├── Error handling and edge cases
├── Test coverage
├── Documentation clarity
└── Performance considerations
```

---

### Onboarding Plan (Week 1)

```
Day 1 (Monday)
├── Welcome & company context
├── Product demo and strategy discussion
├── Tech stack overview (TECH-STACK.md)
├── Development environment setup
└── Git repository access

Day 2 (Tuesday)
├── API architecture deep dive (API-DOCUMENTATION.md)
├── Database schema review (DATABASE-SCHEMA.md)
├── AWS/Railway setup walkthrough
└── S3 permissions and presigned URL strategy

Day 3 (Wednesday)
├── Authentication implementation (Firebase + JWT)
├── Payment integration setup (Stripe test mode)
├── First task: POST /auth/signup endpoint
└── Code review with lead (if applicable)

Day 4 (Thursday)
├── Frontend engineer pairing session
├── Mobile API requirements discussion
├── Offline sync requirements
└── Testing strategy review (QA-TESTING-PLAN.md)

Day 5 (Friday)
├── Deploy to staging
├── Run full test suite
├── Team standup & weekly planning
└── Submit 2-3 endpoints for code review
```

---

### Deliverables (4-Week Timeline)

```
Week 1 (Jan 24-30)
├── Development environment setup
├── Auth system (signup, login, logout, refresh)
├── Database schema deployed to staging
└── 30% done

Week 2 (Jan 31-Feb 6)
├── Photo upload + EXIF extraction
├── Photo timeline endpoint with pagination
├── Tags system (CRUD)
├── 60% done

Week 3 (Feb 7-13)
├── Family sharing invitations
├── Subscription management (Stripe integration)
├── Album finalization endpoint
├── Notifications infrastructure
└── 80% done

Week 4 (Feb 14-20)
├── Performance optimization & testing
├── API documentation finalization
├── Staging environment validation
├── Production deployment checklist
└── 100% done

Feb 21-31: Integration testing + bug fixes
```

---

## 3. Frontend Engineer

### Job Description

**Position:** Frontend Engineer (React Native + Next.js)

**Location:** Remote (Turkey preferred)

**Salary:** ₺35,000 - ₺40,000/month

**Contract Type:** Full-time, 3-month initial (renewable)

**Start Date:** January 24, 2026

---

### Responsibilities

**Mobile App Development (60%)**
- Build React Native app using Expo (iOS + Android)
- Implement UI components using React Native Paper
- Photo upload and editing features
- Timeline view with infinite scroll
- Offline-first synchronization
- Push notifications integration
- Album customization interface
- Local SQLite database management

**Web Landing Page (20%)**
- Build minimal Next.js landing page (no app features)
- Email capture form
- Responsive design (mobile-first)
- SEO optimization
- Analytics integration (Segment)
- Performance optimization (<3s load time)

**Testing & Documentation (20%)**
- Write integration tests (Jest + React Native Testing Library)
- E2E tests using Detox
- Performance optimization and debugging
- Create component documentation
- Browser/device testing (iOS + Android)

---

### Required Skills

✅ **Required (Must-Have)**
```
├── 3+ years React experience
├── React Native (2+ years)
├── TypeScript (intermediate+)
├── Next.js or similar SSR framework
├── Responsive design & CSS
├── REST API integration
├── Git & GitHub workflow
├── Testing frameworks (Jest, React Testing Library)
└── Mobile app deployment (App Store, Play Store)
```

✅ **Highly Desired**
```
├── Expo (React Native with batteries included)
├── React Native Paper (Material Design)
├── Redux or Zustand state management
├── React Query for server state
├── Figma to code workflow
├── Firebase integration
├── Stripe payment UI
├── Offline-first app architecture
└── 0-1 startup experience
```

---

### Technical Evaluation

**Screening (30 min)**
```
1. Confirm React Native experience (2+ years)
2. Ask about complex UI implementations
3. State management approach
4. API integration experience
5. Mobile app deployment experience
```

**Technical Interview (90 min)**
```
1. Implement React component: PhotoTimeline
   ├── Infinite scroll / pagination
   ├── Offline support
   ├── Loading states
   └── Error handling

2. React Native specific: How to handle offline sync?
   ├── Local SQLite storage
   ├── Sync queue
   ├── Conflict resolution
   └── Battery optimization

3. Performance: Optimize a slow photo grid
   ├── FlatList optimization
   ├── Image loading strategy
   ├── Memory management
   └── Frame rate profiling

4. State management: Design photo state flow
   ├── Async actions (upload)
   ├── Optimistic updates
   ├── Error recovery
   └── Offline handling
```

**Take-Home Assignment (4-6 hours)**
```
Build a React Native screen:
├── Display photo grid with thumbnails
├── Pull-to-refresh functionality
├── Add to favorites interaction
├── Offline support
├── Unit tests
└── Performance optimized

Evaluation criteria:
├── Code quality and organization
├── Component reusability
├── State management patterns
├── Accessibility (a11y)
├── Performance (60fps)
└── Error handling
```

---

### Onboarding Plan (Week 1)

```
Day 1 (Monday)
├── Welcome & company context
├── Product demo and vision
├── Tech stack overview (TECH-STACK.md, MOBILE-APP-GUIDE.md)
├── Development environment setup
└── Expo setup and testing

Day 2 (Tuesday)
├── Mobile app architecture deep dive
├── Design system review (DESIGN-SYSTEM.md)
├── API documentation walkthrough (API-DOCUMENTATION.md)
├── Component library planning
└── Figma design system access

Day 3 (Wednesday)
├── Backend engineer pairing session
├── API integration patterns
├── Authentication flow implementation
├── Testing strategy (Detox setup)
└── First components: Login screen

Day 4 (Thursday)
├── Photo upload implementation
├── Offline sync architecture
├── SQLite local database setup
└── Push notifications testing

Day 5 (Friday)
├── Deploy test build to TestFlight/Play Store
├── Run full test suite
├── Team standup & weekly planning
└── Code review of initial components
```

---

### Deliverables (4-Week Timeline)

```
Week 1 (Jan 24-30)
├── Project setup (Expo, navigation, routing)
├── Design system implementation (React Native Paper)
├── Authentication screens (login, signup)
├── Local SQLite database setup
└── 25% done

Week 2 (Jan 31-Feb 6)
├── Photo upload + EXIF handling
├── Photo timeline view with pagination
├── Offline sync mechanism
├── Push notification setup
└── 55% done

Week 3 (Feb 7-13)
├── Family sharing screens
├── Album customization interface
├── Subscription management UI
├── Milestone notifications
└── 80% done

Week 4 (Feb 14-20)
├── Performance optimization
├── Comprehensive testing (unit + E2E)
├── TestFlight/Play Store deployment
├── Landing page web completion
└── 100% done

Feb 21-31: Bug fixes + beta refinement
```

---

## 4. Designer (UI/UX)

### Job Description

**Position:** UI/UX Designer (Product Design)

**Location:** Remote (flexible timezone)

**Salary:** ₺30,000/month OR ₺200-300/hour (contractor)

**Contract Type:** Full-time OR Part-time contractor, 8-week

**Start Date:** January 22, 2026

---

### Responsibilities

**Design System (40%)**
- Create Figma component library
- Define colors, typography, spacing, shadows
- Design 10 iOS + Android safe variants
- Create reusable components for dev team
- Document design specifications
- Accessibility compliance review

**App UI Design (40%)**
- Design all app screens (10-15 screens)
- Photo timeline and editor interfaces
- Album customization and preview
- Family sharing and subscription flows
- Onboarding flow (6 screens)
- Push notification designs

**Album Templates (20%)**
- Design 10 album cover variants
- Interior page layouts (multi-page)
- Photo grid arrangements
- Typography and spacing for print
- Annotation and caption placement
- Print specifications (bleed, safe area)

---

### Required Skills

✅ **Required (Must-Have)**
```
├── 3+ years product design experience
├── Figma (expert level)
├── iOS + Android design patterns
├── Responsive design thinking
├── Typography & color theory
├── Interactive prototyping
├── Design system creation
└── User-centered design mindset
```

✅ **Highly Desired**
```
├── Mobile app design (2+ apps shipped)
├── React Native component design
├── Design-to-code workflow
├── Accessibility (WCAG 2.1)
├── Animation & interaction design
├── Emotional design & UX copywriting
├── Print design experience
└── Design tokens & CSS knowledge
```

---

### Technical Evaluation

**Portfolio Review**
```
Look for:
├── Mobile-first thinking
├── Consistency across screens
├── Accessibility considerations
├── Clear information hierarchy
├── Emotional/empathetic design
└── Attention to detail (spacing, alignment)
```

**Design Interview (60 min)**
```
1. Design critique: Show existing app
   ├── What's working?
   ├── What's confusing?
   ├── How would you improve?
   └── Mobile-first considerations?

2. Design task: Sketch photo upload screen
   ├── Key elements to include?
   ├── How to guide user?
   ├── Error states?
   └── Success feedback?

3. Design system: What's the approach?
   ├── Component structure?
   ├── Figma organization?
   ├── Documentation strategy?
   └── Developer handoff process?
```

**Design Exercise (4 hours)**
```
Task: Design onboarding screens (3 screens)
├── Welcome screen
├── Signup form
├── Phone number verification

Requirements:
├── Mobile-first (375px width)
├── Emotional/warm tone
├── Clear CTA buttons
├── Error states
├── Accessibility (contrast, sizing)
└── Ready for developer handoff (with specs)

Evaluation:
├── Visual hierarchy
├── Emotional resonance
├── Usability
├── Attention to detail
└── Developer collaboration mindset
```

---

### Onboarding Plan (Week 1)

```
Day 1 (Monday)
├── Welcome & product vision presentation
├── Competitive analysis (FamilyAlbum, Tinybeans)
├── User persona deep dive (Elif, Murat & Ayşe)
├── Product strategy overview
└── Timeline and MVP scope

Day 2 (Tuesday)
├── Design system requirements (DESIGN-SYSTEM.md)
├── Mobile app flow walkthrough (wireframes)
├── Album design specifications
├── Reference design system audit
└── Figma workspace setup

Day 3 (Wednesday)
├── Create design tokens in Figma
├── Build base component library
├── Typography system setup
├── Color and shadow systems
└── Create iOS safe area guidelines

Day 4 (Thursday)
├── Start app screen designs
├── Photography and onboarding screens
├── Album templates exploration
├── Feedback and iteration
└── Design critique with team

Day 5 (Friday)
├── Design system documentation
├── Handoff preparation for frontend eng
├── Review accessibility standards
├── Team standup & next week planning
└── Figma sharing and annotation tips
```

---

### Deliverables (8-Week Timeline)

```
Week 1 (Jan 22-28)
├── Design system setup (colors, typography, spacing)
├── Base components in Figma (buttons, inputs, cards)
├── Design tokens documentation
├── Accessibility review
└── 20% done

Week 2 (Jan 29-Feb 4)
├── All app screens wireframes (low-fidelity)
├── High-fidelity designs for critical flows
├── Album template sketches (3 variants)
├── Component refinement
└── 40% done

Week 3 (Feb 5-11)
├── Complete high-fidelity app designs
├── 10 album template designs (with specs)
├── Handoff documentation for frontend
├── Accessibility audit (WCAG 2.1)
└── 65% done

Week 4 (Feb 12-18)
├── Design iteration based on dev feedback
├── Animation and interaction specs
├── Print specifications for albums
├── Landing page design (desktop)
└── 85% done

Week 5-8 (Feb 19-Mar 18)
├── Polish and refinement
├── QA testing on device
├── Feedback incorporation
├── Design documentation finalization
└── 100% done

Continuous: Design review with dev, feedback incorporation
```

---

## 5. Operations Manager (Part-Time/Contractor)

### Job Description

**Position:** Operations Manager / Growth Manager

**Location:** Remote (Turkey, overlapping hours preferred)

**Salary:** ₺20,000 - ₺25,000/month OR ₺150-200/hour

**Contract Type:** Part-time (20-30 hours/week), 3-month initial

**Start Date:** February 1, 2026

---

### Responsibilities

**Marketing & Beta (50%)**
- Execute beta waitlist strategy (email, ads, content)
- Manage influencer outreach (parenting accounts)
- Create social content and community management
- Monitor beta feedback and feature requests
- Manage beta user groups (Discord, WhatsApp)
- Create case studies from beta users

**Operations (30%)**
- Printer logistics coordination (Mega Print)
- Album order fulfillment tracking
- Customer support (email, chat)
- Subscription management troubleshooting
- User onboarding and tutorial creation
- Analytics monitoring and reporting

**Product Support (20%)**
- Collect user feedback from beta testers
- Bug reporting and prioritization
- Feature request organization
- Help docs and FAQ creation
- Onboarding email sequence setup

---

### Required Skills

✅ **Required (Must-Have)**
```
├── 2+ years operations/growth/marketing
├── SaaS experience (ideal)
├── User research and feedback collection
├── Project management and tracking
├── Analytics basics (Segment, Mixpanel)
├── Email marketing tools (Sendgrid, Mailchimp)
├── Social media management
├── Turkish language (native)
└── Communication skills
```

✅ **Highly Desired**
```
├── Startup 0-1 experience
├── Community management
├── Content creation
├── Influencer relationship building
├── Logistics coordination
├── Customer success experience
├── Product-market fit validation
└── Growth hacking mindset
```

---

### Onboarding Plan (Week 1)

```
Day 1 (Monday)
├── Welcome & company context
├── Product demo and market positioning
├── Beta strategy overview (BETA-WAITLIST-STRATEGY.md)
├── Marketing plan review
└── Success metrics and KPIs

Day 2 (Tuesday)
├── Printer logistics deep dive
├── Album fulfillment process
├── Vendor relationships (Mega Print)
├── Backup plan (Ofset Basım)
└── Timeline and volume projections

Day 3 (Wednesday)
├── Marketing tools setup (email, analytics)
├── Influencer list review
├── Social media account access
├── Content calendar planning
└── Beta user database setup

Day 4 (Thursday)
├── Customer support infrastructure
├── FAQ and help docs creation
├── Onboarding email sequence setup
├── Discord/WhatsApp community setup
└── First content creation

Day 5 (Friday)
├── Analytics dashboard setup
├── KPI tracking and reporting
├── Team standup & weekly planning
└── Next week priorities
```

---

### Deliverables (3-Month Timeline)

```
Feb 1-28: Setup & Planning
├── Operations infrastructure ready
├── Marketing tools configured
├── Influencer outreach campaign live
├── Beta user recruitment campaign started
├── Customer support processes documented
└── 25% done

Mar 1-20: Execution & Testing
├── 100+ beta users recruited
├── Influencer partnerships active
├── Beta feedback system operational
├── Album orders fulfilled
├── Customer support tickets tracked
└── 75% done

Mar 21-31: Optimization & Scale
├── Beta feedback analyzed and prioritized
├── Marketing ROI measured and optimized
├── Fulfillment process refined
├── Launch readiness verified
├── Go-live checklist completed
└── 100% done
```

---

## 6. Founder/CEO Responsibilities (You)

```
Jan 17-24 (Week 1): Pre-team Phase
├── Finalize product strategy and roadmap
├── Prepare hiring documentation
├── Setup company basics (legal, banking)
├── Close printer partnership (Mega Print)
├── Validate pricing with target users
└── 10 hours/day

Jan 24-Feb 20 (Weeks 2-4): Building Phase
├── Daily standup with team
├── Code review and architectural decisions
├── Design feedback and approval
├── Customer development interviews
├── Seed investor outreach (passive)
└── 12 hours/day

Feb 21-Mar 31 (Weeks 5-8): Beta Launch Phase
├── Beta coordination and feedback synthesis
├── Press and influencer outreach
├── Feature prioritization and roadmap adjustments
├── Investor pitching and fundraising
├── Customer support and user interviews
└── 14 hours/day (startup intensity)

Key Focus Areas:
├── Product-market fit validation
├── Unit economics verification
├── Team culture and velocity
├── Investor relations
└── Long-term vision and sustainability
```

---

## 7. Salary & Budget Summary

```
Monthly Salaries (MVP Phase: Jan-Mar)
├── Backend Engineer: ₺35,000 - ₺40,000
├── Frontend Engineer: ₺35,000 - ₺40,000
├── Designer (full-time): ₺30,000
├── Operations Manager (part-time): ₺12,500 - ₺20,000
└── Total: ₺112,500 - ₺130,000/month

Additional Costs (Jan-Mar)
├── AWS/Railway hosting: ₺5,000 - ₺7,500/month
├── Software licenses (Figma, etc): ₺2,000/month
├── Marketing & ads: ₺10,000 - ₺15,000/month
├── Contingency (15%): ₺15,000 - ₺20,000/month
└── Total ops: ₺32,000 - ₺42,500/month

Total Monthly Burn: ₺144,500 - ₺172,500
Total 3-Month Burn: ₺433,500 - ₺517,500

Runway Needed: ₺500,000 - ₺600,000
Funding Target: $100,000 - $150,000 USD (SAFE note)
```

---

## 8. Hiring Timeline

```
Jan 17 (Today)
├── Publish job postings
├── Reach out to networks
└── Begin screening

Jan 18-20
├── Phone screening phase
├── Technical interview scheduling
└── 20-30 candidates per role

Jan 21-22
├── Technical interviews
├── Take-home assignments
└── Final round interviews

Jan 23
├── Offers extended
├── Negotiations complete
└── Start date confirmations

Jan 24
├── Backend engineer starts
├── Frontend engineer starts
├── Onboarding begins
└── Product development kicks off

Jan 22 (Earlier)
├── Designer onboarding (earlier start)
└── Design system development begins

Feb 1
├── Operations manager starts
└── Marketing and beta launch prep

---

## 9. Where to Post Jobs

✅ **Recommended Platforms**
```
├── LinkedIn (Job posting feature)
├── AngelList (for startups)
├── Tech communities (Dev.to, HackerNews)
├── Turkish tech channels (Teknolojiokusu, SliceOfCode)
├── Referrals from network (FASTEST + BEST)
├── Upwork / Toptal (contractor backup)
└── Direct outreach to portfolio/GitHub profiles
```

**Estimated Response Rate**
```
├── Job posting: 50-100 applications/week
├── Qualified candidates: 10-20%
├── Screened candidates: 20-30
├── Technical interview: 8-10
├── Offers: 1-2/role
```

---

## 10. Candidate Evaluation Matrix

```
Technical Skills: 40 points
├── Required experience (15 points)
├── Technology proficiency (15 points)
├── Problem-solving approach (10 points)

Soft Skills: 30 points
├── Communication clarity (10 points)
├── Teamwork and collaboration (10 points)
├── Ownership mindset (10 points)

Startup Fit: 20 points
├── Adaptability and flexibility (10 points)
├── Learning ability (5 points)
├── Passion for mission (5 points)

Culture Fit: 10 points
├── Alignment with values (10 points)

Minimum Passing Score: 70/100
Target Score: 80+/100
```

---

## 11. Post-MVP Team Expansion

```
After Q1 (April onwards):
├── Growth Manager: Full-time, ₺35,000/month
├── 2nd Frontend Engineer: Full-time, ₺35,000/month (React web)
├── Customer Support Lead: Part-time, ₺20,000/month
├── Data Analyst: Part-time, ₺25,000/month

After Series A (Q3):
├── VP Engineering (founding engineer promoted or external hire)
├── Product Manager: Full-time, ₺45,000/month
├── Community Manager: Full-time, ₺30,000/month
├── Designer 2: Full-time, ₺30,000/month
└── Total team: 10-12 people
```

---

**Status**: ✅ Hiring plan complete, ready to post jobs Jan 17
