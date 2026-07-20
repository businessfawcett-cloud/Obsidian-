# Skora Admit — Marketing & Outreach Infrastructure

## Overview

The Skora Admit outreach system is an autonomous agent orchestration layer running on a VPS. It handles lead generation, email outreach, reply processing, and content marketing — all automated via cron jobs and LLM-driven workflows.

---

## Core Components

### 1. LLM-Native Outreach Agent (`llm_outreach_agent.py`)
- **Runs:** Continuous daemon (1-hour cycles)
- **Does:** Discovers sources → Explores → Enriches → Qualifies → Writes emails → Sends → Processes replies → Plans followups
- **State:** `~/.hermes/llm-outreach-agent/agent_state.json`
- **Models:** Local LM Studio (ornith-1.0-35b) primary, OpenRouter fallback
- **Process:**
  1. Discover new leads from web search
  2. Explore company websites for qualification signals
  3. Enrich contact data (emails, roles, company size)
  4. Qualify leads against ICP scoring
  5. Write personalized outreach emails
  6. Send via Himalaya CLI
  7. Process replies and classify sentiment
  8. Plan follow-up sequences

### 2. Weekly Engineering Loop (Cron: Mon 7 AM)
- **Job ID:** `4b38c732074c`
- **Measures:** GA4, Contact DB, sent/reply/bounce logs, A/B weights, cron health, content pipeline
- **Diagnoses:** Scores blockers 0-10 vs targets
- **Researches:** Web search for solutions
- **Engineers:** Patches code, configs, queries
- **Deploys:** Content pipeline → Vercel → IndexNow
- **Logs:** `~/.hermes/cron/output/weekly-self-assessment/`

### 3. Content Pipeline (Cron: 2 AM daily)
- **Script:** `~/skora-content/content-pipeline.py`
- **Generates:** 5 college pages, 10 state pages, 20 blog posts per run
- **Outputs:** `/home/clause/skora-content/programmatic/`
- **Deploys:** Triggers Vercel, submits to IndexNow

### 4. Reply Processor (Cron: every 15 min)
- **Job ID:** `b2e86e0b1973`
- **Reads:** `info@skoraadmit.com` via Himalaya
- **Classifies:** interested / not_interested / unsubscribe / question / OOO / bounce
- **Actions:** Auto-replies, forwards to Parker, updates Contact DB

### 5. GA4 Daily Brief (Cron: 8 AM daily)
- **Job ID:** `8ec5c7c6d4b9`
- **Outputs:** Traffic, conversions, sources, pages

---

## Data Stores

| Store | Path | Description |
|-------|------|-------------|
| Contact DB | `~/.hermes/outreach/contacts/contacts.jsonl` | All leads, status, history |
| A/B Learning | `~/.hermes/outreach/learning/ab_test_state.json` | Thompson Sampling weights |
| Agent State | `~/.hermes/llm-outreach-agent/agent_state.json` | Continuous agent memory |
| Sent Logs | `~/.hermes/outreach/sent/sent_YYYYMMDD.jsonl` | Email send records |
| Reply Logs | `~/.hermes/outreach/replies/replies_YYYYMMDD.jsonl` | Inbound processing |
| Weekly Targets | `~/.hermes/outreach/learning/weekly_targets.json` | Targets vs actuals |

---

## Email Infrastructure

- **Provider:** PrivateEmail (Himalaya CLI)
- **Address:** `info@skoraadmit.com`
- **Reply-to:** `parkerscottfawcett@gmail.com`
- **Tracking:** 1x1 pixel at `https://skoraadmit.com/track/open/{email}/{variant}`

---

## A/B Variants (7 Total)

| Variant | Hook | Best For |
|---------|------|----------|
| A1 | Pain-Point Direct | High-ICP founders |
| A2 | Case Study | Similar firm social proof |
| B1 | Social Proof First | Skeptical buyers |
| B2 | Curiosity Question | Cold opens |
| C1 | Follow-Up Bump | 3-day no-reply |
| C2 | Demo Sandbox | Visual learners |
| C3 | Re-Engagement | 14+ day cold |

---

## ICP Scoring System

