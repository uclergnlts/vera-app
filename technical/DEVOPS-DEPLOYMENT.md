# 🚀 DevOps & Deployment Guide

## Infrastructure Overview

```
Production Environment:

┌─────────────────────────────────────────────────────────┐
│                    USERS (iOS + Android)                 │
└────────────────────────┬────────────────────────────────┘
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
   (React Native)   (Web Landing)    (Third Parties)
   Expo App Store   Vercel/CDN       Stripe/AWS/etc
        │                │                │
        └────────────────┼────────────────┘
                         │
                    ┌────▼────┐
                    │ Cloudflare
                    │ (DNS, DDoS)
                    └────┬────┘
                         │
    ┌────────────────────┼────────────────────┐
    │                    │                    │
    ▼                    ▼                    ▼
┌────────────┐   ┌────────────┐       ┌───────────┐
│ App Store  │   │ Google     │       │ Web App   │
│ (iOS)      │   │ Play       │       │ (Next.js) │
│ TestFlight │   │ (Android)  │       │ Vercel    │
└────────────┘   └────────────┘       └───────────┘
                                            │
    ┌───────────────────────────────────────┼───────────────────────────────────┐
    │                                       │                                   │
    ▼                                       ▼                                   ▼
┌─────────────────────┐         ┌────────────────────┐         ┌──────────────────┐
│  Backend (Node.js)  │         │  Database          │         │  Storage (S3)    │
│  Railway.app        │         │  PostgreSQL        │         │  AWS             │
│  - API servers      │         │  Railway.app       │         │  CloudFront      │
│  - Workers          │◄────────┤  - Main            │         │  CDN             │
│  - Cron jobs        │         │  - Read replica    │         │                  │
│  - Stripe webhooks  │         │  - Backup          │         │  Photos & files  │
│                     │         │                    │         │                  │
│  Auto-scaling:      │         │  Encryption:       │         │  Encryption:     │
│  1-10 dynos         │         │  AES-256 at rest   │         │  AES-256 at rest │
│  Memory: 512MB-1GB  │         │  TLS in transit    │         │  HTTPS only      │
└─────────────────────┘         └────────────────────┘         └──────────────────┘
        │                               │                              │
        └───────────────────┬───────────┴──────────────────┬───────────┘
                            │                              │
                    ┌───────▼──────────┐         ┌────────▼─────────┐
                    │ Monitoring       │         │ Analytics        │
                    │ - Sentry         │         │ - Mixpanel       │
                    │ - LogRocket      │         │ - Google Analytics
                    │ - Uptime Robot   │         │ - DataDog (logs) │
                    └──────────────────┘         └──────────────────┘
```

---

## Deployment Pipeline

### Git Workflow

```
Local development (feature branch)
    │
    ▼
Create pull request
    │
    ├─ Automated tests run (GitHub Actions)
    │  ├─ Jest (unit tests)
    │  ├─ ESLint (code quality)
    │  ├─ TypeScript check
    │  └─ Security scan (Snyk)
    │
    ├─ Code review (1 approval)
    │
    ▼
Merge to main
    │
    ├─ Staging deployment (automatic)
    │  └─ Railway: staging.vera.app
    │     └─ Run smoke tests
    │        └─ If OK, ready for production
    │
    ▼
Tag release (v1.0.1)
    │
    ├─ Production deployment (automatic)
    │  ├─ Backend (Railway: api.vera.app)
    │  ├─ Web (Vercel: vera.app)
    │  └─ Database migration (if needed)
    │
    ├─ Post-deployment checks
    │  ├─ Health check: GET /health (200 OK?)
    │  ├─ Smoke test: Critical flows work?
    │  └─ Monitoring: No error spikes?
    │
    ▼
Deployment complete
    │
    ├─ Slack notification
    ├─ Changelog update
    └─ Release notes published
```

### GitHub Actions CI/CD

