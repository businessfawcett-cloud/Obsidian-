# Scheduled Jobs (Cron)

All times in **Mountain Time (MT)**.

---

<details>
<summary><strong>🔄 LLM Outreach Agent</strong> — Continuous (1-hr cycles)</summary>

**Job ID:** Background process (pid 56747)
**Schedule:** Runs every hour continuously
**Owner:** Hermes
**Script:** `/home/clause/skora-content/llm_outreach_agent.py`
**State:** `~/.hermes/llm-outreach-agent/agent_state.json`

**What it does:**
- Discovers new lead sources dynamically
- Explores sources for leads
- Enriches leads with deep research
- Qualifies leads via LLM (ICP scoring)
- Writes personalized emails (7 variants)
- Sends via Himalaya (info@skoraadmit.com)
- Processes replies
- Plans follow-ups (C1 at 3d, C2 at 7d, C3 at 14d)

**Logs:** `~/.hermes/llm-outreach-agent/`

</details>

---

<details>
<summary><strong>📝 Content Pipeline</strong> — Daily at 2 AM</summary>

**Job ID:** `2a8e8a2b4a59`
**Schedule:** `0 2 * * *`
**Owner:** Hermes
**Script:** `/home/clause/skora-content/content-pipeline.py`

**What it does:**
- Generates 5 college pages
- Generates 10 state pages
- Generates 20 blog posts
- Updates sitemap.xml
- Submits new URLs to IndexNow (Bing/Yandex)
- Triggers Vercel deploy

**Output:** `/home/clause/skora-content/programmatic/`

</details>

---

<details>
<summary><strong>📬 Reply Processor</strong> — Every 15 minutes</summary>

**Job ID:** `b2e86e0b1973`
**Schedule:** `*/15 * * * *`
**Owner:** Hermes

**What it does:**
- Fetches unread from `info@skoraadmit.com` via Himalaya
- Classifies: interested / not_interested / unsubscribe / question / OOO / bounce
- Auto-replies where appropriate
- Forwards to Parker with AI analysis
- Updates Contact DB with sentiment, tags, conversion status

</details>

---

<details>
<summary><strong>📊 GA4 Daily Brief</strong> — Daily at 8 AM</summary>

**Job ID:** `8ec5c7c6d4b9`
**Schedule:** `0 8 * * *`
**Owner:** Hermes
**Script:** `~/.hermes/scripts/ga4_daily_brief.py`

**What it does:**
- Pulls 7-day GA4 metrics
- Reports: sessions, users, conversions, sources, pages
- Delivers to Telegram

**GA4 Property:** 544246547

</details>

---

<details>
<summary><strong>🧠 Weekly Engineering Loop</strong> — Monday 7 AM</summary>

**Job ID:** `4b38c732074c`
**Schedule:** `0 7 * * 1`
**Owner:** Hermes
**Skills:** `marketing-outreach`, `software-development`

**What it does:**
1. **Measure** — GA4 (7d), Contact DB stats, sent/reply/bounce logs, A/B weights, cron health
2. **Diagnose** — Score blockers 0-10 vs targets in `weekly_targets.json`
3. **Research** — Web search for top 5 blockers ≥7 severity
4. **Engineer** — Patch code/config/queries for each blocker
5. **Deploy** — Content pipeline → Vercel → IndexNow
6. **Log** — `~/.hermes/cron/output/weekly-self-assessment/YYYY-MM-DD.md`
7. **Update** — `weekly_targets.json` with actuals

</details>

---

<details>
<summary><strong>🧹 Inbox Cleanup</strong> — Daily at 3 AM</summary>

**Job ID:** `a854c5fdebdd`
**Schedule:** `0 3 * * *`
**Owner:** Hermes

**What it does:**
- Removes bounced emails from Contact DB
- Marks spam/auto-replies
- Cleans up old logs

</details>

---

## Quick Commands

```bash
# View all cron outputs
ls ~/.hermes/cron/output/

# Latest weekly engineering log
cat ~/.hermes/cron/output/weekly-self-assessment/$(date +%Y-%m-%d).md

# Latest GA4 brief
cat ~/.hermes/cron/output/8ec5c7c6d4b9/$(date +%Y-%m-%d)_*.md

# Outreach agent state
cat ~/.hermes/llm-outreach-agent/agent_state.json

# Contact DB stats
python ~/.hermes/outreach/scripts/contact_db.py stats
```