### Qualification Signals (Positive)
| Signal | Weight |
|--------|--------|
| Uses Slate / TargetX / Element451 / CRM | +20 |
| "Former admissions officer" on team | +15 |
| Team size 5–50 counselors | +15 |
| 500+ apps/year mentioned | +15 |
| "Scaling", "capacity", "bottleneck", "burnout" | +10 |
| Hiring admissions consultants | +10 |
| White-label / branded portal interest | +10 |
| "3x student capacity" resonance | +10 |

### Disqualification Signals (Negative)
| Signal | Weight |
|--------|--------|
| .edu / .k12. / .school / .district / .isd. domain | -50 (auto-reject) |
| "University", "College", "School District" in name | -40 |
| "Dean", "Director of Admissions" (university) | -40 |
| "Guidance counselor", "School counselor" | -30 |
| "Test prep", "Tutoring", "SAT", "ACT" | -25 |
| "Non-profit", "College access", "Scholarship" | -25 |
| Solo / 1-3 person without team scaling pain | -20 |
| Generic email (info@, hello@, admin@) | -10 |

### LLM Batch Qualification Prompt
```json
{
  "leads": [...],
  "instructions": "Score each lead 0-100. Qualified ≥60. High Priority ≥80. Return JSON array with: email, score, qualified, high_priority, reasoning, key_signals[], red_flags[]"
}
```

---

## Current Verified Leads (18 contacts)

| Company | Contact | Role | Score | Variant |
|---------|---------|------|-------|---------|
| Collegewise | Team | General | 95 | A1/A2 |
| Spark Admissions | Dr. Rachel Rubin | Founder & CEO | 95 | A2 |
| Spark Admissions | Connor Beatty | Chief Consulting Officer | 90 | B1 |
| AcceptU | Team | General | 85 | C1 |
| Solomon Admissions | Vitaly Borishan | Cofounder | 90 | B1 |
| Solomon Admissions | Dan Lee | Cofounder | 90 | B2 |
| Top Tier Admissions | Michele Hernandez | Founder | 85 | A1 |
| IvyWise | Team | General | 90 | A2 |
| Ivy Insight | Dr. Aviva Legatt | Founder | 85 | B2 |
| S Blumer Consulting | Sam Blumer | Founder (ex-Slate) | 85 | C1 |
| Launch IV | Amy Miller | Founder & CEO | 95 | A1 |
| Prepory | Team | General | 80 | A2 |
| Admissionado | Team | General | 80 | B1 |
| Collegiate Gateway | Team | General | 75 | B2 |
| Command Education | Team | General | 85 | C1 |
| The Admissions Angle | Team | General | 75 | C2 |
| Empowerly | Team | General | 80 | A1 |

---

## Weekly Targets

| Metric | Target |
|--------|--------|
| Bounce Rate | <10% |
| A/B Differentiated | ≥2 variants |
| Open Rate (best) | >15% |
| GA4 Sessions/Day | >5 |
| GA4 Conversions/Week | >1 |
| Meetings Booked | >1 |
| High-ICP Contacts | >15 |

---

## Cron Jobs (All Times Mountain Time)

| Job | Schedule | Description | Job ID |
|-----|----------|-------------|--------|
| LLM Outreach Agent | Continuous (1-hr cycles) | Autonomous outreach daemon | `proc_...` (background) |
| Content Pipeline | `0 2 * * *` (2 AM) | Generates SEO pages, deploys, IndexNow | `2a8e8a2b4a59` |
| Reply Processor | `*/15 * * * *` | Processes inbound emails | `b2e86e0b1973` |
| GA4 Daily Brief | `0 8 * * *` (8 AM) | Daily analytics report | `8ec5c7c6d4b9` |
| Weekly Engineering Loop | `0 7 * * 1` (Mon 7 AM) | Measure → Diagnose → Fix → Deploy | `4b38c732074c` |
| Inbox Cleanup | `0 3 * * *` (3 AM) | Removes bounces, spam | `a854c5fdebdd` |

---

## Viewing Logs

```bash
# All cron outputs
ls ~/.hermes/cron/output/

# Latest weekly engineering log
cat ~/.hermes/cron/output/weekly-self-assessment/$(date +%Y-%m-%d).md

# Latest GA4 brief
cat ~/.hermes/cron/output/8ec5c7c6d4b9/$(date +%Y-%m-%d)_*.md

# Outreach agent state
cat ~/.hermes/llm-outreach-agent/agent_state.json

# Contact DB
python ~/.hermes/outreach/scripts/contact_db.py stats
```

---

*Last updated: July 19, 2026*
