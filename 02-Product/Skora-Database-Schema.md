# Skora — Database Schema

## Overview

Skora uses **Neon (Postgres)** with **Drizzle ORM**. College data comes from IPEDS/College Scorecard.

---

## Tables

### colleges
| Column | Type | Description |
|--------|------|-------------|
| id | integer | Primary key |
| name | text | College name |
| city | text | City |
| state | text | State |
| acceptance_rate | numeric | Acceptance rate (0-1) |
| sat_score | integer | Median SAT |
| act_score | integer | Median ACT |
| median_gpa | numeric | Median GPA |
| tuition_in_state | integer | In-state tuition |
| tuition_out_state | integer | Out-of-state tuition |
| enrollment | integer | Total enrollment |
| graduation_rate | numeric | Graduation rate |
| school_url | text | Website URL |
| image_url | text | Logo URL |
| created_at | timestamp | Created timestamp |

### subscriptions
| Column | Type | Description |
|--------|------|-------------|
| id | text | Primary key |
| user_id | text | Clerk user ID |
| plan | text | free / pro / basic / standard / agency |
| status | text | active / canceled / past_due |
| stripe_customer_id | text | Stripe customer ID |
| stripe_session_id | text | Checkout session ID |
| stripe_subscription_id | text | Subscription ID |
| interval | text | month / year |
| created_at | timestamp | Created timestamp |
| updated_at | timestamp | Updated timestamp |

### college_wishlist
| Column | Type | Description |
|--------|------|-------------|
| id | text | Primary key |
| user_id | text | Clerk user ID |
| college_id | integer | FK to colleges |
| created_at | timestamp | Created timestamp |

### counselor_notes
| Column | Type | Description |
|--------|------|-------------|
| id | text | Primary key |
| counselor_id | text | Clerk user ID |
| student_id | text | Clerk user ID |
| note | text | Note content |
| created_at | timestamp | Created timestamp |

### essays
| Column | Type | Description |
|--------|------|-------------|
| id | text | Primary key |
| user_id | text | Clerk user ID |
| title | text | Essay title |
| content | text | Essay body |
| stage | text | brainstorm / draft / polishing / final |
| word_count | integer | Word count |
| created_at | timestamp | Created timestamp |
| updated_at | timestamp | Updated timestamp |

### essay_versions
| Column | Type | Description |
|--------|------|-------------|
| id | text | Primary key |
| essay_id | text | FK to essays |
| content | text | Version content |
| version_number | integer | Version number |
| created_at | timestamp | Created timestamp |

### essay_snippets
| Column | Type | Description |
|--------|------|-------------|
| id | text | Primary key |
| essay_id | text | FK to essays |
| content | text | Snippet content |
| line_start | integer | Start line |
| line_end | integer | End line |
| comment | text | AI comment |
| rating | integer | Rating 1-6 |
| created_at | timestamp | Created timestamp |

### affiliates
| Column | Type | Description |
|--------|------|-------------|
| id | text | Primary key |
| code | text | Unique referral code |
| user_id | text | Clerk user ID |
| plan | text | Plan earned |
| conversions | integer | Total conversions |
| created_at | timestamp | Created timestamp |

### affiliate_conversions
| Column | Type | Description |
|--------|------|-------------|
| id | text | Primary key |
| affiliate_id | text | FK to affiliates |
| referred_user_id | text | Referred user |
| plan | text | Plan purchased |
| amount | integer | Amount in cents |
| created_at | timestamp | Created timestamp |

---

## Schema Location

- **Schema file:** `apps/web/src/lib/db/schema.ts`
- **Migrations:** `apps/web/src/lib/db/migrations/`
- **Config:** `apps/web/drizzle.config.ts`

## Commands

```bash
npx drizzle-kit generate  # Generate migration
npx drizzle-kit push      # Push schema to DB
```

---

*Last updated: July 19, 2026*
