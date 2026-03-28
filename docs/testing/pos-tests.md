---
layout: default
title: POS App Tests
parent: Testing Manuals
---

# POS App — Manual Test Plan

> **App URL**: `https://pos.cibus.app`
> **Role Required**: Staff with POS access
> **Estimated Time**: 3–4 hours (full suite)

---

## Table of Contents

1. [Authentication & Login](#1-authentication--login)
2. [Terminal Selection](#2-terminal-selection)
3. [Shift Open](#3-shift-open)
4. [Lock Screen](#4-lock-screen)
5. [Tables & Floor View](#5-tables--floor-view)
6. [Order Editor (Creating Orders)](#6-order-editor-creating-orders)
7. [Table Order Overview](#7-table-order-overview)
8. [Payment Processing](#8-payment-processing)
9. [Live Orders](#9-live-orders)
10. [Kitchen Overview](#10-kitchen-overview)
11. [Manager Actions (PIN-Protected)](#11-manager-actions-pin-protected)
12. [Shift Close & Reconciliation](#12-shift-close--reconciliation)
13. [Settings](#13-settings)

---

## 1. Authentication & Login

### POS-AUTH-001 — Login with Email (P0)
1. Go to `https://pos.cibus.app`
2. You should see the login page
3. Enter valid staff email and password
4. Click "Sign In"
5. **Expect**: You are authenticated and proceed to terminal selection

### POS-AUTH-002 — Login with PIN (P0)
1. On the login page, look for a PIN login option
2. Enter your staff PIN
3. **Expect**: You are authenticated

### POS-AUTH-003 — Invalid Credentials (P1)
1. Enter incorrect email/password or PIN
2. **Expect**: An error message appears
3. **Expect**: You remain on the login page

### POS-AUTH-004 — Logout (P0)
1. While logged in, find and click the logout option
2. **Expect**: You are returned to the login page
3. **Expect**: Cannot access POS pages without logging in again

---

## 2. Terminal Selection

### POS-TERM-001 — Terminal Selection Page (P0)
1. After login, the terminal selection page appears
2. **Expect**: A list of available POS terminals is displayed
3. **Expect**: Each terminal shows: name, status (Online/Offline), IP address

### POS-TERM-002 — Select Terminal (P0)
1. Click on an available (online) terminal
2. **Expect**: The terminal is registered/assigned to you
3. **Expect**: You proceed to the shift open page or main POS view

### POS-TERM-003 — Offline Terminal (P2)
1. If a terminal shows as offline, try to select it
2. **Expect**: Either you cannot select it, or a warning appears

---

## 3. Shift Open

### POS-SHIFT-OPEN-001 — Shift Open Page (P0)
1. After selecting a terminal, the shift open page appears (if no active shift)
2. **Expect**: A cash float counting interface is displayed
3. **Expect**: Denomination fields are shown for the restaurant's currency

### POS-SHIFT-OPEN-002 — Count Float Cash (P0)
1. Enter the starting cash float amounts by denomination
2. **Expect**: The total is calculated automatically as you enter amounts
3. **Expect**: The total matches your manual calculation

### POS-SHIFT-OPEN-003 — Currency-Aware Denominations (P1)
1. Check that the denominations match the restaurant's configured currency
2. **Expect**: USD shows bills ($100, $50, $20, $10, $5, $1) and coins ($0.25, $0.10, $0.05, $0.01)
3. **Expect**: Other currencies show their appropriate denominations

### POS-SHIFT-OPEN-004 — Open Shift (P0)
1. Fill in the float count
2. Click "Open Shift" or "Start"
3. **Expect**: The shift is opened and you proceed to the main POS view (Tables page)
4. **Expect**: A success notification appears

### POS-SHIFT-OPEN-005 — Zero Float (P2)
1. Try to open a shift with $0 cash float
2. **Expect**: Either a warning appears asking to confirm, or it's allowed (depending on policy)

---

## 4. Lock Screen

### POS-LOCK-001 — Lock Screen Activation (P1)
1. Find the lock/screen lock button (typically in the header or settings)
2. Click it
3. **Expect**: The POS screen locks with a lock overlay
4. **Expect**: The overlay shows the locked staff member's info

### POS-LOCK-002 — Unlock with PIN (P1)
1. While the screen is locked, enter your PIN
2. **Expect**: The screen unlocks and you return to where you left off

### POS-LOCK-003 — Wrong PIN (P2)
1. While locked, enter an incorrect PIN
2. **Expect**: An error message appears
3. **Expect**: The screen remains locked

### POS-LOCK-004 — Switch Staff from Lock Screen (P2)
1. While the screen is locked, look for a "Sign Out" option
2. Click it
3. **Expect**: You are signed out and redirected to the login page
4. **Expect**: A different staff member can now log in

---

## 5. Tables & Floor View

### POS-TABLE-001 — Tables Page Loads (P0)
1. The tables page is the main landing after shift open
2. **Expect**: A grid/layout of all tables is displayed
3. **Expect**: Each table shows: number, capacity, current status

### POS-TABLE-002 — Table Status Colors (P0)
1. Review the table display
2. **Expect**: Tables are color-coded by status:
   - Green/neutral = Available
   - Red/orange = Occupied (has active orders)
   - Blue/yellow = Reserved
   - Gray = Cleaning/Unavailable

### POS-TABLE-003 — Section Filtering (P1)
1. If there are multiple floor sections, look for section filter buttons
2. Click each section
3. **Expect**: Only tables from that section are displayed

### POS-TABLE-004 — Click Available Table (P0)
1. Click on an available table
2. **Expect**: You are navigated to the order editor to start a new order for that table

### POS-TABLE-005 — Click Occupied Table (P0)
1. Click on an occupied table (one with active orders)
2. **Expect**: You see the table's order overview with existing orders

### POS-TABLE-006 — Real-time Table Updates (P1)
1. Keep the tables page open
2. From the Customer app, create an order for a table (via QR dine-in)
3. **Expect**: The table's status updates in real time on the POS screen

---

## 6. Order Editor (Creating Orders)

### POS-ORDER-001 — Order Editor Layout (P0)
1. Enter the order editor (by clicking a table)
2. **Expect**: A split-view layout:
   - Left side: Menu with categories and items
   - Right side: Cart/order with added items

### POS-ORDER-002 — Menu Categories (P0)
1. In the order editor, review the category tabs/buttons
2. Click different categories
3. **Expect**: Menu items update to show only items from the selected category

### POS-ORDER-003 — Add Item to Order (P0)
1. Click on a menu item
2. **Expect**: The item is added to the cart on the right
3. **Expect**: The cart total updates

### POS-ORDER-004 — Item with Modifiers (P0)
1. Click an item that has modifiers (e.g., a burger with size and topping options)
2. **Expect**: A modifier selection modal/panel appears
3. Select the modifiers
4. Confirm
5. **Expect**: The item is added to the cart with the selected modifiers and updated price

### POS-ORDER-005 — Quantity Controls (P0)
1. In the cart, use the +/- buttons to change item quantity
2. **Expect**: The quantity and line total update
3. **Expect**: The order total recalculates

### POS-ORDER-006 — Remove Item (P1)
1. Remove an item from the cart (set quantity to 0 or use delete button)
2. **Expect**: The item is removed
3. **Expect**: Totals recalculate

### POS-ORDER-007 — Special Instructions (P1)
1. Click on an item in the cart
2. Find the special instructions/notes field
3. Type instructions (e.g., "No onions")
4. **Expect**: The instructions are saved with the item

### POS-ORDER-008 — Order Totals Calculation (P0)
1. Add multiple items to the cart
2. Review the order totals section
3. **Expect**: You see:
   - Subtotal (sum of all items)
   - Tax amount(s)
   - Service charge (if configured)
   - Grand total
4. **Verify**: Calculate manually that the math is correct

### POS-ORDER-009 — Submit Order (P0)
1. After adding items, click "Submit Order" or "Send to Kitchen"
2. **Expect**: The order is created
3. **Expect**: A success notification appears
4. **Expect**: The table status updates to "Occupied"

### POS-ORDER-010 — Menu Search (P1)
1. In the order editor, find the search bar
2. Type an item name
3. **Expect**: Matching items appear
4. Click one to add it

### POS-ORDER-011 — Kitchen Status on Items (P1)
1. On a table with an existing order that's been sent to kitchen
2. Check the cart/order items
3. **Expect**: Items show their kitchen status (e.g., "Sent", "Preparing", "Ready")

---

## 7. Table Order Overview

### POS-OVERVIEW-001 — Table Order Overview (P0)
1. Click on an occupied table
2. **Expect**: An overview of all orders for this table is displayed
3. **Expect**: Each order shows: order number, status, items, total

### POS-OVERVIEW-002 — Multiple Orders Per Table (P1)
1. Find a table with multiple orders (e.g., different rounds or different group members)
2. **Expect**: All orders are listed separately
3. **Expect**: You can view each order's details

### POS-OVERVIEW-003 — Add Items to Existing Order (P1)
1. From the table overview, choose to add items to an existing order
2. **Expect**: The order editor opens with the existing items
3. Add new items and submit
4. **Expect**: The order is updated with the new items

### POS-OVERVIEW-004 — Navigate to Payment (P0)
1. From the table overview, find the "Payment" or "Pay" button
2. Click it
3. **Expect**: You are navigated to the payment page for that order/table

---

## 8. Payment Processing

### POS-PAY-001 — Payment Page Layout (P0)
1. Navigate to the payment page for an order
2. **Expect**: The page shows:
   - Order summary with all items
   - Total amount due
   - Payment method selection (Cash, Card)

### POS-PAY-002 — Cash Payment (P0)
1. Select "Cash" as the payment method
2. **Expect**: A cash tendered input appears
3. Enter the amount the customer is handing over
4. **Expect**: Change due is calculated and displayed

### POS-PAY-003 — Cash Denomination Tracking (P1)
1. During cash payment, check if denomination tracking is available
2. Enter cash by denomination
3. **Expect**: The total is calculated from denominations

### POS-PAY-004 — Cash Exact Amount (P1)
1. Look for an "Exact" button when paying by cash
2. Click it
3. **Expect**: The tendered amount is set to exactly the total due (change = $0)

### POS-PAY-005 — Card Payment (P0)
1. Select "Card" as the payment method
2. **Expect**: A reference number field appears (for manual card terminal entry)
3. Enter the reference number
4. Complete the payment
5. **Expect**: Payment is recorded as card payment

### POS-PAY-006 — Complete Payment (P0)
1. After entering the payment details, click "Complete" or "Pay"
2. **Expect**: The payment is processed
3. **Expect**: A success notification or receipt appears
4. **Expect**: The order status updates to "Paid"

### POS-PAY-007 — Split Payment (P1)
1. Look for a "Split Payment" option
2. **Expect**: You can split the total across multiple payment methods
3. Pay part in cash and part by card
4. **Expect**: Both payments are recorded

### POS-PAY-008 — Payment Lock (P2)
1. While a payment is being processed for a table
2. Try to initiate another payment for the same table from a different terminal
3. **Expect**: A lock or warning prevents double-payment

### POS-PAY-009 — Change Calculation (P1)
1. During cash payment, enter an amount larger than the total
2. **Expect**: The change due is clearly displayed
3. **Expect**: The change amount is mathematically correct

### POS-PAY-010 — Prepay Flow (P2)
1. Look for a prepay or "Pay Before Kitchen" option
2. Complete payment before sending to kitchen
3. **Expect**: The order is marked as paid and then sent to kitchen

### POS-PAY-011 — Table Release After Payment (P1)
1. Complete payment for all orders on a table
2. Return to the tables view
3. **Expect**: The table status changes back to "Available"

---

## 9. Live Orders

### POS-LIVE-001 — Live Orders Page (P0)
1. Navigate to Live Orders (from navigation or sidebar)
2. **Expect**: All active orders are displayed, organized by status
3. **Expect**: Orders show: order number, items, table, total, status, elapsed time

### POS-LIVE-002 — Status Grouping (P1)
1. Check the order groupings
2. **Expect**: Orders are grouped by status: Pending, In Progress, Ready, Completed

### POS-LIVE-003 — Order Actions (P1)
1. Click on an order in the live view
2. **Expect**: You can:
   - View full order details
   - Navigate to payment
   - See kitchen status per item

### POS-LIVE-004 — Real-time Updates (P0)
1. Keep the live orders page open
2. From the KDS app, bump a ticket to "Ready"
3. **Expect**: The order status updates in real time on the POS live orders page

### POS-LIVE-005 — Order Search/Filter (P2)
1. Look for search or filter options on the live orders page
2. Filter by status or search by order number
3. **Expect**: The list filters accordingly

---

## 10. Kitchen Overview

### POS-KITCHEN-001 — Kitchen Overview Page (P1)
1. Navigate to Kitchen Overview (from navigation)
2. **Expect**: A read-only view of kitchen tickets across stations
3. **Expect**: Similar to the KDS view but without action buttons

### POS-KITCHEN-002 — Station Breakdown (P1)
1. Check the kitchen overview
2. **Expect**: Tickets are organized by kitchen station
3. **Expect**: Each ticket shows: number, items, elapsed time, status

### POS-KITCHEN-003 — Ticket Status Colors (P2)
1. Review ticket status indicators
2. **Expect**: Tickets are color-coded by status (Pending = yellow, In Progress = blue, Ready = green)

---

## 11. Manager Actions (PIN-Protected)

### POS-MGR-001 — Void Item (P0)
1. Find an order with items
2. Select an item and choose "Void"
3. **Expect**: A manager PIN prompt appears
4. Enter the manager PIN
5. **Expect**: The item is voided
6. **Expect**: The order total recalculates

### POS-MGR-002 — Comp Item (P1)
1. Select an item and choose "Comp" (complimentary)
2. Enter manager PIN
3. **Expect**: The item price becomes $0
4. **Expect**: The order total recalculates

### POS-MGR-003 — Apply Discount (P0)
1. Find the discount option on an order
2. **Expect**: Options for percentage or fixed amount discount
3. Enter a discount (e.g., 15% off)
4. Enter manager PIN
5. **Expect**: The discount is applied to the order
6. **Expect**: The total reflects the discount

### POS-MGR-004 — Percentage Discount Calculation (P1)
1. Apply a 10% discount on an order
2. **Expect**: The discount amount = subtotal × 10%
3. **Verify**: The math is correct

### POS-MGR-005 — Fixed Amount Discount (P1)
1. Apply a fixed $5 discount
2. **Expect**: $5 is deducted from the total  
3. **Verify**: The math is correct

### POS-MGR-006 — Adjust Item Price (P1)
1. Select an item and choose "Adjust Price"
2. Enter manager PIN
3. Enter the new price
4. **Expect**: The item price updates
5. **Expect**: The order total recalculates

### POS-MGR-007 — Cancel Entire Order (P0)
1. Find the cancel option for an entire order
2. Enter manager PIN
3. Confirm the cancellation
4. **Expect**: The order status changes to "Cancelled"
5. **Expect**: The table may be released (if no other orders)

### POS-MGR-008 — View Modification History (P2)
1. On an order that has had voids, comps, or discounts
2. Look for a modification history or audit log
3. **Expect**: All modifications are listed with: action, who authorized (manager), timestamp

### POS-MGR-009 — Wrong Manager PIN (P1)
1. Attempt any manager action
2. Enter an incorrect PIN
3. **Expect**: An error message appears
4. **Expect**: The action is not performed

### POS-MGR-010 — Approve Shift Variance (P2)
1. During shift close, if there's a cash variance
2. A manager approval step appears
3. Enter manager PIN
4. **Expect**: The variance is approved and documented

---

## 12. Shift Close & Reconciliation

### POS-CLOSE-001 — Initiate Shift Close (P0)
1. Find the "Close Shift" option (from settings or navigation)
2. Click it
3. **Expect**: A multi-step shift close wizard begins

### POS-CLOSE-002 — Count Cash (P0)
1. In the shift close wizard, a cash counting step appears
2. Enter the cash in the drawer by denomination
3. **Expect**: The total is calculated automatically
4. **Expect**: Denominations match the restaurant's currency

### POS-CLOSE-003 — Reconciliation Summary (P0)
1. After counting cash, a reconciliation summary appears
2. **Expect**: You see:
   - Expected cash (float + cash payments received)
   - Actual cash (what you counted)
   - Variance (difference)
   - Payment breakdown by method (cash, card)
   - Number of transactions

### POS-CLOSE-004 — Zero Variance (P1)
1. If the counted cash exactly matches the expected amount
2. **Expect**: Variance shows $0 and is highlighted positively (green)

### POS-CLOSE-005 — Cash Variance Detection (P1)
1. If the counted cash doesn't match the expected amount
2. **Expect**: The variance is highlighted (typically in red)
3. **Expect**: Manager approval may be required

### POS-CLOSE-006 — Complete Shift Close (P0)
1. After reconciliation, confirm and close the shift
2. **Expect**: The shift is marked as closed
3. **Expect**: A printable shift report is generated
4. **Expect**: You are returned to the shift open page or login

### POS-CLOSE-007 — Cash Handover Notes (P2)
1. During shift close, look for a handover/notes field
2. Add notes about the shift
3. **Expect**: Notes are saved with the shift record

### POS-CLOSE-008 — Shift Report (P1)
1. After closing the shift, view the shift report
2. **Expect**: The report shows:
   - Shift start/end times
   - Staff member
   - Terminal
   - Opening float
   - Total sales by payment method
   - Cash reconciliation
   - Variance (if any)

---

## 13. Settings

### POS-SET-001 — Settings Page (P1)
1. Navigate to Settings
2. **Expect**: Configuration options are available for:
   - Terminal info
   - Shift management
   - Display preferences

### POS-SET-002 — Terminal Info (P2)
1. Review terminal information in settings
2. **Expect**: Current terminal name, IP, and status are shown

### POS-SET-003 — Shift Info (P1)
1. In settings, review current shift info
2. **Expect**: Current shift status, start time, and staff member are shown

---

## Summary — Test Count by Section

| Section | Total Tests | P0 | P1 | P2 | P3 |
|---------|:-----------:|:--:|:--:|:--:|:--:|
| Authentication | 4 | 3 | 1 | 0 | 0 |
| Terminal Selection | 3 | 2 | 0 | 1 | 0 |
| Shift Open | 5 | 3 | 1 | 1 | 0 |
| Lock Screen | 4 | 0 | 2 | 2 | 0 |
| Tables & Floor | 6 | 3 | 2 | 1 | 0 |
| Order Editor | 11 | 6 | 4 | 1 | 0 |
| Table Order Overview | 4 | 2 | 2 | 0 | 0 |
| Payment Processing | 11 | 4 | 4 | 3 | 0 |
| Live Orders | 5 | 2 | 2 | 1 | 0 |
| Kitchen Overview | 3 | 0 | 2 | 1 | 0 |
| Manager Actions | 10 | 3 | 4 | 3 | 0 |
| Shift Close | 8 | 3 | 3 | 2 | 0 |
| Settings | 3 | 0 | 2 | 1 | 0 |
| **TOTAL** | **77** | **31** | **29** | **17** | **0** |
