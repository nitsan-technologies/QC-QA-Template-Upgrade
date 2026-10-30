---
name: typo3-qa-clickup
description: >-
  Nitsan TYPO3 FE/BE QA with ClickUp filing for theme/template upgrade projects
  (any ns_theme_* / Content Blocks). Use when testing staging FE/BE, content
  elements/CEs, blank-image crashes, retest/close ClickUp issues, QC/QA comments,
  or find→Add issue→resume flows on a theme upgrade.
---

# TYPO3 Theme Upgrade QA + ClickUp (Nitsan)

Reusable FE/BE QA for **any** TYPO3 theme / template upgrade.  
**Never assume** theme key, URLs, CE set, or ClickUp parent — load intake first.

## When this skill applies
- FE/BE review, Content Blocks / CE testing, staging vs live
- Retest / close / reopen ClickUp issues
- User shares QC/QA parent + token, or says ADD / file majors
- Theme upgrade, template update, `ns_theme_*`, Content Blocks QA
- Developer self-check before passing a task to QA testing (`dev-precheck`)

## First action
1. Read [`PROJECT-INTAKE.md`](PROJECT-INTAKE.md).
2. If a filled `projects/{slug}-intake.md` (or chat paste) exists, use it.
3. If required fields are missing → **ask only for missing fields**. Do not invent URLs, credentials, CE lists, or ClickUp IDs.
4. Do **not** reuse another project’s theme CE matrix, staging host, or parent task.
5. **TYPO3 site MCP** must be connected when scope includes BE or CEs. Check it responds before BE/CE work; if missing or erroring, ask the user to connect it (Cursor Settings → MCP) and continue with FE only until it is.
6. **Mode** (`qa` | `dev-precheck`) is required — ask if missing. In `dev-precheck`, follow **Developer pre-check mode** below; it overrides every ClickUp rule in this skill.

## Developer pre-check mode (`dev-precheck`)

A developer runs this **before moving the task to QA testing**, to catch issues QA would find.

- Run the same testing: mandatory interactive FE smoke, live vs staging filter, BE, CEs per [`CE-REAL-EDITOR.md`](CE-REAL-EDITOR.md), filing hygiene.
- **No ClickUp writes at all** — no issues, comments, status changes, or assignments. ClickUp parent, token, assignee, and filing mode are not required.
- Report each confirmed issue in chat and in `reports/{slug}/precheck-{YYYY-MM-DD}.md` using the issue template (Description / Steps / Actual / Expected / Environment / Evidence). Evidence under `qa-evidence/{slug}/precheck/`.
- On rerun after fixes, re-verify the previous report’s open items first, then repeat the smoke.
- Finish: **delete QA test pages**, then give a verdict — **Ready for QA** (no open majors) or **Fix before passing to testing** (list open items). Skip retest and closeout.

## Hard operating rules

1. **Find → Add issue → resume** — never wait for the full suite. Confirm major → ClickUp → continue.
2. **Majors → ClickUp without asking** once filing mode is `majors-auto` (or user said so).
3. **`show-first-then-ADD`** — list confirmed issues first; create ClickUp only after user says ADD.
4. **Confirmed issues only** — no speculative bugs. See **Filing hygiene** below.
5. **Issue body:** Description / Steps / Actual / Expected (+ environment + evidence).
6. **Assignee:** no default. Use the intake assignee; if missing, **ask the user** before filing the first issue. Resolve the name to a ClickUp user id. Real ClickUp @mention when tagging.
7. **Comments:** one comment on **parent QC/QA** per batch — not on every subtask. Assignment alone is enough for new issues. Short close/reopen notes on the subtask itself are OK.
8. **Retest:** only issues assigned to the QA owner. Always **read developer comments first**. Then: **Pass / not-a-bug → `Closed`**. **Fail → `in development`** only when still broken after that review (+ tagged comment + evidence). If the user asks to **confirm before reopen**, propose the action and wait — do not auto-reopen.
9. **After full BE+FE / CE testing:** parent QC/QA comment — testing done; after fixes can share with client.
10. **Cleanup before completion message:** when the CE / bug-review cycle is done, **remove QA test pages first**, then post the “testing and bug review is completed” parent comment. Do not leave QA pages after claiming complete.
11. **Client-share / demo content:** separate task; **image/video links** in description, not attachments.
12. **No theme/extension code patches** unless the user explicitly asks. File findings only.

## Filing hygiene (confirmed majors only)

Do **not** file (or close as invalid / expected if already filed) when:

