# Agent Registry

## Ownership

| Agent | Domain | Folders | Can Delegate To |
|-------|--------|---------|-----------------|
| **Hermes** | Outreach, Marketing, ICP | `01-Marketing/` | OpenCode (code tasks) |
| **OpenCode** | System Architecture, Code | `00-System/`, `02-Product/` | Claude (strategy) |
| **Claude** | Future Planning, Strategy | `03-Strategy/` | Hermes (outreach), OpenCode (implementation) |

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
