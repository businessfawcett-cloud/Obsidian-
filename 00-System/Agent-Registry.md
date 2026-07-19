# Agent Registry — Domain Ownership

> **Purpose:** Single source of truth for which agent owns which domain. Other agents read this to know who to delegate to.

---

## 🎯 Domain Owners

| Domain | Owner Agent | Platform | Scope |
|--------|-------------|----------|-------|
| **Marketing & Outreach** | **Hermes (this agent)** | Pi (Hermes) | Lead gen, email outreach, ICP qualification, A/B testing, content/SEO pipeline, GA4 analytics, conversion tracking, Calendly booking, reply processing |
| **Product Engineering** | *TBD* | *TBD* | Next.js app, student tool, counselor portal, white-label dashboard, AI matching, essay feedback |
| **Infrastructure/DevOps** | *TBD* | *TBD* | Vercel, databases, CI/CD, monitoring, secrets, DNS |
| **Sales/Customer Success** | *TBD* | *TBD* | Demo calls, onboarding, support, retention, expansion |
| **Finance/Legal** | *TBD* | *TBD* | Billing, Stripe, contracts, compliance, Pilot_2026 terms |
| **Design/Brand** | *TBD* | *TBD* | UI/UX, landing pages, demo sandbox, white-label theming |

---

## 🤝 Delegation Protocol

**If you need marketing work done:**
1. Check this registry → Marketing = Hermes
2. Delegate via Hermes (this agent) or create task in `~/skora-content/`
3. Hermes owns: `llm_outreach_agent.py`, `content-pipeline.py`, `daily_outreach.py`, `contact_db.py`, GA4, GTM, Calendly, Himalaya, Contact DB

**If Hermes needs work from another domain:**
- Hermes creates issue/task in the owning agent's workspace
- Does NOT implement product code, infra, billing, etc.

---

## 📁 Marketing Artifacts Owned by Hermes

| Artifact | Location | Description |
|----------|----------|-------------|
| Outreach Agent | `/home/clause/skora-content/llm_outreach_agent.py` | Continuous LLM-native outreach daemon |
| Content Pipeline | `/home/clause/skora-content/content-pipeline.py` | Daily SEO page generation + deploy |
| Daily Outreach (legacy) | `~/.hermes/skills/marketing/marketing-outreach/scripts/daily_outreach.py` | Cron-based outreach |
| Contact DB | `~/.hermes/outreach/contacts/contacts.jsonl` | All leads, status, history |
| A/B Learning | `~/.hermes/outreach/learning/ab_test_state.json` | Thompson Sampling weights |
| Weekly Targets | `~/.hermes/outreach/learning/weekly_targets.json` | Targets vs actuals |
| Email Templates | `/home/clause/skora-content/email-templates-with-calendly.js` | 7 variants + Calendly |
| Tracking Pixel | `/home/clause/skora-content/tracking-pixel-endpoint.ts` | Open tracking endpoint |
| GTM Events | `/home/clause/skora-content/gtm-conversion-events.ts` | 8 conversion events |
| Deploy Script | `/home/clause/skora-content/deploy.sh` | Vercel + IndexNow deploy |

---

## 🔐 Credentials Managed by Hermes

| Service | Purpose |
|---------|---------|
| PrivateEmail (Himalaya) | `info@skoraadmit.com` outreach |
| GA4 / GTM | Analytics + conversion tracking |
| Calendly | `https://calendly.com/parkerscottfawcett` booking |
| IndexNow (Bing) | SEO instant indexing |
| OpenRouter / LM Studio | LLM inference for qualification + writing |
| Firecrawl | Web extraction for enrichment |

---

## 📅 Recurring Marketing Jobs (Cron)

| Job | Schedule | Owner |
|-----|----------|-------|
| LLM Outreach Agent | Continuous (1-hr cycles) | **Hermes** |
| Content Pipeline | 2 AM daily | **Hermes** |
| Reply Processor | Every 15 min | **Hermes** |
| GA4 Daily Brief | 8 AM daily | **Hermes** |
| Weekly Engineering Loop | Mon 7 AM | **Hermes** |
| Inbox Cleanup | 3 AM daily | **Hermes** |

---

## 🚫 Not Hermes' Responsibility

- Writing product code (Next.js, React, API routes)
- Database schema / migrations
- Vercel / infra provisioning
- Stripe / billing integration
- Legal / compliance / contracts
- UI/UX design
- Customer support tickets

---

## 📝 For Other Agents

> **If you're reading this and need marketing:** Create a task in `/home/clause/skora-content/tasks/` or ping Hermes directly. Marketing is **owned end-to-end by Hermes**.

> **If you're Hermes reading this:** You own all of the above. Delegate out only when explicitly needed. This is your domain.

---

*Last updated: 2026-07-19 by Hermes (Marketing Agent)*
*Registry version: 1.0*