| Situation | Correct action |
|-----------|----------------|
| Image/media “missing on FE” but FAL was never uploaded in BE | Upload → save → FE check first; else do not file |
| Field alleged missing on FE but **no such field in FormEngine UI** | Assert only editor-visible fields; DB-only columns ≠ bugs |
| FE rendering matches **live** / existing theme behavior (e.g. Alert description-only) | Treat as expected; do not file as staging defect |
| Embed/structure matches existing design (e.g. Map URL-only, full iframe unsupported) | Ignore / do not file |
| `pages:0` / `tt_content not allowed` after create **without page context** | Create from Layout on a real page; not a product bug |
| Live-only ops (font ACL, server 403) while staging is fine | Out of staging theme-QA scope unless intake says otherwise |

Always compare staging vs live for FE CE output before calling it staging-only.

## Retest / developer-comment review

1. Fetch comments on each assigned task **before** changing status.
2. If developer says fixed → retest → close on pass.
3. If developer says not a bug / expected / QA setup error → verify their claim → **close with a short correction comment** (do not reopen).
4. If developer mentions an **extra fix** on the parent (no dedicated subtask) — e.g. BE Layout preview showing multiple times — verify it, note it in the close/completion comment.
5. Reopen only when retest still fails **and** comments do not invalidate the bug. Prefer user confirmation when they asked for it.

## Issue template

```text
## Description
[What is wrong — concise]

## Steps to reproduce
1. …
2. …

## Actual result
[Observed — HTTP code, Oops id, missing content, etc.]

## Expected result
[Correct behavior]

## Environment
- FE: …
- BE: … (if relevant)
- Theme / CE: …

## Evidence
- [path or public image/video URL]
```

## Parent QC/QA comments

Use real ClickUp API @mentions (not markdown `@Name`). Intake developer assignee plus Mahesh on client-ready closeout. ClickUp issue/comment bodies: **plain text**, not markdown.

**Testing complete / issues filed:**
```text
Hello, @{assignee}

I have completed the FE and BE testing for the template update and added the confirmed issues as subtasks under this parent task.

Please review and fix them. Each issue includes Description, Steps, Actual, Expected, and evidence.

Once fixed, we can share an update with the client. If you need clarification, let me know.
```

**Retest / bug review complete** (only after QA test pages are removed):
```text
Hello, @{assignee} and @{Mahesh}

Testing and bug review is completed for the resolved issues (closed where fixed). We can share an update with the client.

QA test pages created for this cycle have been removed.

Open items remaining (if any) stay in development. Ready for the client update.
```

## FE / BE flow

1. Prefer checklist path from intake. Default quality bar: **zero tolerance** (minors count) unless scope says otherwise.
2. Evidence under intake evidence root; **red-highlight** the broken area. For CE FE proof prefer **element-only** shots (`fe-el-*.png`), not full-page only.
3. Live vs staging when live URL is set; mark pre-existing live issues (exclude from filing if user said staging-only).
4. Forms: submit only if intake/user allows; use provided test email. Target the real form (exclude indexed-search chrome). **Always** compare form **input background / border** vs live (see mandatory upgrade checks).
5. BE: login, then run the **mandatory template-upgrade checks** below (Site Set for this theme, Administration log, Upgrade wizard, Test mail). FormEngine for theme CEs; save from **Layout on a real page** → cache clear → FE.
6. BE Layout: check CE **preview once per element** (no duplicate preview blocks).

### Mandatory early interactive smoke (do NOT skip)

Static URL/screenshot compare alone is **not enough**. In the **first FE pass** (before claiming “no staging-only issues”), **actually use** these flows on staging **and** live (same steps):

| Check | Action | Fail if |
|-------|--------|---------|
| **Site search** | Open header/footer search → type a real term → **Submit/Enter** | Staging 404/Oops/empty while live shows results |
| **Main nav** | Click each top-level + key subnav item | Wrong page, 404, or dead link on staging only |
| **Footer legal** | Open Impressum / Datenschutz / similar | 404 or swapped content on staging only |
| **Primary CTAs** | Spenden/Kontakt/Login/etc. if present | Staging-only break |
| **Language switch** | If multi-lang flags/links exist | Staging-only 404/wrong lang |
| **Forms** | Compare field styling vs live; submit only when allowed | Staging-only fail (including input BG / border) |

Capture **live vs staging** evidence with red highlight on the staging failure. File staging-only majors per filing mode (`find → Add → resume` or show-first).

**Never** mark FE compare complete if search (or equivalent site-wide tool) was not submitted end-to-end.

### Mandatory template-upgrade checks (do NOT skip)

These are required on **every** `ns_theme_*` / template upgrade, for **this** theme and **this** site only (never copy another project’s Site Set, wizard list, or screenshots). They exist because they were missed on past upgrades. Run them in the BE pass (plus FE compare for design / form BG). Scope `FE` still does the two FE rows; scope `BE` / `CEs` / `full` must do all six.

