# Scotland Trip Planner Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single self-contained `index.html` file presenting a 10-day Scotland photography road trip itinerary with a green nature theme, vertical timeline, and light JS interactivity.

**Architecture:** Everything lives in one `index.html` — embedded `<style>` block for CSS, inline content for all sections, and a single `<script>` block at the bottom for interactivity. No external resources of any kind.

**Tech Stack:** Vanilla HTML5, CSS3 (custom properties, flexbox, grid), ~30 lines of vanilla JS (IntersectionObserver, smooth scroll).

---

## File Structure

- **Create:** `index.html` — the entire deliverable. All CSS in `<style>`, all JS in `<script>` at end of `<body>`.

No other files. No build tools.

---

## GitHub Workflow

Every task ends with a commit on a feature branch. A single PR is opened after all tasks are complete. **Never commit directly to `main`.**

Branch name: `feature/trip-planner-html`

---

### Task 1: HTML skeleton, CSS variables, and hero section

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create the branch**

```bash
git checkout -b feature/trip-planner-html
```

- [ ] **Step 2: Create `index.html` with full skeleton, CSS variables, and hero section**

Write the following complete file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Scotland 2026</title>
  <style>
    :root {
      --green-dark:   #2d5a27;
      --green-mid:    #4a7c59;
      --green-light:  #6b9e6b;
      --green-pale:   #f1f8e9;
      --green-accent: #a5d6a7;
      --white:        #ffffff;
      --text-dark:    #212121;
      --text-mid:     #555555;
      --text-muted:   #888888;
      --shadow:       0 1px 4px rgba(0,0,0,0.10);
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
      background: var(--green-pale);
      color: var(--text-dark);
      line-height: 1.5;
    }

    /* ── Hero ─────────────────────────────────────── */
    .hero {
      background: linear-gradient(160deg, #1b3a1f 0%, var(--green-dark) 60%, var(--green-mid) 100%);
      padding: 48px 32px 40px;
    }
    .hero-eyebrow {
      color: var(--green-accent);
      font-size: 11px;
      letter-spacing: 3px;
      text-transform: uppercase;
      margin-bottom: 10px;
    }
    .hero-title {
      color: var(--white);
      font-size: 36px;
      font-weight: 300;
      margin-bottom: 6px;
    }
    .hero-subtitle {
      color: #c8e6c9;
      font-size: 15px;
      margin-bottom: 28px;
    }
    .hero-stats {
      display: flex;
      gap: 12px;
      flex-wrap: wrap;
    }
    .stat-card {
      background: rgba(255,255,255,0.10);
      border: 1px solid rgba(255,255,255,0.18);
      border-radius: 8px;
      padding: 10px 18px;
      text-align: center;
      color: var(--white);
      min-width: 80px;
    }
    .stat-card .stat-value {
      font-size: 22px;
      font-weight: 700;
      line-height: 1.1;
    }
    .stat-card .stat-label {
      font-size: 10px;
      color: var(--green-accent);
      letter-spacing: 1px;
      text-transform: uppercase;
      margin-top: 2px;
    }

    /* ── Page container ───────────────────────────── */
    .container {
      max-width: 860px;
      margin: 0 auto;
      padding: 0 24px 64px;
    }

    /* ── Section headings ─────────────────────────── */
    .section-heading {
      font-size: 13px;
      font-weight: 700;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: var(--green-dark);
      margin: 40px 0 18px;
      padding-bottom: 8px;
      border-bottom: 2px solid var(--green-accent);
    }
  </style>
</head>
<body>

  <!-- Hero -->
  <div class="hero" id="top">
    <div class="hero-eyebrow">Prague → Edinburgh → Inverness</div>
    <h1 class="hero-title">Scotland 2026</h1>
    <p class="hero-subtitle">10 days &middot; 2 people &middot; June 2026 &middot; Photography</p>
    <div class="hero-stats">
      <div class="stat-card"><div class="stat-value">10</div><div class="stat-label">Days</div></div>
      <div class="stat-card"><div class="stat-value">2</div><div class="stat-label">People</div></div>
      <div class="stat-card"><div class="stat-value">~1 300</div><div class="stat-label">km</div></div>
      <div class="stat-card"><div class="stat-value">June</div><div class="stat-label">2026</div></div>
    </div>
  </div>

  <div class="container">
    <!-- sections go here in later tasks -->
  </div>

  <script>
    // JS added in Task 6
  </script>
</body>
</html>
```

- [ ] **Step 3: Open in browser and verify**

Open `index.html` in a browser. Verify:
- Dark green gradient hero
- Title "Scotland 2026" visible
- 4 stat cards render in a row (wrap on narrow window)
- Page background is light green (`#f1f8e9`)

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add HTML skeleton and hero section"
```

---

### Task 2: Sticky navigation bar

**Files:**
- Modify: `index.html` — add nav CSS inside `<style>`, add `<nav>` element after `<div class="hero">`, before `<div class="container">`

- [ ] **Step 1: Add nav CSS inside the `<style>` block (after `.section-heading` rule)**

```css
    /* ── Sticky nav ───────────────────────────────── */
    .nav {
      position: sticky;
      top: 0;
      z-index: 100;
      background: var(--green-dark);
      display: flex;
      align-items: center;
      gap: 0;
      padding: 0 24px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.18);
    }
    .nav-brand {
      color: var(--green-accent);
      font-size: 12px;
      font-weight: 700;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      padding: 14px 20px 14px 0;
      margin-right: 8px;
      border-right: 1px solid rgba(255,255,255,0.15);
    }
    .nav a {
      color: var(--green-accent);
      text-decoration: none;
      font-size: 13px;
      padding: 14px 16px;
      transition: color 0.15s;
      border-bottom: 2px solid transparent;
    }
    .nav a:hover   { color: var(--white); }
    .nav a.active  { color: var(--white); border-bottom-color: #81c784; }
```

- [ ] **Step 2: Add `<nav>` HTML between `.hero` and `.container`**

```html
  <!-- Sticky nav -->
  <nav class="nav">
    <div class="nav-brand">Scotland '26</div>
    <a href="#route">Route</a>
    <a href="#itinerary">Itinerary</a>
    <a href="#stays">Stays</a>
    <a href="#tips">Tips</a>
  </nav>
```

- [ ] **Step 3: Open in browser and verify**

Scroll down (add temporary `<div style="height:2000px">` in container if needed, remove after).
Verify:
- Nav sticks to top on scroll
- Links are green-tinted, turn white on hover
- No active state yet (added in Task 6)

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add sticky navigation bar"
```

---

### Task 3: Route overview section

**Files:**
- Modify: `index.html` — add route CSS + section HTML inside `.container`

- [ ] **Step 1: Add route CSS inside `<style>` (after nav rules)**

```css
    /* ── Route overview ───────────────────────────── */
    .route-strip {
      display: flex;
      align-items: center;
      flex-wrap: wrap;
      gap: 6px 0;
      background: var(--white);
      border-radius: 10px;
      padding: 20px 24px;
      box-shadow: var(--shadow);
    }
    .route-node {
      text-align: center;
      padding: 0 8px;
    }
    .route-node-label {
      background: var(--green-dark);
      color: var(--white);
      border-radius: 6px;
      padding: 6px 12px;
      font-size: 12px;
      font-weight: 700;
      white-space: nowrap;
    }
    .route-node-label.endpoint { background: #1b3a1f; }
    .route-node-meta {
      font-size: 10px;
      color: var(--text-muted);
      margin-top: 4px;
    }
    .route-arrow {
      color: var(--green-accent);
      font-size: 20px;
      padding: 0 2px;
      line-height: 1;
      margin-bottom: 14px;
    }
```

- [ ] **Step 2: Replace `<!-- sections go here in later tasks -->` comment with route section HTML**

```html
    <!-- Route Overview -->
    <h2 class="section-heading" id="route">Route</h2>
    <div class="route-strip">
      <div class="route-node">
        <div class="route-node-label endpoint">Edinburgh ✈</div>
        <div class="route-node-meta">Day 1</div>
      </div>
      <div class="route-arrow">→</div>
      <div class="route-node">
        <div class="route-node-label">Glencoe</div>
        <div class="route-node-meta">Day 1–2 · 2.5h</div>
      </div>
      <div class="route-arrow">→</div>
      <div class="route-node">
        <div class="route-node-label">Isle of Skye</div>
        <div class="route-node-meta">Day 3–5 · 2h</div>
      </div>
      <div class="route-arrow">→</div>
      <div class="route-node">
        <div class="route-node-label">Torridon</div>
        <div class="route-node-meta">Day 6–7 · 3h</div>
      </div>
      <div class="route-arrow">→</div>
      <div class="route-node">
        <div class="route-node-label">NC500</div>
        <div class="route-node-meta">Day 8–9 · 2h</div>
      </div>
      <div class="route-arrow">→</div>
      <div class="route-node">
        <div class="route-node-label endpoint">Inverness ✈</div>
        <div class="route-node-meta">Day 10</div>
      </div>
    </div>

    <!-- Itinerary, Stays, Tips added in later tasks -->
```

- [ ] **Step 3: Open in browser and verify**

Verify:
- Route strip shows all 6 nodes connected by arrows
- Dark endpoint nodes for Edinburgh/Inverness
- Wraps cleanly on a narrow window

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add route overview section"
```

---

### Task 4: Timeline CSS and structure

**Files:**
- Modify: `index.html` — add timeline + day card CSS

- [ ] **Step 1: Add timeline and card CSS inside `<style>` (after route rules)**

```css
    /* ── Timeline ─────────────────────────────────── */
    .timeline {
      position: relative;
      display: flex;
      flex-direction: column;
      gap: 0;
    }
    .timeline-item {
      display: flex;
      gap: 14px;
      align-items: flex-start;
    }
    .timeline-spine {
      display: flex;
      flex-direction: column;
      align-items: center;
      flex-shrink: 0;
      width: 40px;
    }
    .day-circle {
      width: 40px;
      height: 40px;
      background: var(--green-dark);
      color: var(--white);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 14px;
      font-weight: 700;
      flex-shrink: 0;
      z-index: 1;
    }
    .timeline-line {
      width: 2px;
      background: var(--green-accent);
      flex: 1;
      min-height: 24px;
    }
    .timeline-item:last-child .timeline-line { display: none; }

    /* ── Day card ─────────────────────────────────── */
    .day-card {
      background: var(--white);
      border-radius: 8px;
      padding: 14px 18px;
      box-shadow: var(--shadow);
      flex: 1;
      margin-bottom: 16px;
    }
    .day-card-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      margin-bottom: 10px;
      gap: 10px;
    }
    .day-card-title {
      font-size: 15px;
      font-weight: 700;
      color: var(--green-dark);
    }
    .day-card-meta {
      font-size: 11px;
      color: var(--text-muted);
      margin-top: 2px;
    }
    .day-card-badges {
      display: flex;
      gap: 5px;
      flex-shrink: 0;
      flex-wrap: wrap;
      justify-content: flex-end;
    }
    .badge {
      font-size: 10px;
      font-weight: 700;
      padding: 2px 9px;
      border-radius: 10px;
      white-space: nowrap;
    }
    .badge-region { background: #e8f5e9; color: var(--green-dark); }
    .badge-nights { background: #e3f2fd; color: #0d47a1; }
    .day-card-body {
      display: flex;
      flex-direction: column;
      gap: 6px;
      font-size: 13px;
    }
    .day-card-row { display: flex; gap: 8px; }
    .day-card-row span:first-child {
      font-weight: 600;
      color: var(--green-dark);
      flex-shrink: 0;
    }
    .day-card-row span:last-child { color: var(--text-mid); }
    .airbnb-link { color: var(--green-mid); text-decoration: none; }
    .airbnb-link:hover { text-decoration: underline; }
    .tbd { color: var(--text-muted); font-style: italic; }
```

- [ ] **Step 2: Add the itinerary section wrapper after the route section (replace the `<!-- Itinerary ... -->` comment)**

```html
    <!-- Itinerary -->
    <h2 class="section-heading" id="itinerary">Itinerary</h2>
    <div class="timeline">
      <!-- Day cards added in Task 5 -->
    </div>

    <!-- Stays, Tips added in later tasks -->
```

- [ ] **Step 3: Open in browser and verify**

Verify the section heading "Itinerary" renders with green underline. No cards yet — that's fine.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add timeline CSS and itinerary section structure"
```

---

### Task 5: All 10 day cards

**Files:**
- Modify: `index.html` — replace `<!-- Day cards added in Task 5 -->` with all 10 `.timeline-item` blocks

- [ ] **Step 1: Replace `<!-- Day cards added in Task 5 -->` with all 10 day cards**

```html
      <!-- Day 1 -->
      <div class="timeline-item">
        <div class="timeline-spine">
          <div class="day-circle">1</div>
          <div class="timeline-line"></div>
        </div>
        <div class="day-card">
          <div class="day-card-header">
            <div>
              <div class="day-card-title">Edinburgh → Glencoe</div>
              <div class="day-card-meta">Arrival day &middot; Drive ~170 km &middot; ~2.5h</div>
            </div>
            <div class="day-card-badges">
              <span class="badge badge-region">Central</span>
              <span class="badge badge-nights">1 night</span>
            </div>
          </div>
          <div class="day-card-body">
            <div class="day-card-row"><span>✈ Arrive</span><span>Edinburgh Airport — pick up rental car (Arnold Clark)</span></div>
            <div class="day-card-row"><span>📸 En route</span><span>Stirling Castle viewpoint &middot; Loch Lomond glimpse</span></div>
            <div class="day-card-row"><span>🏠 Stay</span><span class="tbd">Glencoe area AirBnB — link TBD</span></div>
            <div class="day-card-row"><span>📝 Notes</span><span>Long day with flight — keep driving to minimum, settle in early</span></div>
          </div>
        </div>
      </div>

      <!-- Day 2 -->
      <div class="timeline-item">
        <div class="timeline-spine">
          <div class="day-circle">2</div>
          <div class="timeline-line"></div>
        </div>
        <div class="day-card">
          <div class="day-card-header">
            <div>
              <div class="day-card-title">Glencoe</div>
              <div class="day-card-meta">Local exploration &middot; ~50 km &middot; ~1h driving</div>
            </div>
            <div class="day-card-badges">
              <span class="badge badge-region">Highlands</span>
              <span class="badge badge-nights">1 night</span>
            </div>
          </div>
          <div class="day-card-body">
            <div class="day-card-row"><span>📸 Photo spots</span><span>Three Sisters &middot; Rannoch Moor &middot; Glen Etive (Game of Thrones road)</span></div>
            <div class="day-card-row"><span>🏠 Stay</span><span class="tbd">Glencoe area AirBnB — link TBD</span></div>
            <div class="day-card-row"><span>📝 Notes</span><span>Glen Etive road is narrow and unmarked — worth it for sunrise shots</span></div>
          </div>
        </div>
      </div>

      <!-- Day 3 -->
      <div class="timeline-item">
        <div class="timeline-spine">
          <div class="day-circle">3</div>
          <div class="timeline-line"></div>
        </div>
        <div class="day-card">
          <div class="day-card-header">
            <div>
              <div class="day-card-title">Glencoe → Isle of Skye</div>
              <div class="day-card-meta">Travel day &middot; Drive ~120 km &middot; ~2h</div>
            </div>
            <div class="day-card-badges">
              <span class="badge badge-region">Skye</span>
              <span class="badge badge-nights">1 night</span>
            </div>
          </div>
          <div class="day-card-body">
            <div class="day-card-row"><span>📸 En route</span><span>Eilean Donan Castle (iconic — stop for photos)</span></div>
            <div class="day-card-row"><span>📸 Arrival</span><span>Old Man of Storr if arriving before sunset</span></div>
            <div class="day-card-row"><span>🏠 Stay</span><span class="tbd">Portree AirBnB — link TBD</span></div>
            <div class="day-card-row"><span>📝 Notes</span><span>Eilean Donan is best mid-morning before tour buses arrive</span></div>
          </div>
        </div>
      </div>

      <!-- Day 4 -->
      <div class="timeline-item">
        <div class="timeline-spine">
          <div class="day-circle">4</div>
          <div class="timeline-line"></div>
        </div>
        <div class="day-card">
          <div class="day-card-header">
            <div>
              <div class="day-card-title">Isle of Skye — North</div>
              <div class="day-card-meta">Local exploration &middot; ~60 km &middot; ~1.5h driving</div>
            </div>
            <div class="day-card-badges">
              <span class="badge badge-region">Skye</span>
              <span class="badge badge-nights">1 night</span>
            </div>
          </div>
          <div class="day-card-body">
            <div class="day-card-row"><span>📸 Photo spots</span><span>Old Man of Storr &middot; Kilt Rock &middot; Mealt Falls</span></div>
            <div class="day-card-row"><span>🏠 Stay</span><span class="tbd">Portree AirBnB — link TBD</span></div>
            <div class="day-card-row"><span>📝 Notes</span><span>Old Man of Storr: start before 8am — crowds build fast. 45 min hike.</span></div>
          </div>
        </div>
      </div>

      <!-- Day 5 -->
      <div class="timeline-item">
        <div class="timeline-spine">
          <div class="day-circle">5</div>
          <div class="timeline-line"></div>
        </div>
        <div class="day-card">
          <div class="day-card-header">
            <div>
              <div class="day-card-title">Isle of Skye — South &amp; West</div>
              <div class="day-card-meta">Local exploration &middot; ~70 km &middot; ~1.5h driving</div>
            </div>
            <div class="day-card-badges">
              <span class="badge badge-region">Skye</span>
              <span class="badge badge-nights">1 night</span>
            </div>
          </div>
          <div class="day-card-body">
            <div class="day-card-row"><span>📸 Photo spots</span><span>Fairy Pools &middot; Neist Point lighthouse &middot; Elgol (Cuillin view)</span></div>
            <div class="day-card-row"><span>🏠 Stay</span><span class="tbd">Portree AirBnB — link TBD</span></div>
            <div class="day-card-row"><span>📝 Notes</span><span>Neist Point at sunset is exceptional — June sunset ~10pm</span></div>
          </div>
        </div>
      </div>

      <!-- Day 6 -->
      <div class="timeline-item">
        <div class="timeline-spine">
          <div class="day-circle">6</div>
          <div class="timeline-line"></div>
        </div>
        <div class="day-card">
          <div class="day-card-header">
            <div>
              <div class="day-card-title">Skye → Torridon via Applecross</div>
              <div class="day-card-meta">Heavy drive day &middot; ~130 km &middot; ~3h</div>
            </div>
            <div class="day-card-badges">
              <span class="badge badge-region">Torridon</span>
              <span class="badge badge-nights">1 night</span>
            </div>
          </div>
          <div class="day-card-body">
            <div class="day-card-row"><span>📸 En route</span><span>Applecross Peninsula (Bealach na Bà pass — dramatic hairpin road)</span></div>
            <div class="day-card-row"><span>📸 Arrive</span><span>Loch Torridon viewpoint</span></div>
            <div class="day-card-row"><span>🏠 Stay</span><span class="tbd">Torridon area AirBnB — link TBD</span></div>
            <div class="day-card-row"><span>📝 Notes</span><span>Bealach na Bà is the highest road in Scotland — not suitable in bad weather. Check forecast.</span></div>
          </div>
        </div>
      </div>

      <!-- Day 7 -->
      <div class="timeline-item">
        <div class="timeline-spine">
          <div class="day-circle">7</div>
          <div class="timeline-line"></div>
        </div>
        <div class="day-card">
          <div class="day-card-header">
            <div>
              <div class="day-card-title">Torridon</div>
              <div class="day-card-meta">Local exploration &middot; ~50 km &middot; ~1.5h driving</div>
            </div>
            <div class="day-card-badges">
              <span class="badge badge-region">Torridon</span>
              <span class="badge badge-nights">1 night</span>
            </div>
          </div>
          <div class="day-card-body">
            <div class="day-card-row"><span>📸 Photo spots</span><span>Beinn Alligin &middot; Loch Maree &middot; Gairloch beach</span></div>
            <div class="day-card-row"><span>🏠 Stay</span><span class="tbd">Torridon area AirBnB — link TBD</span></div>
            <div class="day-card-row"><span>📝 Notes</span><span>Loch Maree has beautiful Scots pine islands — great morning light</span></div>
          </div>
        </div>
      </div>

      <!-- Day 8 -->
      <div class="timeline-item">
        <div class="timeline-spine">
          <div class="day-circle">8</div>
          <div class="timeline-line"></div>
        </div>
        <div class="day-card">
          <div class="day-card-header">
            <div>
              <div class="day-card-title">Torridon → Assynt (NC500)</div>
              <div class="day-card-meta">Travel day &middot; ~100 km &middot; ~2h</div>
            </div>
            <div class="day-card-badges">
              <span class="badge badge-region">NC500</span>
              <span class="badge badge-nights">1 night</span>
            </div>
          </div>
          <div class="day-card-body">
            <div class="day-card-row"><span>📸 Photo spots</span><span>Stac Pollaidh &middot; Suilven &middot; Loch Assynt &middot; Ardvreck Castle</span></div>
            <div class="day-card-row"><span>🏠 Stay</span><span class="tbd">Assynt area AirBnB — link TBD</span></div>
            <div class="day-card-row"><span>📝 Notes</span><span>Stac Pollaidh short hike (1h circuit) gives panoramic views of Assynt</span></div>
          </div>
        </div>
      </div>

      <!-- Day 9 -->
      <div class="timeline-item">
        <div class="timeline-spine">
          <div class="day-circle">9</div>
          <div class="timeline-line"></div>
        </div>
        <div class="day-card">
          <div class="day-card-header">
            <div>
              <div class="day-card-title">NC500 — North Coast</div>
              <div class="day-card-meta">Heavy drive day &middot; ~180 km &middot; ~3.5h</div>
            </div>
            <div class="day-card-badges">
              <span class="badge badge-region">NC500</span>
              <span class="badge badge-nights">1 night</span>
            </div>
          </div>
          <div class="day-card-body">
            <div class="day-card-row"><span>📸 Photo spots</span><span>Smoo Cave &middot; Sandwood Bay (2h walk) &middot; Duncansby Head sea stacks</span></div>
            <div class="day-card-row"><span>🏠 Stay</span><span class="tbd">Durness or Thurso AirBnB — link TBD</span></div>
            <div class="day-card-row"><span>📝 Notes</span><span>Sandwood Bay walk is 4 miles return on rough track — allow 2.5h total</span></div>
          </div>
        </div>
      </div>

      <!-- Day 10 -->
      <div class="timeline-item">
        <div class="timeline-spine">
          <div class="day-circle">10</div>
          <div class="timeline-line"></div>
        </div>
        <div class="day-card">
          <div class="day-card-header">
            <div>
              <div class="day-card-title">→ Inverness, Fly Out</div>
              <div class="day-card-meta">Departure day &middot; ~120 km &middot; ~2h</div>
            </div>
            <div class="day-card-badges">
              <span class="badge badge-region">Inverness</span>
            </div>
          </div>
          <div class="day-card-body">
            <div class="day-card-row"><span>📸 En route</span><span>Culloden Battlefield &middot; Loch Ness viewpoint</span></div>
            <div class="day-card-row"><span>✈ Depart</span><span>Inverness Airport (INV) — drop rental car at airport</span></div>
            <div class="day-card-row"><span>📝 Notes</span><span>Return car with full tank — nearest petrol station to INV is Dalcross (2 km)</span></div>
          </div>
        </div>
      </div>
```

- [ ] **Step 2: Open in browser and verify**

Verify:
- 10 day cards visible in vertical timeline
- Numbered circles connected by green lines
- Last card (Day 10) has no trailing line
- All badge colours correct (green region, blue nights)
- "TBD" stays are italic and muted

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add all 10 day cards to timeline"
```

---

### Task 6: Accommodation summary and Tips sections

**Files:**
- Modify: `index.html` — add stays + tips CSS and HTML after timeline

- [ ] **Step 1: Add stays and tips CSS inside `<style>` (after day card rules)**

```css
    /* ── Accommodation ────────────────────────────── */
    .stays-list {
      display: flex;
      flex-direction: column;
      gap: 8px;
    }
    .stay-row {
      background: var(--white);
      border-radius: 6px;
      padding: 10px 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: var(--shadow);
      font-size: 13px;
      gap: 16px;
    }
    .stay-row-label { font-weight: 700; color: var(--green-dark); }
    .stay-row-location { color: var(--text-mid); }

    /* ── Tips ─────────────────────────────────────── */
    .tips-list {
      background: var(--white);
      border-radius: 10px;
      padding: 20px 24px;
      box-shadow: var(--shadow);
      display: flex;
      flex-direction: column;
      gap: 10px;
      font-size: 13px;
      color: var(--text-mid);
    }
    .tips-list strong { color: var(--green-dark); }

    /* ── Back to top ──────────────────────────────── */
    .back-to-top {
      position: fixed;
      bottom: 28px;
      right: 28px;
      background: var(--green-dark);
      color: var(--white);
      border: none;
      border-radius: 50%;
      width: 44px;
      height: 44px;
      font-size: 20px;
      cursor: pointer;
      box-shadow: 0 2px 8px rgba(0,0,0,0.25);
      display: none;
      align-items: center;
      justify-content: center;
      text-decoration: none;
      line-height: 1;
    }
    .back-to-top.visible { display: flex; }
    .back-to-top:hover { background: var(--green-mid); }
```

- [ ] **Step 2: Replace `<!-- Stays, Tips added in later tasks -->` with stays + tips HTML**

```html
    <!-- Accommodation -->
    <h2 class="section-heading" id="stays">Stays</h2>
    <div class="stays-list">
      <div class="stay-row">
        <div><span class="stay-row-label">Night 1–2</span> &nbsp;<span class="stay-row-location">Glencoe area</span></div>
        <span class="tbd">AirBnB link TBD</span>
      </div>
      <div class="stay-row">
        <div><span class="stay-row-label">Night 3–5</span> &nbsp;<span class="stay-row-location">Portree, Isle of Skye</span></div>
        <span class="tbd">AirBnB link TBD</span>
      </div>
      <div class="stay-row">
        <div><span class="stay-row-label">Night 6–7</span> &nbsp;<span class="stay-row-location">Torridon area</span></div>
        <span class="tbd">AirBnB link TBD</span>
      </div>
      <div class="stay-row">
        <div><span class="stay-row-label">Night 8</span> &nbsp;<span class="stay-row-location">Assynt area</span></div>
        <span class="tbd">AirBnB link TBD</span>
      </div>
      <div class="stay-row">
        <div><span class="stay-row-label">Night 9</span> &nbsp;<span class="stay-row-location">Durness or Thurso</span></div>
        <span class="tbd">AirBnB link TBD</span>
      </div>
    </div>

    <!-- Tips -->
    <h2 class="section-heading" id="tips">Tips &amp; Links</h2>
    <div class="tips-list">
      <div>🚗 <strong>Car rental:</strong> Arnold Clark — one-way Edinburgh (EDI) → Inverness (INV). Book early for June.</div>
      <div>📷 <strong>Golden hour:</strong> June sunsets ~10pm, sunrises ~4:30am — pack a headtorch for early starts.</div>
      <div>🌦 <strong>Weather:</strong> Always carry full waterproofs. June averages 12–16°C. Wind is the real enemy.</div>
      <div>🛣 <strong>NC500 accommodation:</strong> Book at least 3–4 months ahead — fills up fast in June.</div>
      <div>🚧 <strong>Single-track roads:</strong> Most Highland roads are single-track with passing places. Add 30–50% to Google Maps estimates.</div>
      <div>🦟 <strong>Midges:</strong> Peak midge season — bring repellent (Smidge brand is best). Worst at dawn/dusk near water.</div>
      <div>⛽ <strong>Petrol:</strong> Fill up whenever you see a station in the far north — gaps of 50+ km are common.</div>
    </div>

  <!-- back to top button -->
  <a href="#top" class="back-to-top" id="backToTop" aria-label="Back to top">↑</a>
```

- [ ] **Step 3: Open in browser and verify**

Verify:
- 5 stay rows visible, all showing "TBD" in muted italic
- 7 tips visible with emoji icons
- Back-to-top button not yet visible (JS wires it up in Task 7)

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add accommodation summary and tips sections"
```

---

### Task 7: Light JS — smooth scroll, active nav, back-to-top

**Files:**
- Modify: `index.html` — replace `// JS added in Task 6` comment inside `<script>` with full JS

- [ ] **Step 1: Replace `// JS added in Task 6` with the following script**

```js
    // Smooth scroll for nav links
    document.querySelectorAll('a[href^="#"]').forEach(a => {
      a.addEventListener('click', e => {
        const target = document.querySelector(a.getAttribute('href'));
        if (!target) return;
        e.preventDefault();
        target.scrollIntoView({ behavior: 'smooth', block: 'start' });
      });
    });

    // Active nav highlight via IntersectionObserver
    const navLinks = document.querySelectorAll('.nav a');
    const sections = document.querySelectorAll('[id]');
    const observer = new IntersectionObserver(entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          navLinks.forEach(l => l.classList.remove('active'));
          const active = document.querySelector(`.nav a[href="#${entry.target.id}"]`);
          if (active) active.classList.add('active');
        }
      });
    }, { rootMargin: '-30% 0px -60% 0px' });
    sections.forEach(s => observer.observe(s));

    // Back-to-top button
    const btn = document.getElementById('backToTop');
    window.addEventListener('scroll', () => {
      btn.classList.toggle('visible', window.scrollY > 400);
    });
```

- [ ] **Step 2: Open in browser and verify**

Verify:
- Clicking a nav link scrolls smoothly to that section
- As you scroll through sections, the corresponding nav link turns white with underline
- After scrolling 400px, the ↑ button appears bottom-right
- Clicking ↑ scrolls smoothly back to top

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add smooth scroll, active nav, back-to-top JS"
```

---

### Task 8: Update CLAUDE.md and open Pull Request

**Files:**
- Modify: `CLAUDE.md` — tick off completed sections
- Open: Pull Request on GitHub

- [ ] **Step 1: Update CLAUDE.md — mark sections as complete**

In `CLAUDE.md`, change the Content Tracking checkboxes:

```markdown
### Sections planned
- [x] Trip overview (dates, travelers, summary)
- [x] Day-by-day itinerary
- [x] Map / route overview
- [x] Accommodation list
- [x] Key links and resources
```

Also add to the Decisions log:
```markdown
- 2026-04-02: Built index.html — Nature & Fresh theme, timeline layout, rich day cards, light JS
```

- [ ] **Step 2: Commit CLAUDE.md update**

```bash
git add CLAUDE.md
git commit -m "docs: mark all sections complete in CLAUDE.md"
```

- [ ] **Step 3: Read GitHub token**

```bash
cat ClaudeToken.txt
```

Use the token value as `GITHUB_TOKEN` in the next step.

- [ ] **Step 4: Push branch and open PR**

```bash
git push -u origin feature/trip-planner-html

GITHUB_TOKEN=<token-from-file> gh pr create \
  --title "Add Scotland 2026 trip planner HTML page" \
  --body "$(cat <<'EOF'
## Summary
- Single self-contained `index.html` with Nature & Fresh green theme
- Hero section with trip stats, sticky nav, visual route strip
- Vertical timeline with 10 rich day cards (photo spots, stays, notes)
- Accommodation summary and tips sections
- Light JS: smooth scroll, active nav highlight, back-to-top button
- Fully offline — no external dependencies

## Test plan
- [ ] Open `index.html` in browser — hero renders correctly
- [ ] Scroll down — nav sticks and highlights active section
- [ ] Click nav links — smooth scroll to sections
- [ ] Verify all 10 day cards present with correct content
- [ ] Verify ↑ button appears after scrolling 400px
- [ ] Verify page works with no internet connection

🤖 Generated with [Claude Code](https://claude.com/claude-code)
EOF
)"
```

---

## Self-Review

**Spec coverage:**
- ✅ Hero section with stats (Task 1)
- ✅ Sticky nav with active highlight (Task 2 + Task 7)
- ✅ Route overview offline strip (Task 3)
- ✅ Timeline with rich day cards (Task 4 + Task 5)
- ✅ Accommodation summary with TBD placeholders (Task 6)
- ✅ Tips & links section (Task 6)
- ✅ Light JS — smooth scroll, IntersectionObserver, back-to-top (Task 7)
- ✅ Single `index.html`, no external dependencies (all tasks)
- ✅ PR via GitHub, no direct merge to main (Task 8)
- ✅ Nature & Fresh green palette applied throughout

**Placeholder scan:** None. All day card content is fully written out. AirBnB links are intentionally "TBD" per spec.

**Type consistency:** No shared types — pure HTML/CSS/JS. CSS class names used consistently: `.day-card`, `.day-circle`, `.timeline-line`, `.badge`, `.tbd`, `.back-to-top`.
