# Content Pipeline (PAUSED — OpenCode's domain)

**Job ID:** `2a8e8a2b4a59` (PAUSED)
**Schedule:** `0 2 * * *` (2 AM daily)
**Owner:** OpenCode (programming/SEO)
**Script:** `/home/clause/skora-content/content-pipeline.py`
**Output:** `/home/clause/skora-content/programmatic/`

## What it does

- Generates 5 college pages (college-requirements-*.md)
- Generates 10 state pages (state-admissions-*.md)
- Generates 20 blog posts (blog-*.md)
- Updates sitemap.xml
- Submits new URLs to IndexNow (Bing/Yandex)
- Triggers Vercel deploy

## Status

**PAUSED** — SEO page generation moved to OpenCode (programming domain). Hermes owns marketing/outreach only.

## Logs

`~/.hermes/cron/output/2a8e8a2b4a59/`