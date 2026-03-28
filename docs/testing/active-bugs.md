---
layout: default
title: Active Bugs
parent: Testing Manuals
---

# Active Bug Report — Cibus Platform

> **Generated**: 15 March 2026 | Sessions 1–3 | **10 Open Bugs**

---

## Summary by Severity

| High | Medium | Low-Med | Low |
|:----:|:------:|:-------:|:---:|
| 1 | 3 | 5 | 1 |

## Distribution by App

- **POS**: 4 bugs (BUG-006, BUG-014, BUG-026, BUG-027)
- **Admin**: 3 bugs (BUG-018, BUG-028, BUG-029)
- **Customer App**: 2 bugs (BUG-004, BUG-025)
- **Multi-App**: 1 bug (BUG-020)

---

## All Open Bugs (Ordered by Priority)

### 🔴 High

| ID | App | Description |
|----|-----|-------------|
| BUG-014 | POS | POS shift-open silently fails on backend error (HTTP 300 from stale shifts) — no user feedback, UI resets to Count Float screen without explanation. Needs stale shift scenario to reproduce. |

### 🟠 Medium

| ID | App | Description |
|----|-----|-------------|
| BUG-018 | Admin | Group order payment status stays "Unpaid" after POS cash payment completes. Partially verified fixed for single-member group order in CROSS-060, but may still manifest with multi-member group orders where only some members have paid. |
| BUG-026 | POS | POS Orders list does not reflect kitchen status changes. Orders remain in "Pending" throughout full KDS lifecycle (Claim → Bump → Serve). Filter tabs exist (Pending/Preparing/Ready/Completed) but orders never move between them. |
| BUG-028 | Admin | Payments Dashboard "Taxes Collected" card shows £0.00 despite VAT being charged on all orders. Three completed payments totalling £47.92 exist with VAT applied, yet dashboard reports zero tax collected. |

### 🟡 Low-Medium

| ID | App | Description |
|----|-----|-------------|
| BUG-004 | Customer | Product card image badge shows "1 in_cart" raw i18n key instead of translated text. Bottom bar was partially fixed to show "View Order" but the product card badge remains untranslated. |
| BUG-025 | Customer | Product card badge shows "1 in_cart" raw key — same symptom as BUG-004. The partial fix for BUG-004 resolved the bottom bar but not the product card badge overlay. |
| BUG-006 | POS | POS shift counter (header £ amount + order count) only updates when POS itself processes a payment. Orders placed via QR/Customer App and served through KDS are not counted in the shift totals. |
| BUG-027 | POS | POS Order Detail panel omits Service Charge line from the price breakdown. Total still includes SC (e.g. £9.04 = £6.95 + £1.39 VAT + £0.70 SC), but only Subtotal, VAT, and Total are displayed. |
| BUG-029 | Admin | Payments Dashboard "Payment Methods" chart shows "No payment data available" despite 3 completed payments (mix of cash and card). Revenue Trend chart also appears empty. |

### 🔵 Low

| ID | App | Description |
|----|-----|-------------|
| BUG-020 | Multi-App | Tax label inconsistent across apps: Customer App shows "VAT (20%)", POS shows "VAT", Admin shows "Tax" — three different labels for the same charge. May be by design but creates confusion. |

---

## Notes

- **BUG-004 and BUG-025** are closely related — both stem from incomplete i18n translation of the `in_cart` key on product card badges. Fixing one should resolve the other.
- **BUG-014** cannot be reproduced without creating stale open shifts in the backend. The code path exists but requires specific database conditions to trigger.
- **BUG-018** was partially verified during CROSS-060 testing — a single-member group order correctly showed "Paid" after POS cash payment. Multi-member scenarios still need verification.
