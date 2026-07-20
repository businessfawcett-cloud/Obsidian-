# Weekly Engineering Loop

**Job ID:** `4b38c732074c`
**Schedule:** `0 7 * * 1` (Monday 7 AM MT)
**Owner:** Hermes
**Skills:** `marketing-outreach`, `software-development`

## What it does

1. **Measure** — GA4 (7d), Contact DB stats, sent/reply/bounce logs, A/B weights, cron health
2. **Diagnose** — Score blockers 0-10 vs targets in `weekly_targets.json`
3. **Research** — Web search for top 5 blockers ≥7 severity
4. **Engineer** — Patch code/config/queries for each blocker ≥7
5. **Deploy** — Content pipeline → Vercel → IndexNow
6. **Log** — `~/.hermes/cron/output/weekly-self-assessment/YYYY-MM-DD.md`
7. **Update** — `weekly_targets.json` with actuals → previous_week_actuals

## Logs

`~/.hermes/cron/output/4b38c732074c/`