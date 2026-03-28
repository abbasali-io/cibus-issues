---
layout: default
title: Customer App Tests
parent: Testing Manuals
---

# Customer App — Manual Test Plan

> **App URL**: `https://hi.cibus.app`
> **Role Required**: Customer account (or guest for some flows)
> **Estimated Time**: 4–5 hours (full suite)

---

## Table of Contents

1. [Authentication & Login](#1-authentication--login)
2. [Home & Discovery](#2-home--discovery)
3. [Menu Browsing](#3-menu-browsing)
4. [Cart & Order Review](#4-cart--order-review)
5. [Payment & Checkout](#5-payment--checkout)
6. [Pickup Timeslots (Pre-order)](#6-pickup-timeslots-pre-order)
7. [Order Confirmation](#7-order-confirmation)
8. [Order Tracking](#8-order-tracking)
9. [Order History](#9-order-history)
10. [Reviews & Ratings](#10-reviews--ratings)
11. [Profile & Loyalty](#11-profile--loyalty)
12. [Vouchers & Coupons](#12-vouchers--coupons)
13. [Payment Methods](#13-payment-methods)
14. [Settings & Preferences](#14-settings--preferences)
15. [Notifications](#15-notifications)
16. [Language & RTL](#16-language--rtl)
17. [Help & Support](#17-help--support)
18. [Dine-In Group Ordering (QR Menu)](#18-dine-in-group-ordering-qr-menu)
19. [Staff Operations](#19-staff-operations)

---

## 1. Authentication & Login

### CUST-AUTH-001 — Successful Login (P0)
1. Go to `https://hi.cibus.app/login`
2. Enter valid customer email and password
3. Click "Sign In"
4. **Expect**: You are redirected to the home page
5. **Expect**: Your name/avatar appears in the profile area

### CUST-AUTH-002 — Invalid Credentials (P1)
1. Enter incorrect email or password
2. Click "Sign In"
3. **Expect**: An error message appears
4. **Expect**: You remain on the login page

### CUST-AUTH-003 — Guest Mode (P1)
1. On the login page, look for a "Continue as Guest" or "Skip" option
2. Click it
3. **Expect**: You can browse the menu without logging in
4. **Expect**: Checkout may require login

### CUST-AUTH-004 — QR Scan Login (P2)
1. Look for a QR scan option on the login page
2. **Expect**: Camera/scanner UI opens (may be simulated in dev)

### CUST-AUTH-005 — Staff Login (P2)
1. On the login page, look for a "Staff Login" option
2. Log in with staff credentials
3. **Expect**: You are directed to the staff section

### CUST-AUTH-006 — Logout (P0)
1. While logged in, navigate to profile or settings
2. Click "Logout"
3. **Expect**: You are logged out and redirected

---

## 2. Home & Discovery

### CUST-HOME-001 — Home Page Loads (P0)
1. After login, the home page loads
2. **Expect**: The page shows:
   - Recommended restaurants (if applicable)
   - Quick action buttons (QR Scan, Order Now, Pre-order)
   - Recent orders or restaurants

### CUST-HOME-002 — Order Now vs Pre-order Toggle (P1)
1. On the home page, find the Order Now / Pre-order toggle or tabs
2. Switch between them
3. **Expect**: The available restaurants/options change based on selection

### CUST-HOME-003 — Quick Actions (P1)
1. Click each quick action button on the home page
2. **Expect**: QR Scan opens the scanner
3. **Expect**: Order Now navigates to the menu
4. **Expect**: Pre-order navigates to saved restaurants or timeslot selection

### CUST-HOME-004 — Loyalty Rewards Highlight (P2)
1. Check the home page for loyalty/rewards info
2. **Expect**: Current loyalty tier and points are displayed (if applicable)

---

## 3. Menu Browsing

### CUST-MENU-001 — Menu Page Loads (P0)
1. Navigate to the menu (via home page or `/menu`)
2. **Expect**: Menu items are displayed with:
   - Item names, images, and prices
   - Category groupings
   - A sticky category navigation bar

### CUST-MENU-002 — Category Navigation (P0)
1. Click on different categories in the navigation bar
2. **Expect**: The menu scrolls to the selected category
3. **Expect**: The active category is highlighted in the navigation

### CUST-MENU-003 — Search Items (P1)
1. Find and click the search icon/bar
2. Type a menu item name (e.g., "burger")
3. **Expect**: An overlay appears with matching results
4. **Expect**: You can click a result to go to that item

### CUST-MENU-004 — View Toggle (Compact/List) (P2)
1. Look for a view toggle (compact cards vs. list view)
2. Switch between views
3. **Expect**: Items display in the selected layout
4. **Expect**: All information remains accessible

### CUST-MENU-005 — Item Detail Page (P0)
1. Click on any menu item
2. **Expect**: The item detail page shows:
   - Item name, image, and description
   - Price (or price range for sized items)
   - Nutrition badges (calories, allergens, spicy)
   - Modifier/option selection (if applicable)
   - Special instructions text area
   - Quantity controls (+/-)
   - "Add to Cart" button with the total price

### CUST-MENU-006 — Item Options/Variants (P0)
1. Open an item that has size options (e.g., Small/Medium/Large)
2. **Expect**: Size options are displayed with different prices
3. Select a size
4. **Expect**: The price updates to reflect the selected size

### CUST-MENU-007 — Item Modifiers (P0)
1. Open an item with modifiers (e.g., "Extra Cheese", "No Onions")
2. **Expect**: Modifier groups are displayed with their rules (required/optional)
3. Select modifiers
4. **Expect**: The price updates to include modifier price additions

### CUST-MENU-008 — Required Modifiers Validation (P1)
1. Open an item with required modifiers
2. Try to add to cart WITHOUT selecting the required modifier
3. **Expect**: A validation message appears asking you to make a selection
4. Select the required modifier and add to cart
5. **Expect**: Item is added successfully

### CUST-MENU-009 — Special Instructions (P1)
1. On the item detail page, type special instructions (e.g., "No mayo, extra lettuce")
2. Add the item to cart
3. **Expect**: The instructions are saved with the item

### CUST-MENU-010 — Quantity Adjustment (P1)
1. On the item detail page, use the +/- buttons to change quantity
2. **Expect**: The total price updates (unit price × quantity)
3. Add to cart
4. **Expect**: The cart shows the correct quantity

### CUST-MENU-011 — Allergen/Dietary Badges (P1)
1. Browse items and look for allergen or dietary tags
2. **Expect**: Items show tags like "Contains Nuts", "Vegan", "Gluten-Free" etc.
3. **Expect**: Tags are clearly visible with icons

### CUST-MENU-012 — Out of Stock Items (P1)
1. If any items are marked as out of stock (set in Admin app)
2. **Expect**: The item is grayed out or shows "Sold Out"
3. **Expect**: You cannot add it to cart
4. **Expect**: Clicking it shows an "unavailable" message

### CUST-MENU-013 — Add to Cart (P0)
1. Select an item with desired options
2. Click "Add to Cart"
3. **Expect**: A confirmation appears (toast or animation)
4. **Expect**: The cart icon updates with item count
5. **Expect**: The cart badge number increases

---

## 4. Cart & Order Review

### CUST-CART-001 — View Cart (P0)
1. Click the cart icon or navigate to `/order`
2. **Expect**: All added items are listed with:
   - Item name
   - Selected options/modifiers
   - Quantity
   - Item price (including modifier additions)
   - Special instructions (if added)

### CUST-CART-002 — Quantity Adjustment in Cart (P0)
1. In the cart, use +/- buttons to change an item's quantity
2. **Expect**: The quantity updates
3. **Expect**: The line total and cart total recalculate

### CUST-CART-003 — Remove Item from Cart (P0)
1. Remove an item from the cart (delete button or set quantity to 0)
2. **Expect**: The item disappears from the cart
3. **Expect**: The totals recalculate

### CUST-CART-004 — Price Calculation (P0)
1. Review the cart totals section
2. **Expect**: You see a breakdown of:
   - Subtotal (sum of all item prices)
   - Tax amount(s) with labels
   - Service charge (if configured)
   - Discount (if a voucher is applied)
   - Grand total
3. **Verify**: Calculate manually that the math is correct
4. **Expect**: Currency symbol matches the restaurant's setting

### CUST-CART-005 — Empty Cart State (P1)
1. Remove all items from the cart
2. **Expect**: An empty cart message is displayed
3. **Expect**: A link or button to "Browse Menu" is shown

### CUST-CART-006 — Cart Persistence (P1)
1. Add items to the cart
2. Close the browser tab
3. Reopen `https://hi.cibus.app` and go to the cart
4. **Expect**: Your cart items are still there (persisted in localStorage)

### CUST-CART-007 — My Items vs Group Items Tabs (P2)
1. In a group order scenario, check for "My Items" vs "Group Items" tabs
2. **Expect**: "My Items" shows only your personal items
3. **Expect**: "Group Items" shows all members' items combined

---

## 5. Payment & Checkout

### CUST-PAY-001 — Proceed to Payment (P0)
1. From the cart, click "Checkout" or "Proceed to Payment"
2. **Expect**: The payment page loads showing:
   - Order summary
   - Payment method selection
   - Total amount

### CUST-PAY-002 — Payment Method Selection (P0)
1. On the payment page, select different payment methods (Card, eWallet, Bank)
2. **Expect**: The selected method is highlighted
3. **Expect**: Additional fields may appear based on method (e.g., card details)

### CUST-PAY-003 — Apply Voucher Code (P1)
1. On the payment page, find the voucher/coupon code input
2. Enter a valid voucher code
3. Click "Apply"
4. **Expect**: The discount appears in the order summary
5. **Expect**: The total is reduced by the correct amount

### CUST-PAY-004 — Invalid Voucher Code (P1)
1. Enter an invalid or expired voucher code
2. Click "Apply"
3. **Expect**: An error message appears (e.g., "Invalid code" or "Expired")

### CUST-PAY-005 — Tip Entry (P2)
1. Look for a tip entry option on the payment page
2. Select a preset percentage or enter a custom amount
3. **Expect**: The tip is added to the total

### CUST-PAY-006 — Submit Order (P0)
1. With a valid payment method selected, click "Place Order" or "Submit"
2. **Expect**: A loading state appears
3. **Expect**: On success, you are redirected to the order confirmation page

### CUST-PAY-007 — Payment Failure Handling (P1)
1. Attempt to complete a payment that will fail (if testable)
2. **Expect**: An error message appears
3. **Expect**: You remain on the payment page to retry

### CUST-PAY-008 — Address Entry for Delivery (P2)
1. If delivery mode is selected, check for an address entry section
2. **Expect**: Address fields are available and required
3. Fill in a delivery address
4. **Expect**: The address is associated with the order

---

## 6. Pickup Timeslots (Pre-order)

### CUST-PRE-001 — Timeslot Page Loads (P1)
1. Navigate to the pickup timeslot page (via pre-order flow)
2. **Expect**: A date selector shows the next 5 days
3. **Expect**: Time slots are displayed grouped by hour

### CUST-PRE-002 — Select Date (P1)
1. Click on different dates
2. **Expect**: Available timeslots update for the selected date

### CUST-PRE-003 — Select Timeslot (P1)
1. Click on an available timeslot
2. **Expect**: The slot is highlighted as selected
3. Proceed to the menu
4. **Expect**: The selected pickup time is carried through the order flow

### CUST-PRE-004 — Operating Hours Respect (P1)
1. Check timeslots against the restaurant's operating hours
2. **Expect**: No timeslots are offered outside operating hours

### CUST-PRE-005 — Pickup Token (P1)
1. Complete a pre-order
2. On the confirmation page, look for a pickup token/code
3. **Expect**: A unique pickup token is displayed for identification

---

## 7. Order Confirmation

### CUST-CONF-001 — Confirmation Page (P0)
1. After placing an order, the confirmation page loads
2. **Expect**: The page shows:
   - Order ID (with copy button)
   - Confetti/celebration animation
   - Receipt summary (items, totals)
   - "Track Order" button
   - "Reorder" button

### CUST-CONF-002 — Copy Order ID (P1)
1. Click the "Copy" button next to the order ID
2. **Expect**: The order ID is copied to clipboard
3. **Expect**: A "Copied!" confirmation appears

### CUST-CONF-003 — Track Order Navigation (P0)
1. Click "Track Order"
2. **Expect**: You are navigated to the order tracking page

### CUST-CONF-004 — Reorder Button (P2)
1. Click "Reorder"
2. **Expect**: The same items are added to your cart for a new order

### CUST-CONF-005 — Pre-order Confirmation (P1)
1. Complete a pre-order
2. **Expect**: The confirmation shows the pickup date, time, and token

### CUST-CONF-006 — Share Receipt (P2)
1. Look for a "Share" option on the confirmation page
2. **Expect**: Share options are available

---

## 8. Order Tracking

### CUST-TRACK-001 — Tracking Page Loads (P0)
1. Navigate to order tracking (via confirmation or `/track-order/:id`)
2. **Expect**: The page shows the current order status with a visual progress indicator

### CUST-TRACK-002 — Status Progression (P0)
1. View the order status steps
2. **Expect**: You see stages like: Queued → Preparing → Ready → Served/Collected
3. **Expect**: The current stage is highlighted

### CUST-TRACK-003 — Kitchen Station Breakdown (P1)
1. Look for a kitchen station breakdown on the tracking page
2. **Expect**: You can see which stations are working on your items (e.g., Grill, Bar, Main)
3. **Expect**: Progress bars show completion per station

### CUST-TRACK-004 — Estimated Time (P1)
1. Check for an estimated time display
2. **Expect**: An ETA or estimated remaining time is shown

### CUST-TRACK-005 — Real-time Updates (P0)
1. Keep the tracking page open
2. Have someone update the order status from POS or KDS
3. **Expect**: The tracking page updates in real time without manual refresh

### CUST-TRACK-006 — Copy Order ID (P2)
1. Find the order ID on the tracking page
2. Copy it
3. **Expect**: The ID is copied to clipboard

### CUST-TRACK-007 — Pre-order Tracking (P1)
1. Track a pre-order
2. **Expect**: Additional stages like "Confirmed" are shown before "Preparing"

---

## 9. Order History

### CUST-HIST-001 — Order History Page (P0)
1. Navigate to `/orders` or "My Orders" from the bottom navigation
2. **Expect**: A list of past orders is displayed
3. **Expect**: Orders are grouped by date (Today, Yesterday, This Week, etc.)

### CUST-HIST-002 — Order Details (P1)
1. Click on a past order
2. **Expect**: Full order details are shown:
   - Order items with quantities and prices
   - Payment method and amount
   - Tax/charge breakdown
   - Date and time
   - Order status (completed, cancelled, etc.)

### CUST-HIST-003 — Reorder from History (P2)
1. On an order detail page, click "Reorder"
2. **Expect**: Items from that order are added to your cart

### CUST-HIST-004 — Copy Order ID from History (P2)
1. On an order detail page, copy the order ID
2. **Expect**: The ID is copied to clipboard

### CUST-HIST-005 — Item Details in History (P2)
1. Click on a specific item within an order
2. **Expect**: Item details page shows nutrition info, allergens, preparation details

---

## 10. Reviews & Ratings

### CUST-REV-001 — Rate Order Page (P1)
1. Navigate to rate an order (via order history or `/rate-order/:id`)
2. **Expect**: A rating interface shows:
   - Star/emoji rating selector (1–5)
   - Option to rate the restaurant overall
   - Option to rate individual items

### CUST-REV-002 — Submit Rating (P1)
1. Select a star rating (e.g., 4 stars)
2. Write a short review
3. Submit
4. **Expect**: A success message appears
5. **Expect**: The rating is saved

### CUST-REV-003 — Photo Upload in Review (P2)
1. While writing a review, click to add a photo
2. Upload an image
3. **Expect**: The photo preview appears
4. Submit the review
5. **Expect**: The photo is included in the review

### CUST-REV-004 — Social Sharing (P2)
1. After submitting a review, look for social sharing options
2. **Expect**: Options for WhatsApp, Instagram, Facebook, Twitter are available

### CUST-REV-005 — Pending Reviews (P1)
1. Navigate to `/pending-reviews`
2. **Expect**: Orders that haven't been rated yet are listed
3. Click on one to rate it

### CUST-REV-006 — Prevent Duplicate Reviews (P2)
1. Try to rate an order you've already rated
2. **Expect**: You cannot submit a duplicate review
3. **Expect**: The existing review is shown or you're informed it's already rated

---

## 11. Profile & Loyalty

### CUST-PROF-001 — Profile Page (P0)
1. Navigate to `/profile`
2. **Expect**: Profile page shows:
   - User name and avatar
   - KPI cards (total orders, monthly spend, restaurants visited, etc.)
   - Loyalty tier (if applicable)
   - Quick links to orders, vouchers, payment methods, settings

### CUST-PROF-002 — Loyalty Tier Display (P2)
1. Check the loyalty section
2. **Expect**: Your current tier (e.g., Gold, Platinum) is displayed
3. **Expect**: Points balance is shown

### CUST-PROF-003 — Loyalty Streak (P3)
1. Check for a streak counter
2. **Expect**: Consecutive ordering streak is displayed

### CUST-PROF-004 — Pending Reviews Badge (P2)
1. On the profile page, look for a pending reviews badge/counter
2. **Expect**: If you have unrated orders, the badge shows the count

---

## 12. Vouchers & Coupons

### CUST-VOUCH-001 — Vouchers Page (P1)
1. Navigate to `/vouchers`
2. **Expect**: Two tabs: Active and Expired

### CUST-VOUCH-002 — Active Vouchers (P1)
1. On the Active tab, review available vouchers
2. **Expect**: Each voucher shows code, discount amount, and expiry date

### CUST-VOUCH-003 — Copy Voucher Code (P1)
1. Click the "Copy" button on a voucher
2. **Expect**: The voucher code is copied to clipboard

### CUST-VOUCH-004 — Expired Vouchers (P2)
1. Switch to the Expired tab
2. **Expect**: Expired vouchers are listed (grayed out or clearly expired)

### CUST-VOUCH-005 — Use Voucher in Checkout (P1)
1. Copy a voucher code
2. Go through the order flow to the payment page
3. Apply the voucher code
4. **Expect**: The discount is applied correctly

---

## 13. Payment Methods

### CUST-PMETH-001 — Payment Methods Page (P1)
1. Navigate to `/payment-methods`
2. **Expect**: A list of saved payment methods (cards, eWallets, banks)

### CUST-PMETH-002 — Add Payment Method (P1)
1. Click "Add" or "+"
2. **Expect**: Options to add a card, eWallet, or bank account

### CUST-PMETH-003 — Set Default Payment (P2)
1. Set a payment method as default
2. **Expect**: The default method is marked and pre-selected at checkout

### CUST-PMETH-004 — Remove Payment Method (P2)
1. Delete a saved payment method
2. **Expect**: The method is removed from the list

---

## 14. Settings & Preferences

### CUST-SET-001 — Settings Page (P1)
1. Navigate to `/settings`
2. **Expect**: Settings page shows:
   - Theme selector (Light, Dark, System)
   - Privacy & Terms links
   - Data management options

### CUST-SET-002 — Theme Toggle (P1)
1. Switch between Light and Dark modes
2. **Expect**: The app's appearance changes immediately
3. **Expect**: The preference persists after page refresh

### CUST-SET-003 — Dark Mode Full Test (P2)
1. Switch to Dark mode
2. Navigate through multiple pages (Home, Menu, Cart, Profile)
3. **Expect**: All pages render correctly in dark mode
4. **Expect**: Text is readable, images have proper backgrounds

### CUST-SET-004 — Data Export (P3)
1. Look for a data export option
2. Click it
3. **Expect**: Your data is prepared for download

### CUST-SET-005 — Account Deletion (P3)
1. Look for the account deletion option
2. **Expect**: A confirmation dialog appears with warnings
3. **Do NOT confirm** unless using a disposable test account

---

## 15. Notifications

### CUST-NOTIF-001 — Notifications Settings Page (P1)
1. Navigate to `/notifications`
2. **Expect**: Toggle switches for different notification types:
   - Order updates (push/email/SMS)
   - Promotions
   - Rewards
   - Reviews

### CUST-NOTIF-002 — Toggle Notification Types (P2)
1. Toggle each notification type on and off
2. **Expect**: The toggle states save correctly
3. **Expect**: Settings persist after page refresh

---

## 16. Language & RTL

### CUST-LANG-001 — Language Page (P1)
1. Navigate to `/language`
2. **Expect**: Available languages are listed with flag icons

### CUST-LANG-002 — Change Language (P1)
1. Select a different language (e.g., Arabic)
2. **Expect**: The app language changes
3. **Expect**: All text is translated (or falls back gracefully)

### CUST-LANG-003 — RTL Layout (P1)
1. Switch to a RTL language (Arabic)
2. **Expect**: The entire layout flips to right-to-left
3. **Expect**: Navigation, menus, text alignment all adjust correctly
4. **Expect**: No visual overlaps or broken layouts

### CUST-LANG-004 — Locale-Aware Formatting (P2)
1. In a non-English locale, check date and number formatting
2. **Expect**: Dates and numbers follow the locale's conventions

---

## 17. Help & Support

### CUST-HELP-001 — Help Page (P2)
1. Navigate to `/help`
2. **Expect**: FAQ section with expandable accordions
3. **Expect**: Contact support options (chat, phone, email)

### CUST-HELP-002 — FAQ Accordion (P2)
1. Click on FAQ questions
2. **Expect**: Answers expand/collapse correctly

### CUST-HELP-003 — Contact Support (P2)
1. Click contact support
2. **Expect**: A form or modal with chat/phone/email options appears

---

## 18. Dine-In Group Ordering (QR Menu)

### CUST-QR-001 — QR Menu Page Load (P0)
1. Navigate to a QR menu URL: `/qrm/:restId/:tableId/:groupOrderId`
2. **Expect**: The QR menu page loads with:
   - Restaurant info
   - Table number
   - Group member list
   - Menu browsing capability

### CUST-QR-002 — Join Group Order (P0)
1. Open a QR menu link (simulating scanning a QR code)
2. **Expect**: A join flow appears (enter name or use account)
3. Join the group
4. **Expect**: You appear in the group member list

### CUST-QR-003 — Browse and Add Items (P0)
1. In the QR menu, browse menu items
2. Add items to the order
3. **Expect**: Items are added under your name in the group order

### CUST-QR-004 — View Group Cart (P0)
1. Navigate to the group cart
2. **Expect**: You can see:
   - Items organized by group member
   - Totals per member
   - Grand total for the group

### CUST-QR-005 — Cart Lock (P1)
1. Look for a "Lock Cart" option (typically for the table host)
2. Lock the cart
3. **Expect**: No one can add new items after locking

### CUST-QR-006 — QR Menu Payment (P0)
1. In the group order, proceed to payment
2. **Expect**: Payment options appear:
   - Full payment
   - Split bill options
   - Tip entry

### CUST-QR-007 — Bill Split Options (P1)
1. On the QR payment page, select "Split Bill"
2. **Expect**: Options for splitting (equal split, pay for my items, custom amounts)

### CUST-QR-008 — Tip Entry in QR Order (P2)
1. Enter a tip amount (percentage or fixed)
2. **Expect**: The tip is added to the total

### CUST-QR-009 — Group Order Auto-Close (P2)
1. After all payments are completed
2. **Expect**: The group order auto-closes
3. **Expect**: The table is released

### CUST-QR-010 — Theme Toggle in Dine-In (P3)
1. In the QR menu view, look for a theme toggle
2. Switch themes
3. **Expect**: The dine-in interface switches between light/dark

### CUST-QR-011 — QR Order Review (P2)
1. After the QR order is complete, a review page appears
2. **Expect**: You can rate the dining experience

---

## 19. Staff Operations

### CUST-STAFF-001 — Staff Home Page (P1)
1. Log in as staff and navigate to `/staff`
2. **Expect**: A table overview showing:
   - All tables with their status (Available, Occupied, Pending)
   - Guest count per table
   - Waiting time tracking
   - Stats summary

### CUST-STAFF-002 — Create Hosted Order (P1)
1. Click on an available/occupied table
2. Navigate to create a new order
3. Browse the menu and add items
4. Submit the order
5. **Expect**: The order is created for that table
6. **Expect**: The table status updates to "Occupied"

### CUST-STAFF-003 — Edit Existing Order (P1)
1. Click on a table with an active order
2. Edit the order (add/remove items)
3. Save changes
4. **Expect**: The order updates with the modifications

### CUST-STAFF-004 — Table QR Code (P2)
1. Navigate to a table's QR page
2. **Expect**: A QR code is displayed for the table
3. **Expect**: Options to print or download the QR code

### CUST-STAFF-005 — Staff Logout (P1)
1. Click the logout button in the staff interface
2. **Expect**: You are logged out and redirected to the login page

---

## 20. Bottom Navigation & General UI

### CUST-NAV-001 — Bottom Navigation (P0)
1. Check the bottom navigation bar
2. **Expect**: 4 main tabs are visible (Home, Menu, Orders, Profile)
3. Click each tab
4. **Expect**: You navigate to the correct page
5. **Expect**: The active tab is highlighted

### CUST-NAV-002 — Scroll to Top (P2)
1. Scroll down a long page (e.g., menu with many items)
2. Navigate to another page and come back
3. **Expect**: The page starts at the top (auto scroll-to-top)

### CUST-NAV-003 — Back Navigation (P1)
1. Navigate several pages deep (Home → Menu → Item → Cart)
2. Use the browser back button
3. **Expect**: You navigate back through the pages correctly
4. **Expect**: No pages are skipped or duplicated

### CUST-NAV-004 — Toast Notifications (P1)
1. Perform actions that trigger notifications (add to cart, place order, etc.)
2. **Expect**: Toast notifications appear briefly with success/error messages
3. **Expect**: Toasts auto-dismiss after a few seconds

---

## Summary — Test Count by Section

| Section | Total Tests | P0 | P1 | P2 | P3 |
|---------|:-----------:|:--:|:--:|:--:|:--:|
| Authentication | 6 | 2 | 2 | 2 | 0 |
| Home & Discovery | 4 | 1 | 2 | 1 | 0 |
| Menu Browsing | 13 | 5 | 6 | 2 | 0 |
| Cart & Order Review | 7 | 4 | 2 | 1 | 0 |
| Payment & Checkout | 8 | 2 | 3 | 3 | 0 |
| Pickup Timeslots | 5 | 0 | 5 | 0 | 0 |
| Order Confirmation | 6 | 2 | 2 | 2 | 0 |
| Order Tracking | 7 | 3 | 2 | 2 | 0 |
| Order History | 5 | 1 | 1 | 3 | 0 |
| Reviews & Ratings | 6 | 0 | 3 | 3 | 0 |
| Profile & Loyalty | 4 | 1 | 0 | 2 | 1 |
| Vouchers & Coupons | 5 | 0 | 4 | 1 | 0 |
| Payment Methods | 4 | 0 | 2 | 2 | 0 |
| Settings & Preferences | 5 | 0 | 2 | 1 | 2 |
| Notifications | 2 | 0 | 1 | 1 | 0 |
| Language & RTL | 4 | 0 | 3 | 1 | 0 |
| Help & Support | 3 | 0 | 0 | 3 | 0 |
| QR Group Ordering | 11 | 4 | 2 | 4 | 1 |
| Staff Operations | 5 | 0 | 4 | 1 | 0 |
| Navigation & UI | 4 | 1 | 2 | 1 | 0 |
| **TOTAL** | **114** | **26** | **48** | **34** | **4** |