```yaml
# .github/workflows/deploy.yml

name: Deploy

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run tests
        run: npm test -- --coverage
      
      - name: Upload coverage
        uses: codecov/codecov-action@v3
      
      - name: Lint
        run: npm run lint
      
      - name: TypeScript check
        run: npm run type-check
      
      - name: Security scan
        run: npx snyk test --severity-threshold=high

  deploy-staging:
    needs: test
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Deploy to Railway (staging)
        env:
          RAILWAY_TOKEN: ${{ secrets.RAILWAY_TOKEN }}
        run: |
          npm install -g @railway/cli
          railway up --environment staging
      
      - name: Run smoke tests
        run: npm run test:smoke
      
      - name: Notify Slack
        uses: slackapi/slack-github-action@v1
        with:
          webhook-url: ${{ secrets.SLACK_WEBHOOK }}
          payload: |
            {
              "text": "✅ Staging deployed (commit: ${{ github.sha }})"
            }

  deploy-production:
    needs: [test, deploy-staging]
    if: github.event_name == 'push' && startsWith(github.ref, 'refs/tags/v')
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Deploy to Railway (production)
        env:
          RAILWAY_TOKEN: ${{ secrets.RAILWAY_TOKEN }}
        run: |
          npm install -g @railway/cli
          railway up --environment production
      
      - name: Run health checks
        run: curl -f https://api.vera.app/health || exit 1
      
      - name: Database migration
        env:
          DATABASE_URL: ${{ secrets.DATABASE_URL_PROD }}
        run: npm run migrate:prod
      
      - name: Notify team
        uses: slackapi/slack-github-action@v1
        with:
          webhook-url: ${{ secrets.SLACK_WEBHOOK }}
          payload: |
            {
              "text": "🚀 Production deployed: v${{ github.ref_name }}"
            }
```

---

## Backend Deployment (Railway)

### Railway Configuration

```yaml
# railway.toml (at root)

[build]
builder = "nixpacks"
buildCommand = "npm ci && npm run build"
startCommand = "node dist/index.js"

[environment]
NODE_ENV = "production"
PORT = "8080"

# Secrets (configured via Railway dashboard):
DATABASE_URL = "postgresql://..."
STRIPE_SECRET_KEY = "sk_live_..."
AWS_ACCESS_KEY_ID = "..."
REDIS_URL = "redis://..."
```

### Environment Variables

```bash
# .env.production (Railway dashboard)

NODE_ENV=production
PORT=8080

# Database
DATABASE_URL=postgresql://user:pass@host:5432/vera

# Authentication
FIREBASE_PROJECT_ID=vera-prod
FIREBASE_PRIVATE_KEY=...
JWT_SECRET=<random 64 char string>

# AWS S3
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...
AWS_REGION=eu-west-1
S3_BUCKET=vera-prod-photos

# Payments
STRIPE_SECRET_KEY=sk_live_...
STRIPE_WEBHOOK_SECRET=whsec_...

# Email
MAILCHIMP_API_KEY=...
MAILCHIMP_LIST_ID=...

# Monitoring
SENTRY_DSN=https://...
DATADOG_API_KEY=...

# External APIs
EXPO_ACCESS_TOKEN=... (for push notifications)
```

### Health Check Endpoint

```typescript
// src/routes/health.ts

app.get('/health', (req, res) => {
  const health = {
    status: 'ok',
    timestamp: new Date(),
    uptime: process.uptime(),
    checks: {
      database: 'checking...',
      redis: 'checking...',
      s3: 'checking...'
    }
  };

  // Quick DB check
  db.query('SELECT 1')
    .then(() => health.checks.database = 'ok')
    .catch(e => health.checks.database = `error: ${e.message}`);

  // Quick Redis check
  redis.ping()
    .then(() => health.checks.redis = 'ok')
    .catch(e => health.checks.redis = `error: ${e.message}`);

  // Quick S3 check
  s3.headBucket({ Bucket: process.env.S3_BUCKET })
    .promise()
    .then(() => health.checks.s3 = 'ok')
    .catch(e => health.checks.s3 = `error: ${e.message}`);

  const allOk = Object.values(health.checks).every(v => v === 'ok');
  res.status(allOk ? 200 : 503).json(health);
});
```

---

## Web Deployment (Vercel)

### Vercel Configuration

```json
// vercel.json

{
  "buildCommand": "npm run build",
  "outputDirectory": ".next",
  "env": {
    "NEXT_PUBLIC_API_URL": "@api_url",
    "STRIPE_PUBLIC_KEY": "@stripe_public_key"
  }
}
```

### Automatic Deployments

```
GitHub push → Vercel auto-builds
    ├─ Staging: Every commit to 'staging' branch
    └─ Production: Every commit to 'main' branch

Preview URLs: https://vera-git-{branch}.vercel.app
Production: https://vera.app
```

---

## Database Backup & Recovery

### Automated Backups (Railway)

```
Daily backups:
├─ Full backup: 1:00 AM UTC
├─ Incremental: Every 6 hours
├─ Retention: 30 days
├─ Encryption: AES-256
└─ Location: AWS S3 (separate region)

Point-in-time recovery:
├─ Available: Last 7 days
├─ Recovery time: <1 minute
└─ Data loss: <1 minute
```

### Manual Backup

```bash
# Backup to file
pg_dump postgresql://user:pass@host/vera > backup.sql

# Restore from file
psql postgresql://user:pass@host/vera < backup.sql

# Test restore (on staging)
psql postgresql://staging-user:pass@staging-host/vera < backup.sql
```

