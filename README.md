# Template Upgrade Agent Kit

Reusable Nitsan QA kit for **any** TYPO3 theme / template upgrade (`ns_theme_*`, Content Blocks).

Same operating model as the Blushift upgrade workspace: **intake first → interactive FE smoke → staging-only filter → BE/CE testing → find → Add ClickUp → resume**.

Do **not** assume theme key, URLs, CE set, or ClickUp parent. Load intake every time.

## Start here

1. Paste the chat block from [`PROJECT-INTAKE.md`](.cursor/skills/typo3-qa-clickup/PROJECT-INTAKE.md), or save `projects/{slug}-intake.md` (no passwords or tokens).
2. Agent follows [`typo3-qa-clickup`](.cursor/skills/typo3-qa-clickup/SKILL.md) and [`WORKFLOW.md`](WORKFLOW.md).
3. Secrets stay session-only (chat or env). Never commit them.

## Chat trigger

```text
Use typo3-qa-clickup. Theme upgrade QA intake:

- Project slug:
- Theme key (ns_theme_…):
- Staging FE:
- Staging BE:
- BE user / pass: (session only)
- Live FE:
- FE Basic Auth: (optional)
- ClickUp parent QC/QA:
- ClickUp token: (session only)
- Scope: FE | BE | CEs | full
- Filing: majors-auto | show-first-then-ADD
- CE list: discover
- Forms submit: no
- Assignee: (required)
```

## Folders

| Path | Purpose |
|------|---------|
| [`.cursor/skills/typo3-qa-clickup/`](.cursor/skills/typo3-qa-clickup/) | QA + ClickUp skill and intake template |
| [`.cursor/rules/typo3-qa-clickup.mdc`](.cursor/rules/typo3-qa-clickup.mdc) | Always-on process rule |
| [`projects/`](projects/) | Per-project `{slug}-intake.md` (no secrets) |
| [`reports/`](reports/) | Confirmed issues, CE matrices, compare notes |
| [`qa-evidence/`](qa-evidence/) | Screenshots and probes (`{slug}/fe`, `issues`, `content-blocks`, `retest`, `compare`) |
| [`scripts/`](scripts/) | Optional helpers later — v1 has no DTS/Blueshift-hardcoded scripts |
| [`WORKFLOW.md`](WORKFLOW.md) | Common phases for a new chat |
| [`AGENTS.md`](AGENTS.md) | Read order for the agent |

## Required to start testing

Project slug, staging FE, staging BE, BE login, ClickUp parent, scope, filing mode, assignee.

**To file issues:** ClickUp token (session).  
**For staging-only decisions:** live FE URL.

## What this kit is not

- Not Porto / t3karma Live-vs-Local (`Karma-Upgrade-QA`)
- Not Blueshift Phase 2 PDF-scope / client-query extras
- Not a theme-code patch workspace — file findings only unless asked to patch
