# Ideal Customer Profile (ICP)

## Target Segments

### Primary: Independent Consulting Firms
- **Size:** 3–50 counselors
- **Volume:** 500+ applications/year
- **Tech Stack:** Slate, TargetX, Element451, Salesforce, HubSpot, CRM
- **Pain Points:** Manual review bottlenecks, reader fatigue, scaling capacity, inconsistent scoring, counselor burnout
- **Decision Makers:** Founder, Principal, Director, VP, Partner, Owner
- **Qualification Score:** ≥60 (LLM batch qualified)

### Secondary: EdTech SaaS Building Admissions Tools
- **Size:** 10–200 employees
- **Product:** Admissions/enrollment management software
- **Tech:** Modern stack (React, Postgres, cloud)
- **Pain:** Building matching/essay/scoring features in-house, time-to-market
- **Decision Makers:** VP Engineering, CTO, VP Product, Founder
- **Qualification Score:** ≥70

## Explicitly NOT ICP (Auto-disqualify)
| Category | Reason |
|----------|--------|
| University/College admissions staff | No purchasing authority, public procurement |
| High school counselors | No budget, not decision makers |
| School districts (.k12., .isd., .school) | Public procurement, no SaaS budget |
| Test prep / tutoring companies | Different workflow, no admissions mgmt |
| Non-profits / college access orgs | Grant-funded, different buying process |
| International recruitment / visa agents | Different regulatory/compliance |
| Solo essay coaches (<3 counselors) | No scaling pain, no team coordination need |
| K-12 private/boarding school admissions | Different market, different tools |

## Qualification Signals (Positive)
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

## Disqualification Signals (Negative)
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

## LLM Batch Qualification Prompt
```json
{
  "leads": [...],
  "instructions": "Score each lead 0-100. Qualified ≥60. High Priority ≥80. Return JSON array with: email, score, qualified, high_priority, reasoning, key_signals[], red_flags[]"
}
```

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

## Email Templates (7 Variants)
All include: **Pilot_2026 code (free month)**, **Calendly link**, **info@skoraadmit.com direct line**, **Trailblazer framing**

| Variant | Core Hook | CTA |
|---------|-----------|-----|
| A1 | Pain-Point: 3x capacity + free $19/mo Pro | Book 10-min chat |
| A2 | Case Study: Similar firm scaled 3x | See case study |
| B1 | Social Proof: Peer firm scaled without hiring | 1-pager |
| B2 | Curiosity: What if students got Pro free? | 5-min call |
| C1 | Follow-up: Floating up — no is fine | Quick no/reply |
| C2 | Demo Sandbox: Branded portal link | Click demo |
| C3 | Re-engage (14+ days): Still relevant? | Case study / chat |

## Contact DB Fields
```json
{
  "email": "string",
  "first_name": "string",
  "last_name": "string",
  "company": "string",
  "role": "string",
  "company_size": "string",
  "source": "string",
  "source_url": "string",
  "status": "new|contacted|replied|qualified|do_not_contact|bounced",
  "icp_score": 0-100,
  "icp_fit": "high|medium|low|not",
  "variant_sent": "A1|A2|B1|B2|C1|C2|C3",
  "last_contacted": "ISO8601",
  "replies": 0,
  "positive_replies": 0,
  "bounce_count": 0,
  "tags": [],
  "notes": "string"
}
```