---

## Monitoring & Alerts

### Sentry (Error Tracking)

```typescript
// src/index.ts

import * as Sentry from "@sentry/node";

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  environment: process.env.NODE_ENV,
  tracesSampleRate: 0.1,
  integrations: [
    new Sentry.Integrations.Http({ tracing: true }),
    new Sentry.Integrations.OnUncaughtException(),
    new Sentry.Integrations.OnUnhandledRejection(),
  ],
});

app.use(Sentry.Handlers.requestHandler());
app.use(Sentry.Handlers.errorHandler());

// Errors automatically sent to Sentry
```

**Alerts configured:**
- ❌ Error rate spike (>5 errors/min)
- ❌ Unhandled exceptions (immediate)
- ⚠️ Performance degradation (p95 >1s)

### DataDog (Logs + APM)

```typescript
// APM tracing
import tracer from 'dd-trace';

tracer.init();

// Structured logging
const logger = require('pino');
logger.info({ userId: '123', action: 'photo_upload' });
```

### Uptime Monitoring

```
UptimeRobot checks:
├─ API health: Every 5 minutes
├─ Web site: Every 5 minutes
├─ Stripe webhook: Every 1 hour
└─ Database: Every 10 minutes

Alert on downtime: >5 min = immediate Slack
```

---

## Scaling Strategy

### Auto-scaling

```
Railway dynos (backend):

Load                    Dynos required
0-100 req/s            1 (512MB)
100-500 req/s          2 (512MB each)
500-1000 req/s         3-5 (1GB each)
1000+ req/s            Scale + load balance

Manual scaling triggers:
└─ Performance tests show needed
```

### Database Scaling

```
PostgreSQL growth:

Current (Year 1):   1000 users × 100 photos = 100K photos
Space needed:       ~10GB (with backups)
→ Standard 10GB instance (Railway)

Year 2:             5000 users × 500 photos = 2.5M photos
Space needed:       ~50GB
→ Upgrade to 50GB instance

Year 3+:            Shard by child_id if needed
```

---

## Disaster Recovery Plan

### Failure Scenarios

```
Scenario 1: Database down
├─ RTO: 5 minutes (auto-failover to replica)
├─ RPO: <1 minute (binary logs)
└─ Recovery: Automatic, no action needed

Scenario 2: API server down
├─ RTO: <1 minute (Vercel auto-restart)
├─ RPO: 0 (stateless)
└─ Recovery: Automatic, with notification

Scenario 3: S3 bucket corrupted
├─ RTO: 1 hour (restore from backup)
├─ RPO: <1 day (daily backups)
└─ Recovery: Manual + notification

Scenario 4: Complete data center outage
├─ RTO: <1 hour (redeploy to different region)
├─ RPO: <1 day (daily backups)
└─ Recovery: Manual failover, with team notification
```

---

## Rollback Strategy

### Automatic Rollback

```
If health checks fail post-deploy:
├─ Automatic rollback to previous version
├─ Alert team on Slack
├─ Investigation required before re-deploy
└─ Time: <5 minutes

Manual rollback (if needed):
├─ Railway: Reset to previous release
├─ Vercel: Click "Rollback" button
├─ Database: From backup (if needed)
└─ Verify: Health checks pass
```

---

## Cost Estimation (Year 1)

```
Monthly costs:

Railway Backend:      $500 (1-3 dynos, ~$200/dyno)
Railway Database:     $300 (10GB PostgreSQL)
AWS S3 Storage:       $500 (10TB at $0.05/GB)
AWS CloudFront:       $300 (data transfer)
Vercel Web:           $150 (pro plan)
Stripe Processing:    $600 (2.9% of revenue)
Monitoring:           $200 (Sentry, DataDog, Uptime)
─────────────────
Total:               ~$2,550/month
                     ~$30,600/year

Per-user cost (1000 users):
                     ~$31/year per user
                     ~$2.58/month per user

vs Revenue (999/year pricing):
                     Break-even: 51 users
                     Profitable at: 100+ users
```

---

## Pre-Launch Checklist

- [ ] CI/CD pipeline working (GitHub Actions)
- [ ] Staging environment deployed
- [ ] Production environment configured
- [ ] Database backups automated
- [ ] Monitoring alerts set up
- [ ] Error tracking (Sentry) working
- [ ] Performance monitoring (Datadog) active
- [ ] Uptime monitoring running
- [ ] Disaster recovery plan tested
- [ ] Rollback procedure documented & tested
- [ ] Load testing completed (1000 concurrent users)
- [ ] Security audit passed
- [ ] Cost optimizations implemented

---

**Status**: ✅ Infrastructure ready for MVP launch
