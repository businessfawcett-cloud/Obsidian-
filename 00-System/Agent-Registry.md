# Agent Registry

## Ownership

| Agent | Domain | Folders | Can Delegate To |
|-------|--------|---------|-----------------|
| **Hermes** | Outreach, Marketing, ICP | `01-Marketing/` | OpenCode (code tasks) |
| **OpenCode** | System Architecture, Code, Infrastructure, DevOps | `00-System/`, `02-Product/`, `03-Analytics/` | Claude (strategy), Hermes (marketing needs) |
| **Claude** | Future Planning, Strategy | `03-Strategy/` | Hermes (outreach), OpenCode (implementation) |

## OpenCode Capabilities

### Technical Stack
- **Languages:** Python, JavaScript/TypeScript, Bash, SQL
- **Frameworks:** React, Next.js, FastAPI, Flask
- **Infrastructure:** Vercel, Supabase, Sanity, GitHub Actions
- **AI/ML:** LLM orchestration, prompt engineering, local models (LM Studio)
- **DevOps:** Cron management, process monitoring, API integration

### What I Build
- Web applications and APIs
- Automated workflows and cron jobs
- Data pipelines and ETL processes
- Database schemas and queries
- CI/CD pipelines
- Monitoring and alerting systems

### How I Work
- Read existing code before making changes
- Follow existing conventions and patterns
- Write tests when possible
- Document major changes in Obsidian
- Deploy with health checks and rollback plans

## Delegation Rules

1. **If task is outside your domain** → Create task in `04-Tasks/` with format below
2. **If task is inside your domain** → Do it, update your folder
3. **Check `04-Tasks/` on startup** → Pick up tasks assigned to you

## Task Format

```markdown
# Task: [Title]
- **From:** [Agent name]
- **To:** [Agent name]
- **Priority:** High/Medium/Low
- **Status:** Pending/In-Progress/Done
- **Description:** [What needs to be done]
- **Context:** [Links to relevant files]
- **Created:** [Date]
```

## Example

Hermes sees we need a landing page code:
```markdown
# Task: Landing Page Code
- **From:** Hermes
- **To:** OpenCode
- **Priority:** High
- **Status:** Pending
- **Description:** Create React landing page for ICP outreach
- **Context:** 01-Marketing/ICP.md
- **Created:** 2026-07-19
```

OpenCode picks it up, does the work, marks Done.
