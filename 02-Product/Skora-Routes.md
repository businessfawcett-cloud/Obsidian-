# Skora — Pages & Routes

## Complete Route List

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

## Route Groups

### Marketing (Public)
- `/`, `/sign-in`, `/sign-up`, `/pricing`, `/terms`, `/privacy`, `/cookies`, `/join`, `/counselor-signup`

### Student App (Authenticated)
- `/dashboard`, `/explore`, `/college/[id]`, `/applications`, `/essays`, `/my-essays`, `/outcomes`, `/schedule`, `/chat`, `/scholarships`, `/messages`, `/wishlist`, `/billing`, `/profile/edit`

### Counselor App (Authenticated)
- `/counselor`, `/counselor/billing`, `/counselor/settings`, `/counselor/invite`, `/counselor/whitelabel-setup`, `/counselor/student/[id]`, `/counselor/essay-review/[essayId]`

### Admin (Authenticated)
- `/admin`, `/admin/analytics`, `/admin/students`, `/admin/counselors`, `/admin/affiliates`, `/admin/affiliates/[code]`

### API Routes
- `/api/essay/review`, `/api/stripe/*`, `/api/student/*`

---

*Last updated: July 19, 2026*
