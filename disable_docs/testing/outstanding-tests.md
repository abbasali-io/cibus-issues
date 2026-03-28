---
layout: default
title: Outstanding Tests
parent: Testing Manuals
nav_order: 8
---

# Cross-App Tests — Living Status Tracker

> **Last Updated**: 15 March 2026 (Session 3)
> **Total Tests**: 41 | **Completed**: 8 | **Partial**: 5 | **Blocked**: 3 | **Not Started**: 25

---

## Overall Progress

| Status | Count | % |
|--------|:-----:|:-:|
| ✅ Passed | 8 | 20% |
| ⚠️ Partial | 5 | 12% |
| 🚫 Blocked | 3 | 7% |
| ⬜ Not Started | 25 | 61% |

### Progress by Priority

| Priority | Total | Done | Partial | Blocked | Remaining |
|----------|:-----:|:----:|:-------:|:-------:|:---------:|
| P0 | 13 | 5 | 3 | 1 | 4 |
| P1 | 23 | 3 | 2 | 2 | 16 |
| P2 | 5 | 0 | 0 | 0 | 5 |

---

## Section 1: Customer → Kitchen → Serve (Happy Path)

| ID | Test Name | Priority | Status | Session | Notes |
|----|-----------|:--------:|:------:|---------|-------|
| CROSS-001 | Complete Order Lifecycle | P0 | ⚠️ PARTIAL | 1/2 | Core flow tested across Sessions 1–2 as part of CROSS-010 happy path. Modifiers not fully tested. |
| CROSS-002 | Multi-Station Order | P0 | ⬜ NOT STARTED | — | Needs items routed to different KDS stations (e.g. Drinks Kitchen + Main Kitchen in single order). Coffee item exists in Drinks category. |
| CROSS-003 | Order with Modifiers and Special Instructions | P0 | ⬜ NOT STARTED | — | Needs order with size variant, modifiers, and special instructions. Verify display on KDS ticket, Admin, and POS. |

---

## Section 2: POS Counter Order Flow

| ID | Test Name | Priority | Status | Session | Notes |
|----|-----------|:--------:|:------:|---------|-------|
| CROSS-010 | POS Order to Kitchen | P0 | ✅ PASS | 1/2 | POS order submitted, appeared on KDS and Admin. |
| CROSS-011 | POS Payment Flow | P0 | ✅ PASS | 3 | Full flow: POS order → KDS process → cash payment → Admin verified. Tested during CROSS-060. |
| CROSS-012 | POS Card Payment | P1 | ⬜ NOT STARTED | — | Need to test card payment with reference number via POS. |
| CROSS-013 | POS Multiple Orders per Table | P1 | ⚠️ PARTIAL | 1/2/3 | Multiple orders placed on same table (M2) across sessions. Not formally verified as distinct test — need to verify both orders show as separate KDS tickets and Admin entries. |

---

## Section 3: QR Dine-In Group Order Flow

| ID | Test Name | Priority | Status | Session | Notes |
|----|-----------|:--------:|:------:|---------|-------|
| CROSS-020 | Complete Group Order Lifecycle | P0 | ⚠️ PARTIAL | 1/2 | Single-guest group order tested end-to-end. Multi-guest blocked by shared browser session (RDBLK-003). Needs second device or incognito. |
| CROSS-021 | Group Order Cart Lock | P1 | ⬜ NOT STARTED | — | Requires multi-guest setup. Test that host can lock cart and prevent further additions. |
| CROSS-022 | Group Order Bill Split | P1 | ⬜ NOT STARTED | — | Requires multi-guest setup. Test split payment options at checkout. |

---

## Section 4: Real-time Sync Across Apps

