# Skora — Multi-Tenancy / White-Label Routing

## Overview

Skora supports white-label portals for counselors on Standard and Agency plans. Students see a branded experience when accessing via counselor subdomains or path slugs.

---

## Routing Methods

### 1. Subdomain Routing
- **Pattern:** `<slug>.skoraadmit.com`
- **Mechanism:** Sets `skora_subdomain` cookie
- **Example:** `collegewise.skoraadmit.com`

### 2. Path-Slug Routing (Standard plan)
- **Pattern:** `skoraadmit.com/<slug>`
- **Mechanism:** Rewrites to `/` with `skora_path_slug` cookie
- **Example:** `skoraadmit.com/collegewise`

---

## Implementation

### Middleware
- **File:** `apps/web/src/middleware.ts`
- Detects subdomain or path slug
- Sets appropriate cookie
- Rewrites to root for branded experience

### Root Page Logic
1. Reads cookie (`skora_subdomain` or `skora_path_slug`)
2. Fetches counselor's brand from database
3. Renders branded sign-in screen instead of default marketing homepage
4. Caches brand in `localStorage['skora_brand']` for persistence

---

## Branding Elements

| Element | Source |
|---------|--------|
| Logo | Counselor upload |
| Colors | Counselor config |
| Company name | Counselor profile |
| Custom domain | Agency plan only |

---

## Plan Limits

| Plan | White-Label | Custom Domain |
|------|-------------|---------------|
| Basic | No | No |
| Standard | Yes (path slug) | No |
| Agency | Yes (subdomain) | Yes |

---

## Student Experience

When a student accesses via white-label:
1. Sees branded sign-in page
2. Linked to counselor's account
3. Gets free Pro account (Standard/Agency counselors)
4. Sees counselor's branding throughout

---

*Last updated: July 19, 2026*
