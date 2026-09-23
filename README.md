<div align="center">

<img src="public/Logo_Light_Mode.svg#gh-light-mode-only" alt="Promedia Space" height="60"/>
<img src="public/Logo_Dark_Mode.svg#gh-dark-mode-only" alt="Promedia Space" height="60"/>

# PROMEDIA SPACE

**Version 1.0.0**

*An internal web tool for monitoring warehouse utilization, staging capacity, inbound and outbound logistics,<br/>and a Control Center for final inspections*

*Built by [Engin Sarak](https://github.com/EnginSarak)*

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
- [Features](#features)
  - [Dashboard](#dashboard)
  - [Tile System](#tile-system)
  - [Outbound Order Management](#outbound-order-management)
  - [Shipment Grouping](#shipment-grouping)
  - [Pickup ETA & Pick Order](#pickup-eta--pick-order)
  - [Inbound Tracking](#inbound-tracking)
  - [Bin Usage Monitoring](#bin-usage-monitoring)
  - [Forecast Mode](#forecast-mode)
  - [Task List](#task-list)
  - [Control Center](#control-center)
  - [Issues Center](#issues-center)
  - [3D Warehouse View](#3d-warehouse-view)
  - [Monitor Mode](#monitor-mode)
  - [Maintenance Panel](#maintenance-panel)
  - [Theming](#theming)
- [Access Control](#access-control)

---

## Overview

PROMEDIA SPACE is a closed-source, access-controlled internal web application built for Promedia's logistics operations. It gives everyone involved the same picture of what is currently standing in the warehouse, what is about to arrive, and what is about to leave.

The tool is used daily by logistics coordinators, customer service and warehouse staff to:

- See how much staging space is actually left, and avoid over-committing it
- Track outbound orders through their full lifecycle from picking to pickup
- Group orders that leave on the same truck and pick them in the smartest order
- Monitor inbound stock arrivals, both expected and already received
- Log and analyze daily bin occupancy over time
- Plan ahead with Forecast mode, which previews the floor on any future date
- Check assembled goods against the delivery note before they leave the building
- Keep multi-step paperwork such as customs documents on a checklist so nothing gets forgotten
- Record open problems with photos so they stay visible to everyone

---

## Preview

<div align="center">
  <img src="https://raw.githubusercontent.com/enginsarak/space/main/public/preview.png?v=2" alt="Promedia Space Dashboard Preview" width="100%"/>
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

## Features

### Dashboard

The dashboard is the first screen after login and shows the current state of the warehouse. Viewers see it read-only. Every date picker in the app carries a **CW** column with the calendar week.

**Warehouse Floor Map**
A grid of all pallet staging slots, each one a colored tile. The grid is color-coded by customer and destination country at the same time:

- The tile background shows the **destination country**
- The tile border shows the **customer**
- Tiles animate in sequentially on page load

**Capacity Bar**
A segmented bar showing how staging capacity is currently spent:

| Segment | Style | Meaning |
|---|---|---|
| Picked | Solid | Orders picked and staged |
| Pending Outbound | Dashed | Ordered but not yet confirmed |
| Arrived Inbound | Solid | Stock deliveries that have arrived |
| Expected Inbound | Dashed | Future-dated inbound reservations |

Above the bar, two pointers show the capacity level at a glance. The solid pointer marks the percentage of slots occupied right now, and a dashed pulsing pointer appears whenever pending picks or expected inbound entries exist, pointing at the projected total once everything lands. A warning shows up automatically when that projected total goes over the configured capacity.

**Outbound Panel**
Lists all active outbound orders with customer name, pallet count, destination country and a status badge. The list is sorted by pick urgency rather than alphabetically, see [Pickup ETA & Pick Order](#pickup-eta--pick-order). Maintainers additionally see a red printed badge on orders whose pick list has been printed, and a yellow warning triangle on orders with open tasks.

**Problem Badge**
Right-clicking a status badge in the sidebar (long-press on touch) lets a Maintainer mark that order as a problem and add a short reason. The badge turns red and reads **PROBLEM**, and the order is greyed out on the floor map. The reason shows up in the tile detail card. It is purely a flag that something is wrong and does not change the pick order.

**Inbound Panel**
Lists logged inbound deliveries, both upcoming (shown as "Expected") and already received ("Arrived"). Deliveries are shown up to 7 days in advance; anything further out stays hidden until it moves into that window. Each entry shows supplier, pallet count and date.

**Bin Usage Panel**
Shows today's bin occupancy against the total configured bin count, with a color-coded bar, the current month's daily average and a log of recent entries.

---

### Tile System

Each occupied pallet slot is an interactive tile containing:

- **Customer abbreviation**: a short label identifying the customer
- **Pallet index**: shows which pallet this is out of the customer's total, for example `2/5` means the second of five pallets belonging to that order
- **Country-coded background**: a fixed dark color per destination country (IT, DE, FR, PL, ES, BE, DK, SE, LT, CH, QA, NL, AT, UK, and more)
- **Shipment-coded border**: a color per shipment. Orders that leave on the same truck share one border color, while separate shipments of the same customer get distinct colors so they read as separate on the floor, see [Shipment Grouping](#shipment-grouping)
- **Status corner markers**: small symbols in the top-right corner showing progress

| Symbol | Status |
|---|---|
| `✓` | Controlled |
| `✓✓` | Ordered |
| `★` | Confirmed |

Hovering over a tile highlights the whole shipment it belongs to, which makes it easy to spot which slots leave together across a busy floor map.

Clicking or tapping a tile opens a detail card with everything on the order: customer, delivery date, picks, SORD number, destination country, forwarder, colli count, internal notes and current status. If the order has already been inspected in the Control Center, the card shows that too.

Free slots are rendered as empty tiles and are not interactive.

---

### Outbound Order Management

Outbound orders move through five stages:

```
Pending Pick → Picked → Controlled → Ordered → Confirmed
```

The stage follows automatically from four checkboxes, and the floor map, capacity bar, sidebar and tile markers all update with it.

**Printed Flag**
Maintainers can mark an order as printed once the pick list has physically gone to the warehouse. This runs alongside the order lifecycle and is visible to Maintainers only. A small red badge appears next to the customer name.

**Picked Up Date**
Marking an order as picked up moves it into History, where it gets an automatic pickup date shown in orange. Maintainers can confirm or correct that date by clicking it, and it turns green once it has been set by hand. Archived entries are kept for 365 days.

**Automatic Task Detection**
Saving a new outbound order can trigger a checklist in the [Task List](#task-list) on its own, depending on the destination country or customer, so paperwork that is easy to forget gets tracked without anyone having to remember the rule. Each task is linked to the order it came from, and a task that has been deleted does not come back the next time the order is saved.

---

### Shipment Grouping

Not every order from the same customer travels on the same truck. PROMEDIA SPACE recognizes which orders actually belong together and groups them automatically: they share one color on the floor map, sit together in the 3D view, and count as a single entry in the sidebar, with their own table view for a closer look. A group can also be split apart or merged back by hand when needed.

---

### Pickup ETA & Pick Order

PROMEDIA SPACE keeps track of when an order came in, when the customer wants it, and when it will actually leave the warehouse, and estimates that last date automatically based on the destination. The Outbound sidebar and Monitor board then rank orders by how urgent they really are to pick, so the most time-critical ones always float to the top. An order can also be flagged ASAP or pinned to a manual priority when something simply has to go first.

---

### Inbound Tracking

Inbound deliveries can be pre-registered with a supplier name, pallet count and expected arrival date.

- **Future-dated entries** appear on the floor map as dashed tiles and count as expected inbound in the capacity bar
- **Past-dated or same-day entries** count as arrived inbound and appear as solid tiles

Inbound tiles are distinguishable from outbound tiles by their shape: outbound slots are fully closed squares, inbound tiles are half-open with a cut-off top edge.

---

### Bin Usage Monitoring

Bin usage is tracked separately from pallet staging and counts how many bins are occupied on each day. Maintainers can log today's count, backdate a missed entry with the date picker, and edit or delete past entries.

The Bin Usage Sidebar shows a utilization bar color-coded by fill level, today's count against the total, the monthly average and a recent log. Historical entries are grouped by calendar week with each page showing one full week from Monday to Friday, labelled with its week number.

---

### Forecast Mode

The Forecast button in the Floor Plan header opens a date picker for previewing the projected warehouse state on any future date. The floor map and capacity bar switch over and show:

- Inbound deliveries expected to have arrived by that date
- Outbound orders still likely to be standing, based on when they are expected to leave. An order leaving on the 16th still occupies its slot for all of the 16th and only drops out of the forecast on the 17th

A banner makes clear this is a projection and not live data, with a "Back to Live" link to exit. The arrow buttons on either side of the Forecast button step through days without reopening the calendar.

NRW public holidays are highlighted in red in the date picker and trigger a warning when selected, noting that no pickups are expected that day.

---

### Task List

The Task List is a workflow module for **Maintainers**, reachable through the clipboard icon in the dashboard header. A badge on the button shows how many tasks are still open.

Each task has a type badge, a title, an optional link to an outbound or inbound order, a progress bar with a checklist that can be ticked off item by item, and buttons to mark it done or delete it.

Tasks are often created automatically when an order is saved, see [Automatic Task Detection](#outbound-order-management), and come pre-filled with the right checklist for that situation. **General tasks** can also be created by hand with a custom title and an optional order link, for ad-hoc items such as warehouse queries, damage reports or follow-up reminders. The order link can point at either an outbound order or an inbound delivery.

Every checklist can be edited in place without leaving the panel. Steps can be added, renamed inline, dragged into a different order by long-pressing the grip handle, or deleted, up to eight per task. Changes sync immediately, so everyone sees the same state.

When an order has open tasks, a yellow warning triangle appears next to the customer name in the sidebar and the outbound table, so it is obvious that something still needs attention. Maintainers only.

---

### Control Center

The last check before goods leave the building, reachable through the **Control Center** button in the header. Open to Maintainers, Customer Service and Warehouse Operators.

**What it is for.** Between picking and loading, somebody has to confirm that what is on the pallet matches the delivery note: article, batch, quantity. The batch number in particular is what a recall is later traced by.

**How it works.** The delivery note is exported from Business Central as XML and dropped into PROMEDIA SPACE from any PC. It becomes a target list with one row per article and batch, and the quantity that should be there. The controller then works through the goods on a phone, scanning as they go. Each scan identifies a row by its lot number, which is the one field the barcode and the delivery note reliably share.

**Counting instead of scanning quantities.** No barcode on the goods carries a carton quantity, so quantities are calculated rather than scanned. There are four counting units to choose from, valid for every following scan: pallet, layer, carton or single item. A layer also takes whole cartons on top or missing plus loose pieces, so a broken pallet resolves in one booking instead of two. Both fields accept arithmetic, so something like `12x8x3-1` can be typed straight in. Pack sizes are learned per article and shared across devices, and the Business Central article catalog ships with the app.

**Nothing closes half-finished.** An inspection can only be filed when every position matches its target exactly, and booking beyond a target needs a second confirmation. Every booking gives a short tone and a flash at the edge of the screen, because whoever is counting is looking at the goods rather than at the phone. Filed inspections move into an archive kept for four weeks.

**Filed inspections tick their rows.** Both sides carry the same order number, so filing an inspection automatically marks the matching outbound rows as printed, picked and controlled. Where a number would match two rows, or none, the Control Center asks instead of guessing. If the customer was not in the table yet at inspection time, the rows can still be assigned afterwards from the archive, and unassigning gives back exactly the ticks that inspection had set.

**One address, two screens.** The same button opens different things depending on the device:

| Device | What opens |
|---|---|
| Phone / tablet | The inspection: job list, count sheet, calculator, sound, archive |
| PC | The drop-off: add XML documents and start scanning |

Delivery notes reach the PC page two ways: the button opens the file picker, or a multi-selection is dragged out of Explorer or Finder and dropped on the page, where the button arms itself as the files come over the window. Folders and anything that is not XML are filtered out before a file is read.

While an inspection is running, the PC page greys out and shows only a counter, so a stray click cannot interrupt a run in progress. A log on the PC page shows recent scans, documents and filed inspections, which is what you look at when a scan does not seem to have arrived.


**Everything is shared.** There is no pairing step, since both ends are already signed into PROMEDIA SPACE. A delivery note dropped in the office is on every phone in the warehouse seconds later, and scans made in the hall show up on the desk.

---

### Issues Center

Operational problems and complaints that need to stay visible to more than one person, reachable through the **Issues** button in the header.

All roles can read the list, since the whole point is a shared picture. Creating, editing and deleting is Maintainer only.

Entries are called cases, and there is no Done button: a case is either open or deleted. The trash icon asks for confirmation first, because it sits next to the button that opens the editor.

The list reads like a classifieds page. Each case is a card with a key photo, the title, the first lines of the text and a "Read more" link. Upload one image and it becomes the key photo; upload several and you pick which one. Opening a case shows the date, the full text and the image strip, and tapping an image opens it full screen with zoom and pan.

Text can be bold, italic, underlined and set in one of six colors. Up to 20 images fit on a case, and they are compressed in the browser before they are sent, so a phone photo uploads in seconds instead of minutes. Cases are kept for two years.

---

### 3D Warehouse View

The **3D** button on the Floor Plan card opens an interactive three-dimensional model of the staging area, showing current occupancy as colored pallet stacks inside a scale model of the hall, with free slots as flat pads. Hovering a pallet shows its order details.

The view rotates and zooms with mouse drag and scroll, or pinch on touch devices, and there is an on-screen D-pad and zoom slider on desktop. It uses the same colors as the flat floor map, so a shipment looks the same in both views. Handy on a large screen or when walking someone through the current layout.

---

### Monitor Mode

The Monitor button is available to the **Warehouse Operator** role and switches the app into a fullscreen layout intended for TV monitors in the warehouse.

Two full-screen views then cycle automatically:

- **Floor Screen**: capacity bar, warehouse grid and inbound sidebar. Shown for 15 seconds.
- **Board Screen**: a large outbound table with customer, picks, SORD number, country, delivery date, forwarder, colli and status. Long lists are paged, each page shown for 10 seconds with dot indicators, so every page always gets equal time before the display switches back to the floor.

Pressing **F5** toggles browser fullscreen without reloading the page. Monitor Mode is remembered per token, so a dedicated warehouse display can be set up once and stays that way across reloads.

Warehouse Operators can also switch the interface between English and German, and mark staged orders as picked up straight from the outbound list.

---

### Maintenance Panel

The Maintenance Panel is open to **Maintainer** and **Customer Service** roles. It opens as a fullscreen-capable overlay with four tabs.

#### Outbound Tab

**For Maintainers, full access:**
- Fully editable table with inline editing for all order fields: customer, date, picks, SORD number, country, forwarder, colli, notes
- Checkbox columns for Printed, Picked, Controlled, Ordered, Confirmed and Picked Up, saved immediately
- A **Pickup ETA** column showing each order's expected departure, color-coded green when confirmed and orange while estimated, see [Pickup ETA & Pick Order](#pickup-eta--pick-order)
- **String bridges** down the left edge connecting the rows that ship together, in the customer's color, see [Shipment Grouping](#shipment-grouping)
- Set or remove **ASAP** on a delivery date, and detach or reattach an order from its shipment group, by right-click or long-press
- **Autosave**: text changes are saved a moment after the last keystroke, and rows that are still missing a customer or a date are held back until they are complete. A **Save Changes** button is there for saving on demand
- **Add Row** to create a blank order, or just press `N`. Pressing `Enter` on the dashboard opens the outbound table
- **Delete** individual orders
- **Undo** reverts the last action, up to 10 steps
- **History** shows archived picked-up orders, with editable and pickup dates
- **Zoom** buttons scale the table from 50 to 100 percent for long lists on small screens
- Ticking **Picked** on a row that counts in pallets asks the warehouse operator to verify or correct the pallet count first
- Small conveniences: the Picks and SORD fields turn `&` into a comma, and common misspellings of a forwarder name correct themselves

**For Customer Service, restricted access:**
- Can add rows and edit all text fields
- All checkbox columns are greyed out and read-only
- Pickup ETA is visible but not editable
- The delete button is hidden, so existing orders cannot be removed
- History is visible but fully read-only

#### Inbound Tab
Maintainer and Customer Service both have full access to add, edit and delete inbound deliveries.

#### Config Tab
Maintainer only: total pallet staging capacity, total bin count, and managing bin usage entries.

#### Users Tab
Maintainer only: generate access tokens with a selectable role, copy them to the clipboard, and delete tokens to revoke access. Greyed out for Customer Service.

---

### Theming

PROMEDIA SPACE has three theme modes, switchable from the dashboard header:

| Mode | Behaviour |
|---|---|
| `system` | Follows the OS or browser preference |
| `light` | Always light |
| `dark` | Always dark |

The choice is remembered and restored on every visit, and the login screen follows it too.

---

## Access Control

PROMEDIA SPACE uses a token-based access model. There are no user accounts, passwords or registration. Tokens are issued by a Maintainer from the Users tab.

| Role | Access |
|---|---|
| **Viewer** | Dashboard and Issues Center, read-only |
| **Customer Service** | Dashboard, Issues Center, Control Center, and the Maintenance Panel with restrictions on the Outbound tab and no access to Config or Users |
| **Maintainer** | Everything: full Maintenance Panel, Task List, Control Center, and write access in the Issues Center |
| **Warehouse Operator** | Dashboard (read-only), Monitor Mode, Control Center, Issues Center, language switch, and marking staged orders as picked up |

Once a valid token is entered on the login screen it is stored in the browser and validated automatically on later visits.

Access tokens are credentials. They should never be committed to version control or shared outside authorized channels.

---

<div align="center">

**PROMEDIA SPACE** is proprietary software developed for internal use at Promedia Medizintechnik A. Ahnfeldt GmbH.  
Unauthorized access, redistribution, or use is not permitted.

*Built by [Engin Sarak](https://github.com/EnginSarak) · © Promedia Medizintechnik A. Ahnfeldt GmbH · All rights reserved*

</div>
