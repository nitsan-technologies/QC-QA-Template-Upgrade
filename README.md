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

- Mode: qa | dev-precheck
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

## MCP connections

| MCP | Needed for | Setup |
|-----|-----------|-------|
| Playwright (browser) | All modes | Included in `.cursor/mcp.json`. Needs Node.js 18+. Turn it on in Cursor Settings → MCP when prompted. |
| ClickUp | `qa` mode only | Cursor Settings → MCP → Add → URL `https://mcp.clickup.com/mcp` → sign in. Not needed for `dev-precheck`. |
| TYPO3 site MCP | **BE / CE testing** (scope BE, CEs, full) | Cursor Settings → MCP → Add → the project’s TYPO3 MCP URL (e.g. `https://<site-host>/mcp`). Must show green before BE/CE testing. Put its name in intake. FE-only runs don’t need it. |

**MCP connect notes:** `GET /mcp` returning `{"error":"Missing authentication token"}` with `WWW-Authenticate: Bearer` means the MCP endpoint is up and waiting for a token — it is not a 404. Complete Cursor OAuth, or use a personal Bearer token from AI Foundation → MCP. If staging also has **HTTP Basic Auth**, Cursor cannot send both `Authorization: Basic` and `Authorization: Bearer`. Prefer excluding `/mcp` and `/.well-known/oauth-*` from Basic, or put Basic in the URL userinfo and the MCP token in the path (`/mcp/r/{token}`) / `?token=`.

## Developer pre-check (before passing to QA)

```text
Use typo3-qa-clickup. Theme upgrade QA intake:
- Mode: dev-precheck
- Project slug:
- Theme key (ns_theme_…):
- Staging FE:
- Staging BE:
- BE user / pass: (session only)
- Live FE:
- FE Basic Auth: (optional)
- Scope: FE | BE | CEs | full
- CE list: discover
- TYPO3 site MCP name: (required for BE / CEs / full)
```

No ClickUp changes. Findings go to `reports/{slug}/precheck-*.md`; the run ends with **Ready for QA** or **Fix before passing to testing**.

## Required to start testing

`qa` mode: project slug, staging FE, staging BE, BE login, ClickUp parent, scope, filing mode, assignee.
`dev-precheck` mode: project slug, staging FE, staging BE, BE login, scope.
Both modes: TYPO3 site MCP connected when scope includes BE or CEs.

**Mandatory on every template upgrade** (this theme / this site only — see skill): Site Set assigned and working; Administration log php errors; live vs staging design crop/wrap and form-field background; Upgrade wizard remaining tables/fields + wizards; Environment test mail **received** (not only “sent”).

**To file issues:** ClickUp token (session).  
**For staging-only decisions:** live FE URL.

## What this kit is not

- Not Porto / t3karma Live-vs-Local (`Karma-Upgrade-QA`)
- Not Blueshift Phase 2 PDF-scope / client-query extras
- Not a theme-code patch workspace — file findings only unless asked to patch