| Check | Where | Action | Fail if |
|-------|--------|--------|---------|
| **Site Set for this template** | Sites → this site; theme `Configuration/Sets/` | Confirm **this** theme’s Site Set is assigned to **this** site. Open site settings and check values that used to live in TypoScript constants (logo, colors, contact, plugin settings). Spot-check FE that those settings apply. | Site has no Site Set, the wrong set, or TypoScript still holds theme constants that should have been migrated. Settings exist but FE ignores them. |
| **Administration log errors** | Administration → Log. Channel `php`, Levels include `error` | After upgrade traffic, list errors. File **new** upgrade-related exceptions (example: `DocHeaderComponent::setPageBreadcrumb()` TypeError, MFA `InvalidArgumentException`). Ignore inherited DDEV/import noise unless it also Oopses on staging. | PHP errors from the upgraded core / theme / BE modules remain uncleared. |
| **Design / layout parity** | Same FE section on live **and** staging | Compare card/grid image crop and aspect, text wrap (below vs beside image), CTA placement (`mehr erfahren` / equivalent). | Staging-only layout, crop, or wrap regression vs live for this template. |
| **Form field background** | Contact / any EXT:form (or theme form) on live **and** staging | Compare input/textarea **background color and border** vs live. Do this even when form submit is not allowed. | Staging fields lose the template treatment (e.g. grey fill vs white / missing border). |
| **Upgrade wizard remaining** | Admin Tools → Upgrade → Run Upgrade Wizard | Complete remaining process: create missing tables/fields first (example: `tt_content` index `parent_uid_2`), then run pending wizards. Re-open the wizard until the missing-schema block is gone. | Missing DB tables/fields still listed, or required wizards still pending after the upgrade. |
| **Test mail received** | Admin Tools → Environment → Test Mail Setup | Send to the intake test email. **Inbox delivery** is the pass — the green “Test mail sent” flash is not enough. | Mail not received (transport `mail`/`sendmail`/`smtp` misconfigured, spam, or no inbox). |

Do **not** mark BE complete if Site Set, log, upgrade wizard, or test-mail checks were skipped. Do **not** mark FE compare complete if design crop/wrap and form-field background were not compared to live.

## Content blocks / CE flow

1. **List this theme’s CEs** (intake list, or discover from theme package / BE). Never copy another theme’s CE set.
2. Share estimate + case types before deep CE work when user asks.
3. Cases: happy path (complete fields) · blank/required image edge · BE→FE edit · interactive.
4. Dedicated QA page(s) (`nav_hide`, noindex) via MCP/DataHandler when available. **Never create QA pages outside the site root page** — parent must be the site root or a folder under it (e.g. root → `misc`). Use a correct slug; avoid outside-root / autogenerated path mistakes. Full CE method: [`CE-REAL-EDITOR.md`](CE-REAL-EDITOR.md) (one CE at a time, FormEngine fields, FAL before image bugs, IRRE “Create new” not Image “Create new relation”, file majors immediately).
5. Create CEs editor-like: flexform / denormalized fields / theme JSON columns / **upload FAL** when the CE needs images / set required links (e.g. Card CTA link) before FE assert.
6. FE assert only **FormEngine-visible** fields + live parity → sample BE edits → cache clear → FE reassert.
7. Each confirmed major → ClickUp under parent → assign → evidence → **resume**.
8. Progress in `reports/`.
9. **Closeout order:** retest issues **assigned to the QA owner** (`testing` / resolved) → close tasks → **delete QA pages** → parent “bug review complete” comment tagging **intake assignee and Mahesh** (ready for client update).

## ClickUp

- ClickUp: subtasks under intake parent; statuses QA `testing` → `Closed` / `in development` per retest. **Plain text** bodies (not markdown). Real @mention via comment `tag` + user id.
- Token failure → draft in `reports/` + ask for fresh token. Never invent task IDs.
- Prefer public image/video URLs for client-share tasks.

## Evidence layout

Under intake evidence root (default `qa-evidence/`):

`fe/` · `issues/` · `content-blocks*/` · `retest/` · `compare/`

Prefer `fe-el-*.png` for CE FE failures. Scripts under `scripts/` as needed. Never claim pass without checking that case.

## What not to do

- Claim FE parity complete after screenshot-only compares (must submit search / key interactive flows)
- Skip Site Set / TypoScript-migration, Administration log, Upgrade wizard, or Test mail on a template upgrade
- Skip live vs staging form-field background and card/grid crop/wrap checks
- Hardcode a prior project’s theme, URLs, CEs, or ClickUp parent
- Wait until all CEs finish before filing majors
- Comment “additional issue added” on every subtask
- File image/FE-field bugs without upload / without FormEngine field / without live compare
- Treat page-0 create Speichern errors as theme bugs
- Reopen without reading developer comments (or without user confirm when they asked)
- Post “bug review complete” while QA test pages still exist
- Close failing issues; leave QA pages after CE close
- Store secrets in skill or committed intake files
