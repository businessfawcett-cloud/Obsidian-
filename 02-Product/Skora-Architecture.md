# Skora — Complete Architecture & Build Log

## Overview

**Skora** (formerly AdmitPath) is an AI-powered college counseling platform. Students get free essay feedback, admission-chance estimates, and college matching. Independent counselors and agencies pay for management tools and white-labeled portals to run their practice.

---

## Business Model: The B2B2C Flywheel

```
More free students → Richer data → Better matching → More valuable counselor tools
    ↑                                                           ↓
    └───────────── More counselors pay → More of their students ─┘
```

### Student Tiers (B2C)
| Plan | Price | Features |
|------|-------|----------|
| Free | $0 | College matching, acceptance chance, basic dashboard, limited AI essay reviews |
| Pro | $19/mo | Unlimited AI essays, AI chat counselor, app tracker, scholarship finder |

### Counselor Tiers (B2B)
| Plan | Price | Features |
|------|-------|----------|
| Basic | $49/mo | Up to 15 students, dashboard, action queue, task management |
| Standard | $99/mo | Up to 40 students, white-labeled portal, priority support |
| Agency | $199/mo | Unlimited students, custom subdomain, dedicated support |

**The Hook:** Students linked to Standard/Agency counselors get free Pro accounts.

---

## Tech Stack

### Core
- **Framework:** Next.js 14 (App Router)
- **Language:** TypeScript
- **Styling:** TailwindCSS
- **Monorepo:** Turborepo + pnpm workspaces

### Authentication
- **Provider:** Clerk (@clerk/nextjs)
- **Roles:** student, counselor, admin
- **Storage:** publicMetadata.role

### Database
- **Provider:** Neon (Postgres)
- **ORM:** Drizzle ORM
- **Tables:** colleges, subscriptions, college_wishlist, counselor_notes, essays, essay_versions, essay_snippets, affiliates, affiliate_conversions

### Payments
- **Provider:** Stripe
- **Integration:** Checkout, Billing Portal, Webhooks
- **Sync:** Clerk metadata + subscriptions table

### AI
- **Provider:** Groq SDK
- **Use Cases:** Essay review, AI chat counselor

### Analytics
- **Provider:** PostHog
- **Error Tracking:** Sentry
- **Events:** Server + Client tracking

### Email
- **Provider:** Resend
- **Webhooks:** Svix

### Validation
- **Library:** Zod

---

## System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    SKORA PLATFORM                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   Students  │    │  Counselors │    │    Admin    │     │
│  │   (B2C)     │    │    (B2B)    │    │             │     │
│  └──────┬──────┘    └──────┬──────┘    └──────┬──────┘     │
│         │                  │                  │             │
│         └──────────────────┼──────────────────┘             │
│                            │                                │
│                    ┌───────▼───────┐                        │
│                    │   Next.js     │                        │
│                    │   App Router  │                        │
│                    └───────┬───────┘                        │
│                            │                                │
│         ┌──────────────────┼──────────────────┐             │
│         │                  │                  │             │
│  ┌──────▼──────┐    ┌──────▼──────┐    ┌──────▼──────┐     │
│  │   Clerk     │    │   Stripe    │    │   Groq AI   │     │
│  │   Auth      │    │   Payments  │    │   Engine    │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│                                                             │
│         ┌──────────────────┼──────────────────┐             │
│         │                  │                  │             │
│  ┌──────▼──────┐    ┌──────▼──────┐    ┌──────▼──────┐     │
│  │   Neon      │    │   PostHog   │    │   Resend    │     │
│  │   Postgres  │    │   Analytics │    │   Email     │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Features Built (Complete List)

### 1. Landing Page (`/`)
- Hero section with value proposition
- Feature highlights (Essay Review, Admission Chancing, College Matching)
- College logo strip (Harvard, Yale, Princeton, Columbia, MIT, Stanford, Penn, Duke, UGA)
- Sign up/Sign in integration with Clerk
- Two-column conversion layout
- Dedicated counselor signup page at `/counselor-signup`

### 2. Authentication System
- Clerk Next.js SDK integration
- Protected routes with SignedIn component
- Role-based access (student, counselor, admin)
- White-label brand support