| ID | Test Name | Priority | Status | Session | Notes |
|----|-----------|:--------:|:------:|---------|-------|
| CROSS-030 | Order Creation Sync | P0 | ✅ PASS | 3 | All 4 apps received order within seconds. No manual refresh needed. |
| CROSS-031 | Kitchen Status Sync | P0 | ⚠️ PARTIAL PASS | 3 | Customer App + Admin sync at all stages. **POS does NOT sync** (BUG-026). |
| CROSS-032 | Payment Sync | P1 | ✅ PASS | 3 | Cash payment via POS synced to Admin (order "Paid", payment in Payments list). Tested during CROSS-060. |
| CROSS-033 | Table Status Sync | P1 | ⚠️ PARTIAL | 3 | POS table turned green after payment (Available). Admin table status not explicitly verified — Admin Floor Plan shows tables but sync not formally tested. |

---

## Section 5: Menu Configuration → Customer Display

| ID | Test Name | Priority | Status | Session | Notes |
|----|-----------|:--------:|:------:|---------|-------|
| CROSS-040 | Menu Item Visibility | P0 | ✅ PASS | 3 | New item created in Admin appeared in Customer App after reload. |
| CROSS-041 | Price Change Propagation | P0 | ✅ PASS | 3 | Price change in Admin reflected in Customer App after reload. |
| CROSS-042 | Out of Stock Propagation | P1 | ⬜ NOT STARTED | — | Mark item as out-of-stock in Admin, verify Customer App and POS show unavailable. |
| CROSS-043 | Category Changes | P1 | ⬜ NOT STARTED | — | Move item between categories in Admin, verify Customer App updates. |
| CROSS-044 | Modifier Configuration → Display | P1 | ⬜ NOT STARTED | — | Add new modifier in Admin, verify it appears in Customer App and flows through to KDS. |

---

## Section 6: Tax & Pricing Consistency

| ID | Test Name | Priority | Status | Session | Notes |
|----|-----------|:--------:|:------:|---------|-------|
| CROSS-050 | Tax Calculation Consistency | P0 | ⚠️ PARTIAL PASS | 3 | Tax **amounts** consistent across all 4 apps. Labels differ: "VAT (20%)" / "VAT" / "Tax" (BUG-020). POS order detail omits Service Charge line (BUG-027). |
| CROSS-051 | Service Charge Consistency | P1 | ⚠️ PARTIAL | 3 | SC amount (10%) correct across Customer App, POS edit view, Admin. POS order detail panel omits SC line (BUG-027). |
| CROSS-052 | Tax Change Propagation | P1 | ⬜ NOT STARTED | — | Change tax rate in Admin, verify both Customer App and POS use new rate. |
| CROSS-053 | Multi-Tax Scenario | P2 | ⬜ NOT STARTED | — | Only single tax (VAT 20%) configured currently. Would need second tax to test. |
| CROSS-054 | Discount + Tax Interaction | P1 | ⬜ NOT STARTED | — | Need to test voucher/discount code and verify tax calculated on discounted amount. |
| CROSS-055 | Currency Display Consistency | P1 | ✅ PASS | 1/2/3 | All apps consistently show £ (GBP). No mismatches observed across all sessions. |

---

## Section 7: Payment Reconciliation

| ID | Test Name | Priority | Status | Session | Notes |
|----|-----------|:--------:|:------:|---------|-------|
| CROSS-060 | Cash Payment Tracking | P0 | ✅ PASS | 3 | Cash payment £9.04 processed. POS shift counter updated correctly (£25.94/1 → £34.98/2). Admin Payments shows record. Note: only 1 cash payment tested, spec says 3. Also found BUG-028 (Taxes Collected £0.00) and BUG-029 (Payment Methods chart empty). |
| CROSS-061 | Mixed Payment Methods | P1 | ⬜ NOT STARTED | — | Need to process both cash and card payments in same shift, then verify shift report breakdown. |
| CROSS-062 | Online Payment Tracking | P1 | ⬜ NOT STARTED | — | Need to pay via Customer App (Stripe) and verify payment tracked in Admin. |

---

## Section 8: Order Cancellation Flows

