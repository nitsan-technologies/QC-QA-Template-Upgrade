# Common template upgrade workflow

Use this for **every** `ns_theme_*` / Content Blocks upgrade. Details and templates live in the [`typo3-qa-clickup`](.cursor/skills/typo3-qa-clickup/SKILL.md) skill.

## Phases

1. **Intake** — Load `projects/{slug}-intake.md` or the chat paste. Confirm a summary with **no secrets echoed**.
2. **Mandatory interactive FE smoke** — On staging **and** live (same steps): submit site search, click main nav + key subnav, footer legal, primary CTAs, language switch, forms only if allowed. Screenshot-only compare is not enough.
3. **Live vs staging filter** — File **staging-only** confirmed majors. Do not file issues that also exist on live / match expected theme behavior.
4. **Backend** — Login, check logs, FormEngine for this theme’s CEs, save from Layout on a real page → cache clear → FE. Check Layout CE preview is **once per element** (no duplicates).
5. **Content elements** — Discover **this** theme’s CEs (never copy another theme’s list). Follow [`CE-REAL-EDITOR.md`](.cursor/skills/typo3-qa-clickup/CE-REAL-EDITOR.md): one hidden QA page under site root, one CE at a time, FormEngine fields, FAL before image asserts, file majors immediately.
6. **ClickUp** — Each confirmed major: Description / Steps / Actual / Expected / Environment / Evidence. Filing mode from intake. Default assignee Mahesh unless overridden. Follow skill **Filing hygiene** (no speculative / setup-error bugs).
7. **Parent comment** — One comment on the parent QC/QA per batch (testing done / retest done). Not on every subtask.
8. **Retest** — Only issues assigned to the QA owner. **Read developer comments first.** Pass / not-a-bug → `Closed`. Fail → `in development` only if still broken (confirm with user first when they ask). Verify extra fixes mentioned on the parent even without a subtask.
9. **Cleanup → then complete** — Retest issues assigned to the QA owner, close passes, **delete QA test pages**, then parent comment tagging **intake assignee and Mahesh** (testing completed, ready for client update).

## Filing modes

- `show-first-then-ADD` — list confirmed issues; create ClickUp only after the user says ADD.
- `majors-auto` — file majors without asking.

## Evidence

Under `qa-evidence/{slug}/`: `fe/` · `issues/` · `content-blocks*/` · `retest/` · `compare/`

Prefer element-only CE shots (`fe-el-*.png`). Red-highlight the broken area. Reports go in `reports/{slug}/`.

## Out of this common kit

Blueshift Phase 2 PDF-scope items and client-confirmation tickets are project-specific. Do not treat them as the default upgrade path.

Do not patch theme or extension code unless the user explicitly asks.
