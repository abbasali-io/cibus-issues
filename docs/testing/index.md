---
layout: default
title: Testing Manuals
nav_order: 1
has_children: true
---

# Cibus Manual Testing Guide

> **Purpose**: Comprehensive manual test plans for human testers across all Cibus apps.
>
> Each document below covers one app with detailed step-by-step scenarios.
>
> **Last Updated**: March 12, 2026

---

## Quick Reference

| App | URL | Test Plan | Scenarios | Priority |
|-----|-----|-----------|-----------|----------|
| **Admin** | `admin.cibus.app` | [Admin Tests](admin-tests) | 180+ | High |
| **Customer** | `hi.cibus.app` | [Customer Tests](customer-tests) | 120+ | High |
| **POS** | `pos.cibus.app` | [POS Tests](pos-tests) | 100+ | High |
| **KDS** | `kds.cibus.app` | [KDS Tests](kds-tests) | 50+ | High |
| **Cross-App** | All | [Cross-App Tests](cross-app-tests) | 40+ | Critical |

---

## How to Use These Test Plans

### For Testers

1. **Pick an app** from the table above
2. **Open the app** in your browser at the listed URL
3. **Work through scenarios** section by section
4. **Record results** using the status markers:
   - ✅ Pass — Feature works as described
   - ❌ Fail — Feature broken or behaves incorrectly
   - ⚠️ Partial — Works but with issues (note the issue)
   - ⏭️ Skip — Cannot test (blocked by another issue)
5. **Log bugs** with the scenario ID (e.g., `ADM-MENU-003`) for easy tracking

### Priority Levels

Each scenario has a priority:
- **P0 — Critical**: Core functionality. Must work. Test first.
- **P1 — High**: Important features. Test after P0.
- **P2 — Medium**: Nice-to-have features. Test if time allows.
- **P3 — Low**: Edge cases, cosmetic. Test last.

### Test Order (Recommended)

For the most efficient testing, follow this order:

1. **Cross-App Tests** — These validate the end-to-end order lifecycle that spans multiple apps
2. **Customer App** — The primary ordering entry point
3. **POS App** — Counter-based ordering and payments
4. **KDS App** — Kitchen ticket processing
5. **Admin App** — Management and configuration (largest test surface)

---

## Prerequisites

Before testing, ensure:

- [ ] All 4 apps are accessible at their deployed URLs
- [ ] You have valid login credentials for each role (admin, staff, customer)
- [ ] A test restaurant exists with menus, tables, kitchen stations, and tax config
- [ ] A test customer account exists
- [ ] A test staff account exists with POS access
- [ ] A test kitchen staff account exists with KDS access

---

## Additional Resources

| File | Description |
|------|-------------|
| [Test Log](test-log) | Full test execution log with detailed results |
| [Active Bugs](active-bugs) | Currently open defects |
| [Outstanding Tests](outstanding-tests) | Tests not yet completed |
| [Roadblocks](roadblocks) | Testing infrastructure blockers |

---

[← Back to Documentation Home](../)
