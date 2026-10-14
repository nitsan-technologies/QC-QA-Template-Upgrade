# Theme Upgrade QA — Project Intake

Fill this for **each** theme / template upgrade. Paste into chat or save as `projects/{project-slug}-intake.md`.

Do **not** put passwords or ClickUp tokens in git-tracked files if the repo is shared — paste those in chat or use env for the session.

---

## Chat paste (copy for a new project)

```text
Theme upgrade QA intake:
- Mode: qa | dev-precheck
- Project slug:
- Theme key (ns_theme_…):
- Staging FE:
- Staging BE:
- BE user / pass: (session only)
- Live FE: (optional)
- FE Basic Auth: (optional)
- ClickUp parent QC/QA:
- ClickUp token: (session only)
- Scope: FE | BE | CEs | full
- Filing: majors-auto | show-first-then-ADD
- CE list: discover | (comma-separated CTypes)
- Checklist path: (optional)
- Evidence root: qa-evidence/
- Forms submit: yes/no + test email (if yes)
- Assignee: (required — who gets the ClickUp issues)
- MCP / site name: (optional)
- Known issues / skip: (optional)
```

---

## Full intake

| Field | Value |
|-------|--------|
| Mode | `qa` / `dev-precheck` (dev-precheck: no ClickUp fields needed) |
| Project slug | |
| Project display name | |
| Theme extension | |
| TYPO3 version | |
| DDEV / project path | |
| Staging FE URL | |
| Staging BE URL | |
| Live FE URL | |
| FE Basic Auth user/pass | session only |
| BE user/pass | session only |
| Theme / site MCP name | |
| ClickUp parent QC/QA | |
| ClickUp token | session only |
| Assignee ClickUp user id | required — ask if missing (no default) |
| Scope | FE / BE / CEs / full |
| Filing mode | majors-auto / show-first-then-ADD |
| CE / Content Block list | discover / list: |
| Checklist markdown path | |
| Evidence root | `qa-evidence/` |
| Reports root | `reports/` |
| Known issues / out of scope | |
| Forms submit allowed? | yes / no + test email |
| Notes | |

---

## After intake

1. Agent confirms intake summary (**no secrets echoed**).
2. If CEs = `discover` → list from theme package / BE (this theme only).
3. Estimate time + case types; then run FE/BE/CE per `typo3-qa-clickup` + `CE-REAL-EDITOR.md`.
