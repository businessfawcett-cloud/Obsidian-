# GA4 & GTM Setup

## GA4 Property
- **Property ID:** 544246547
- **Stream:** Web (skoraadmit.com)
- **Enhanced Measurement:** ON

## GTM Container
- **Container ID:** GTM-54KPDD7F
- **GA4 Config Tag:** Fires on all pages

## Conversion Events (Configure in GTM)
| Event Name | Trigger | Parameters |
|------------|---------|------------|
| `sign_up` | Form submit / Clerk auth success | `method`, `plan` |
| `demo_request` | Calendly booking success | `source`, `variant` |
| `meeting_booked` | Calendly confirmed | `meeting_type`, `calendly_event_id` |
| `email_open` | Tracking pixel hit | `email_hash`, `variant`, `campaign` |
| `email_click` | Link click in email | `link_type`, `variant`, `destination` |
| `sandbox_demo_started` | Sandbox demo page load | `variant` |
| `pricing_view` | Pricing page view | `plan_viewed` |
| `begin_checkout` | Checkout initiated | `plan`, `value`, `currency` |

## GA4 Measurement Protocol (Server-side)
```bash
# Tracking pixel endpoint receives:
GET /track/open/{email_hash}/{variant}
# Logs to GA4 via MP:
POST https://www.google-analytics.com/mp/collect?measurement_id=G-XXXXXXXX&api_secret=SECRET
{
  "client_id": "email_hash",
  "events": [{"name": "email_open", "params": {"variant": "A1", "campaign": "outreach"}}]
}
```

## Required Vercel Deployment
1. Deploy tracking pixel endpoint: `app/track/open/[...params]/route.ts`
2. Add GA4 Measurement Protocol secret to Vercel env vars
3. Configure GTM tags for all 8 conversion events
4. Test in GA4 Realtime > Events