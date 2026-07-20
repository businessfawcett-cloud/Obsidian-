# Skora — Features Built (Complete List)

## 1. Landing Page (`/`)
- Hero section with value proposition
- Feature highlights (Essay Review, Admission Chancing, College Matching)
- College logo strip (Harvard, Yale, Princeton, Columbia, MIT, Stanford, Penn, Duke, UGA)
- Sign up/Sign in integration with Clerk
- Two-column conversion layout
- Dedicated counselor signup page at `/counselor-signup`

## 2. Authentication System
- Clerk Next.js SDK integration
- Protected routes with SignedIn component
- Role-based access (student, counselor, admin)
- White-label brand support

## 3. User Onboarding (`/onboarding`)
- 5-step profile creation flow:
  - Step 1: Academic stats (GPA, SAT/ACT)
  - Step 2: Target schools
  - Step 3: Intended major
  - Step 4: Early decision preferences
  - Step 5: Completion/save
- White-label brand support in top bar

## 4. Student Dashboard (`/dashboard`)
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

## 5. College Detail (`/college/[id]`)
- Redesigned 3-zone layout: hero header, two-column grid, sticky bottom bar
- Stats comparison bars (dual-bar: grey baseline + orange overlay)
- Program strength display for user's major
- College logo retrieval (Wikipedia API)
- Application links

## 6. Essay System
- **Essay editor (`/essays`):** Redesigned with stages (Brainstorm, Draft, Polishing, Final), word count, save/save version/submit buttons
- **My Essays page (`/my-essays`):** Horizontal cards, stage badges, progress bars, empty state
- **AI Review:** Three-panel review workspace with inline comments, snippets, general comments, Harvard-style personal rating (1-6)
- **AI Feedback API (`/api/essay/review`):** Groq integration, line-by-line suggestions, personalRating prompt, admissions calculator integration

## 7. AI Counselor (`/chat`)
- AI chat interface for college admissions questions
- Plan-gated (Pro upgrade wall for free users)
- Stripe checkout integration

## 8. Explore (`/explore`)
- College discovery with cards, donut chart, scrollable category tabs, search icon
- College detail page (`/explore/[collegeId]`) for direct linking

## 9. Wishlist (`/wishlist`)
- Save colleges to personal wishlist
- Manage saved colleges

## 10. Applications (`/applications`)
- Kanban-style application tracker

## 11. Messages (`/messages`)
- Redesigned with 280px conversation panel, chat area, orange accent, cream bg

## 12. Scholarships (`/scholarships`)
- Redesigned scholarship finder with new visual layout
- Shows real college names

## 13. Schedule (`/schedule`)
- Calendar for deadlines and tasks

## 14. Outcomes (`/outcomes`)
- My Results page showing admission decisions

## 15. Pricing & Subscriptions (`/pricing`)
- Dual-tab (Counselor/Student) pricing page
- Student plans: Free ($0), Pro ($19/mo)
- Counselor plans: Starter ($49/mo), Growth ($99/mo), Agency ($199/mo)
- Stripe Checkout integration for both student and counselor plans
- Affiliate tracking via cookie/referral codes

## 16. Student Billing (`/billing`)
- Current plan display (live from Clerk metadata)
- Plan status badge (active/canceled/past_due)
- Monthly usage stats (essay reviews)
- Manage Subscription button (opens Stripe billing portal)
- Upgrade to Pro button for free users
- Payment method management
- Subscription history table from database

## 17. Counselor Features
- Counselor dashboard (`/counselor`)
- Billing page (`/counselor/billing`) with plan info and Stripe portal
- Settings page (`/counselor/settings`) with plan badge
- Student invitation (`/counselor/invite`) with plan limits
- White-label portal support (`/counselor/whitelabel-setup`)
- Student detail view (`/counselor/student/[id]`)
- Essay review for counselors (`/counselor/essay-review/[essayId]`)

## 18. Stripe Integration
- **Checkout:** `/api/stripe/create-checkout` (counselor), `/api/stripe/student-checkout` (student)
- **Billing Portal:** `/api/stripe/portal` (counselor), `/api/stripe/student-portal` (student)
- **Webhook:** `/api/stripe/webhook` - handles checkout.completed, subscription.updated, subscription.deleted, invoice.payment_failed
- Clerk metadata sync (plan, planStatus, stripeSubscriptionId, stripeCustomerId)
- Email notifications (upgrade confirmation, cancellation, payment failed)

## 19. Analytics
- PostHog integration for event tracking
- Admin analytics dashboard (`/admin/analytics`)
- Server-side tracking (`trackServer`)

## 20. Admin Features
- Admin dashboard (`/admin`)
- Students management (`/admin/students`)
- Counselors management (`/admin/counselors`)
- Affiliates management (`/admin/affiliates`)
- Affiliate detail with per-conversion plan data

## 21. User Profile (`/profile/edit`)
- Profile editor with form fields
- Local storage persistence

## 22. Major Rankings System (`/data/majorRankings.ts`)
- US News rankings for 45+ schools
- Categories: Business, CS, Engineering, Pre-Health, Fine Arts, Law & Politics, Communications, Sciences, Social Sciences, Humanities
- Helper functions: getMajorRank, getMajorRankByName, getMajorRankingsForSchool, formatMajorKey

## 23. College API (`/lib/collegeApi.ts`)
- fetchColleges: Database query to Neon
- calculateUserChance: Admission probability calculation
- determineCategory: Safety/Target/Reach classification
- fetchCollegeLogo: Wikipedia API integration

## 24. Database Integration
- Neon database with Drizzle ORM
- College data from IPEDS/College Scorecard
- Tables: colleges, college_wishlist, subscriptions, counselor_notes, essays, essay_versions, essay_snippets, affiliates, affiliate_conversions

## 25. Additional Features
- Join page (`/join`)
- Support page (`/support`)
- Resend integration for transactional emails
- Svix for webhook management
- Zod for form validation

---

*Last updated: July 19, 2026*
