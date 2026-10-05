<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="public/Logo_Dark_Mode.svg"/>
  <source media="(prefers-color-scheme: light)" srcset="public/Logo_Light_Mode.svg"/>
  <img src="public/Logo_Light_Mode.svg" alt="Promedia Space" height="60"/>
</picture>

# PROMEDIA SPACE

**Version 1.4.0**

*An internal web tool for monitoring warehouse utilization, staging capacity, inbound and outbound logistics<br/>and a integrated Control Center for final inspections*

*Built by [Engin Sarak](https://github.com/EnginSarak)*

![Version](https://img.shields.io/badge/version-1.4.0-blue)
![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.110-009688?logo=fastapi&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?logo=mongodb&logoColor=white)
![Vercel](https://img.shields.io/badge/Deployed%20on-Vercel-000000?logo=vercel&logoColor=white)
![License](https://img.shields.io/badge/license-Proprietary-red)
![Status](https://img.shields.io/badge/status-Active-brightgreen)

</div>

---

## Table of Contents

- [Overview](#overview)
- [Install it as an app](#install-it-as-an-app)
- [Getting Started](#getting-started)
- [Features](#features)
  - [Dashboard](#dashboard)
  - [Pallet Staging Capacity](#pallet-staging-capacity)
  - [Floor Plan](#floor-plan)
  - [Forecast](#forecast)
  - [Outbound](#outbound)
  - [Priorities](#priorities)
  - [Problem Flags](#problem-flags)
  - [Task List](#task-list)
  - [Inbound and Bin Usage](#inbound-and-bin-usage)
  - [Maintenance Panel](#maintenance-panel)
  - [Control Center](#control-center)
  - [Issues Center](#issues-center)
  - [Monitor Mode](#monitor-mode)
  - [Warehouse Operator](#warehouse-operator)
  - [On the Phone](#on-the-phone)
  - [Theming](#theming)
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [Access Control](#access-control)
- [Changelog](#changelog)

---

## Overview

PROMEDIA SPACE is a closed-source, access-controlled internal web application built for Promedia's logistics operations. It shows how full the pallet staging area is right now. Every staging slot in the warehouse is a slot on screen, so anyone can see at a glance which orders are standing there, what still has to be picked and which deliveries are on their way.

Everyone sees the same live picture, and every change shows up on all screens within seconds. With PROMEDIA SPACE the team can:

- see the staging area live as a 3D model, together with every outbound order and inbound delivery
- preview any future day with Forecast
- create and edit orders, tick off the warehouse steps, set pickup dates and delete rows
- assign priorities and flag orders as problems
- work through tasks with checklists in the Task List
- log deliveries and mark them as stored
- manage capacity, bin counts and access tokens
- check goods against the delivery note in the Control Center
- keep unresolved cases with photos in the Issues Center
- run a board on the TV screen in the warehouse with Monitor Mode

What each person sees depends on their role, see [Access Control](#access-control).

---

## Preview

<div align="center">
  <img src="public/preview.png" alt="Promedia Space Dashboard Preview" width="100%"/>
</div>

---

## Install it as an app

PROMEDIA SPACE runs in the browser, but it can also be installed as a standalone app on any device.

| Device | How |
|---|---|
| **iPhone / iPad** | Open the site in Safari, tap **Share**, then **Add to Home Screen** |
| **Android** | Open it in Chrome, tap the **⋮** menu, then **Install app**. Chrome often offers this by itself |
| **Windows / macOS** | In Chrome or Edge, click the install icon at the right-hand end of the address bar. In Edge it also sits under **⋯ → Apps → Install this site as an app** |

---

## Getting Started

PROMEDIA SPACE runs in Chrome, Edge or Safari. Open it, enter your personal access token and press **Enter**. The browser remembers the token, so the next visit opens the dashboard straight away.

<p align="center">
  <img src="public/screenshots/login.webp" alt="Login screen" width="48%"/>
</p>

> [!IMPORTANT]
> The token is your key to the app. Don't share it. If someone else may know it, generate a new one in the [Users](#users) tab and delete the old one.

---

## Features

### Dashboard

The first screen after login. It updates itself, no reload needed.

<p align="center">
  <img src="public/screenshots/dashboard.webp" alt="Dashboard with numbered elements" width="100%"/>
</p>

| # | Element | # | Element |
|---|---|---|---|
| **1** | Theme: system, light or dark | **6** | Logout |
| **2** | Task List with open tasks | **7** | Pallet Staging Capacity |
| **3** | Control Center | **8** | Floor Plan, the 3D model of the staging area |
| **4** | Issues Center | **9** | Switch to 2D, and Forecast |
| **5** | Maintenance | **10** | Outbound: every active order with its status |

The **Inbound** and **Bin Usage** lists sit below the Floor Plan.

---

### Pallet Staging Capacity

<p align="center">
  <img src="public/screenshots/capacity.webp" alt="Pallet Staging Capacity bar" width="100%"/>
</p>

The big number counts the pallets standing on the floor right now, out of all staging slots.

| Segment | Meaning |
|---|---|
| **picked** | Picked outbound orders on the floor |
| **inbound** | Arrived deliveries waiting to be stored |
| **pending pick** | Logged orders not picked yet |
| **expected inbound** | Deliveries due tomorrow |
| **free** | Unclaimed slots |

The first marker above the bar shows the current fill level, the pulsing second one where the floor ends up once everything open has arrived or been picked. If that goes over capacity, a warning shows how many slots are missing.

---

### Floor Plan

On a computer the Floor Plan opens as a 3D model of the staging area. Every box is a pallet.

<p align="center">
  <img src="public/screenshots/floor-3d.webp" alt="Floor Plan in 3D" width="100%"/>
</p>

| What you see | Meaning |
|---|---|
| Color of a pallet | The shipment. Pallets leaving on the same truck share a color and stand together |
| Flag | Destination country |
| Solid pallet | Picked, standing on the floor |
| See-through, pulsing pallet | Reserved: an order still to be picked or a delivery expected tomorrow |
| White INBOUND sign | Arrived delivery waiting to be stored |
| Grey pad | Free slot |

Picked orders and arrived deliveries keep their slots until they are picked up or stored, always with all of their pallets. Pending picks and expected deliveries fill the free slots and are the first to go when space runs out.

<p align="center">
  <img src="public/screenshots/floor-3d-rotated.webp" alt="Rotated 3D view" width="48%"/>
  <img src="public/screenshots/floor-3d-zoom.webp" alt="Zoomed 3D view" width="48%"/>
</p>

Drag to rotate, scroll or use the slider to zoom. The blue button in the control pad, or `P`, starts and stops the auto-rotation.

Hovering a pallet shows the order data, clicking it opens the full order card with notes. Every value in the card copies with a click. The pickup date is green when confirmed, orange when estimated and red for ASAP or overdue.

<p align="center">
  <img src="public/screenshots/hover-card.webp" alt="Hover card on a pallet" width="80%"/>
</p>

<p align="center">
  <img src="public/screenshots/order-card.webp" alt="Order card" width="50%"/>
</p>

**2D view.** The **2D** button shows the floor as a flat grid. The tile fill is the country, the thick border the shipment, and the label a customer code plus pallet number (`CA · 3` is the third pallet of Customer A). Striped tiles are pending picks. Corner marks show progress: `✓` Controlled, `✓✓` Ordered, `★` Confirmed.

<p align="center">
  <img src="public/screenshots/floor-2d.webp" alt="Floor Plan in 2D" width="100%"/>
</p>

---

### Forecast

**Forecast** previews the floor on any future day, in 3D and 2D. It is the quickest way to check whether a new order still fits. Pick a day in the calendar, step through days with the arrows next to the date, and return with **Back to Live**. Public holidays in NRW are marked red and named under the banner.

<p align="center">
  <img src="public/screenshots/forecast-calendar.webp" alt="Forecast calendar" width="44%"/>
</p>

<p align="center">
  <img src="public/screenshots/holiday.webp" alt="Holiday notice" width="100%"/>
</p>

An order stays on the floor up to and including its pickup day. A delivery appears on its arrival day and counts as stored the day after.

<p align="center">
  <img src="public/screenshots/forecast.webp" alt="Forecast in 3D" width="100%"/>
</p>

---

### Outbound

The Outbound card lists every active order, sorted by priority, then ASAP, then pickup date.

<p align="center">
  <img src="public/screenshots/outbound.webp" alt="Outbound list" width="60%"/>
</p>

Maintainers see two extra marks: a **red check** when the pick list is printed and a **yellow triangle** when the order has an open task. A row pulsing yellow has an upcoming pickup but no printed pick list yet.

| Badge | Meaning |
|---|---|
| **Pending Pick** | Logged, not picked yet |
| **Picked** | On the floor |
| **Controlled** | Checked by the warehouse |
| **Ordered** | Forwarder booked |
| **Confirmed** | Pickup confirmed |

A dark **P1**, **P2** and so on marks a [priority](#priorities), a red **PROBLEM** a [problem flag](#problem-flags).

**Groupage.** Orders for the same customer with the same forwarder and delivery date travel on one truck, up to 33 pallets. PROMEDIA SPACE groups them automatically: one color on the floor and one row in the list. Clicking that row opens the **Groupage** table with every order of the shipment.

<p align="center">
  <img src="public/screenshots/groupage.webp" alt="Groupage table" width="80%"/>
</p>

**Full lists.** The icons in the card header open all orders (`E`) and the **Outbound Overview** with every column (`T`), CSV export and a 365-day **History**.

<p align="center">
  <img src="public/screenshots/outbound-overview.webp" alt="Outbound Overview" width="100%"/>
</p>

---

### Priorities

Right-click an order in the Outbound list (long-press on touch), choose a free priority number and confirm.

<p align="center">
  <img src="public/screenshots/priority-menu.webp" alt="Priority menu" width="50%"/>
</p>

All orders of a groupage share one priority. Once an order is set to **Ordered**, picked up or deleted, its priority disappears and every number behind it moves up by one. A number only moves up once no order holds it anymore, so it never shows up twice.

<p align="center">
  <img src="public/screenshots/priority-before.webp" alt="Before: three orders with a priority" width="48%"/>
  <img src="public/screenshots/priority-after.webp" alt="After: the priorities moved up" width="48%"/>
</p>

---

### Problem Flags

Maintainers right-click an order's status badge, choose **PROBLEM** and enter a reason. The row turns grey, the badge turns red and the reason appears at the top of the order card. **Clear problem** in the same menu removes it. The flag does not change the pick order.

<p align="center">
  <img src="public/screenshots/problem-menu.webp" alt="Problem menu on the status badge" width="48%"/>
  <img src="public/screenshots/problem-dialog.webp" alt="Problem reason dialog" width="48%"/>
</p>

<p align="center">
  <img src="public/screenshots/problem-card.webp" alt="Order card with problem reason" width="50%"/>
</p>

---

### Task List

Checklists for customs, labeling and follow-ups, so nothing gets forgotten. Maintainers only. The red number on **Tasks** shows how many are open.

<p align="center">
  <img src="public/screenshots/tasks.webp" alt="Task List" width="42%"/>
  <img src="public/screenshots/tasks-new.webp" alt="New EX1 task" width="42%"/>
</p>

Each task has a type (**EX1** for customs, otherwise **General**), an optional link to an order or delivery, a progress bar and a checklist of up to eight steps. Steps can be renamed, added, removed and reordered by drag. **Mark done** moves a task to **Completed**.

Saving an order creates some tasks automatically:

<p align="center">
  <img src="public/screenshots/ex1-dialog.webp" alt="Export declaration prompt" width="50%"/>
</p>

| Trigger | Task |
|---|---|
| Destination outside the EU | Asks whether an export declaration is needed. Above 1,000 € customs value or 1,000 kg gross weight it creates an EX1 checklist with six steps |
| Saudi Arabia | Asks about air freight with pumps on board and creates a UN 3481 / SAG-06 labeling task |
| Brazil | ISPM 15: IPPC marking on every wooden pallet |
| Certain customers | Customer-specific reminders, such as booking a delivery slot |

A linked order shows the yellow triangle until its task is done.

---

### Inbound and Bin Usage

<p align="center">
  <img src="public/screenshots/inbound.webp" alt="Inbound list" width="100%"/>
</p>

**Inbound** lists known deliveries: **EXPECTED** with a date, or **ARRIVED** once they occupy slots. On the arrival day they already get their slots from the morning on. Right-click (long-press) and **Mark as Stored** removes a delivery once it has been put away.

<p align="center">
  <img src="public/screenshots/stored-menu.webp" alt="Mark as Stored menu" width="60%"/>
</p>

<p align="center">
  <img src="public/screenshots/bin-usage.webp" alt="Bin Usage card" width="100%"/>
</p>

**Bin Usage** shows today's occupied bins, the monthly average and the current week. Clicking the heading opens a yearly overview.

---

### Maintenance Panel

`M` or **Maintenance** opens the data tables, for Maintainers and, restricted, Customer Service. Four tabs: **Outbound**, **Inbound**, **Config** and **Users**. In fullscreen the table zooms from 50 to 100 percent.

<p align="center">
  <img src="public/screenshots/maintenance.webp" alt="Maintenance Panel in fullscreen" width="100%"/>
</p>

#### Outbound orders

**Add Row** (or `N`) adds an order. Rows save themselves as soon as they have a customer and a delivery date; incomplete rows wait so half-typed orders never reach the dashboard. **Undo** reverts up to ten steps, including a delete.

<p align="center">
  <img src="public/screenshots/new-row.webp" alt="A new order row" width="100%"/>
</p>

<p align="center">
  <img src="public/screenshots/country.webp" alt="Country suggestions" width="40%"/>
</p>

| Field | Content |
|---|---|
| **Customer** | Customer name |
| **Date** | Day the order was announced, not the delivery date |
| **Pick No.** / **SORD No.** | Pick list and order numbers, several per cell |
| **Country** | Two-letter destination code, with suggestions |
| **Delivered by** | Requested delivery date, or ASAP |
| **Forwarder** | Forwarder |
| **Colli** | Number plus `PAL` or `BOX`. Only PAL orders take slots on the floor |
| **Notes** | Anything the warehouse should know |

The checkboxes follow the order's path and save instantly:

| Checkbox | Effect |
|---|---|
| **Printed** | Pick list printed, red check in the Outbound list |
| **Picked** | On the floor. PAL orders first confirm the pallet count |
| **Control** | Goods checked, also set by the [Control Center](#control-center) |
| **Ordered** | Forwarder booked, the priority is released |
| **Confirmed** | Pickup confirmed. Asks for a pickup date if there is none |
| **Picked Up** | Goods gone, the row moves to History |

<p align="center">
  <img src="public/screenshots/pallet-confirm.webp" alt="Pallet count check on Picked" width="48%"/>
  <img src="public/screenshots/pickup-required.webp" alt="Pickup date required on Confirmed" width="48%"/>
</p>

**Pickup date.** PROMEDIA SPACE suggests it from country, order date and delivery date. A blue dot means the date still follows that suggestion. A date picked by hand stays as set, and a confirmed date is never changed automatically.

<p align="center">
  <img src="public/screenshots/pickup-dialog.webp" alt="Pickup date picker" width="36%"/>
</p>

**ASAP.** Right-click **Delivered by** and choose **Set ASAP**. The pickup turns ASAP too until the order is confirmed.

<p align="center">
  <img src="public/screenshots/asap-menu.webp" alt="ASAP menu" width="44%"/>
</p>

**Shipments.** Right-clicking a customer name detaches an order from its shipment, reattaches it, or links it by hand to another order, showing the free pallets left on the truck. A colored line on the left joins the rows of one shipment.

<p align="center">
  <img src="public/screenshots/shipment-menu.webp" alt="Shipment menu on the customer name" width="44%"/>
</p>

**History** keeps picked-up orders for 365 days. The picked-up date starts orange and turns green once confirmed by hand. The blue arrow brings an order back into the table.

<p align="center">
  <img src="public/screenshots/history.webp" alt="History" width="100%"/>
</p>

<p align="center">
  <img src="public/screenshots/history-date.webp" alt="Confirming the picked-up date" width="34%"/>
</p>

**Customer Service** can add rows, edit text fields and set priorities. Checkboxes, pickup dates and deleting are reserved for Maintainers.

#### Inbound deliveries

Supplier, pallet count and expected date, then **Add**. Today or earlier counts as **ARRIVED**, later as **PENDING**.

<p align="center">
  <img src="public/screenshots/maintenance-inbound.webp" alt="Inbound tab" width="90%"/>
</p>

#### Config

Maintainers only: number of staging slots, total bins, and the daily bin usage log, including missed days.

<p align="center">
  <img src="public/screenshots/config.webp" alt="Config tab" width="100%"/>
</p>

#### Users

Maintainers only. There are no passwords: every access is a token with a role. **Generate Token** creates one and copies it to the clipboard. Deleting a token locks that person out immediately.

<p align="center">
  <img src="public/screenshots/users.webp" alt="Users tab" width="100%"/>
</p>

---

### Control Center

The last check before goods leave: does the pallet match the delivery note in article, batch and quantity? The batch is what a recall is traced by.

The Control Center works with two devices on the same token, no pairing needed. The PC loads delivery notes exported from Business Central as XML (button or drag and drop) and forwards scans. The phone does the counting. A note dropped in the office is on every phone in the warehouse seconds later.

<p align="center">
  <img src="public/screenshots/control-desk.webp" alt="Control Center on the PC" width="70%"/>
</p>

<p align="center">
  <img src="public/screenshots/control-phone.webp" alt="Control Center on the phone: start page, inspection and count sheet" width="100%"/>
</p>

On the phone, each scan of a lot number finds its line on the delivery note. Quantities are counted, not scanned: pick a unit (pallet, layer, carton or single) and type the amount, with arithmetic such as `12x8x3-1`. **Cashier mode** books one unit per scan. Pack sizes are learned per article and shared across devices. Every booking gives a tone and a flash at the screen edge.

<p align="center">
  <img src="public/screenshots/control-summary.webp" alt="Inspection summary on the phone" width="30%"/>
</p>

Filing an inspection asks which outbound rows it belongs to, with matching rows preselected. A complete inspection ticks **Printed**, **Picked** and **Control**, an incomplete one only **Printed** and **Picked**. The order card then links to the final inspection, and an ⓘ next to the customer opens the shipment details from the delivery notes: packages, weights, destination and customer address.

---

### Issues Center

Unresolved problems and complaints with photos, visible to everyone so they don't get forgotten. Maintainers create, edit and delete cases.

<p align="center">
  <img src="public/screenshots/issues.webp" alt="Issues Center" width="100%"/>
</p>

A case has a title, formatted text and up to 20 photos, compressed in the browser before upload. There is no "done" button: a solved case is deleted. Cases older than two years are removed automatically.

<p align="center">
  <img src="public/screenshots/issues-editor.webp" alt="New case editor" width="48%"/>
  <img src="public/screenshots/issues-case.webp" alt="An open case" width="48%"/>
</p>

---

### Monitor Mode

A fullscreen board for the TV screen in the warehouse hall, for the **Warehouse Operator** role on screens from 1024 pixels wide. **Monitor** in the header switches it on, and it stays on for that token after reloads.

<p align="center">
  <img src="public/screenshots/monitor-outbound.webp" alt="Monitor Mode: outbound board" width="100%"/>
</p>

The **outbound board** lists every open order in pick order. Orders of one groupage stand together, share their P badge and are joined by a bridge, so it is clear from across the hall that they leave on one truck.

<p align="center">
  <img src="public/screenshots/monitor-inbound.webp" alt="Monitor Mode: inbound board" width="100%"/>
</p>

The **inbound board** shows supplier, pallets and status. The two boards alternate. Each page holds 14 rows, longer lists turn pages every 10 seconds.

<p align="center">
  <img src="public/screenshots/monitor-header.webp" alt="Header shown over the board" width="100%"/>
</p>

The header and mouse pointer hide themselves and come back for three seconds on any movement. `F5` toggles browser fullscreen.

---

### Warehouse Operator

The role for the warehouse floor: a read-only dashboard plus the actions that belong to the hall.

<p align="center">
  <img src="public/screenshots/operator-header.webp" alt="Warehouse Operator header" width="85%"/>
</p>

**EN / DE** switches the interface language, **Monitor** starts [Monitor Mode](#monitor-mode), and the Control Center is available. A right-click (long-press) on an order offers **Mark as Picked Up**, which moves the order, or the whole groupage, to History and frees its slots. Arrived deliveries are marked with **Mark as Stored**.

<p align="center">
  <img src="public/screenshots/operator-pickup.webp" alt="Mark as Picked Up menu" width="60%"/>
</p>

---

### On the Phone

Installed on the home screen, PROMEDIA SPACE opens full screen like an app. Safari shows a hint for it.

<p align="center">
  <img src="public/screenshots/phone-install.webp" alt="Install hint in Safari and the app opened from the home screen" width="66%"/>
</p>

The layout is stacked, the header shows icons only, and a long-press replaces the right-click everywhere. The Control Center is built for the phone.

<p align="center">
  <img src="public/screenshots/phone.webp" alt="3D floor, order card and Maintenance on the phone" width="100%"/>
</p>

---

### Theming

System, light or dark, switchable in the header. The choice is remembered and the 3D hall follows it.

<p align="center">
  <img src="public/screenshots/header.webp" alt="Header with theme switch" width="100%"/>
</p>

<p align="center">
  <img src="public/screenshots/floor-3d-dark.webp" alt="3D Floor Plan in dark mode" width="80%"/>
</p>

---

## Keyboard Shortcuts

Every shortcut is ignored while a text field has focus, and while a dialog is
handling the key itself.

### Dashboard

| Key | Action |
| --- | --- |
| `E` or `Enter` | Extended outbound view |
| `T` | Outbound table |
| `P` | Pause or resume the auto-rotation of the 3D warehouse view |
| `M` | Maintenance panel |
| `C` | Control Center |
| `I` | Issues Center |
| `F5` | Fullscreen, monitor mode only |
| `Esc` | Close the panel that is open |

### Maintenance Panel

| Key | Action |
| --- | --- |
| `N` | New outbound row |
| `Esc` | Close |

### Control Center, desk

| Key | Action |
| --- | --- |
| `S` or `Enter` | Start scanning |
| `U` | Add XML documents |
| `Esc` | Back. Closes the log, else stops scanning, else leaves the desk |

### Control Center, device

| Key | Action |
| --- | --- |
| `Esc` | One step back |

### Issues Center

| Key | Action |
| --- | --- |
| `←` `→` | Previous or next image |

---

## Access Control

PROMEDIA SPACE uses a token-based access model. There are no user accounts, passwords or registration. Tokens are issued by a Maintainer from the [Users](#users) tab.

| Role | Access |
|---|---|
| **Viewer** | Dashboard and Issues Center, read-only |
| **Customer Service** | Dashboard, priorities, Issues Center to read, and the Maintenance Panel with restrictions on the Outbound tab. No Config, Users, Task List or Control Center |
| **Maintainer** | Everything: full Maintenance Panel, Task List, problem flags, Control Center, and write access in the Issues Center |
| **Warehouse Operator** | Dashboard (read-only), Monitor Mode, Control Center, Issues Center to read, the EN / DE language switch, marking orders as picked up and deliveries as stored |

---

## Changelog

### 1.4.0

- Inbounds can now be marked as a problem, just like outbounds: right click the status, or long press on touch devices. The problem box offers Discrepancy (orange), Not arrived (violet) or a free reason, and a free text field is always available. A discrepancy can carry an optional pallet difference, for example -2.
- Only arrived inbounds can be marked as a problem. An inbound that already has a problem label can still be changed or cleared.
- An inbound marked as Not arrived no longer appears on the floor plan and does not count anywhere. For a discrepancy, the floor shows the delivered number of pallets, that is the expected pallets plus the difference.
- An inbound dated today now counts as arrived from 7:00 hall time. Before that it shows as expected. The switch happens on its own while the page is open.
- Problem outbounds and inbounds can be moved to the Issues Center with one click, where photos and more details can be added. The case opens directly from the notice, and its card shows whether it is an outbound or an inbound together with the problem type. Customer and supplier names in these cases always follow the current name.
- Inbounds marked as stored are now kept in a history for 365 days, including any problem, with CSV export. Maintenance can restore or delete history entries.
- Problem badges in the inbound list are right-aligned, and pallet counts line up underneath each other.

### 1.3.1

- Minor bug fixes

### 1.3.0

- New customer colors. The first ten customers on the floor get ten clearly different hues (blue, orange, magenta, gold, violet, red, sky blue, lime, jade and brown), with only one pink among them. Lighter and darker shades are only used when more customers are on the floor, and they never stand next to each other.

### 1.2.2

- Marking a customer as picked up now takes effect immediately. The row slides out of the outbound list and its pallets leave the floor plan right away while saving continues in the background. If saving fails, the row comes back and a notice says it was not marked as picked up.
- All orders of a customer are now saved in a single request instead of one after another, so the pickup reaches the server noticeably faster.

### 1.2.1

- An invalid Colli value such as 4-5 PAL can no longer be saved, even when a correct value was entered first and changed afterwards. Confirming the pallet count when ticking Picked now sets Colli to that exact number, and the server rejects any Colli change that is not a whole number with PAL or BOX.
- Every row you change in the outbound overview, including ticking a checkbox, must be complete before you can leave Maintenance.

### 1.2.0

- The outbound overview in Maintenance now checks every new or changed row before you leave it: Colli must be a fixed number with PAL or BOX (for example 12 PAL or 1 BOX), Forwarder must be filled in, and either Delivered by or Pickup date must be set. While you are filling in rows nothing interrupts you. Only when you save, close Maintenance or switch tabs does a short notice list what is still missing, and the affected fields are marked until they are fixed.

### 1.1.12

- The 3D floor plan tries many more arrangements before it accepts a free slot inside a block.

### 1.1.11

- In the 3D floor plan a customer's pallets always stand directly next to each other. A pallet no longer ends up on its own between other customers.

### 1.1.10

- The 3D floor plan no longer places customers with similar colors next to each other.
- A customer that needs more than one block no longer leaves single stray pallets elsewhere and continues in the block next to it instead of across the hall.

### 1.1.9

- The 3D floor plan no longer leaves empty slots inside a block. Smaller shipments move up to fill a gap, and a customer's pallets still stay together.

### 1.1.8

- An arrived delivery that no longer fits completely on the floor is now shown translucent and pulsing on the free slots instead of being hidden, so a full hall is visible at a glance. Picked orders keep their place.

### 1.1.7

- Pallets of the same customer now stay together in the 3D floor plan instead of being split across an aisle.

### 1.1.6

- Minor bug fixes.

### 1.1.5

- Priority badges now show as P1, P2 and so on right next to the status badge instead of alternating with it.

### 1.1.4

- Minor bug fixes and an improved floor plan color scheme.

### 1.1.3

- Outbound rows with a filed Control Center inspection now show an ⓘ next to the customer name in the order popup, the groupage popup and the extended outbound view. It opens the shipment info from the delivery notes: pallets, net and gross weight, every delivery note, destination and customer address.
- Every value in the shipment info is copied to the clipboard with a click.

### 1.1.2

- Minor fixes.

### 1.1.1

- Priority levels are no longer capped at 3, any number can be assigned.

### 1.1.0

- Minor bug fixes.
