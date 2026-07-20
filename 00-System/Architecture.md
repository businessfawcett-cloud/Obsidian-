# System Architecture

## Overview
Skora Admit runs on an **autonomous agent orchestration layer** (Hermes) with scheduled cron jobs executing LLM-driven workflows.

## Related
- [[00-System/Agent-Registry]] — Who does what
- [[00-System/Crons]] — Scheduled jobs
- [[02-Product/Skora-Architecture]] — Platform architecture

## Core Components

### 1. LLM-Native Outreach Agent (`llm_outreach_agent.py`)
- **Runs:** Continuous daemon (1-hour cycles)
- **Does:** Discovers sources → Explores → Enriches → Qualifies → Writes emails → Sends → Processes replies → Plans followups
- **State:** `~/.hermes/llm-outreach-agent/agent_state.json`
- **Models:** Local LM Studio (ornith-1.0-35b) primary, OpenRouter fallback

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

## Data Stores
| Store | Path | Description |
|-------|------|-------------|
| Contact DB | `~/.hermes/outreach/contacts/contacts.jsonl` | All leads, status, history |
| A/B Learning | `~/.hermes/outreach/learning/ab_test_state.json` | Thompson Sampling weights |
| Agent State | `~/.hermes/llm-outreach-agent/agent_state.json` | Continuous agent memory |
| Sent Logs | `~/.hermes/outreach/sent/sent_YYYYMMDD.jsonl` | Email send records |
| Reply Logs | `~/.hermes/outreach/replies/replies_YYYYMMDD.jsonl` | Inbound processing |
| Weekly Targets | `~/.hermes/outreach/learning/weekly_targets.json` | Targets vs actuals |

## Email Infrastructure
- **Provider:** PrivateEmail (Himalaya CLI)
- **Address:** `info@skoraadmit.com`
- **Reply-to:** `parkerscottfawcett@gmail.com`
- **Tracking:** 1x1 pixel at `https://skoraadmit.com/track/open/{email}/{variant}`

## A/B Variants (7 total)
| Variant | Hook | Best For |
|---------|------|----------|
| A1 | Pain-Point Direct | High-ICP founders |
| A2 | Case Study | Similar firm social proof |
| B1 | Social Proof First | Skeptical buyers |
| B2 | Curiosity Question | Cold opens |
| C1 | Follow-Up Bump | 3-day no-reply |
| C2 | Demo Sandbox | Visual learners |
| C3 | Re-Engagement | 14+ day cold |

## Targets (Weekly)
| Metric | Target |
|--------|--------|
| Bounce Rate | <10% |
| A/B Differentiated | ≥2 variants |
| Open Rate (best) | >15% |
| GA4 Sessions/Day | >5 |
| GA4 Conversions/Week | >1 |
| Meetings Booked | >1 |
| High-ICP Contacts | >15 |