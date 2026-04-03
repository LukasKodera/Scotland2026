# Scotland Trip Planner — Design Spec

**Date:** 2026-04-02  
**Status:** Approved

---

## Overview

A single self-contained `index.html` file for planning and presenting a 10-day Scotland photography road trip in June 2026. Intended for local browser use only — not deployed as a website.

---

## Trip Details

- **Travelers:** 2 people
- **Duration:** 10 days, June 2026
- **Route:** Prague → fly in Edinburgh (EDI) → drive north → fly out Inverness (INV)
- **Transport:** Rental car, one-way Edinburgh → Inverness (Arnold Clark or equivalent)
- **Total distance:** ~1,300 km
- **Purpose:** Photography trip — natural landscapes

### Day-by-Day Route

| Day | Location | Drive from previous | Drive time |
|-----|----------|-------------------|------------|
| 1 | Edinburgh → Glencoe | 170 km | ~2.5h |
| 2 | Glencoe (local) | 50 km | ~1h |
| 3 | Glencoe → Isle of Skye (via Eilean Donan) | 120 km | ~2h |
| 4 | Isle of Skye (local — Storr, Kilt Rock) | 60 km | ~1.5h |
| 5 | Isle of Skye (local — Fairy Pools, Neist Point) | 70 km | ~1.5h |
| 6 | Skye → Torridon via Applecross | 130 km | ~3h |
| 7 | Torridon (local) | 50 km | ~1.5h |
| 8 | Torridon → Assynt (NC500) | 100 km | ~2h |
| 9 | NC500 north coast | 180 km | ~3.5h |
| 10 | → Inverness, fly out | 120 km | ~2h |

---

## Visual Design

- **Style:** Nature & Fresh — forest greens (`#2d5a27`, `#4a7c59`, `#6b9e6b`) with white cards and light green backgrounds (`#f1f8e9`)
- **Typography:** System sans-serif, no external fonts
- **No external dependencies** — fully offline

---

## Page Structure

### 1. Hero Section
- Dark green gradient background
- Title: "Scotland 2026"
- Subtitle: "10 days · 2 people · June 2026 · Photography"
- Subheading: "Prague → Edinburgh → Inverness"
- Stat cards: 10 days · 2 people · ~1,300 km · June

### 2. Sticky Navigation Bar
- Fixed to top on scroll
- Links: Route · Itinerary · Stays · Tips
- Active section highlighted with white underline
- Implemented with ~30 lines of vanilla JS (IntersectionObserver)

### 3. Route Overview
- Visual horizontal route strip (fully offline, no map embed)
- Nodes: Edinburgh ✈ → Glencoe → Isle of Skye → Torridon → NC500 → Inverness ✈
- Each node shows day range and drive time from previous stop
- Wraps gracefully on narrow screens

### 4. Timeline — Day-by-Day Itinerary
- Vertical timeline with numbered circle + connecting line
- 10 rich day cards, one per day
- **Each card contains:**
  - Day number (circle), location name, date, drive time from previous
  - Region tag (e.g. "Highlands") + nights count badge
  - 📸 Photo spots
  - 🏠 Stay: AirBnB placeholder (links filled in later)
  - 📝 Notes / tips

### 5. Accommodation Summary
- Simple list of all stays in order
- Columns: nights, location, AirBnB link (placeholder "TBD" for now)
- Will be updated once bookings are made

### 6. Tips & Links
- Static bullet list of practical reminders:
  - Car rental: one-way Arnold Clark Edinburgh → Inverness
  - Golden hour: June sunsets ~10pm, sunrises ~4:30am
  - Weather: always bring waterproofs
  - NC500: book accommodation well in advance
  - Driving: mostly single-track roads, add time for stops

---

## Interactivity (Approach B — Light JS)

~30 lines of embedded vanilla JavaScript:
- Smooth scroll when clicking nav links
- IntersectionObserver to highlight active nav section as user scrolls
- "Back to top" button appears after scrolling past the hero

No libraries. No external scripts. All JS embedded in `<script>` tag at bottom of `<body>`.

---

## Constraints

- Single file: `index.html`
- No external CDN, no frameworks, no external images
- Must work fully offline
- No build tools

---

## Out of Scope (for now)

- AirBnB links (placeholders only — to be filled manually)
- Actual flight details (TBD)
- Budget tracking
- Packing list
