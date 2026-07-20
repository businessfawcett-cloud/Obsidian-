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

| Layer | Tech |
|-------|------|
| Framework | Next.js 14 (App Router) |
| Language | TypeScript |
| Styling | TailwindCSS |
| Monorepo | Turborepo + pnpm workspaces |
| Auth | Clerk (@clerk/nextjs) — roles: student, counselor, admin |
| Database | Neon (Postgres) + Drizzle ORM |
| Payments | Stripe — Checkout, Billing Portal, Webhooks |
| AI | Groq SDK — essay review, AI chat counselor |
| Analytics | PostHog + Sentry |
| Email | Resend + Svix |
| Validation | Zod |

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

## Detailed Documentation

| Document | Description |
|----------|-------------|
| `02-Product/Skora-Features.md` | All 25 features built |
| `02-Product/Skora-Database-Schema.md` | Database tables and schema |
| `02-Product/Skora-Multi-Tenancy.md` | White-label routing system |
| `02-Product/Skora-Routes.md` | Complete page and route list |
| `02-Product/Skora-Build-History.md` | Timeline and milestones |
| `02-Product/Skora-Known-Issues.md` | Issues, TODOs, success criteria |
| `02-Product/Skora-Admit-Outreach.md` | Outreach system and email infra |
| `02-Product/Skora-Content-SEO.md` | Content pipeline and SEO |
| `02-Product/Roadmap.md` | Product roadmap |

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

*Last updated: July 19, 2026*
