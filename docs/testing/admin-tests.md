---
layout: default
title: Admin App Tests
parent: Testing Manuals
nav_order: 1
---

# Admin App — Manual Test Plan

> **App URL**: `https://admin.cibus.app`
> **Role Required**: Admin (restaurant owner/manager)
> **Estimated Time**: 6–8 hours (full suite)

---

## Table of Contents

1. [Authentication & Login](#1-authentication--login)
2. [Dashboard](#2-dashboard)
3. [Orders](#3-orders)
4. [Payments](#4-payments)
5. [Menu Management](#5-menu-management)
6. [Staff Management](#6-staff-management)
7. [Schedule & Shifts](#7-schedule--shifts)
8. [Floor Plan & Tables](#8-floor-plan--tables)
9. [Kitchen Stations](#9-kitchen-stations)
10. [POS Terminal Management](#10-pos-terminal-management)
11. [Restaurants & Brands](#11-restaurants--brands)
12. [Printers](#12-printers)
13. [Taxes & Charges](#13-taxes--charges)
14. [Promotions](#14-promotions)
15. [Settings](#15-settings)

---

## 1. Authentication & Login

### ADM-AUTH-001 — Successful Login (P0)
1. Go to `https://admin.cibus.app`
2. You should see the login page
3. Enter valid admin email and password
4. Click "Sign In"
5. **Expect**: You are redirected to the Admin Dashboard

### ADM-AUTH-002 — Invalid Credentials (P1)
1. On the login page, enter an incorrect email or password
2. Click "Sign In"
3. **Expect**: An error message appears (e.g., "Invalid credentials")
4. **Expect**: You remain on the login page

### ADM-AUTH-003 — Empty Fields Validation (P2)
1. On the login page, leave email and/or password empty
2. Click "Sign In"
3. **Expect**: Validation messages appear for required fields

### ADM-AUTH-004 — Logout (P0)
1. While logged in, find and click the logout button/menu
2. **Expect**: You are redirected to the login page
3. **Expect**: Navigating back to `/admin` redirects you to login

### ADM-AUTH-005 — Session Persistence (P1)
1. Log in successfully
2. Close the browser tab (don't log out)
3. Open `https://admin.cibus.app/admin` in a new tab
4. **Expect**: You are still logged in (session persists)

---

## 2. Dashboard

### ADM-DASH-001 — Dashboard Loads (P0)
1. Log in and navigate to `/admin`
2. **Expect**: The dashboard page loads with:
   - Restaurant name/info displayed
   - KPI cards/metrics visible (orders, revenue, etc.)
   - Activity feed or recent activity section

### ADM-DASH-002 — KPI Metrics Display (P1)
1. On the dashboard, review the KPI cards
2. **Expect**: Metrics like total orders, revenue, active tables, etc. are displayed
3. **Expect**: Numbers look reasonable (not zero if restaurant has data, or zero for a fresh restaurant)

### ADM-DASH-003 — Navigation from Dashboard (P1)
1. On the dashboard, click on various quick action links or cards
2. **Expect**: Each click navigates you to the correct section (e.g., clicking an orders summary takes you to the Orders page)

---

## 3. Orders

### ADM-ORD-001 — View Active Orders (P0)
1. Navigate to the Orders section from the sidebar
2. **Expect**: A list/grid of active/recent orders is displayed
3. **Expect**: Each order shows: order number, status, table/customer, total amount, timestamp

### ADM-ORD-002 — Order Status Filters (P0)
1. On the Orders page, look for status filter buttons/tabs (e.g., All, Pending, In Progress, Completed, Cancelled)
2. Click each filter
3. **Expect**: The list updates to show only orders matching the selected status
4. **Expect**: Counts on filter buttons match the number of displayed orders

### ADM-ORD-003 — Search Orders (P1)
1. On the Orders page, find the search bar
2. Type an order number or customer name
3. **Expect**: The list filters to show matching orders in real time

### ADM-ORD-004 — View Order Detail (P0)
1. Click on any order in the list
2. **Expect**: A detail view/sheet opens showing:
   - Order number and status
   - List of items with quantities and prices
   - Subtotal, taxes, charges, and total
   - Payment status
   - Table/section information (if dine-in)
   - Timestamp (created, updated)

### ADM-ORD-005 — Order Items Display (P1)
1. In the order detail, review the items list
2. **Expect**: Each item shows name, quantity, unit price, and line total
3. **Expect**: Items with modifiers show the modifier names and any price additions
4. **Expect**: Special instructions are visible if any were added

### ADM-ORD-006 — Order Status History (P2)
1. In the order detail, look for a timeline or status history
2. **Expect**: You can see when the order was created, status changes, and timestamps

### ADM-ORD-007 — Historical Orders (P1)
1. Look for a Historical/Past Orders tab or date filter
2. Select a past date range
3. **Expect**: Past orders load with pagination
4. **Expect**: You can click on historical orders to view their details

### ADM-ORD-008 — Date Range Filtering (P1)
1. On the Orders page, find date filter controls
2. Select different date ranges (Today, Yesterday, This Week, custom)
3. **Expect**: The orders list updates to show only orders from the selected period

### ADM-ORD-009 — Section/Table Filtering (P2)
1. Look for section or table filter options
2. Filter by a specific floor section or table
3. **Expect**: Only orders from that section/table are displayed

### ADM-ORD-010 — Order View Toggle (P2)
1. Look for a view toggle (Cards/Grid vs. List/Table)
2. Switch between views
3. **Expect**: The same orders are shown in a different layout
4. **Expect**: All critical information remains visible in both views

### ADM-ORD-011 — Record Payment on Order (P0)
1. Find an unpaid/pending order
2. Open the order detail
3. Look for a "Record Payment" or "Mark as Paid" action
4. Select a payment method and confirm
5. **Expect**: The order's payment status updates to "Paid"
6. **Expect**: The change is reflected in the order list

### ADM-ORD-012 — Cancel Order (P1)
1. Find an active order that hasn't been sent to the kitchen
2. Open the order detail
3. Look for a "Cancel" action
4. Confirm the cancellation
5. **Expect**: The order status changes to "Cancelled"
6. **Expect**: The order moves to the cancelled filter

### ADM-ORD-013 — Edit Order Items (P1)
1. Find an active order
2. Open the order detail
3. Try to add or remove items from the order
4. **Expect**: You can modify the order items
5. **Expect**: The totals recalculate after modification

### ADM-ORD-014 — Export Orders (P2)
1. On the Orders page, look for an export/download button
2. Click it and select a format (CSV, etc.)
3. **Expect**: A file downloads containing order data

### ADM-ORD-015 — Real-time Order Updates (P0)
1. Keep the Orders page open
2. From the Customer app (another browser), create a new order
3. **Expect**: The new order appears in the Admin orders list without manual refresh
4. **Expect**: Order status updates appear in real time

---

## 4. Payments

### ADM-PAY-001 — Payments Dashboard (P0)
1. Navigate to Payments from the sidebar
2. **Expect**: A payments dashboard loads showing:
   - Payment KPIs (total collected, pending, methods breakdown)
   - Recent payment activity

### ADM-PAY-002 — Payments List (P1)
1. Navigate to the Payments list tab
2. **Expect**: A list of all payment transactions is displayed
3. **Expect**: Each payment shows: amount, method, status, associated order, timestamp

### ADM-PAY-003 — Payment Method Breakdown (P1)
1. On the Payments dashboard, review the method breakdown
2. **Expect**: Payments are categorized by method (Cash, Card, etc.)
3. **Expect**: Icons or labels clearly identify each method

### ADM-PAY-004 — Outstanding Orders (P1)
1. Look for an "Outstanding" or "Unpaid" tab
2. **Expect**: A list of orders that haven't been fully paid
3. **Expect**: You can click on each to navigate to the order or record a payment

### ADM-PAY-005 — Settlements (P2)
1. Look for a Settlements tab
2. **Expect**: Settlement/reconciliation data is displayed
3. **Expect**: Shows settlement periods and amounts

### ADM-PAY-006 — Payment Detail (P1)
1. Click on any payment in the list
2. **Expect**: A detail view shows:
   - Full payment amount and method
   - Order reference
   - Timestamp
   - Status (completed, refunded, etc.)

---

## 5. Menu Management

### ADM-MENU-001 — View Menus List (P0)
1. Navigate to Menu from the sidebar
2. **Expect**: A list of menus is displayed (e.g., Main Menu, Breakfast Menu)
3. **Expect**: Each menu shows its name, status, and number of categories/items

### ADM-MENU-002 — Create New Menu (P0)
1. Click "Create Menu" or "+" button
2. Fill in the menu name (e.g., "Test Menu")
3. Optionally set a schedule (e.g., available only for lunch)
4. Save the menu
5. **Expect**: The new menu appears in the list
6. **Expect**: A success notification appears

### ADM-MENU-003 — Edit Menu (P1)
1. Click on an existing menu to edit it
2. Change the name or schedule
3. Save the changes
4. **Expect**: The changes are reflected in the menu list

### ADM-MENU-004 — Set Default Menu (P1)
1. Find the option to set a menu as the default
2. Set a different menu as default
3. **Expect**: The selected menu is marked as "Default"
4. **Expect**: The previous default menu loses its default label

### ADM-MENU-005 — Delete Menu (P2)
1. Find a menu you want to delete (preferably the test one)
2. Click the delete/remove action
3. Confirm the deletion
4. **Expect**: The menu is removed from the list

### ADM-MENU-006 — View Categories (P0)
1. Navigate to Menu > Categories
2. **Expect**: A list of categories is displayed with names, images, item counts

### ADM-MENU-007 — Create Category (P0)
1. Click "Add Category" or "+"
2. Fill in: name, optional image, color/icon
3. Save
4. **Expect**: The new category appears in the list
5. **Expect**: A success notification appears

### ADM-MENU-008 — Reorder Categories (P1)
1. On the categories list, try to drag and drop categories to reorder them
2. **Expect**: Categories can be rearranged
3. **Expect**: The new order is saved and persists on page refresh

### ADM-MENU-009 — Edit Category (P1)
1. Click on a category to edit
2. Change the name or image
3. Save
4. **Expect**: Changes are reflected

### ADM-MENU-010 — Delete Category (P2)
1. Delete a test category
2. **Expect**: The category is removed
3. **Expect**: Items in that category are handled (moved to uncategorized or warning shown)

### ADM-MENU-011 — View Menu Items (P0)
1. Navigate to Menu > Items
2. **Expect**: A grid/list of all menu items is displayed
3. **Expect**: Each item shows: name, image, price, category, availability status

### ADM-MENU-012 — Create Menu Item (P0)
1. Click "Add Item" or "+"
2. Fill in:
   - Name (e.g., "Test Burger")
   - Description
   - Category (select from dropdown)
   - Base price
   - Image (upload one)
3. Save
4. **Expect**: The item appears in the items list
5. **Expect**: The image is displayed correctly

### ADM-MENU-013 — Item Pricing with Sizes (P1)
1. Create or edit a menu item
2. Add size variants (e.g., Small, Medium, Large) with different prices
3. Save
4. **Expect**: The item shows its size options and price range
5. **Expect**: In the Customer app, the item shows size selection

### ADM-MENU-014 — Item Modifiers (P1)
1. Create or edit a menu item
2. Add modifiers (e.g., "Extra Cheese +$1.50", "No Onions")
3. Set modifier rules (required/optional, single/multi-select, min/max)
4. Save
5. **Expect**: Modifiers are listed on the item detail
6. **Expect**: In the Customer app, the modifiers appear when adding the item to cart

### ADM-MENU-015 — Item Allergen/Dietary Tags (P1)
1. Edit a menu item
2. Add allergen tags (e.g., Contains Nuts, Gluten-Free, Vegan)
3. Save
4. **Expect**: Tags are visible on the item in the admin
5. **Expect**: Tags are visible in the Customer app

### ADM-MENU-016 — Item Stock Control (P1)
1. Edit a menu item
2. Find stock/availability controls
3. Mark the item as "Out of Stock" or set a quantity limit
4. Save
5. **Expect**: The item shows as unavailable/out of stock
6. **Expect**: In the Customer app, the item is grayed out or shows "Sold Out"

### ADM-MENU-017 — Item Kitchen Instructions (P2)
1. Edit a menu item
2. Add kitchen preparation instructions
3. Save
4. **Expect**: The instructions are saved and visible when the item appears in kitchen tickets

### ADM-MENU-018 — Search/Filter Items (P1)
1. On the Items page, use the search bar
2. Type an item name
3. **Expect**: Results filter in real time
4. Filter by category
5. **Expect**: Only items from that category are shown

### ADM-MENU-019 — Modifier Groups (P1)
1. Navigate to Menu > Modifiers
2. **Expect**: A list of modifier groups is displayed
3. Create a new modifier group with options and pricing
4. **Expect**: The group appears in the list and can be assigned to menu items

### ADM-MENU-020 — AI Menu Import (P1)
1. Navigate to Menu and find the "AI Import" or "Import from Image" feature
2. Upload a photo of a physical menu
3. **Expect**: The AI wizard starts processing:
   - Step 1: Upload/preview the image
   - Step 2: AI extracts menu items
   - Step 3: Review extracted items
   - Step 4: Resolve conflicts
   - Step 5: Handle duplicates
   - Step 6: Summary and confirm
4. **Expect**: Extracted items are added to your menu

### ADM-MENU-021 — Delete Menu Item (P2)
1. Delete a test menu item
2. **Expect**: The item is removed from the list
3. **Expect**: The item no longer appears in the Customer app

---

## 6. Staff Management

### ADM-STAFF-001 — View Staff List (P0)
1. Navigate to Staff from the sidebar
2. **Expect**: A list/grid of all staff members is displayed
3. **Expect**: Each entry shows: name, role, department, status (active/disabled)

### ADM-STAFF-002 — Search Staff (P1)
1. Use the search bar on the Staff page
2. Type a staff member's name
3. **Expect**: The list filters to matching staff members

### ADM-STAFF-003 — Filter by Role/Department (P1)
1. Use role or department filter options
2. Select a specific role (e.g., Cashier) or department (e.g., Kitchen)
3. **Expect**: The list shows only matching staff members

### ADM-STAFF-004 — Create New Staff Member (P0)
1. Click "Add Staff" or "+"
2. The creation wizard should open with multiple steps:
   - **Step 1**: Personal info (name, email, phone)
   - **Step 2**: Role selection and permissions
   - **Step 3**: Station assignment (if kitchen staff)
   - **Step 4**: Department assignment
   - **Step 5**: Contact details
   - **Step 6**: Review and confirm
3. Complete all steps and submit
4. **Expect**: The new staff member appears in the list
5. **Expect**: They can log into their assigned app

### ADM-STAFF-005 — Edit Staff Member (P1)
1. Click on a staff member in the list
2. Edit their information (e.g., change role, update phone)
3. Save changes
4. **Expect**: The changes are reflected in the staff list

### ADM-STAFF-006 — Disable Staff Account (P1)
1. Find the option to disable a staff member's account
2. Disable a test staff member
3. **Expect**: The staff member is marked as "Disabled"
4. **Expect**: They can no longer log into the system

### ADM-STAFF-007 — Enable Staff Account (P1)
1. Find a disabled staff member
2. Re-enable their account
3. **Expect**: The staff member is marked as "Active" again

### ADM-STAFF-008 — Roles & Permissions (P0)
1. Navigate to Staff > Roles & Permissions
2. **Expect**: A list of role templates is displayed (e.g., Owner, Manager, Cashier, Waiter, Chef, Kitchen Staff)
3. Click on a role to view its permissions
4. **Expect**: A detailed list of capabilities/permissions is shown

### ADM-STAFF-009 — Custom Role Creation (P2)
1. Create a new custom role
2. Select specific permissions for the role
3. Save
4. **Expect**: The new role appears in the roles list and can be assigned to staff

### ADM-STAFF-010 — Staff Attendance (P2)
1. Navigate to Staff > Attendance
2. **Expect**: A monthly attendance view is displayed
3. **Expect**: Shows clock in/out times, overtime, and stats per staff member

### ADM-STAFF-011 — Bulk Actions (P2)
1. On the Staff list, select multiple staff members (checkbox/shift+click)
2. Look for bulk action options (e.g., bulk disable, bulk role change)
3. **Expect**: Bulk actions apply to all selected staff members

---

## 7. Schedule & Shifts

### ADM-SCHED-001 — View Operating Hours (P0)
1. Navigate to Schedule > Operating Hours
2. **Expect**: A weekly view showing operating hours per day
3. **Expect**: Each day shows open/close times

### ADM-SCHED-002 — Edit Operating Hours (P0)
1. Click to edit operating hours for a day
2. Change the opening or closing time
3. Save
4. **Expect**: The updated hours are saved and displayed
5. **Expect**: The Customer app respects these hours (e.g., shows "Closed" outside hours)

### ADM-SCHED-003 — Service Type Hours (P1)
1. Look for service type variations (Dine-in, Takeaway, Delivery, Pre-order)
2. Set different hours for different service types
3. **Expect**: Each service type can have its own schedule

### ADM-SCHED-004 — Break Times (P2)
1. Add break times within operating hours
2. **Expect**: Break periods are displayed and excluded from service hours

### ADM-SCHED-005 — Special Hours (P2)
1. Look for "Special Hours" or "Holiday Hours" option
2. Add special hours for a specific date (e.g., close early on a holiday)
3. **Expect**: The special hours override the regular schedule for that date

### ADM-SCHED-006 — View Staff Shifts (P1)
1. Navigate to Schedule > Staff Shifts
2. **Expect**: A calendar view showing shifts for all staff
3. **Expect**: Shifts show: staff name, start/end time, status

### ADM-SCHED-007 — Create Staff Shift (P1)
1. Click to create a new shift
2. Assign a staff member, set start/end time, set role
3. Save
4. **Expect**: The shift appears on the calendar

### ADM-SCHED-008 — Shift Status Management (P2)
1. Review shift statuses (Confirmed, Pending, Swap Requested)
2. Confirm or modify pending shifts
3. **Expect**: Status updates are reflected in the calendar

### ADM-SCHED-009 — Shift Templates (P2)
1. Navigate to Schedule > Shift Templates
2. Create a reusable shift template
3. Apply it to a week
4. **Expect**: Shifts are auto-populated based on the template

---

## 8. Floor Plan & Tables

### ADM-FLOOR-001 — View Sections (P0)
1. Navigate to Floor Plan from the sidebar
2. **Expect**: A list of floor sections is displayed (e.g., Main Dining, Patio, Bar Area)
3. **Expect**: Each section shows: name, capacity, table count, indoor/outdoor

### ADM-FLOOR-002 — Create Section (P1)
1. Click "Add Section" or "+"
2. Fill in: name, capacity, floor level, indoor/outdoor
3. Optionally set a color
4. Save
5. **Expect**: The new section appears in the list

### ADM-FLOOR-003 — Edit Section (P2)
1. Edit an existing section's details
2. Save changes
3. **Expect**: Changes are reflected

### ADM-FLOOR-004 — View Tables (P0)
1. Navigate to Floor Plan > Tables
2. **Expect**: Tables are displayed in grid or table view
3. **Expect**: Each table shows: number, capacity, section, current status

### ADM-FLOOR-005 — Create Table (P1)
1. Click "Add Table" or "+"
2. Fill in: table number, capacity, section assignment
3. Save
4. **Expect**: The new table appears
5. **Expect**: The table is assignable in the POS app

### ADM-FLOOR-006 — Table Status Display (P0)
1. Review table statuses in the list
2. **Expect**: Tables show their current status: Available, Occupied, Reserved, Cleaning
3. **Expect**: Status is color-coded

### ADM-FLOOR-007 — Edit Table (P2)
1. Edit a table's details (number, capacity, section)
2. Save
3. **Expect**: Changes are reflected

### ADM-FLOOR-008 — QR Code for Table (P1)
1. Find the QR code option for a table
2. Generate or view the QR code
3. **Expect**: A QR code is displayed that links to the Customer app's dine-in ordering for that table

### ADM-FLOOR-009 — Server Assignment (P2)
1. Assign a server/waiter to a table
2. **Expect**: The server assignment is saved and visible

### ADM-FLOOR-010 — Combine Tables (P2)
1. Look for an option to combine/merge tables
2. Select two adjacent tables and combine them
3. **Expect**: The tables are shown as a combined unit

### ADM-FLOOR-011 — Live Floor View (P1)
1. Navigate to Floor Plan > Live View
2. **Expect**: An interactive floor plan visualization showing:
   - All sections and tables with their real-time status
   - Color-coded table occupancy
3. **Expect**: Activity timeline showing recent table events

### ADM-FLOOR-012 — Table View Toggle (P2)
1. Toggle between Grid View and Table/List View
2. **Expect**: The same data appears in the different layout

---

## 9. Kitchen Stations

### ADM-KITCHEN-001 — View Kitchen Stations (P0)
1. Navigate to Kitchen from the sidebar
2. **Expect**: A list of kitchen stations is displayed (e.g., Main Kitchen, Grill, Salad Bar, Drinks)
3. **Expect**: Each station shows: name, type, assigned staff

### ADM-KITCHEN-002 — Create Station (P1)
1. Click "Add Station" or "+"
2. Fill in: station name, type (e.g., Prep, Grill, Bar)
3. Optionally assign a printer
4. Save
5. **Expect**: The new station appears in the list

### ADM-KITCHEN-003 — Edit Station (P2)
1. Edit a station's details (name, type, printer)
2. Save
3. **Expect**: Changes are reflected

### ADM-KITCHEN-004 — KDS Preview (P1)
1. Look for a KDS or "Kitchen Display" section
2. **Expect**: A Kanban-style view showing tickets across stations (similar to what the KDS app shows)
3. **Expect**: Tickets show: number, items, elapsed time, status

### ADM-KITCHEN-005 — Station Printer Assignment (P2)
1. Assign a printer to a station
2. **Expect**: The printer assignment is saved

---

## 10. POS Terminal Management

### ADM-POS-001 — View Terminals (P0)
1. Navigate to POS from the sidebar
2. **Expect**: A list of POS terminals is displayed
3. **Expect**: Each terminal shows: name, status (Online/Offline), IP address

### ADM-POS-002 — Register Terminal (P1)
1. Click "Add Terminal" or "+"
2. Fill in: terminal name, IP, other settings
3. Save
4. **Expect**: The new terminal appears in the list

### ADM-POS-003 — Terminal Status (P1)
1. Review terminal statuses
2. **Expect**: Online terminals are clearly distinguished from offline ones

### ADM-POS-004 — Terminal Settings (P2)
1. Click on a terminal to view/edit its settings
2. **Expect**: Configuration options like printer assignment, diagnostics, etc.

### ADM-POS-005 — View POS Shifts (P1)
1. Navigate to POS > Shifts
2. **Expect**: A list of POS shifts (current and historical)
3. **Expect**: Each shift shows: date, terminal, staff, status, cash totals

### ADM-POS-006 — Shift Details (P1)
1. Click on a shift to view details
2. **Expect**: Full shift report showing:
   - Transaction list
   - Payment method breakdown
   - Cash reconciliation (expected vs. actual)
   - Variance if any

### ADM-POS-007 — Shift Reconciliation (P2)
1. View a closed shift's reconciliation
2. **Expect**: Cash counted vs. expected amounts are shown
3. **Expect**: Any variance is highlighted

---

## 11. Restaurants & Brands

### ADM-REST-001 — View Restaurants List (P0)
1. Navigate to Restaurants from the sidebar
2. **Expect**: A list of restaurants is displayed
3. **Expect**: Each shows: name, status, staff count, location

### ADM-REST-002 — Restaurant Detail (P1)
1. Click on a restaurant
2. **Expect**: A detail page with restaurant profile, stats, and settings

### ADM-REST-003 — Create New Restaurant (P1)
1. Click "Add Restaurant" or "+"
2. Complete the multi-step setup wizard
3. **Expect**: The new restaurant is created and appears in the list

### ADM-REST-004 — Edit Restaurant Profile (P1)
1. Edit an existing restaurant's profile (name, logo, description)
2. Save
3. **Expect**: Changes are reflected

### ADM-REST-005 — Brand Management (P2)
1. Navigate to Brands
2. **Expect**: Brand groups are displayed
3. Try creating or editing a brand
4. **Expect**: Changes are saved

---

## 12. Printers

### ADM-PRINT-001 — View Printers (P1)
1. Navigate to Printers from the sidebar
2. **Expect**: A list of network printers is displayed
3. **Expect**: Each shows: name, IP, status, assigned station

### ADM-PRINT-002 — Add Printer (P2)
1. Add a new network printer
2. Fill in: name, IP address
3. Save
4. **Expect**: The printer appears in the list

### ADM-PRINT-003 — Printer Status (P2)
1. Review printer statuses
2. **Expect**: Status indicators show whether printers are connected

### ADM-PRINT-004 — Test Print (P2)
1. Click "Test Print" on a printer
2. **Expect**: A test page is sent to the printer (or a success/failure message appears)

### ADM-PRINT-005 — Assign Printer to Station (P2)
1. Assign a printer to a kitchen station
2. **Expect**: The assignment is saved and visible in both the Printers and Kitchen Stations pages

---

## 13. Taxes & Charges

### ADM-TAX-001 — View Tax Rates (P0)
1. Navigate to Taxes & Charges from the sidebar
2. **Expect**: A list of tax rates and service charges is displayed
3. **Expect**: Each shows: name, rate/amount, type (percentage/fixed)

### ADM-TAX-002 — Create Tax Rate (P0)
1. Click "Add Tax" or "+"
2. Fill in: name (e.g., "VAT"), rate (e.g., 15%), type (percentage)
3. Save
4. **Expect**: The tax rate appears in the list

### ADM-TAX-003 — Edit Tax Rate (P1)
1. Edit an existing tax rate
2. Change the percentage
3. Save
4. **Expect**: The change is reflected
5. **Expect**: New orders in the Customer/POS apps use the updated rate

### ADM-TAX-004 — Create Service Charge (P1)
1. Create a new service charge (e.g., "Service Charge 10%")
2. Save
3. **Expect**: The charge is applied to orders

### ADM-TAX-005 — Delete Tax/Charge (P2)
1. Delete a test tax rate or charge
2. **Expect**: It is removed from the list
3. **Expect**: It is no longer applied to new orders

### ADM-TAX-006 — Tax Calculation Priority (P2)
1. If there are multiple taxes, check the calculation priority/order
2. **Expect**: You can set which taxes are calculated first
3. **Expect**: The calculation follows the priority order (e.g., tax on tax vs. tax on subtotal)

### ADM-TAX-007 — Effective Dates (P2)
1. Set effective start/end dates for a tax rate
2. **Expect**: The tax is only applied within those dates

---

## 14. Promotions

### ADM-PROMO-001 — View Promotions (P1)
1. Navigate to Promotions from the sidebar
2. **Expect**: A list of promotions/coupons is displayed
3. **Expect**: Each shows: name, type, discount value, status, expiry

### ADM-PROMO-002 — Create Coupon (P1)
1. Click "Add Promotion" or "+"
2. Create a coupon with:
   - Name (e.g., "SAVE10")
   - Type (percentage or fixed amount)
   - Discount value (e.g., 10% or $5)
   - Expiry date
   - Usage limit
3. Save
4. **Expect**: The coupon appears in the list

### ADM-PROMO-003 — Percentage Discount (P1)
1. Create a percentage-based coupon (e.g., 20% off)
2. **Expect**: The coupon is created
3. Use it in the Customer app and verify the discount is applied correctly as a percentage

### ADM-PROMO-004 — Fixed Amount Discount (P1)
1. Create a fixed-amount coupon (e.g., $5 off)
2. **Expect**: The coupon is created
3. Use it in the Customer app and verify the correct amount is deducted

### ADM-PROMO-005 — BOGO Promotion (P2)
1. Create a Buy One Get One (BOGO) promotion
2. **Expect**: The promotion is created with the correct rules
3. Apply it and verify the second item is free/discounted

### ADM-PROMO-006 — Voucher Generation (P2)
1. Look for bulk voucher generation
2. Generate multiple voucher codes
3. **Expect**: Unique codes are generated

### ADM-PROMO-007 — Deactivate Promotion (P1)
1. Deactivate an active promotion
2. **Expect**: The promotion is no longer applied to new orders

---

## 15. Settings

### ADM-SET-001 — Restaurant Information (P0)
1. Navigate to Settings
2. **Expect**: Restaurant information section showing: name, logo, description, contact info

### ADM-SET-002 — Edit Restaurant Info (P1)
1. Edit the restaurant name, logo, or description
2. Save
3. **Expect**: Changes are saved and reflected across apps

### ADM-SET-003 — Regional Settings (P1)
1. Find regional settings (address, currency, timezone)
2. Review the current configuration
3. **Expect**: Currency symbol, timezone, and address are displayed correctly

### ADM-SET-004 — Currency Configuration (P1)
1. Check the currency setting
2. **Expect**: The currency matches what is shown in orders, menus, and payments across all apps

### ADM-SET-005 — Integration Settings (P2)
1. Navigate to integrations section
2. **Expect**: Integration options like Stripe, delivery partners, etc. are visible
3. **Expect**: Connected integrations show their status

### ADM-SET-006 — Advanced Settings (P3)
1. Look for advanced/developer settings
2. Review API keys or configuration options
3. **Expect**: Settings are configurable and saved

---

## Summary — Test Count by Section

| Section | Total Tests | P0 | P1 | P2 | P3 |
|---------|:-----------:|:--:|:--:|:--:|:--:|
| Authentication | 5 | 2 | 2 | 1 | 0 |
| Dashboard | 3 | 1 | 2 | 0 | 0 |
| Orders | 15 | 4 | 6 | 4 | 1 |
| Payments | 6 | 1 | 3 | 2 | 0 |
| Menu Management | 21 | 5 | 9 | 7 | 0 |
| Staff Management | 11 | 2 | 4 | 5 | 0 |
| Schedule & Shifts | 9 | 2 | 3 | 4 | 0 |
| Floor Plan & Tables | 12 | 3 | 3 | 6 | 0 |
| Kitchen Stations | 5 | 1 | 2 | 2 | 0 |
| POS Management | 7 | 1 | 3 | 3 | 0 |
| Restaurants & Brands | 5 | 1 | 3 | 1 | 0 |
| Printers | 5 | 0 | 1 | 4 | 0 |
| Taxes & Charges | 7 | 2 | 2 | 3 | 0 |
| Promotions | 7 | 0 | 4 | 3 | 0 |
| Settings | 6 | 1 | 3 | 1 | 1 |
| **TOTAL** | **124** | **26** | **50** | **46** | **2** |
