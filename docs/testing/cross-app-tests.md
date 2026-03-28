---
layout: default
title: Cross-App Tests
parent: Testing Manuals
nav_order: 5
---

# Cross-App Tests — Manual Test Plan

> **Apps Involved**: Admin (5175), Customer (8080), POS (5176), KDS (5174)
> **Role Required**: Testers need accounts for all four apps (ideally 2+ testers or multiple browser profiles)
> **Estimated Time**: 3–4 hours (full suite)
> **Priority**: CRITICAL — Test these first. These validate the core order lifecycle that spans all apps.

---

## Table of Contents

1. [Customer → Kitchen → Serve (Happy Path)](#1-customer--kitchen--serve-happy-path)
2. [POS Counter Order Flow](#2-pos-counter-order-flow)
3. [QR Dine-In Group Order Flow](#3-qr-dine-in-group-order-flow)
4. [Real-time Sync Across Apps](#4-real-time-sync-across-apps)
5. [Menu Configuration → Customer Display](#5-menu-configuration--customer-display)
6. [Tax & Pricing Consistency](#6-tax--pricing-consistency)
7. [Payment Reconciliation](#7-payment-reconciliation)
8. [Order Cancellation Flows](#8-order-cancellation-flows)
9. [Staff & Permission Cross-App](#9-staff--permission-cross-app)
10. [Edge Cases & Error Scenarios](#10-edge-cases--error-scenarios)

---

## Setup Instructions

These tests require **multiple apps open simultaneously**. Recommended setup:

- **Screen/Window 1**: Customer App (https://hi.cibus.app) — logged in as customer
- **Screen/Window 2**: POS App (https://pos.cibus.app) — logged in as POS staff, shift open
- **Screen/Window 3**: KDS App (https://kds.cibus.app) — logged in as kitchen staff
- **Screen/Window 4**: Admin App (https://admin.cibus.app) — logged in as admin

Alternatively, use browser profiles or incognito windows to maintain separate sessions.

---

## 1. Customer → Kitchen → Serve (Happy Path)

> This is THE core flow. If this doesn't work, nothing else matters.

### CROSS-001 — Complete Order Lifecycle (P0)
**This scenario walks through the entire journey of an order from creation to completion.**

1. **Customer App**: Browse the menu, add 2–3 items to cart (at least one with modifiers)
2. **Customer App**: Go to the cart page. Verify:
   - Items are correct with proper names, quantities, and prices
   - Subtotal, tax, and total are calculated correctly
3. **Customer App**: Proceed to payment, select a payment method, and place the order
4. **Customer App**: Verify the order confirmation page shows the order ID and receipt

5. **Admin App**: Go to Orders. Verify:
   - The new order appears in the active orders list
   - Order number, items, and total match what was placed
   - Status shows "Pending" (or appropriate initial status)

6. **POS App**: Go to Live Orders. Verify:
   - The same order appears
   - Items and totals match

7. **KDS App**: Go to the appropriate station(s). Verify:
   - Kitchen ticket(s) appear in the Pending column
   - Ticket shows correct items with quantities
   - Special instructions and allergen warnings are visible (if applicable)

8. **KDS App**: CLAIM the ticket
9. **KDS App**: Verify it moves to In Progress column

10. **Customer App**: Go to Order Tracking. Verify:
    - Status shows "Preparing"
    - Station progress shows the correct station(s)

11. **KDS App**: BUMP the ticket to Ready
12. **KDS App**: Verify it moves to Ready column

13. **Customer App**: Verify tracking updates to "Ready"

14. **KDS App**: SERVE the ticket
15. **KDS App**: Verify it's removed from the board

16. **Customer App**: Verify tracking shows "Served" or "Completed"

17. **Admin App**: Verify the order status is now "Completed"

### CROSS-002 — Multi-Station Order (P0)
**Tests an order that routes to multiple kitchen stations**

1. **Customer App**: Order items that go to different stations (e.g., any items from the Drinks category should go to the Drinks Station)
2. **Customer App**: Place the order
3. **KDS App**: Navigate to different stations and verify:
   - Each station received only its relevant items
   - Burger items appear at the Grill station
   - Salad items appear at the Salad station
   - Drink items appear at the Bar station
4. **KDS App**: Process each station's tickets (CLAIM → BUMP → SERVE)
5. **Customer App**: Verify tracking shows progress per station
6. **Admin App**: Verify the order completes when all stations finish

### CROSS-003 — Order with Modifiers and Special Instructions (P0)
1. **Customer App**: Order a Biryani with:
   - Size variant (e.g., Large)
   - Modifiers (e.g., Mint Yogurt)
   - Special instructions (e.g., "Allergy: tree nuts")
2. **Customer App**: Place the order
3. **KDS App**: Open the ticket detail. Verify:
   - Item shows the correct size
   - All modifiers are listed
   - Special instructions are clearly visible and highlighted
   - Allergy warnings are prominent
4. **Admin App**: Open the order detail. Verify:
   - Modifiers and instructions are shown
   - Price reflects the size and modifier additions
5. **POS App**: Check the order. Verify:
   - Same items with same details and pricing

---

## 2. POS Counter Order Flow

### CROSS-010 — POS Order to Kitchen (P0)
1. **POS App**: Click on an available table
2. **POS App**: Add items to the order from the menu
3. **POS App**: Submit the order
4. **KDS App**: Verify the ticket appears at the correct station
5. **Admin App**: Verify the order appears in the active orders list
6. **Customer App** (if applicable): If the table has a QR link, verify the order appears

### CROSS-011 — POS Payment Flow (P0)
1. **POS App**: Create and submit an order
2. **KDS App**: Process the ticket through CLAIM → BUMP → SERVE
3. **POS App**: Navigate to payment for the order
4. **POS App**: Process a cash payment
5. **POS App**: Verify payment succeeds and table is released
6. **Admin App**: Go to Payments. Verify:
   - The payment appears in the list
   - Amount and method (Cash) are correct
7. **Admin App**: Go to Orders. Verify:
   - The order shows as "Paid"

### CROSS-012 — POS Card Payment (P1)
1. **POS App**: Create an order and proceed to payment
2. **POS App**: Select "Card" payment
3. **POS App**: Enter a reference number
4. **POS App**: Complete the payment
5. **Admin App**: Verify the payment shows as "Card" with the reference number

### CROSS-013 — POS Multiple Orders per Table (P1)
1. **POS App**: Create a first order for a table, submit it
2. **POS App**: Create a second order for the SAME table, submit it
3. **KDS App**: Verify both orders generate separate tickets
4. **Admin App**: Verify both orders appear linked to the same table
5. **POS App**: Verify the table overview shows both orders

---

## 3. QR Dine-In Group Order Flow

### CROSS-020 — Complete Group Order Lifecycle (P0)
1. **Admin App**: Find a table and get its QR code URL
2. **Customer App (Person A)**: Open the QR URL, join the group order
3. **Customer App (Person B)**: Open the same QR URL in a different browser/profile, join the group
4. **Customer App (Person A)**: Add items to the order
5. **Customer App (Person B)**: Add different items to the order
6. **Customer App**: View the group cart. Verify:
   - Person A's items show under their name
   - Person B's items show under their name
   - Grand total includes all items from both members
   - Taxes and charges are calculated on the full group order
7. **Customer App (Host)**: Proceed to checkout and pay
8. **KDS App**: Verify tickets appear at the correct stations
9. **KDS App**: Process all tickets
10. **Admin App**: Verify the order shows all items from all members
11. **POS App**: Verify the table shows the group order

### CROSS-021 — Group Order Cart Lock (P1)
1. Start a group order with 2 members
2. Both add items
3. **Customer App (Host)**: Lock the cart
4. **Customer App (Other member)**: Try to add more items
5. **Expect**: The other member cannot add items after cart lock
6. Proceed with payment and verify the kitchen flow

### CROSS-022 — Group Order Bill Split (P1)
1. Complete a group order with multiple members
2. At payment, select "Split Bill"
3. **Expect**: Split options work correctly
4. **Admin App**: Verify payments are recorded correctly

---

## 4. Real-time Sync Across Apps

### CROSS-030 — Order Creation Sync (P0)
1. **Customer App**: Place an order
2. Within 5 seconds, check ALL other apps:
   - **Admin App**: New order visible in Orders list?
   - **POS App**: New order visible in Live Orders?
   - **KDS App**: New ticket visible in station queue?
3. **Expect**: All apps show the new order within a few seconds (no manual refresh needed)

### CROSS-031 — Kitchen Status Sync (P0)
1. **KDS App**: CLAIM a ticket
2. **Customer App**: Check order tracking. Does it show "Preparing"?
3. **POS App**: Check the order. Does it show updated kitchen status?
4. **Admin App**: Check the order. Does the status update?
5. **Expect**: All apps reflect the status change in real time

### CROSS-032 — Payment Sync (P1)
1. **POS App**: Record a payment for an order
2. **Admin App**: Does the order show as "Paid"?
3. **Admin App**: Does the payment appear in the Payments section?
4. **Customer App**: Does the order history show the payment?
5. **Expect**: Payment status syncs across all apps

### CROSS-033 — Table Status Sync (P1)
1. **POS App**: Open a table and start an order
2. **Admin App**: Does the table show as "Occupied" in Floor Plan?
3. **POS App**: Complete payment and release the table
4. **Admin App**: Does the table show as "Available"?
5. **Expect**: Table status changes sync between POS and Admin

---

## 5. Menu Configuration → Customer Display

### CROSS-040 — Menu Item Visibility (P0)
1. **Admin App**: Create a new menu item with a name, price, and image
2. **Customer App**: Browse the menu
3. **Expect**: The new item appears in the correct category
4. **Expect**: Name, price, and image match what was configured

### CROSS-041 — Price Change Propagation (P0)
1. **Admin App**: Change the price of an existing menu item (e.g., from $10 to $12)
2. **Customer App**: Find the item
3. **Expect**: The updated price ($12) is shown
4. **Customer App**: Add the item to cart
5. **Expect**: The cart uses the new price
6. **POS App**: Add the same item to a POS order
7. **Expect**: The POS also uses the new price

### CROSS-042 — Out of Stock Propagation (P1)
1. **Admin App**: Mark a menu item as "Out of Stock"
2. **Customer App**: Find the item
3. **Expect**: The item shows as "Sold Out" and cannot be added to cart
4. **POS App**: Try to find/add the item
5. **Expect**: The item is marked as unavailable

### CROSS-043 — Category Changes (P1)
1. **Admin App**: Move an item from one category to another
2. **Customer App**: Verify the item now appears in the new category
3. **Expect**: The item is no longer in the old category

### CROSS-044 — Modifier Configuration → Display (P1)
1. **Admin App**: Add a new modifier to a menu item (e.g., "Add Bacon +$2")
2. **Customer App**: Open the item. Verify the modifier appears
3. **Customer App**: Select the modifier and add to cart
4. **Expect**: The price includes the modifier addition
5. **KDS App**: When the order reaches the kitchen, verify the modifier is listed on the ticket

---

## 6. Tax & Pricing Consistency

### CROSS-050 — Tax Calculation Consistency (P0)
1. **Admin App**: Note the configured tax rate (e.g., 15% VAT)
2. **Customer App**: Add an item priced at $10.00 to the cart
3. **Customer App**: Verify the tax calculation:
   - Subtotal: $10.00
   - Tax (15%): $1.50
   - Total: $11.50
4. **POS App**: Add the same item to a POS order
5. **POS App**: Verify the same tax calculation:
   - Subtotal: $10.00
   - Tax (15%): $1.50
   - Total: $11.50
6. **Expect**: Both apps calculate identical totals

### CROSS-051 — Service Charge Consistency (P1)
1. **Admin App**: Note the configured service charge (e.g., 10%)
2. **Customer App**: Calculate expected service charge on an order
3. **POS App**: Calculate expected service charge on the same items
4. **Expect**: Service charge is applied consistently

### CROSS-052 — Tax Change Propagation (P1)
1. **Admin App**: Change the tax rate (e.g., from 15% to 16%)
2. **Customer App**: Start a new order and check the tax calculation
3. **Expect**: The new rate (16%) is used
4. **POS App**: Start a new order
5. **Expect**: The new rate (16%) is also used here

### CROSS-053 — Multi-Tax Scenario (P2)
1. If the restaurant has multiple taxes (e.g., VAT + City Tax)
2. Place an order from both Customer and POS apps
3. **Expect**: Both taxes are applied
4. **Expect**: The tax breakdown matches between all apps

### CROSS-054 — Discount + Tax Interaction (P1)
1. **Customer App**: Apply a voucher code for 10% off on an order
2. Verify the tax is calculated correctly (tax on discounted amount, not original)
3. **POS App**: Apply a 10% discount (manager action)
4. Verify the tax is calculated the same way
5. **Expect**: The discount-then-tax logic is consistent

### CROSS-055 — Currency Display Consistency (P1)
1. Check that the currency symbol/format is the same across all four apps
2. **Admin App**: Note the configured currency (e.g., USD $)
3. **Customer App**: Check prices → same currency symbol
4. **POS App**: Check prices → same currency symbol
5. **KDS App**: If prices are shown on tickets → same format
6. **Expect**: No currency mismatches

---

## 7. Payment Reconciliation

### CROSS-060 — Cash Payment Tracking (P0)
1. **POS App**: Process 3 different cash payments during a shift
2. Note the exact amounts
3. **POS App**: Close the shift and count cash
4. **Expect**: The expected cash total = opening float + sum of cash payments
5. **Admin App**: View the shift report. Verify:
   - Transaction count matches (3)
   - Cash total matches

### CROSS-061 — Mixed Payment Methods (P1)
1. **POS App**: Process orders with different payment methods (2 cash, 1 card)
2. **POS App**: Close the shift
3. **Admin App**: View shift report. Verify:
   - Cash and card totals are broken down separately
   - Cash expected = float + cash payments only
   - Card total = sum of card payments

### CROSS-062 — Online Payment Tracking (P1)
1. **Customer App**: Place and pay for an order (card/online)
2. **Admin App**: Verify the payment appears in the Payments section
3. **Admin App**: Verify the payment method is correctly identified
4. **Expect**: Online payments from the Customer app are tracked in Admin

---

## 8. Order Cancellation Flows

### CROSS-070 — Cancel Before Kitchen (P0)
1. **Customer App**: Place an order
2. **Admin App**: Cancel the order before it reaches the kitchen
3. **KDS App**: Verify NO ticket appears for the cancelled order
4. **Customer App**: Verify the order shows as "Cancelled"
5. **POS App**: Verify the order shows as "Cancelled"

### CROSS-071 — Cancel After Kitchen Claim (P1)
1. **Customer App**: Place an order
2. **KDS App**: CLAIM the ticket (start preparing)
3. **POS App**: Cancel the order (manager action with PIN)
4. **KDS App**: Verify the ticket is removed or marked as cancelled
5. **Customer App**: Verify the order shows as "Cancelled"
6. **Admin App**: Verify the cancellation is recorded

### CROSS-072 — POS Void Item After Kitchen (P1)
1. **POS App**: Create an order with 3 items and submit to kitchen
2. **KDS App**: CLAIM the ticket
3. **POS App**: Void one item (manager PIN required)
4. **KDS App**: Verify the ticket updates to show only 2 active items (or the voided item is marked)
5. **Admin App**: Verify the order total recalculates

---

## 9. Staff & Permission Cross-App

### CROSS-080 — Staff Access Control (P1)
1. **Admin App**: Create a new staff member with "Cashier" role (POS access only)
2. **POS App**: Log in as that staff member. Verify they can access the POS
3. **KDS App**: Try to log in as that staff member
4. **Expect**: Access is denied (they don't have kitchen access)

### CROSS-081 — Kitchen Staff Access (P1)
1. **Admin App**: Create a staff member with "Kitchen Staff" role
2. **KDS App**: Log in as that staff member. Verify they can access all KDS features
3. **POS App**: Try to log in as that staff member
4. **Expect**: Access is denied (they don't have POS access)

### CROSS-082 — Disable Staff → Access Denied (P1)
1. **Admin App**: Disable a staff member's account
2. Try to log into POS or KDS with that disabled account
3. **Expect**: Login fails with "Account disabled" or similar message

### CROSS-083 — Manager PIN Across POS (P1)
1. **Admin App**: Set up a manager with a PIN
2. **POS App**: Attempt a manager action (void, comp, discount)
3. Enter the manager PIN
4. **Expect**: The action is authorized with the correct PIN

---

## 10. Edge Cases & Error Scenarios

### CROSS-090 — Simultaneous Orders to Same Table (P1)
1. **Customer App (via QR)**: Start adding items to a table order
2. **POS App**: Simultaneously start creating an order for the same table
3. Complete both orders
4. **Expect**: Both orders are handled without data loss or conflict
5. **Expect**: The table shows both orders

### CROSS-091 — Network Interruption Handling (P2)
1. Start placing an order in the Customer App
2. Temporarily disconnect the internet (or stop the dev server)
3. Reconnect
4. **Expect**: The app recovers gracefully (pending data is saved or user is notified)

### CROSS-092 — Concurrent Kitchen Ticket Claim (P2)
1. Have two KDS screens open (different staff, same station)
2. Both attempt to CLAIM the same ticket simultaneously
3. **Expect**: Only one succeeds; the other is notified

### CROSS-093 — Large Order Performance (P2)
1. **Customer App**: Create an order with 15+ items (variety of categories and modifiers)
2. Place the order
3. **Expect**: All apps handle the large order without performance issues
4. **KDS App**: Tickets are created for all items across stations
5. **Admin App**: The order detail shows all 15+ items correctly

### CROSS-094 — Rapid Status Changes (P2)
1. **KDS App**: Quickly CLAIM → BUMP → SERVE a ticket in rapid succession
2. **Customer App**: Check order tracking
3. **Expect**: The status updates correctly (may show final state rather than each intermediate state)
4. **Admin App**: The final order status is correct

### CROSS-095 — Empty Restaurant (P1)
1. Start with no active orders across all apps
2. Verify each app handles the empty state gracefully:
   - **Admin App**: Orders page shows "No active orders" or empty state
   - **POS App**: Live orders shows empty state
   - **KDS App**: Station queues show empty columns
3. Create one order and verify it appears everywhere

---

## Summary — Test Count by Section

| Section | Total Tests | P0 | P1 | P2 | P3 |
|---------|:-----------:|:--:|:--:|:--:|:--:|
| Customer→Kitchen→Serve | 3 | 3 | 0 | 0 | 0 |
| POS Counter Flow | 4 | 2 | 2 | 0 | 0 |
| QR Group Order Flow | 3 | 1 | 2 | 0 | 0 |
| Real-time Sync | 4 | 2 | 2 | 0 | 0 |
| Menu Config → Display | 5 | 2 | 3 | 0 | 0 |
| Tax & Pricing | 6 | 1 | 4 | 1 | 0 |
| Payment Reconciliation | 3 | 1 | 2 | 0 | 0 |
| Order Cancellation | 3 | 1 | 2 | 0 | 0 |
| Staff & Permissions | 4 | 0 | 4 | 0 | 0 |
| Edge Cases | 6 | 0 | 2 | 4 | 0 |
| **TOTAL** | **41** | **13** | **23** | **5** | **0** |

---

## Recommended Test Order

For maximum efficiency and to catch the most critical bugs first:

1. **CROSS-001** — The complete happy path. If this fails, stop and fix before continuing.
2. **CROSS-010, CROSS-011** — POS counter flow (second most common path).
3. **CROSS-030, CROSS-031** — Real-time sync verification.
4. **CROSS-050** — Tax calculation consistency.
5. **CROSS-040, CROSS-041** — Menu configuration propagation.
6. All remaining P0 tests.
7. All P1 tests.
8. P2 edge cases if time allows.