### 3. User Onboarding (`/onboarding`)
- 5-step profile creation flow:
  - Step 1: Academic stats (GPA, SAT/ACT)
  - Step 2: Target schools
  - Step 3: Intended major
  - Step 4: Early decision preferences
  - Step 5: Completion/save
- White-label brand support in top bar

### 4. Student Dashboard (`/dashboard`)
- College listing with categories:
  - Safety (high chance > 70%)
  - Target (30-70% chance)
  - Reach (< 30% chance)
- Filters: All, Safety, Target, Reach
- Major filters: Top 10, Top 25 programs (US News rankings)
- Sorting: By major rank
- College cards display:
  - Logo/image
  - Name, city, state
  - Category badge
  - Major rank badge (if applicable)
  - Acceptance rate, SAT score, Median GPA
  - Calculated user chance
  - Link to detail page
- Student Action Queue: Bell icon with live notification dropdown

### 5. College Detail (`/college/[id]`)
- Redesigned 3-zone layout: hero header, two-column grid, sticky bottom bar
- Stats comparison bars (dual-bar: grey baseline + orange overlay)
- Program strength display for user's major
- College logo retrieval (Wikipedia API)
- Application links

### 6. Essay System
- **Essay editor (`/essays`):** Redesigned with stages (Brainstorm, Draft, Polishing, Final), word count, save/save version/submit buttons
- **My Essays page (`/my-essays`):** Horizontal cards, stage badges, progress bars, empty state
- **AI Review:** Three-panel review workspace with inline comments, snippets, general comments, Harvard-style personal rating (1-6)
- **AI Feedback API (`/api/essay/review`):** Groq integration, line-by-line suggestions, personalRating prompt, admissions calculator integration

### 7. AI Counselor (`/chat`)
- AI chat interface for college admissions questions
- Plan-gated (Pro upgrade wall for free users)
- Stripe checkout integration

### 8. Explore (`/explore`)
- College discovery with cards, donut chart, scrollable category tabs, search icon
- College detail page (`/explore/[collegeId]`) for direct linking

### 9. Wishlist (`/wishlist`)
- Save colleges to personal wishlist
- Manage saved colleges

### 10. Applications (`/applications`)
- Kanban-style application tracker

### 11. Messages (`/messages`)
- Redesigned with 280px conversation panel, chat area, orange accent, cream bg

### 12. Scholarships (`/scholarships`)
- Redesigned scholarship finder with new visual layout
- Shows real college names

### 13. Schedule (`/schedule`)
- Calendar for deadlines and tasks

### 14. Outcomes (`/outcomes`)
- My Results page showing admission decisions

### 15. Pricing & Subscriptions (`/pricing`)
- Dual-tab (Counselor/Student) pricing page
- Student plans: Free ($0), Pro ($19/mo)
- Counselor plans: Starter ($49/mo), Growth ($99/mo), Agency ($199/mo)
- Stripe Checkout integration for both student and counselor plans
- Affiliate tracking via cookie/referral codes

### 16. Student Billing (`/billing`)
- Current plan display (live from Clerk metadata)
- Plan status badge (active/canceled/past_due)
- Monthly usage stats (essay reviews)
- Manage Subscription button (opens Stripe billing portal)
- Upgrade to Pro button for free users
- Payment method management
- Subscription history table from database

### 17. Counselor Features
- Counselor dashboard (`/counselor`)
- Billing page (`/counselor/billing`) with plan info and Stripe portal
- Settings page (`/counselor/settings`) with plan badge
- Student invitation (`/counselor/invite`) with plan limits
- White-label portal support (`/counselor/whitelabel-setup`)
- Student detail view (`/counselor/student/[id]`)
- Essay review for counselors (`/counselor/essay-review/[essayId]`)

### 18. Stripe Integration
- **Checkout:** `/api/stripe/create-checkout` (counselor), `/api/stripe/student-checkout` (student)
- **Billing Portal:** `/api/stripe/portal` (counselor), `/api/stripe/student-portal` (student)
- **Webhook:** `/api/stripe/webhook` - handles checkout.completed, subscription.updated, subscription.deleted, invoice.payment_failed
- Clerk metadata sync (plan, planStatus, stripeSubscriptionId, stripeCustomerId)
- Email notifications (upgrade confirmation, cancellation, payment failed)

