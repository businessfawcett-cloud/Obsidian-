# Skora — Known Issues & TODOs

## Current Issues

### 1. Loading Skeletons
- **Status:** Missing on some pages
- **Priority:** Medium
- **Impact:** UX polish

### 2. College Logo Fetch
- **Status:** May fail for some schools
- **Workaround:** Falls back to initials
- **Priority:** Low

---

## Resolved Issues

### ~~No Automated Tests~~
- **Resolution:** Playwright E2E tests added
- **Date:** June 2026

### ~~Limited Error Boundaries~~
- **Resolution:** Sentry now monitors errors
- **Date:** May 2026

### ~~Sentry Integration~~
- **Resolution:** Production error tracking live
- **Date:** May 2026

---

## TODOs

### Q3 2026
- [ ] Deploy tracking pixel to Vercel
- [ ] Configure GTM with 8 conversion events
- [ ] Add IndexNow API key
- [ ] Fix E2E test login flow
- [ ] Add payment tracking events (payment_started, payment_completed)

### Q4 2026
- [ ] Student-facing free tool (MVP)
- [ ] College matching algorithm
- [ ] Acceptance chances calculator
- [ ] AI essay feedback (Harvard rubric)
- [ ] Counselor portal (B2B)
- [ ] White-label dashboard
- [ ] Student management
- [ ] 3x capacity workflow
- [ ] Pilot_2026 launch (10 counselors)
- [ ] First paid conversions

### 2027
- [ ] Series A preparation
- [ ] Team expansion (engineering, sales, CS)
- [ ] Enterprise features (SSO, SOC2)
- [ ] International expansion

---

## Success Criteria

### Before Soft Launch
- [ ] All 10 E2E tests pass
- [ ] API key moved to environment variable
- [ ] Payment flow verified end-to-end manually
- [ ] `payment_started` and `payment_completed` events tracked

### After Soft Launch (2 weeks)
| Metric | Goal |
|--------|------|
| Onboarding completion | >50% |
| Payment rate (of completers) | >5% |
| Day 2 retention | >20% |
| Error rate | <1% |

### Before Scaling Paid Ads
| Metric | Minimum |
|--------|---------|
| CAC | <$50/user |
| LTV | >$200 |
| Payback period | <6 months |
| Day 30 retention | >5% |

---

*Last updated: July 19, 2026*
