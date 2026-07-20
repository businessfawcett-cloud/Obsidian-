# Reply Processor

**Job ID:** `b2e86e0b1973`
**Schedule:** `*/15 * * * *` (every 15 minutes)
**Owner:** Hermes

## What it does

- Fetches unread emails from `info@skoraadmit.com` via Himalaya
- Classifies: interested / not_interested / unsubscribe / question / OOO / bounce
- Auto-replies where appropriate
- Forwards to Parker with AI analysis
- Updates Contact DB with sentiment, tags, conversion status

## Logs

`~/.hermes/cron/output/b2e86e0b1973/`