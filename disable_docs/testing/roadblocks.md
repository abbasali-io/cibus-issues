---
layout: default
title: Roadblocks
parent: Testing Manuals
nav_order: 9
---

# Cibus Test Session — Roadblocks & Early Findings

> **Session Date**: 2026-03-15
> **Tester**: Claude (AI-assisted)
> **Status**: ROADBLOCK-004 resolved — full test suite resumed in Session 2 (2026-03-15)

---

## Why Testing Was Halted

The POS app cannot load past the "Open Shift" screen due to a data integrity issue (multiple stale open shifts in the database from the previous test session). This blocks all POS-dependent tests: **CROSS-010, CROSS-011**, and the POS verification steps within **CROSS-001, CROSS-002, CROSS-003, CROSS-020**.

Testing was stopped to avoid generating further polluted data and to surface the blockers clearly for the development team.

---

## Blockers

### ROADBLOCK-004: POS — Multiple Open Shifts Cause Infinite Shift-Open Loop — ✅ RESOLVED (Session 2)
- **Severity**: Critical (blocks all POS testing)
- **Page**: POS > Open Shift
- **Root Cause**: From the previous test session, BUG-011 (shift auto-closes after payment) left one or more shifts in an `open` status without being properly closed. When opening a new shift today:
  1. `POST /pos_shifts` → **201 Created** — new shift is written successfully ✅
  2. `GET /pos_shifts?terminal_id=...&status=eq.open` → **300 Multiple Choices** — Supabase/PostgREST returns HTTP 300 because multiple rows with `status=open` exist for this terminal, but the app expects exactly 0 or 1
  3. POS silently resets to the Count Float screen with no error message — the newly created shift is also orphaned
- **Effect**: POS is completely inaccessible. Navigating directly to `/tables` or `/orders` redirects back to `/shift-open`. Admin has no shift management UI (`/admin/pos` returns 404).
- **Workaround needed**: A developer must manually set `status = 'closed'` on all stale open shifts for terminal `f200088b-55f0-4c10-aab0-56474cb734ac` in the `pos_shifts` table. Alternatively, the POS code should handle the 300 gracefully (e.g. use `limit=1` + take the most recent open shift, rather than calling `.single()` after the query).
- **Tests blocked**: CROSS-010, CROSS-011, and POS verification steps in CROSS-001/002/003/020

---

## Bugs Confirmed Fixed ✅

These bugs from the previous session were verified as fixed during setup before testing was halted.

### BUG-002: KDS — Untranslated i18n Keys on Station Queue — ✅ FIXED
- Previously `station.no_in_progress` and `station.no_ready` showed as raw keys
- Now shows: **"No orders in progress"** and **"No orders ready"** — fully translated

### BUG-003: POS — Quick Select Float Buttons Don't Persist Value — ✅ FIXED
- Previously clicking £100 displayed the value but failed validation with "Please enter a valid starting float"
- Now: Clicking £100 correctly populates the field, passes validation, and advances to the Confirm step showing **£100.00**

---

## Bugs Partially Fixed ⚠️

### BUG-001: Admin — Untranslated i18n Keys on Floor Plan / Tables Page — ⚠️ PARTIALLY FIXED
- **Fixed**: `floor.table_title`, `floor.manage_tables_desc`, `floor.details`, `floor.generate_qr`, `floor.remove_table_warning` — all now display correct English text ✅
- **Still broken**: `Floor.Shape_rectangle` (and likely `Floor.Shape_square` etc.) — the shape label in the table detail panel still shows the raw key

---

## New Bugs Found During Setup

### BUG-013: Admin Dashboard — Multiple Untranslated i18n Keys (NEW)
- **Severity**: Medium
- **Page**: Admin > Dashboard (main overview)
- **Details**: The following keys are displayed as raw strings on the dashboard:
  - `status.active` (restaurant status badge — should be "Active")
  - `status.maintenance` (restaurant status badge — should be "Maintenance")
  - `view_all` (link in Restaurant Performance section)
  - `dashboard.activity.order`, `dashboard.activity.alert`, `dashboard.activity.staff`, `dashboard.activity.revenue`, `dashboard.activity.schedule` (Recent Activity feed items)
- **Expected**: All labels should display translated English values

### BUG-014: POS — Open Shift Fails Silently on Backend Error (NEW)
- **Severity**: High
- **Page**: POS > Open Shift > Confirm step
- **Details**: When the `POST /pos_shifts` succeeds (201) but the subsequent `GET` for the active shift returns a non-200 response (e.g. 300 due to multiple open shifts), the app silently resets to the Count Float screen with no error message. The user has no indication of what went wrong or what to do.
- **Expected**: If the shift cannot be loaded after creation, an error message should be shown (e.g. "Could not open shift — please contact your manager")

---

## What Was Not Yet Tested (Session 1)

These tests were blocked/not reached in Session 1, but were completed in Session 2:

| Test | Bug Checks | Session 1 Status | Session 2 Status |
|------|-----------|-----------------|-----------------|
| CROSS-001: Complete Order Lifecycle | BUG-004, BUG-005, BUG-007, BUG-008 | ⏭️ Not reached | ✅ PASS (BUG-007 fixed) |
| CROSS-002: Multi-Station Order | BUG-009 | ⏭️ Not reached | ✅ PASS (BUG-009 fixed) |
| CROSS-003: Modifiers & Special Instructions | (new test) | ⏭️ Not reached | ⚠️ PARTIAL (no modifiers in menu) |
| CROSS-010: POS Order to Kitchen | BUG-006 | ❌ Blocked (ROADBLOCK-004) | ✅ PASS |
| CROSS-011: POS Payment Flow | BUG-010, BUG-011, BUG-012 | ❌ Blocked (ROADBLOCK-004) | ✅ PASS (all 3 bugs fixed) |
| CROSS-020: Group Order Lifecycle | — | ⏭️ Not reached | ⚠️ PARTIAL (multi-user limited by single browser) |

---

## Recommended Next Steps

1. **Fix ROADBLOCK-004** — Developer closes stale open shifts in `pos_shifts` table for terminal `f200088b-55f0-4c10-aab0-56474cb734ac`
2. **Fix BUG-014** — POS should show a meaningful error if the shift GET fails, not silently reset
3. **Fix BUG-013** — Translate remaining dashboard keys (`status.active`, `status.maintenance`, `view_all`, `dashboard.activity.*`)
4. **Fix BUG-001 remainder** — Translate `Floor.Shape_*` keys in the table detail panel
5. Once POS is unblocked, resume testing from **CROSS-001** through **CROSS-020**
