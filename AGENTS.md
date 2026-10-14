# Template Upgrade — agent entry

This workspace is a reusable kit for TYPO3 theme / template upgrade QA. It is not tied to one client.

## Read order (every chat)

1. This file.
2. [`WORKFLOW.md`](WORKFLOW.md) for the common phases.
3. Skill [`typo3-qa-clickup`](.cursor/skills/typo3-qa-clickup/SKILL.md) and [`CE-REAL-EDITOR.md`](.cursor/skills/typo3-qa-clickup/CE-REAL-EDITOR.md).
4. Intake template [`PROJECT-INTAKE.md`](.cursor/skills/typo3-qa-clickup/PROJECT-INTAKE.md).
5. Filled `projects/{slug}-intake.md` or the user’s chat paste.

If required intake fields are missing, ask **only** for those. Do not invent URLs, credentials, CE lists, or ClickUp IDs. Do not reuse another project’s theme, staging host, or parent task.

## Defaults

- Loop: **find → Add ClickUp issue → resume**
- Filing mode from intake (`majors-auto` or `show-first-then-ADD`)
- Issue body: Description / Steps / Actual / Expected / Environment / Evidence
- Assignee: no default — use the intake assignee; if missing, ask the user before filing
- One comment on the parent QC/QA per batch
- Retest: read developer comments first; pass / not-a-bug → `Closed`; fail → `in development` only if still broken (confirm reopen when user asks)
- Filing hygiene: upload FAL before image bugs; FormEngine-visible fields only; live/expected parity ≠ staging bug; no page-0 Speichern false positives
- Closeout: remove QA test pages **before** the “bug review complete” parent comment; tag intake assignee **and Mahesh**; ready for client update
- After CE/FE/BE testing: also retest ClickUp issues **assigned to the QA owner** (`testing` / resolved)
- ClickUp bodies: plain text; real API @mentions; evidence = screenshots + URLs
- Secrets: session only — never write passwords or tokens into intake files
