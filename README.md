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

Planned next: international pack (derived time-zone clocks, currency converter), business pack (wallets/company-vs-personal funds/teammate splits — ported from the Germany Trip app), memory room (past-trip reading view, Year in Travel).

## Storage

- `yatra.shelf` — lightweight trip index + cached stats
- `yatra.trip.<id>` — one key per trip (fast saves, lazy loads)

## Deploy

Static host, repo root = site root. Vercel: framework **Other**, no build step. Then Chrome → ⋮ → Install app.
