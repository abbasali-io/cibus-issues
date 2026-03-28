---
layout: default
title: KDS App Tests
parent: Testing Manuals
nav_order: 4
---

# KDS App — Manual Test Plan

> **App URL**: `https://kds.cibus.app`
> **Role Required**: Kitchen Staff
> **Estimated Time**: 1.5–2 hours (full suite)

---

## Table of Contents

1. [Authentication & Login](#1-authentication--login)
2. [Homepage (Station Selection)](#2-homepage-station-selection)
3. [Station Queue (Ticket Management)](#3-station-queue-ticket-management)
4. [Ticket Detail & Item Management](#4-ticket-detail--item-management)
5. [All Stations View](#5-all-stations-view)
6. [Ticket History & Analytics](#6-ticket-history--analytics)
7. [Settings & Preferences](#7-settings--preferences)
8. [Screen Lock](#8-screen-lock)
9. [Sound & Notifications](#9-sound--notifications)
10. [Timer & Urgency](#10-timer--urgency)

---

## 1. Authentication & Login

### KDS-AUTH-001 — Successful Login (P0)
1. Go to `https://kds.cibus.app`
2. You should see the login page with the ChefHat branding
3. Enter valid kitchen staff email and password
4. Click "Sign In"
5. **Expect**: You are redirected to the homepage (station selection)

### KDS-AUTH-002 — Invalid Credentials (P1)
1. Enter incorrect email or password
2. Click "Sign In"
3. **Expect**: An error message appears
4. **Expect**: You remain on the login page

### KDS-AUTH-003 — Empty Fields (P2)
1. Leave email and/or password empty
2. Click "Sign In"
3. **Expect**: Validation messages appear for required fields

### KDS-AUTH-004 — Loading State (P2)
1. Click "Sign In" with valid credentials
2. **Expect**: A loading spinner appears while authenticating
3. **Expect**: The button is disabled during loading

---

## 2. Homepage (Station Selection)

### KDS-HOME-001 — Homepage Loads (P0)
1. After login, the homepage loads
2. **Expect**: A grid of all kitchen stations is displayed
3. **Expect**: Each station card shows:
   - Station icon (type-specific emoji)
   - Station name
   - Station type badge (e.g., "PREP", "GRILL", "DESSERT", "BAR")
   - Active ticket count badge

### KDS-HOME-002 — Station Ticket Counts (P0)
1. Review each station card
2. **Expect**: Active ticket count is displayed on each card
3. **Expect**: Status breakdown dots show:
   - Yellow dot = pending count
   - Blue dot = in-progress count
   - Green dot = ready count

### KDS-HOME-003 — Rush Indicator (P1)
1. If a station has high-priority tickets
2. **Expect**: A red "Rush" badge appears on the station card
3. **Expect**: The card may have a pulsing animation

### KDS-HOME-004 — Assigned Staff Avatars (P2)
1. Check station cards for staff assignment info
2. **Expect**: First 3 assigned staff avatars are shown
3. **Expect**: If more than 3, a "+N" indicator shows the overflow count

### KDS-HOME-005 — No Tickets State (P1)
1. Find a station with no active tickets
2. **Expect**: The station card appears muted/dimmed
3. **Expect**: No ticket breakdown is shown (just the station info)

### KDS-HOME-006 — Navigate to Station (P0)
1. Click on a station card
2. **Expect**: You are navigated to that station's ticket queue (`/station/:stationId`)

### KDS-HOME-007 — Bottom Navigation Buttons (P0)
1. Check the bottom of the homepage for navigation buttons
2. **Expect**: Three buttons:
   - "All Stations" → navigates to `/all-stations`
   - "History" → navigates to `/history`
   - "Settings" → navigates to `/settings`
3. Click each and verify navigation

### KDS-HOME-008 — Loading State (P2)
1. Refresh the page
2. **Expect**: A loading spinner with "Loading stations" message appears briefly
3. **Expect**: Then station cards render

### KDS-HOME-009 — Error State (P2)
1. If the server is down or data fails to load
2. **Expect**: An error card appears with a retry button
3. Click retry
4. **Expect**: The data attempts to reload

### KDS-HOME-010 — Empty State (P2)
1. If no stations are configured for this restaurant
2. **Expect**: A message like "No stations configured" appears

---

## 3. Station Queue (Ticket Management)

### KDS-QUEUE-001 — Station Queue Loads (P0)
1. Navigate to a station page (`/station/:stationId`)
2. **Expect**: A 3-column Kanban layout:
   - **Pending** (yellow) — tickets not yet claimed
   - **In Progress** (blue) — tickets being prepared
   - **Ready** (green) — tickets ready to serve

### KDS-QUEUE-002 — Station Header (P1)
1. Check the station page header
2. **Expect**: Shows:
   - Station icon and name
   - Active ticket count
   - Refresh button with "Updated Xs ago" indicator
   - Sound toggle button

### KDS-QUEUE-003 — Pending Column (P0)
1. Review the Pending column
2. **Expect**: All unclaimed tickets are listed
3. **Expect**: A count badge shows the number of pending tickets
4. **Expect**: Each ticket card shows CLAIM button

### KDS-QUEUE-004 — Claim Ticket (P0)
1. Click the "CLAIM" button on a pending ticket
2. **Expect**: The ticket moves from Pending to In Progress column
3. **Expect**: The move happens immediately (optimistic update)

### KDS-QUEUE-005 — In Progress Column (P0)
1. Review the In Progress column
2. **Expect**: Claimed tickets are listed here
3. **Expect**: Each ticket card shows BUMP button
4. **Expect**: A count badge shows the number of in-progress tickets

### KDS-QUEUE-006 — Bump Ticket (P0)
1. Click the "BUMP" button on an in-progress ticket
2. **Expect**: The ticket moves from In Progress to Ready column
3. **Expect**: The move happens immediately

### KDS-QUEUE-007 — Ready Column (P0)
1. Review the Ready column
2. **Expect**: Ready-to-serve tickets are listed here
3. **Expect**: Each ticket card shows SERVE button
4. **Expect**: A count badge shows the number of ready tickets

### KDS-QUEUE-008 — Serve Ticket (P0)
1. Click the "SERVE" button on a ready ticket
2. **Expect**: The ticket is completed and removed from the board
3. **Expect**: The ticket is now in the History page

### KDS-QUEUE-009 — Full Ticket Workflow (P0)
1. Start with a pending ticket
2. CLAIM it → moves to In Progress
3. BUMP it → moves to Ready
4. SERVE it → removed from board
5. **Expect**: Each step works smoothly
6. **Expect**: Check History — the ticket should appear as completed

### KDS-QUEUE-010 — Ticket Card Display (P0)
1. Review the information on each ticket card
2. **Expect**: Each card shows:
   - Ticket number (bold)
   - Order type icon (dine-in, takeaway, etc.)
   - Table number or customer name
   - Elapsed time (in large text)
   - Item progress (e.g., "3/5")
   - Abbreviated item list with quantities
   - Allergy badge (⚠️ icon) if items have allergy warnings
   - Priority indicator (star/crown) if set

### KDS-QUEUE-011 — Empty Columns (P1)
1. If a column has no tickets
2. **Expect**: An empty state message with emoji is displayed
3. **Expect**: The column doesn't collapse

### KDS-QUEUE-012 — Manual Refresh (P1)
1. Click the refresh button in the header
2. **Expect**: The data refreshes
3. **Expect**: The "Updated Xs ago" indicator resets

### KDS-QUEUE-013 — Real-time Ticket Arrival (P0)
1. Keep the station queue open
2. From the POS or Customer app, submit an order that routes to this station
3. **Expect**: The new ticket appears in the Pending column automatically
4. **Expect**: No manual refresh needed

---

## 4. Ticket Detail & Item Management

### KDS-DETAIL-001 — Open Ticket Detail (P0)
1. Click on a ticket card (not the action button)
2. **Expect**: A full-screen modal opens showing:
   - Ticket number (large)
   - Order number
   - Order type and table/customer info
   - Started time and elapsed minutes
   - Priority display (if set)

### KDS-DETAIL-002 — Item List in Detail (P0)
1. In the ticket detail modal, review the items list
2. **Expect**: Each item shows:
   - Item name and quantity
   - Special instructions/notes (highlighted)
   - Allergy warnings (emphasized)
   - Completion status (checkbox or toggle)

### KDS-DETAIL-003 — Toggle Item Completion (P1)
1. Click on an item's status toggle/checkbox in the detail modal
2. **Expect**: The item is marked as completed
3. **Expect**: The item completion percentage updates (e.g., "3/5" → "4/5")  
4. Click again to unmark
5. **Expect**: Status reverts

### KDS-DETAIL-004 — Action Buttons in Modal (P0)
1. In the ticket detail modal, check the action buttons
2. **Expect**: The primary action button matches the ticket's current status:
   - Pending → "CLAIM" (blue)
   - In Progress → "BUMP" (green)
   - Ready → "SERVE" (neutral)
3. Click the action button
4. **Expect**: The ticket status advances and the modal updates

### KDS-DETAIL-005 — Unclaim Ticket (P1)
1. Open a ticket that is "In Progress"
2. In the detail modal, find the "UNCLAIM" button
3. Click it
4. **Expect**: A confirmation dialog appears: "Release Ticket?"
5. Confirm
6. **Expect**: The ticket moves back to Pending

### KDS-DETAIL-006 — Unbump Ticket (P1)
1. Open a ticket that is "Ready"
2. In the detail modal, find the "UNBUMP" button
3. Click it
4. **Expect**: A confirmation dialog appears: "Unbump Ticket?"
5. Confirm
6. **Expect**: The ticket moves back to In Progress

### KDS-DETAIL-007 — Confirmation Cancel (P2)
1. Click UNCLAIM or UNBUMP
2. In the confirmation dialog, click "Cancel" instead of "Confirm"
3. **Expect**: The action is cancelled
4. **Expect**: The ticket remains in its current status

### KDS-DETAIL-008 — Special Instructions Visibility (P1)
1. Open a ticket that has items with special instructions
2. **Expect**: Instructions are clearly visible and highlighted (different color or font)
3. **Expect**: Easy to read at a glance

### KDS-DETAIL-009 — Allergy Warnings (P0)
1. Open a ticket with allergy-tagged items
2. **Expect**: Allergy warnings are prominently displayed
3. **Expect**: ⚠️ icon or color-coded badge makes allergies unmissable

### KDS-DETAIL-010 — Close Modal (P1)
1. In the ticket detail modal, find the close/X button
2. Click it
3. **Expect**: The modal closes and you return to the station queue

---

## 5. All Stations View

### KDS-ALL-001 — All Stations Page Loads (P0)
1. Navigate to `/all-stations` (via homepage button or direct URL)
2. **Expect**: The page shows:
   - Header with "Kitchen Overview" title, live clock, refresh button, sound toggle
   - Status summary bar (Pending/In Progress/Ready counts across ALL stations)
   - All station columns in a horizontally scrollable layout

### KDS-ALL-002 — Status Summary Bar (P1)
1. Check the status summary bar at the top
2. **Expect**: Aggregated counts across all stations:
   - Pending: X tickets (yellow)
   - In Progress: X tickets (blue)
   - Ready: X tickets (green)
   - Total Active: X tickets

### KDS-ALL-003 — Station Columns (P0)
1. Review the station columns
2. **Expect**: Each station is a vertical column with:
   - Station header (icon + name)
   - Ticket cards in the column
3. **Expect**: You can scroll horizontally to see all stations

### KDS-ALL-004 — Quick Actions on Cards (P0)
1. On a ticket card in the all-stations view, click the action button
2. **Expect**: The action works the same as in the individual station view:
   - Pending → CLAIM
   - In Progress → BUMP
   - Ready → SERVE

### KDS-ALL-005 — Click Card for Detail (P1)
1. Click on a ticket card (not the action button)
2. **Expect**: The ticket detail modal opens with full information and all actions

### KDS-ALL-006 — Live Clock (P2)
1. Check the clock in the header
2. **Expect**: The current time is displayed in HH:MM format
3. **Expect**: The clock updates in real time

### KDS-ALL-007 — Empty State (P1)
1. If there are no active tickets across any station
2. **Expect**: A "You're all caught up! 🎉" message appears

### KDS-ALL-008 — Real-time Updates (P0)
1. Keep the all-stations view open
2. Submit a new order from POS or Customer app
3. **Expect**: New tickets appear in the appropriate station columns
4. **Expect**: Summary bar counts update

---

## 6. Ticket History & Analytics

### KDS-HIST-001 — History Page Loads (P0)
1. Navigate to `/history` (via homepage button)
2. **Expect**: A history page with:
   - Search field
   - Filter options (Station, Date)
   - Statistics summary
   - Table of completed tickets

### KDS-HIST-002 — Statistics Display (P1)
1. Review the statistics at the top
2. **Expect**: Three metrics:
   - Completed: number of tickets
   - Average Time: average cook time in minutes
   - Total Items: total items across tickets

### KDS-HIST-003 — History Table (P0)
1. Review the history table
2. **Expect**: Each row shows:
   - Ticket Number
   - Order Number
   - Station Name
   - Table / Customer Type
   - Items count
   - Created At time
   - Completed At time
   - Duration (in minutes, color-coded)
   - Order Type

### KDS-HIST-004 — Duration Color Coding (P1)
1. Check the duration column in history
2. **Expect**: Color coding:
   - Green = ≤ 5 min (fast)
   - Yellow = 5–10 min (normal)
   - Red = > 10 min (slow)

### KDS-HIST-005 — Search Tickets (P1)
1. Type a ticket or order number in the search field
2. **Expect**: The table filters to matching tickets in real time

### KDS-HIST-006 — Filter by Station (P1)
1. Use the station filter dropdown
2. Select a specific station
3. **Expect**: Only tickets from that station are shown
4. **Expect**: Statistics recalculate for the filtered data

### KDS-HIST-007 — Filter by Date (P1)
1. Use the date filter
2. Select a specific date
3. **Expect**: Only tickets from that date are shown
4. **Expect**: Statistics recalculate

### KDS-HIST-008 — Click History Row (P1)
1. Click on a row in the history table
2. **Expect**: A ticket detail modal opens (read-only)
3. **Expect**: Shows full ticket information, items, timeline
4. **Expect**: No action buttons (it's historical — read-only)

### KDS-HIST-009 — CSV Export (P1)
1. Find the CSV Export button
2. Click it
3. **Expect**: A file downloads named like `kds-history-YYYY-MM-DD.csv`
4. Open the file
5. **Expect**: Contains columns: Order #, Station, Table, Items, Created, Completed, Duration, Order Type

### KDS-HIST-010 — Combined Filters (P2)
1. Apply both station filter AND date filter AND search
2. **Expect**: Filters stack — results match ALL criteria
3. **Expect**: Statistics update to reflect the combined filtered data

---

## 7. Settings & Preferences

### KDS-SET-001 — Settings Page Loads (P0)
1. Navigate to `/settings` (via homepage button)
2. **Expect**: Settings page with multiple sections

### KDS-SET-002 — Theme Selection (P1)
1. Find the theme options: Dark, High Contrast, Light
2. Select each theme
3. **Expect**: The app appearance changes immediately
4. **Expect**: Dark = dark background, high contrast for visibility
5. **Expect**: High Contrast = maximum contrast
6. **Expect**: Light = light background

### KDS-SET-003 — Font Size (P1)
1. Find the font size slider
2. Adjust it from small to large
3. **Expect**: Text size changes across the interface

### KDS-SET-004 — Compact Mode Toggle (P2)
1. Toggle "Ticket Compact Mode"
2. **Expect**: Ticket cards show less information (compact) or more information (full)
3. Go to a station queue and verify the difference

### KDS-SET-005 — Show Completed Items Toggle (P2)
1. Toggle "Show Completed Items"
2. **Expect**: In ticket details, completed items are shown or hidden based on this setting

### KDS-SET-006 — Audio Settings (P1)
1. Toggle "Sound Enabled" on
2. Adjust the volume slider
3. Click "Test Sound"
4. **Expect**: A chime/bell plays at the set volume

### KDS-SET-007 — Sound Type (P2)
1. Change the sound type (chime, bell, alert)
2. Test each
3. **Expect**: Different sounds play for each type

### KDS-SET-008 — Timer Overdue Threshold (P1)
1. Find the overdue threshold slider (5–30 minutes)
2. Set it (e.g., 10 minutes)
3. **Expect**: Tickets older than the threshold show as overdue (red timer)

### KDS-SET-009 — Auto-Print on Serve (P2)
1. Toggle "Auto-Print on Serve"
2. Serve a ticket
3. **Expect**: A print dialog or print action is triggered automatically

### KDS-SET-010 — Auto-Refresh Interval (P2)
1. Adjust the auto-refresh interval slider (5–60 seconds)
2. **Expect**: The data refresh frequency changes accordingly

### KDS-SET-011 — Save Settings (P0)
1. Make changes to settings
2. Click "Save"
3. **Expect**: A success notification appears
4. Refresh the page
5. **Expect**: All settings persist

### KDS-SET-012 — Reset Settings (P2)
1. Click "Reset" or "Reset All Settings"
2. **Expect**: All settings revert to their defaults

### KDS-SET-013 — Notification Toggles (P2)
1. Toggle notification options:
   - Desktop Notifications
   - High Priority Order alerts
   - Overdue Item alerts
   - Rush Status alerts
2. **Expect**: Each toggle saves and responds correctly

---

## 8. Screen Lock

### KDS-LOCK-001 — Lock Screen (P1)
1. Find the lock button (in the layout header)
2. Click it
3. **Expect**: The screen locks with a large 🔒 icon
4. **Expect**: The locked staff member's info is displayed (name, role, avatar)

### KDS-LOCK-002 — Unlock with PIN (P1)
1. While locked, enter your PIN using the on-screen numpad
2. **Expect**: PIN dots appear as you type (masked)
3. Submit the PIN
4. **Expect**: The screen unlocks and you return to where you were

### KDS-LOCK-003 — Wrong PIN (P2)
1. Enter an incorrect PIN
2. **Expect**: An error message appears
3. **Expect**: The screen remains locked

### KDS-LOCK-004 — Sign Out from Lock Screen (P2)
1. While locked, find the "Sign Out" button
2. Click it
3. **Expect**: You are signed out and redirected to the login page

### KDS-LOCK-005 — PIN Keyboard Support (P2)
1. While on the lock screen, use physical keyboard number keys
2. **Expect**: Numbers are entered into the PIN field
3. Press Backspace
4. **Expect**: The last digit is removed

---

## 9. Sound & Notifications

### KDS-SOUND-001 — Sound Toggle (P1)
1. On the station queue page, find the sound toggle button
2. Toggle sound ON (button should be blue/highlighted)
3. **Expect**: When new tickets arrive, a sound plays

### KDS-SOUND-002 — Sound OFF (P1)
1. Toggle sound OFF (button should be gray)
2. When new tickets arrive
3. **Expect**: No sound plays

### KDS-SOUND-003 — Sound Across Pages (P2)
1. Enable sound on the All Stations page
2. When new tickets arrive on any station
3. **Expect**: Sound plays for new arrivals

---

## 10. Timer & Urgency

### KDS-TIME-001 — Elapsed Time Display (P0)
1. On the station queue, check ticket cards for elapsed time
2. **Expect**: Each ticket shows time in minutes since creation

### KDS-TIME-002 — Timer Color Coding (P0)
1. Observe ticket timers across different ages
2. **Expect**: Color coding based on freshness:
   - Green = under warning threshold (OK)
   - Yellow = 50–80% of threshold (warning)
   - Orange = 80%+ of threshold (alert)
   - Red = exceeded threshold (critical, may pulse)

### KDS-TIME-003 — Critical Timer Pulse (P1)
1. Find a ticket that has exceeded the overdue threshold
2. **Expect**: The timer pulses/blinks in red
3. **Expect**: Very visible — designed to draw attention

### KDS-TIME-004 — Priority Indicators (P1)
1. Find tickets with priority markers
2. **Expect**: High-priority tickets show a star/crown icon
3. **Expect**: Priority badge is color-coded by level

---

## Summary — Test Count by Section

| Section | Total Tests | P0 | P1 | P2 | P3 |
|---------|:-----------:|:--:|:--:|:--:|:--:|
| Authentication | 4 | 1 | 1 | 2 | 0 |
| Homepage | 10 | 3 | 3 | 4 | 0 |
| Station Queue | 13 | 8 | 3 | 2 | 0 |
| Ticket Detail | 10 | 3 | 5 | 2 | 0 |
| All Stations | 8 | 4 | 2 | 2 | 0 |
| History & Analytics | 10 | 2 | 6 | 2 | 0 |
| Settings | 13 | 2 | 4 | 7 | 0 |
| Screen Lock | 5 | 0 | 2 | 3 | 0 |
| Sound & Notifications | 3 | 0 | 2 | 1 | 0 |
| Timer & Urgency | 4 | 2 | 2 | 0 | 0 |
| **TOTAL** | **80** | **25** | **30** | **25** | **0** |