| ID | Test Name | Priority | Status | Session | Notes |
|----|-----------|:--------:|:------:|---------|-------|
| CROSS-070 | Cancel Before Kitchen | P0 | 🚫 BLOCKED | 3 | No cancel/void mechanism found. Admin has no cancel button. POS Manager Actions is PIN-locked. Customer App has no cancel option. |
| CROSS-071 | Cancel After Kitchen Claim | P1 | 🚫 BLOCKED | 3 | Same blocker as CROSS-070. POS Manager Actions PIN unknown. |
| CROSS-072 | POS Void Item After Kitchen | P1 | 🚫 BLOCKED | 3 | Same blocker. Void requires Manager Actions PIN. |

**Blocker**: All cancellation tests require either (a) a cancel feature to be implemented in Admin/Customer, or (b) the POS Manager Actions 4-digit PIN to be provided.

---

## Section 9: Staff & Permission Cross-App

| ID | Test Name | Priority | Status | Session | Notes |
|----|-----------|:--------:|:------:|---------|-------|
| CROSS-080 | Staff Access Control (Cashier → POS only) | P1 | ⬜ NOT STARTED | — | Create cashier-role staff in Admin, verify POS access granted, KDS access denied. |
| CROSS-081 | Kitchen Staff Access (Kitchen → KDS only) | P1 | ⬜ NOT STARTED | — | Create kitchen-role staff in Admin, verify KDS access granted, POS access denied. |
| CROSS-082 | Disable Staff → Access Denied | P1 | ⬜ NOT STARTED | — | Disable a staff account in Admin, verify login fails on POS/KDS. |
| CROSS-083 | Manager PIN Across POS | P1 | ⬜ NOT STARTED | — | Set up manager PIN in Admin, verify it works for POS manager actions. Would also unblock CROSS-070–072. |

---

## Section 10: Edge Cases & Error Scenarios

| ID | Test Name | Priority | Status | Session | Notes |
|----|-----------|:--------:|:------:|---------|-------|
| CROSS-090 | Simultaneous Orders to Same Table | P1 | ⬜ NOT STARTED | — | Customer QR order + POS order on same table simultaneously. Verify no data loss. |
| CROSS-091 | Network Interruption Handling | P2 | ⬜ NOT STARTED | — | Disconnect mid-order, reconnect, verify recovery. Needs DevTools/proxy. |
| CROSS-092 | Concurrent Kitchen Ticket Claim | P2 | ⬜ NOT STARTED | — | Two KDS screens claim same ticket. Needs two KDS sessions. |
| CROSS-093 | Large Order Performance | P2 | ⬜ NOT STARTED | — | 15+ item order. Verify all apps handle without performance issues. |
| CROSS-094 | Rapid Status Changes | P2 | ⬜ NOT STARTED | — | Rapid Claim → Bump → Serve. Verify Customer App tracking handles correctly. |
| CROSS-095 | Empty Restaurant | P1 | ⬜ NOT STARTED | — | Clear all orders, verify each app shows empty state gracefully. |

---

## Recommended Next Steps (Priority Order)

1. **Get POS Manager PIN** → unblocks CROSS-070/071/072 (cancellation) + CROSS-083 (manager PIN test)
2. **CROSS-002** (P0) — Multi-station order (use Coffee from Drinks + food from Main Kitchen)
3. **CROSS-003** (P0) — Modifiers & special instructions (use Biryani with options)
4. **CROSS-020 re-test** (P0) — Multi-guest group order (need second device/incognito)
5. **CROSS-042** (P1) — Out of stock propagation
6. **CROSS-062** (P1) — Online (Stripe) payment tracking
7. **CROSS-080–082** (P1) — Staff permission tests
8. **CROSS-090** (P1) — Simultaneous orders to same table
9. Remaining P1 tests, then P2 edge cases

---

## Related Documents

- **[TEST-LOG.md](./TEST-LOG.md)** — Full test execution log with detailed results
- **[active-bugs.md](./active-bugs.md)** — All 10 open bugs with descriptions
- **[CROSS-APP-TESTS.md](./CROSS-APP-TESTS.md)** — Original test plan (reference)
- **[ROADBLOCKS.md](./ROADBLOCKS.md)** — Testing infrastructure blockers
