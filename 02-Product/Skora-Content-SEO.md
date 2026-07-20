# Skora — Content & SEO System

## Overview

Skora runs an automated content pipeline that generates SEO-optimized pages for college admissions. This drives organic traffic, builds domain authority, and feeds the B2B2C flywheel.

---

## Content Pipeline

### Schedule
- **Runs:** Daily at 2 AM Mountain Time
- **Script:** `~/skora-content/content-pipeline.py`

### Output Per Run
| Content Type | Count | Format |
|--------------|-------|--------|
| College Pages | 5 | `college-requirements-*.md` |
| State Pages | 10 | `state-admissions-*.md` |
| Blog Posts | 20 | `blog-*.md` |

### Output Location
```
/home/clause/skora-content/programmatic/
├── colleges/
│   ├── college-requirements-harvard.md
│   ├── college-requirements-yale.md
│   └── ...
├── states/
│   ├── state-admissions-california.md
│   ├── state-admissions-texas.md
│   └── ...
└── blog/
    ├── blog-how-to-write-college-essay.md
    ├── blog-when-to-apply-to-college.md
    └── ...
```

### Deployment Flow
```
Content Generated → Vercel Deploy Triggered → IndexNow Submitted → Live
```

---

## SEO Strategy

### Target Keywords
- "college admission requirements [school name]"
- "state college admissions [state]"
- "how to write college essay"
- "college application deadlines"
- "college acceptance chances"

### Content Types
1. **College Pages:** Admission requirements, acceptance rates, SAT scores, deadlines for 100+ schools
2. **State Pages:** Overview of college admissions in each state, top schools, state-specific requirements
3. **Blog Posts:** How-to guides, tips, timelines, essay advice

### Technical SEO
- `sitemap.xml` auto-generated
- `robots.txt` configured
- IndexNow submission for rapid indexing
- Structured data (JSON-LD) for colleges

---

## Data Sources

### College Data
- **Source:** IPEDS / College Scorecard
- **Fields:** Name, location, acceptance rate, SAT/ACT scores, GPA, tuition, enrollment, graduation rate
- **API:** College Scorecard API (data.gov)

### Major Rankings
- **Source:** US News
- **Categories:** Business, CS, Engineering, Pre-Health, Fine Arts, Law & Politics, Communications, Sciences, Social Sciences, Humanities
- **Schools:** 45+ institutions ranked

---

## Content Generation Process

### Step 1: Data Collection
- Pull college data from IPEDS API
- Fetch major rankings from US News
- Gather admission requirements from college websites

### Step 2: Content Generation
- LLM generates SEO-optimized content
- Includes target keywords naturally
- Adds unique value (analysis, tips, comparisons)

### Step 3: Quality Checks
- Word count validation
- Keyword density check
- Uniqueness verification
- Link validation

### Step 4: Deployment
- Build static pages
- Deploy to Vercel
- Submit to IndexNow for fast indexing
- Update sitemap.xml

---

## Analytics & Monitoring

### GA4 Tracking
- Page views per content type
- Time on page
- Bounce rate
- Conversion events (signup, upgrade)

### Content Performance
- Top performing pages
- Keyword rankings
- Organic traffic sources
- Backlink growth

---

## Current Content Stats

| Metric | Value |
|--------|-------|
| Total College Pages | 100+ |
| Total State Pages | 50 |
| Total Blog Posts | 200+ |
| Average Word Count | 1,500 |
| Indexing Rate | 95%+ |

---

## Future Enhancements

- [ ] Personalized content based on user profile
- [ ] Dynamic content updates when college data changes
- [ ] A/B testing for content variations
- [ ] Multi-language support
- [ ] Video content integration

---

*Last updated: July 19, 2026*
