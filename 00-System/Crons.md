# Scheduled Jobs (Cron)

All times in **Mountain Time (MT)**.

## Active Crons

| Job | Schedule | Description | Job ID |
|-----|----------|-------------|--------|
| **LLM Outreach Agent** | Continuous (1-hr cycles) | Autonomous outreach daemon | `proc_...` (background) |
| **Content Pipeline** | `0 2 * * *` (2 AM) | Generates SEO pages, deploys, IndexNow | `2a8e8a2b4a59` |
| **Reply Processor** | `*/15 * * * *` | Processes inbound emails | `b2e86e0b1973` |
| **GA4 Daily Brief** | `0 8 * * *` (8 AM) | Daily analytics report | `8ec5c7c6d4b9` |
| **Weekly Engineering Loop** | `0 7 * * 1` (Mon 7 AM) | Measure → Diagnose → Fix → Deploy | `4b38c732074c` |
| **Inbox Cleanup** | `0 3 * * *` (3 AM) | Removes bounces, spam | `a854c5fdebdd` |

## Job Details

### Content Pipeline (2 AM)
```bash
# Runs:
python ~/skora-content/content-pipeline.py
# Generates:
# - 5 college pages (college-requirements-*.md)
# - 10 state pages (state-admissions-*.md)  
# - 20 blog posts (blog-*.md)
# Updates sitemap.xml, submits to IndexNow, triggers Vercel deploy
```

### Weekly Engineering Loop (Mon 7 AM)
1. **Measure** — GA4 (7d), Contact DB stats, sent/reply/bounce logs, A/B weights, cron health
2. **Diagnose** — Score blockers 0-10 vs targets
3. **Research** — Web search for top 5 blockers ≥7 severity
4. **Engineer** — Patch code/config/queries for each blocker
5. **Deploy** — Content pipeline → Vercel → IndexNow
6. **Log** — `~/.hermes/cron/output/weekly-self-assessment/YYYY-MM-DD.md`

### Reply Processor (every 15 min)
- Fetches unread from `info@skoraadmit.com` via Himalaya
- Classifies: interested / not_interested / unsubscribe / question / OOO / bounce
- Auto-replies where appropriate
- Forwards to Parker with AI analysis
- Updates Contact DB with sentiment, tags, conversion status

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