### 19. Analytics
- PostHog integration for event tracking
- Admin analytics dashboard (`/admin/analytics`)
- Server-side tracking (`trackServer`)

### 20. Admin Features
- Admin dashboard (`/admin`)
- Students management (`/admin/students`)
- Counselors management (`/admin/counselors`)
- Affiliates management (`/admin/affiliates`)
- Affiliate detail with per-conversion plan data

### 21. User Profile (`/profile/edit`)
- Profile editor with form fields
- Local storage persistence

### 22. Major Rankings System (`/data/majorRankings.ts`)
- US News rankings for 45+ schools
- Categories: Business, CS, Engineering, Pre-Health, Fine Arts, Law & Politics, Communications, Sciences, Social Sciences, Humanities
- Helper functions: getMajorRank, getMajorRankByName, getMajorRankingsForSchool, formatMajorKey

### 23. College API (`/lib/collegeApi.ts`)
- fetchColleges: Database query to Neon
- calculateUserChance: Admission probability calculation
- determineCategory: Safety/Target/Reach classification
- fetchCollegeLogo: Wikipedia API integration

### 24. Database Integration
- Neon database with Drizzle ORM
- College data from IPEDS/College Scorecard
- Tables: colleges, college_wishlist, subscriptions, counselor_notes, essays, essay_versions, essay_snippets, affiliates, affiliate_conversions

### 25. Additional Features
- Join page (`/join`)
- Support page (`/support`)
- Resend integration for transactional emails
- Svix for webhook management
- Zod for form validation

---

## Multi-Tenancy / White-Label Routing

### Subdomain Routing
- `<slug>.skoraadmit.com` → sets `skora_subdomain` cookie

### Path-Slug Routing (Standard plan)
- `skoraadmit.com/<slug>` → rewritten to `/` with `skora_path_slug` cookie

### Root Page Logic
- Reads cookie, fetches counselor's brand
- Renders branded sign-in screen instead of default marketing homepage
- Cached in `localStorage['skora_brand']`

---

## Pages & Routes (Complete)

| Route | Description | Status |
|-------|-------------|--------|
| `/` | Landing page | ✅ Complete |
| `/sign-in` | Clerk sign in | ✅ Complete |
| `/sign-up` | Clerk sign up | ✅ Complete |
| `/onboarding` | 5-step profile wizard | ✅ Complete |
| `/dashboard` | College recommendations | ✅ Complete |
| `/explore` | College discovery | ✅ Complete |
| `/college/[id]` | College details | ✅ Complete |
| `/applications` | Application tracker | ✅ Complete |
| `/essays` | Essay editor | ✅ Complete |
| `/my-essays` | Manage essays | ✅ Complete |
| `/outcomes` | Admission results | ✅ Complete |
| `/schedule` | Calendar/tasks | ✅ Complete |
| `/chat` | AI Counselor | ✅ Complete |
| `/scholarships` | Scholarship finder | ✅ Complete |
| `/messages` | Messages/inbox | ✅ Complete |
| `/support` | Support page | ✅ Complete |
| `/profile/edit` | Edit profile | ✅ Complete |
| `/billing` | Student billing & subscription | ✅ Complete |
| `/pricing` | Pricing plans | ✅ Complete |
| `/counselor` | Counselor dashboard | ✅ Complete |
| `/counselor/billing` | Counselor billing | ✅ Complete |
| `/counselor/settings` | Counselor settings | ✅ Complete |
| `/counselor/invite` | Invite students | ✅ Complete |
| `/counselor-signup` | Counselor signup | ✅ Complete |
| `/counselor/whitelabel-setup` | White-label config | ✅ Complete |
| `/admin` | Admin dashboard | ✅ Complete |
| `/admin/affiliates` | Affiliate management | ✅ Complete |
| `/terms` | Terms of service | ✅ Complete |
| `/privacy` | Privacy policy | ✅ Complete |
| `/cookies` | Cookie policy | ✅ Complete |
| `/api/essay/review` | AI essay review | ✅ Complete |
| `/api/stripe/*` | Stripe integration | ✅ Complete |
| `/api/student/*` | Student API routes | ✅ Complete |
| `/admin/analytics` | Analytics dashboard | ✅ Complete |
| `/admin/students` | Student management | ✅ Complete |
| `/admin/counselors` | Counselor management | ✅ Complete |
| `/admin/affiliates/[code]` | Affiliate detail | ✅ Complete |
| `/join` | Join page | ✅ Complete |
| `/pricing/student` | Student pricing (alt) | ✅ Complete |
| `/wishlist` | College wishlist | ✅ Complete |
| `/explore/[collegeId]` | Explore detail | ✅ Complete |
| `/counselor/student/[id]` | Student detail view | ✅ Complete |
| `/counselor/essay-review/[essayId]` | Essay review for counselors | ✅ Complete |

