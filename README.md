# Yātrā 🧳

One offline-first app for every journey — business trips, pilgrimages, tournaments, getaways. No accounts, no backend; everything lives on the device.

**Single self-contained `index.html`** plus PWA install files (`manifest.webmanifest`, SVG icons, `sw.js` with network-first navigations so deployed updates reach installed phones).

## The idea

Every trip is a **bundle of modules** you toggle per trip, created in one tap from a template:

| Template | Modules |
|---|---|
| 💼 Business | planner · journal · budget · lists |
| 🌍 Tourism & relaxation | planner · journal · budget · lists |
| 🛕 Pilgrimage | planner · journal · budget · lists (darshan/offerings seeds) |
| 🃏 Tournament | planner · journal · budget · lists (results seed) |
| 🏞️ Local getaway | planner · journal · budget · lists |
| 🪁 Free-form | journal · budget only |

Trips move through a lifecycle automatically by their dates: **Planning → Upcoming → Active → Past**. The shelf shows countdowns for upcoming trips and stats (days, spend, journal entries) for past ones. The app opens straight into the active trip when one is live.

## Phase 1 (this build)

- Trip shelf + create-from-template + per-trip module toggles
- **Today** — day X of Y, today's plan, budget snapshot, quick actions; adapts to lifecycle (countdown when upcoming, stats when past)
- **Plan** — day-by-day itinerary; extending the end date grows the days (one-tap "+ Add a day"); items outside shrunk dates are kept, never lost
- **Money** — trip budget and/or per-diem, categorised expenses, category breakdown, CSV export, per-trip currency
- **Lists** — packing/to-buy/to-do with template seeds, progress bars, un-tick-all
- **Journal** — daily entries with mood; empty entries never persist
- Export/import: single trip or everything; Android back button closes layers instead of exiting

## Phase 2 — international pack + people

- **Bookings timeline** (Plan → Bookings): flights/hotels/trains with journey grouping, layover chips (warns when tight or when leg time zones conflict), inline terminal/gate editing, photo attachments, hotel "show driver" local-language address
- **Airport cards** (Plan → Airports): tickable step lists for each airport/layover
- **Derived clock strip**: home + destination + any layover zones found in your flight legs — appears only on international trips
- **Per-trip currency converter** (Money → Convert) with user-saved rate + date; home-currency equivalents on spend totals
- **Phrasebook**: shared per language across trips; German starter pack; search + full-screen phrase display
- **Travel wallet** (shelf level, shared across trips): document vault (IndexedDB, compressed), people directory, my-info fields, home settings
- **People & operator** per trip: companions from the shared directory (solo/partner/group), tour-operator card (company, contact, booking ref) — both surface on Today and the emergency card
- **Emergency card** per trip: trip fields + operator + companion phones + shared my-info
- Backups now carry the shared wallet and all images

## Phase 3 — wallets & splitting (business pack)

Opt-in **Wallets & splitting** module (on by default for the Business template, toggleable on any trip). Adds to the Money tab:

- **Wallets** — per-trip cash/card wallets, each showing real balance split into **company vs personal** money; top-ups tagged by source; a **company-money audit** card (received / spent / on-hand-to-return) that appears only when there's company activity, with a downloadable Markdown audit report that excludes personal money
- **Split** — divide costs (hotel, dinners, taxis) among the trip's **companions from the people directory**; equal split by default with a "your share" override and per-person participation checkboxes; a running **you-owe / owes-you** balance per person and settlements to square up
- Expenses gain wallet + fund tags when the module is on; per-diem then tracks company spending; expenses CSV gains wallet/fund columns

The money model tracks only *your* position (what you owe / are owed), so group trips and business-audit trips both work. Backups carry all of it.

Planned next: memory room (past-trip reading view, Year in Travel), Germany-trip import.

## Storage

- `yatra.shelf` — lightweight trip index + cached stats
- `yatra.trip.<id>` — one key per trip (fast saves, lazy loads)

## Deploy

Static host, repo root = site root. Vercel: framework **Other**, no build step. Then Chrome → ⋮ → Install app.
