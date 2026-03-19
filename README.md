# Cibus Issues

Issue tracker for the **Cibus Restaurant Operating & Management System**.

> **Code lives in [`abbasali-io/Cibus-6-0`](https://github.com/abbasali-io/Cibus-6-0)**. This repo is for issue tracking only — no source code.

---

## Table of Contents

- [Apps & Labels](#apps--labels)
- [Issue Types](#issue-types)
- [How to Create an Issue](#how-to-create-an-issue)
- [DOs and DON'Ts](#dos-and-donts)
- [Severity Levels](#severity-levels)
- [Priority Labels](#priority-labels)
- [Example Issues](#example-issues)

---

## Apps & Labels

Cibus consists of 7 apps. Always tag the affected app in the issue title and label appropriately.

| App | Port | Label | Title Prefix |
|-----|------|-------|-------------|
| Admin | 5175 | — | `Admin:` |
| Customer | 8080 | — | `Customer:` |
| KDS (Kitchen) | 5174 | — | `KDS:` |
| POS | 5176 | `pos` | `POS:` |
| Sales | 5178 | — | `Sales:` |
| Staff | 5177 | — | `Staff:` |
| Super Admin | 5176 | — | `Super Admin:` |

### Available Labels

| Label | Use For |
|-------|---------|
| `bug` | Something isn't working |
| `enhancement` | New feature or request |
| `i18n` | Localization & translation issues |
| `PH` | High Priority |
| `PM` | Medium Priority |
| `PL` | Low Priority |
| `pos` | POS-specific issues |
| `duplicate` | Already reported |
| `wontfix` | Will not be worked on |

---

## Issue Types

### 1. Bug Report
For broken functionality, incorrect behavior, visual glitches, or data inconsistencies.

### 2. Feature Request / Enhancement
For new functionality, improvements, or missing capabilities.

### 3. i18n / Translation Issue
For missing translations, raw i18n keys shown to users, or RTL layout problems.

### 4. QA Bug (from Testing Sessions)
Bugs discovered during structured QA testing sessions, migrated from test logs.

---

## How to Create an Issue

### Bug Report Template

**Title format:** `[App] Brief description of the bug`

Examples:
- `POS: Shift header counter ignores QR orders`
- `Admin: Payment detail renders orphaned bare 0 row`
- `Customer: Cart service charge label shows 1% instead of 10%`

**Body:**

````markdown
## Bug Description

**App**: [Admin / Customer / KDS / POS / Sales / Staff / Super Admin]
**Page/Route**: [e.g., `/admin/payments`, `Orders list / Live Orders`]
**Severity**: [Critical / High / Medium / Low]

## Summary

[One or two sentences describing the defect clearly.]

## Steps to Reproduce

1. [Step 1]
2. [Step 2]
3. [Step 3]

## Expected Behavior

[What should happen.]

## Actual Behavior

[What actually happens.]

## Evidence

[Screenshots, console errors, or session references if available.]

## Environment (if relevant)

- Browser: [e.g., Chrome 120]
- Language: [e.g., en, zh, ar]
- Device: [e.g., Desktop, iPad]
````

---

### Feature Request Template

**Title format:** `[App]: Feature description`

Examples:
- `Sales: Enforce and implement agent commission`
- `Admin: Add bulk menu item import`

**Body:**

````markdown
## Feature Request

**App**: [Admin / Customer / KDS / POS / Sales / Staff / Super Admin]
**Priority**: [High / Medium / Low]

## Description

[Clear description of the feature or enhancement.]

## Use Case

[Why this is needed. Who benefits and how.]

## Acceptance Criteria

- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

## Technical Notes (optional)

[Any relevant technical context — database tables, existing hooks, related code.]
````

---

### i18n / Translation Issue Template

**Title format:** `I18N-BUG-NNN: [Page/area] description`

Examples:
- `I18N-BUG-012: POS pages content not translated to Chinese + sidebar "Shifts"`
- `I18N-BUG-008: Staff page shows raw i18n keys (CRITICAL)`

**Body:**

````markdown
## Bug Description

**Pages**: [Route path(s), e.g., `/admin/pos/terminals`]
**Severity**: [Critical / High / Medium / Low]
**Language**: [e.g., Simplified Chinese, Arabic]

### What's broken

- **Element**: "Visible text" — ENGLISH / RAW KEY
- **Element**: `raw.i18n.key.shown` — RAW KEY
[List every untranslated element on the page.]

### What's working

- [Element] ✅
[List elements that are correctly translated, for context.]

### Fix

1. [Specific file/key change needed]
2. [Another specific change]
````

---

### QA Bug Template (from Testing Sessions)

**Title format:** `[QA][BUG-NNN] Brief description`

Examples:
- `[QA][BUG-018] Group order payment status remains Unpaid after completed POS cash payment`
- `[QA][BUG-026] POS Orders list does not reflect kitchen status changes from KDS`

**Body:**

````markdown
Bug ID: BUG-NNN
App: [Admin / Customer / KDS / POS / Sales / Super Admin]
Page: [Affected page or route]
Severity: [Critical / High / Medium / Low]

**Summary:**
[Clear, concise description of the defect.]

**Expected:**
[What the correct behavior should be.]

**Session evidence:**
[Reference to QA session, test case ID, or observation details.]
````

---

## DOs and DON'Ts

### ✅ DO

1. **Use a clear, descriptive title** — someone should understand the issue from the title alone
2. **Specify the app** — always include which app (Admin, POS, Customer, etc.)
3. **Include the page/route** — where exactly does the issue occur?
4. **Set severity** — Critical, High, Medium, or Low
5. **Add reproduction steps** — how can someone else reproduce this?
6. **Describe expected vs. actual** — what should happen vs. what does happen
7. **Attach evidence** — screenshots, console errors, session logs
8. **Apply relevant labels** — `bug`, `i18n`, `pos`, priority labels, etc.
9. **Reference related issues** — if this is connected to another issue, link it
10. **Search before creating** — check if the issue already exists
11. **One bug per issue** — keep issues focused and atomic
12. **Use severity consistently** — refer to the [Severity Levels](#severity-levels) table

### ❌ DON'T

1. **Don't use vague titles** — avoid "Something is broken" or "Fix the page"
2. **Don't skip the app identifier** — every issue must specify which app
3. **Don't bundle multiple bugs** — one issue per bug; don't combine unrelated problems
4. **Don't include code solutions in the title** — titles describe the *problem*, not the fix
5. **Don't paste full stack traces without context** — summarize the error, then use a `<details>` block
6. **Don't create issues for typos in code** — fix those directly in PRs
7. **Don't assign priority without justification** — explain why it's high/critical
8. **Don't leave the body empty** — every issue needs a description, even minimal
9. **Don't reopen closed issues for new problems** — create a new issue and reference the old one
10. **Don't include sensitive data** — no API keys, passwords, customer PII, or credentials
11. **Don't duplicate issues** — search existing issues first; if found, comment on the existing one
12. **Don't mix feature requests with bug reports** — use the correct template for each

---

## Severity Levels

| Severity | Definition | Examples |
|----------|-----------|----------|
| **Critical** | App crash, data loss, or complete feature failure blocking business operations | Payment processing fails, orders lost, authentication broken |
| **High** | Major feature broken, significant user impact, no workaround | Status not syncing across apps, incorrect calculations, raw i18n keys on critical pages |
| **Medium** | Feature partially broken, workaround available, or cosmetic issue on important elements | Stale data until refresh, minor calculation display errors, missing translations on secondary pages |
| **Low** | Minor cosmetic issue, edge case, or improvement suggestion | Alignment off, tooltip missing, rare edge case behavior |

---

## Priority Labels

| Label | Meaning | Response |
|-------|---------|----------|
| `PH` | High Priority | Address in the current sprint |
| `PM` | Medium Priority | Plan for next sprint |
| `PL` | Low Priority | Backlog — address when capacity allows |

---

## Example Issues

### Good Bug Report ✅

> **Title:** `[QA][BUG-026] POS Orders list does not reflect kitchen status changes from KDS`
>
> - **App**: POS
> - **Page**: Orders list / Live Orders
> - **Severity**: Medium
> - Clear summary of the sync issue
> - Expected behavior specified
> - Session evidence referenced

### Good i18n Report ✅

> **Title:** `I18N-BUG-012: POS pages content not translated to Chinese + sidebar "Shifts"`
>
> - Pages and routes specified
> - Every untranslated element listed individually
> - Working elements listed for context
> - Specific fix steps provided (which files/keys to change)

### Bad Issue ❌

> **Title:** `It's broken`
>
> **Body:** `The page doesn't work`
>
> *Problems: No app specified, no page, no severity, no steps to reproduce, no details whatsoever.*

---

## Cross-App Issues

When a bug spans multiple apps (e.g., KDS status not syncing to POS), file the issue under the **primary affected app** and reference the other apps in the body.

Example: `[QA][BUG-026] POS Orders list does not reflect kitchen status changes from KDS`

---

## Linking Issues

- Reference related issues: `Related to #91`
- Mark duplicates: `Duplicate of #42` and apply the `duplicate` label
- Reference code repo commits: `Fixed in abbasali-io/Cibus-6-0@<commit-sha>`

---

*Maintained by the Cibus development team.*