---

## Database Schema

### colleges table
- id, name, city, state
- acceptance_rate, sat_score, act_score
- median_gpa, tuition_in_state, tuition_out_state
- enrollment, graduation_rate
- school_url, image_url
- created_at

### subscriptions table
- id, user_id, plan, status
- stripe_customer_id, stripe_session_id, stripe_subscription_id
- interval, created_at, updated_at

### Other tables
- college_wishlist, counselor_notes
- essays, essay_versions, essay_snippets
- affiliates, affiliate_conversions

---

## Environment Variables

| Variable | Purpose |
|----------|---------|
| `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY` | Clerk auth |
| `CLERK_SECRET_KEY` | Clerk server |
| `DATABASE_URL` | Neon Postgres |
| `STRIPE_SECRET_KEY` | Stripe payments |
| `STRIPE_WEBHOOK_SECRET` | Stripe webhooks |
| `NEXT_PUBLIC_APP_URL` | App URL |
| `NEXT_PUBLIC_POSTHOG_KEY` | PostHog analytics |
| `NEXT_PUBLIC_POSTHOG_HOST` | PostHog host |
| `COLLEGE_LOGO_API_KEY` | Wikipedia logos |
| `SENTRY_DSN` | Sentry errors |
| `NEXT_PUBLIC_SENTRY_DSN` | Client Sentry |
| `GROQ_API_KEY` | AI essay review |
| `RESEND_API_KEY` | Email sending |
| `SVIX_SECRET` | Webhook signing |

---

## Key Dependencies

### Production
- `next`: 14.2.5, `react`: ^18.3.1
- `@clerk/nextjs`: ^5.7.6
- `@neondatabase/serverless`: ^0.9.0
- `drizzle-orm`: ^0.31.0, `drizzle-kit`: ^0.22.8
- `stripe`: ^14.0.0
- `posthog-js`: ^1.372.10, `posthog-node`: ^5.33.4
- `@sentry/nextjs`: ^10.51.0
- `lucide-react`: ^0.383.0
- `groq`: (via Groq SDK)
- `resend`: ^3.0.0
- `sonner`: ^2.0.7 (toasts)
- `svix`: ^1.92.2 (webhooks)
- `zod`: ^3.25.76 (validation)

### Dev Dependencies
- `@playwright/test`: ^1.40.0 (E2E tests)
- `dotenv-cli`: ^11.0.0

---

## Testing

### E2E Tests (Playwright)
- Configured with `@playwright/test`: ^1.40.0
- Test file: `tests/e2e.spec.ts`
- Run with: `pnpm test:e2e`
- View reports: `pnpm test:e2e:report`
- CI: GitHub Actions workflow at `.github/workflows/e2e-tests.yml`

---

## Scripts

```bash
pnpm dev       # Start development server (via turbo)
pnpm build    # Build for production
pnpm start    # Start production server
pnpm lint     # Run linter
pnpm format   # Format code
pnpm test     # Run tests (via turbo)
# Within apps/web:
pnpm test:e2e          # Run Playwright E2E tests
pnpm test:e2e:report   # View test report
```

---

## Deployment

- **Platform:** Vercel
- **Domain:** skoraadmit.com
- **Preview:** Automatic on PR

---

## Known Issues / TODOs

1. ~~No automated tests~~ (Playwright E2E tests added)
2. ~~Limited error boundaries~~ (Sentry now monitors errors)
3. No loading skeletons on some pages
4. College logo fetch may fail for some schools (fallback to initials)
5. Sentry integrated for production error tracking (May 2026)

---

## Build History

- **May 2026:** Sentry integration, error monitoring
- **June 2026:** Essay system redesign, AI counselor
- **July 2026:** White-label routing, counselor portal, Stripe webhooks

---

*Last updated: July 19, 2026*
