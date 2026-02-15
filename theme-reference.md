# Dashboard Theme Reference

> **Purpose:** This document captures every visual design token from the Pinion-Staff dashboard so another AI (or developer) can replicate the exact look-and-feel in any framework (Next.js + Tailwind, etc.) without access to the original codebase.

## General Vibe

Dark, immersive glassmorphism dashboard with a single configurable accent color (default deep purple `#7060be`). Cards float on a near-black canvas (`#0f0f13`) with a subtle radial accent-color gradient wash. Surfaces use a consistent dark-navy tone (`#1a1a2e`) with frosted-glass `backdrop-filter: blur(10px)`. Micro-interactions include smooth lift-on-hover (`translateY(-5px)`), colored glow shadows, and accent-tinted borders that brighten on hover. The overall feel is **modern, dark-mode-only, with soft neon accents and depth created through layered translucency**.

---

## 1. CSS Custom Properties (Root Variables)

```css
:root {
  /* Primary accent — user-configurable, default purple */
  --accent-color: #7060be;
  /* RGB triplet for rgba() usage */
  --accent-color-rgb: 112, 96, 190;
}
```

All accent-derived colors use `rgba(var(--accent-color-rgb), <opacity>)` so changing one variable re-themes the entire UI.

---

## 2. Color Palette

### 2.1 Backgrounds

| Token | Value | Usage |
|---|---|---|
| `page-bg` | `#0f0f13` | Base page background (very dark blue-black) |
| `page-bg-gradient` | `radial-gradient(circle at top left, rgba(var(--accent-color-rgb), 0.2) 0%, rgba(var(--accent-color-rgb), 0.15) 50%, rgba(var(--accent-color-rgb), 0.1) 100%), #0f0f13` | Full page background with accent wash |
| `surface-primary` | `#1a1a2e` | Cards, navbar, footer, modals |
| `surface-secondary` | `rgba(24, 21, 31, 0.6)` / `#18151f` | Form inputs, inner settings cards, nested surfaces |
| `surface-tertiary` | `rgba(30, 27, 38, 0.6)` / `#1e1b26` | Appeal cards, report cards, deeper-nested panels |
| `surface-tertiary-solid` | `rgba(35, 32, 44, 0.6)` | Modal header/footer |
| `surface-subtle` | `rgba(255, 255, 255, 0.02)` | Punishment items, member list items, very faint surface |
| `surface-subtle-hover` | `rgba(255, 255, 255, 0.04)` | Hover state of subtle surfaces |
| `surface-hover` | `rgba(255, 255, 255, 0.05)` | Generic hover overlay |
| `surface-input-focus` | `rgba(30, 27, 38, 0.8)` | Input focus background |
| `surface-scrollbar-track` | `rgba(19, 17, 26, 0.8)` | Scrollbar track |

### 2.2 Accent Color Opacity Scale

Used everywhere for tinted backgrounds, borders, and glows:

```css
rgba(var(--accent-color-rgb), 0.03)  /* stat-card gradient overlay */
rgba(var(--accent-color-rgb), 0.05)  /* very faint hover tint */
rgba(var(--accent-color-rgb), 0.08)  /* decorative shapes */
rgba(var(--accent-color-rgb), 0.1)   /* card borders, navbar item hover bg, badge bg */
rgba(var(--accent-color-rgb), 0.15)  /* active nav item bg, button bg, badge bg, border hover */
rgba(var(--accent-color-rgb), 0.2)   /* page gradient start, punishment badge bg, border accent, scrollbar, button hover bg */
rgba(var(--accent-color-rgb), 0.25)  /* stronger button hover, hover emphasis */
rgba(var(--accent-color-rgb), 0.3)   /* border on focus/hover, glow shadows, scrollbar hover, preset borders */
rgba(var(--accent-color-rgb), 0.4)   /* strong glow box-shadows, staff badge glow */
rgba(var(--accent-color-rgb), 0.5)   /* navbar border, footer border, scrollbar hover */
```

### 2.3 Accent Color Preset Palette

Available for user customization — 8 preset options:

| Name | Hex |
|---|---|
| Default Purple | `#7060be` |
| Blue | `#3498db` |
| Green | `#2ecc71` |
| Red | `#e74c3c` |
| Orange | `#f39c12` |
| Violet | `#9b59b6` |
| Teal | `#1abc9c` |
| Pink | `#e91e63` |

### 2.4 Text Colors

| Token | Value | Usage |
|---|---|---|
| `text-primary` | `#ffffff` | Headings, stat values, usernames, primary text |
| `text-secondary` | `rgba(255, 255, 255, 0.9)` | Form labels, modal body text, slightly dimmed primary |
| `text-body` | `rgba(255, 255, 255, 0.85)` | Punishment reasons, body content |
| `text-muted` | `rgba(255, 255, 255, 0.7)` | Stat labels, footer text, descriptions, secondary info, nav items, chart labels |
| `text-subtle` | `rgba(255, 255, 255, 0.6)` | Timestamps, feature items, metadata |
| `text-faint` | `rgba(255, 255, 255, 0.5)` | "Last 24h" text, pagination ellipsis, inactive overlay text |
| `text-placeholder` | `rgba(255, 255, 255, 0.4)` | Input placeholders |
| `text-disabled` | `rgba(255, 255, 255, 0.3)` | Disabled pagination, faint dividers |
| `text-accent` | `var(--accent-color)` | Links, active nav items, icons, usernames, role labels |
| `text-stat-label` | `#908d96` | Stats page secondary labels |

### 2.5 Status / Semantic Colors

| Status | Color | Background (20% opacity) | Usage |
|---|---|---|---|
| **Success / Accepted** | `#48c774` | `rgba(72, 199, 116, 0.1)` | Alerts, appeal accepted badge, approve button |
| **Danger / Denied / Error** | `#f14668` / `#ff3860` | `rgba(241, 70, 104, 0.1)` | Alerts, appeal denied badge, deny button, remove buttons |
| **Danger (alt)** | `#d9534f` | `rgba(217, 83, 79, 0.15)` | Delete buttons, danger modal buttons |
| **Warning / Pending** | `#ffd700` | `rgba(255, 221, 87, 0.15)` | Pending appeal badges, pending status |
| **Info / Warning-alt** | `#ffa500` | `rgba(255, 170, 0, 0.1)` | Inactive overlay, appeal warning badges |
| **Ban** | `#ff6b6b` | `rgba(217, 83, 79, 0.2)` | Ban punishment badge |
| **Kick** | `#5bc0de` | `rgba(91, 192, 222, 0.2)` | Kick punishment badge |
| **Warn** | `#ffc107` | `rgba(255, 193, 7, 0.2)` + border `rgba(255, 193, 7, 0.3)` | Warn punishment badge |
| **Timeout** | `var(--accent-color)` | `rgba(var(--accent-color-rgb), 0.2)` | Timeout punishment badge |
| **Clear button red** | `#ff3b30` | `rgba(255, 59, 48, 0.1)` | Clear/reset button |

### 2.6 Discord Status Colors

| Status | Dot Color | Glow Shadow |
|---|---|---|
| Online | `#43b581` | `0 0 8px rgba(67, 181, 129, 0.3)` |
| Idle | `#faa61a` | `0 0 8px rgba(250, 166, 26, 0.3)` |
| DND | `#f04747` | `0 0 8px rgba(240, 71, 71, 0.3)` |
| Offline | `#747f8d` | `0 0 8px rgba(116, 127, 141, 0.3)` |

---

## 3. Typography

### 3.1 Font Families

```css
/* Primary — used in navbar partial, applied globally */
font-family: 'Rubik', sans-serif;

/* Secondary — used in body declarations across pages */
font-family: 'Inter', sans-serif;

/* Monospace — punishment IDs, code-like elements */
font-family: 'Roboto Mono', monospace;
```

**Google Fonts import:**
```html
<link href="https://fonts.googleapis.com/css2?family=Rubik:wght@400;500;700&display=swap" rel="stylesheet">
```

> **Note:** The navbar partial sets `html, body { font-family: 'Rubik', sans-serif }` which overrides the `'Inter'` declaration in individual page styles. The effective global font is **Rubik**. Use Inter as fallback or for body-heavy content pages.

### 3.2 Font Sizes

| Element | Size | Weight | Extra |
|---|---|---|---|
| Page title (`h1 .title`) | `1.75rem` (28px) | 600 | Login page |
| Section title (`.section-title`) | `1.25rem` (20px) | 600 | — |
| Chart/leaderboard title | `1.1rem` (17.6px) | 600 | — |
| Stat value (`.stat-value`) | `2.5rem` (40px) | 700 | `text-shadow: 0 2px 4px rgba(0,0,0,0.1)` |
| Stat value (stats page) | `1.25rem` (20px) | 600 | Smaller on stats cards |
| Server name | `1.25rem` (20px) | 600 | — |
| Member name | `1.1rem` (17.6px) | 600 | `letter-spacing: 0.02em` |
| Staff name | `1.1rem` (17.6px) | 600 | — |
| Error title | `1.8rem` (28.8px) | 600 | — |
| Error status code (watermark) | `8rem` (128px) | 800 | `color: rgba(accent, 0.05)` |
| Navbar username | `1rem` (16px) | 600 | `line-height: 1.2` |
| Body / form input text | `0.95rem` (15.2px) | 400 | — |
| Button text | `0.9rem` – `1.1rem` | 500–600 | Varies by button type |
| Stat label | `0.9rem` (14.4px) | 400 | `text-transform: uppercase; letter-spacing: 1px` |
| Badge text | `0.8rem` (12.8px) | 600 | `text-transform: uppercase; letter-spacing: 0.5px` |
| Tag text | `0.7rem` (11.2px) | 600 | `text-transform: uppercase; letter-spacing: 0.5px` |
| Status text (small) | `0.85rem` (13.6px) | 500–600 | — |
| "Last 24h" label | `0.8rem` (12.8px) | 400 | — |
| Navbar role label | `0.8rem` (12.8px) | 400 | `opacity: 0.9` |
| Subtitle | `1rem` (16px) | 400 | — |
| Copyright | `0.85rem` (13.6px) | 400 | `opacity: 0.7` |
| Footer body | `0.9rem` (14.4px) | 400 | — |
| Help text | `0.8rem` (12.8px) | 400 | Bulma `.is-size-7` |
| Appeal status badge | `1.2rem` (19.2px) | 700 | `letter-spacing: 1px; text-transform: uppercase` |
| Punishment ID (mono) | `0.8rem` (12.8px) | 600 | Monospace font |
| Error icon | `3.5rem` (56px) | — | Icon size, not text |

### 3.3 Line Heights

```
Default (Bulma):  ~1.5
Error message:    1.6
Body content:     1.5
Compact (badges): 1.2 (navbar username)
Card descriptions: 1.6
Appeal action desc: 1.4
```

---

## 4. Spacing & Layout

### 4.1 Spacing Scale (rem)

```
0.2rem    — nav item horizontal margin
0.25rem   — badge vertical padding, small gaps
0.3rem    — role badge vertical padding
0.35rem   — punishment badge vertical padding
0.4rem    — status item padding, filter select padding
0.5rem    — card gaps, nav padding, footer gap, small margins
0.6rem    — button padding (compact)
0.75rem   — card padding (inner), input padding, badge horizontal padding, button gap
0.85rem   — role badge horizontal padding
1rem      — navbar margin, section padding, card padding (inner), standard gap
1.25rem   — card padding (medium), staff card padding, settings card padding, button horizontal padding
1.5rem    — glass-card padding, section padding, form gap, settings card margin-bottom
2rem      — section gap, chart margin, empty state padding, stat title margin-bottom
2.5rem    — login container padding, error card padding
4rem      — chart bottom padding (extra for labels), empty state vertical padding
```

### 4.2 Container & Layout

```css
/* Page layout — sticky footer pattern */
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.section {
  flex: 1;
  padding: 1rem;
  margin: 0;
}

/* Bulma container — responsive max-width (default Bulma breakpoints):
   - ≤768px: full-width with padding
   - 769px–1023px: 960px
   - 1024px–1215px: 1152px
   - 1216px–1407px: 1344px
   - ≥1408px: 1344px
*/

/* Stat cards grid: 5-column using Bulma */
.columns.is-multiline > .column.is-one-fifth  /* 20% width each */

/* Stats page grid */
.stat-boxes {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 1rem;
}

/* Settings grid */
.settings-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.25rem;
}

/* Reports grid */
.reports-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
  gap: 1.5rem;
}

/* Leaderboard grid */
.leaderboard-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
}

/* Chart row: two charts side by side */
.chart-row {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
}
.half-width {
  flex: 1 1 calc(50% - 0.75rem);
  min-width: 300px;
}

/* Appeal actions grid */
.appeal-actions-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
  gap: 1.5rem;
}

/* Staff stats grid */
.staff-stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 1rem;
}
```

### 4.3 Responsive Breakpoints

```
1023px — Tablet: Navbar collapses to burger menu
768px  — Mobile: Single-column layouts, stacked cards, flex-direction: column
640px  — Small: Tighter stat grids
480px  — XS: Single-column status items, 2-column stat boxes
```

---

## 5. Borders & Shadows

### 5.1 Border Radius Scale

| Value | Usage |
|---|---|
| `4px` / `0.25rem` | Small elements, report ID badge, footer link |
| `6px` | Punishment badges, ID badges, color presets, metadata items |
| `8px` | Form inputs, buttons, nav items, scrollbar thumb, pagination links, filter selects, notifications, alerts |
| `10px` | Navbar avatar, appeal status badge, action buttons (large) |
| `12px` | Medium cards (stat-box, staff-card, report-card, appeal-card, leaderboard-card), search input, modal textarea, settings icon container, back button, navbar mobile menu |
| `14px` | Member avatar |
| `16px` | Glass cards, navbar, login container, modals (modal-card), error card, server icon |
| `24px` | Toggle slider (pill shape) |
| `50%` | Status dots, avatar circles, toggle knob |

### 5.2 Border Widths & Colors

```css
/* Default card border */
border: 1px solid rgba(var(--accent-color-rgb), 0.1);

/* Navbar & footer (more prominent) */
border: 1px solid rgba(var(--accent-color-rgb), 0.5);

/* Form inputs */
border: 1px solid rgba(var(--accent-color-rgb), 0.2);

/* Dashed file upload border */
border: 1px dashed rgba(var(--accent-color-rgb), 0.3);

/* Avatar border */
border: 2px solid var(--accent-color);
/* With padding: 2px for the gap effect */

/* Status dot border */
border: 2px solid #1a1625;
/* (Note: slightly different from #1a1a2e — matches darker bg behind avatar) */

/* Member card left accent bar (pseudo-element, appears on hover) */
width: 4px; background: linear-gradient(to bottom, var(--accent-color), transparent);

/* Report card top accent bar */
height: 4px; background: linear-gradient(to right, var(--accent-color), rgba(var(--accent-color-rgb), 0.5));

/* Section dividers */
border-bottom: 1px solid rgba(var(--accent-color-rgb), 0.1);
border-top: 1px solid rgba(255, 255, 255, 0.1);  /* pagination separator */
```

### 5.3 Box Shadows

```css
/* Glass card hover */
box-shadow: 0 8px 32px rgba(var(--accent-color-rgb), 0.15);

/* Login container / error card (resting) */
box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);

/* Glass card on reports page (resting) */
box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);

/* Member card (resting) */
box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);

/* Member card (hover) */
box-shadow: 0 6px 18px rgba(0, 0, 0, 0.15);

/* Report card (resting) */
box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);

/* Report card (hover) */
box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);

/* Discord login button (resting) */
box-shadow: 0 4px 15px rgba(var(--accent-color-rgb), 0.3);

/* Discord login button (hover) */
box-shadow: 0 8px 25px rgba(var(--accent-color-rgb), 0.4);

/* Save / action button (resting) */
box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);

/* Save button (hover) */
box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);

/* Action button (resting) */
box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);

/* Action button (hover) */
box-shadow: 0 4px 8px rgba(0, 0, 0, 0.25);

/* Large action buttons (accept/deny) resting */
box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);

/* Large action buttons (accept/deny) hover */
box-shadow: 0 6px 15px rgba(0, 0, 0, 0.25);

/* Pagination active */
box-shadow: 0 4px 10px rgba(var(--accent-color-rgb), 0.3);

/* Pagination hover */
box-shadow: 0 5px 15px rgba(var(--accent-color-rgb), 0.2);

/* Accent glow (ID badges, color pickers) */
box-shadow: 0 0 10px rgba(var(--accent-color-rgb), 0.2);
box-shadow: 0 0 15px rgba(var(--accent-color-rgb), 0.3);  /* hover */

/* Logo image */
box-shadow: 0 0 20px rgba(var(--accent-color-rgb), 0.2);

/* Avatar shadow */
box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);  /* resting */
box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3);  /* hover */

/* Staff badge glow animation */
box-shadow: 0 2px 6px rgba(var(--accent-color-rgb), 0.2);   /* 0% */
box-shadow: 0 2px 12px rgba(var(--accent-color-rgb), 0.5);  /* 100% */

/* Input focus glow */
box-shadow: 0 0 15px rgba(var(--accent-color-rgb), 0.15);

/* Focus ring (filter select) */
box-shadow: 0 0 0 2px rgba(var(--accent-color-rgb), 0.2);

/* Modal card */
box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);

/* Text shadow on stat values */
text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);

/* Text shadow on member names */
text-shadow: 0 1px 2px rgba(0, 0, 0, 0.3);
```

---

## 6. Components

### 6.1 Glass Card (Primary Container)

```css
.glass-card {
  background: #1a1a2e;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(var(--accent-color-rgb), 0.1);
  border-radius: 16px;
  padding: 1.5rem;
  transition: all 0.3s ease;
}
.glass-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 32px rgba(var(--accent-color-rgb), 0.15);
  border-color: var(--accent-color);
}
```

### 6.2 Stat Card

```css
.stat-card {
  /* Extends .glass-card */
  position: relative;
  overflow: hidden;
}
.stat-card::before {
  content: '';
  position: absolute; top: 0; left: 0;
  width: 100%; height: 100%;
  background: linear-gradient(45deg, transparent, rgba(var(--accent-color-rgb), 0.03));
  z-index: 0;
}
.stat-icon   { font-size: 1.8rem; color: var(--accent-color); opacity: 0.9; }
.stat-value  { font-size: 2.5rem; font-weight: 700; color: #fff; }
.stat-label  { font-size: 0.9rem; color: rgba(255,255,255,0.7); text-transform: uppercase; letter-spacing: 1px; }
```

### 6.3 Buttons

#### Primary / Accent Button (ghost style — the default pattern)
```css
background: rgba(var(--accent-color-rgb), 0.15);
color: var(--accent-color);
border: none;
border-radius: 8px;
padding: 0.6rem 1.25rem;
font-weight: 500;
font-size: 0.9rem;
transition: all 0.2s ease;
/* Hover: */
background: rgba(var(--accent-color-rgb), 0.25);
transform: translateY(-1px); /* or translateY(-2px) for larger buttons */
```

#### Solid Accent Button (login, primary CTA)
```css
background: var(--accent-color);
color: #ffffff;
padding: 1.25rem 2rem;
border-radius: 12px;
font-size: 1.1rem;
font-weight: 500;
box-shadow: 0 4px 15px rgba(var(--accent-color-rgb), 0.3);
/* Hover: */
background: rgba(var(--accent-color-rgb), 0.9);
transform: translateY(-2px);
box-shadow: 0 8px 25px rgba(var(--accent-color-rgb), 0.4);
/* Shimmer pseudo-element on hover */
```

#### Danger Button
```css
background: rgba(217, 83, 79, 0.15);
color: #d9534f;
border: none;
/* Hover: */
background: rgba(217, 83, 79, 0.25);
transform: translateY(-1px);
```

#### Success / Accept Button
```css
background: rgba(72, 199, 116, 0.15);
color: #48c774;
border: 1px solid rgba(72, 199, 116, 0.3);
/* Hover (fills solid): */
background: #48c774;
color: white;
transform: translateY(-3px);
```

#### Deny Button
```css
background: rgba(255, 56, 96, 0.15);
color: #ff3860;
border: 1px solid rgba(255, 56, 96, 0.3);
/* Hover (fills solid): */
background: #ff3860;
color: white;
transform: translateY(-3px);
```

#### Ghost / Cancel Button
```css
background: rgba(255, 255, 255, 0.05);
color: rgba(255, 255, 255, 0.7);
/* Hover: */
background: rgba(255, 255, 255, 0.1);
transform: translateY(-1px);
```

#### Outline Action Button (review, view)
```css
background: rgba(var(--accent-color-rgb), 0.1);
color: var(--accent-color);
border: 1px solid rgba(var(--accent-color-rgb), 0.2);
border-radius: 8px;
padding: 0.5rem 1.25rem;
font-weight: 600;
/* Hover (fills solid): */
background: var(--accent-color);
color: white;
transform: translateY(-2px);
```

#### Back Button
```css
background: rgba(var(--accent-color-rgb), 0.1);
color: var(--accent-color);
border: 1px solid rgba(var(--accent-color-rgb), 0.15);
border-radius: 12px;
padding: 0.75rem 1.25rem;
backdrop-filter: blur(8px);
/* Hover: */
transform: translateX(-5px);  /* slides left instead of up */
background: rgba(var(--accent-color-rgb), 0.15);
```

### 6.4 Navigation Bar

```css
.navbar {
  background: #1a1a2e;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(var(--accent-color-rgb), 0.5);
  margin: 1rem;
  border-radius: 16px;
  padding: 0.5rem;
}

/* Nav item (default) */
.navbar-item {
  color: rgba(255, 255, 255, 0.7);
  border-radius: 8px;
  margin: 0 0.2rem;
  padding: 0.5rem 1rem;
  background: transparent;
  transition: all 0.3s ease;
}

/* Hover */
.navbar-item:hover {
  background: rgba(var(--accent-color-rgb), 0.1);
  color: #ffffff;
}

/* Active */
.navbar-item.is-active {
  background: rgba(var(--accent-color-rgb), 0.15);
  color: var(--accent-color);
}

/* Icon in nav item */
.navbar-item .icon { color: var(--accent-color); margin-right: 0.5rem; }
.navbar-item:hover .icon i { transform: rotate(20deg); }

/* User profile chip */
.navbar-user-profile {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 12px;
  padding: 0.5rem 1rem;
  gap: 1rem;
}

/* Settings item (special) */
.settings-item {
  background: rgba(var(--accent-color-rgb), 0.15);
  border: 1px solid rgba(var(--accent-color-rgb), 0.3);
}
.settings-item:hover {
  background: rgba(var(--accent-color-rgb), 0.25);
  border-color: rgba(var(--accent-color-rgb), 0.5);
}
.settings-item:hover .icon i { transform: rotate(30deg); }

/* Mobile menu */
@media (max-width: 1023px) {
  .navbar-menu {
    background: rgba(255, 255, 255, 0.03);
    backdrop-filter: blur(10px);
    border-radius: 12px;
    margin-top: 0.5rem;
    padding: 0.5rem;
  }
}
```

### 6.5 Form Inputs

```css
.form-input, .form-select {
  background: rgba(24, 21, 31, 0.6);
  border: 1px solid rgba(var(--accent-color-rgb), 0.2);
  color: #ffffff;
  border-radius: 8px;
  padding: 0.75rem 1rem;
  height: 42px;
  font-size: 0.95rem;
  transition: all 0.3s ease;
}
.form-input:focus, .form-select:focus {
  border-color: var(--accent-color);
  box-shadow: 0 0 15px rgba(var(--accent-color-rgb), 0.15);
  background: rgba(30, 27, 38, 0.8);
  outline: none;
}
.form-input::placeholder {
  color: rgba(255, 255, 255, 0.4);
}

/* Search input (members page — more prominent) */
.search-input {
  background: rgba(30, 27, 38, 0.8);
  border: 1px solid rgba(var(--accent-color-rgb), 0.15);
  border-radius: 12px;
  padding: 0.75rem 1rem 0.75rem 2.5rem; /* space for icon */
  backdrop-filter: blur(8px);
}

/* Textarea (modal) */
.modal-textarea {
  background: rgba(24, 21, 31, 0.6);
  border: 1px solid rgba(var(--accent-color-rgb), 0.2);
  border-radius: 12px;
  min-height: 120px;
  padding: 1rem;
  resize: vertical;
}

/* Select dropdown */
.filter-select {
  appearance: none;
  background-image: url("data:image/svg+xml,...chevron-svg...");
  background-repeat: no-repeat;
  background-position: right 1rem center;
  background-size: 1em;
  padding-right: 2.5rem;
}

/* Select options */
option {
  background: #1e1b26;
  color: #ffffff;
}
```

### 6.6 Badges & Tags

```css
/* Punishment badge (generic) */
.punishment-badge {
  padding: 0.35rem 0.75rem;
  border-radius: 6px;
  font-weight: 600;
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
}

/* Variants — see Section 2.5 for colors */
.punishment-badge.ban     { bg: rgba(217,83,79,0.2);  color: #ff6b6b; }
.punishment-badge.kick    { bg: rgba(91,192,222,0.2);  color: #5bc0de; }
.punishment-badge.timeout { bg: rgba(accent,0.2);      color: accent;  }
.punishment-badge.warn    { bg: rgba(255,193,7,0.2);   color: #ffc107; border: 1px solid rgba(255,193,7,0.3); }

/* Role / member badge */
.member-role {
  background: rgba(var(--accent-color-rgb), 0.15);
  color: var(--accent-color);
  padding: 0.3rem 0.85rem;
  border-radius: 8px;
  font-size: 0.85rem;
  font-weight: 600;
  border: 1px solid rgba(var(--accent-color-rgb), 0.2);
}

/* Staff badge (premium feel with gradient) */
.staff-badge {
  background: linear-gradient(135deg, rgba(var(--accent-color-rgb), 0.3) 0%, rgba(var(--accent-color-rgb), 0.15) 100%);
  border: 1px solid rgba(var(--accent-color-rgb), 0.4);
  border-radius: 8px;
  padding: 4px 10px;
  font-size: 0.8rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  animation: badge-glow 3s infinite alternate;
}

/* ID badge (monospace, code-like) */
.punishment-id, .id-badge {
  font-family: 'Roboto Mono', monospace;
  background: rgba(var(--accent-color-rgb), 0.15);
  color: var(--accent-color);
  padding: 0.25rem 0.75rem;
  border-radius: 6px;
  font-size: 0.8rem;
  font-weight: 600;
  border: 1px solid rgba(var(--accent-color-rgb), 0.3);
  box-shadow: 0 0 10px rgba(var(--accent-color-rgb), 0.2);
}
.punishment-id:hover, .id-badge:hover {
  background: rgba(var(--accent-color-rgb), 0.25);
  box-shadow: 0 0 15px rgba(var(--accent-color-rgb), 0.3);
  color: #ffffff;
}

/* Status badges (appeal) */
.appeal-status-badge {
  font-size: 1.2rem;
  font-weight: 700;
  letter-spacing: 1px;
  padding: 0.5rem 1.25rem;
  border-radius: 10px;
  text-transform: uppercase;
}
.appeal-status-badge.is-pending  { bg: rgba(255,215,0,0.15);  color: #ffd700; border: 1px solid rgba(255,215,0,0.3);  }
.appeal-status-badge.is-accepted { bg: rgba(72,199,116,0.15);  color: #48c774; border: 1px solid rgba(72,199,116,0.3); }
.appeal-status-badge.is-denied   { bg: rgba(255,56,96,0.15);  color: #ff3860; border: 1px solid rgba(255,56,96,0.3);  }

/* Report status badge (small) */
.report-status-badge {
  font-size: 0.7rem;
  padding: 0.2rem 0.5rem;
  border-radius: 4px;
  font-weight: 600;
}
.report-status-approved { bg: rgba(72,199,116,0.2);  color: #48C774; border: 1px solid rgba(72,199,116,0.3); }
.report-status-denied   { bg: rgba(255,56,96,0.2);   color: #FF3860; border: 1px solid rgba(255,56,96,0.3);  }
.report-status-pending  { bg: rgba(255,221,87,0.2);  color: #FFD700; border: 1px solid rgba(255,221,87,0.3); }

/* Tag (generic) */
.tag {
  border-radius: 8px;
  padding: 0.5rem 1rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  font-size: 0.7rem;
}
```

### 6.7 Modal

```css
.modal-background {
  background: rgba(19, 17, 26, 0.8);
  backdrop-filter: blur(8px);
}
.modal-card {
  background: rgba(30, 27, 38, 0.95);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(var(--accent-color-rgb), 0.2);
  border-radius: 16px;
  max-width: 500px;  /* or 700px for larger modals */
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
}
.modal-card-head {
  background: rgba(35, 32, 44, 0.6);
  border-bottom: 1px solid rgba(var(--accent-color-rgb), 0.15);
  border-radius: 16px 16px 0 0;
  padding: 1.25rem;
}
.modal-card-title {
  color: #ffffff;
  font-size: 1.1rem;
  font-weight: 600;
}
.modal-card-body {
  background: none;
  padding: 1.5rem;
  color: rgba(255, 255, 255, 0.9);
  max-height: 70vh;  /* for larger modals */
}
.modal-card-foot {
  background: rgba(35, 32, 44, 0.6);
  border-top: 1px solid rgba(var(--accent-color-rgb), 0.15);
  border-radius: 0 0 16px 16px;
  padding: 1.25rem;
  justify-content: flex-end;
  gap: 0.75rem;
}
```

### 6.8 Alerts / Notifications

```css
.alert, .notification {
  padding: 0.75rem 1.25rem;
  border-radius: 8px;
  display: flex;
  align-items: center;
  gap: 0.75rem;
}
.alert.is-success, .notification.is-success {
  background: rgba(72, 199, 116, 0.1);
  border: 1px solid rgba(72, 199, 116, 0.2);
  color: #48c774;
}
.alert.is-danger, .notification.is-danger {
  background: rgba(241, 70, 104, 0.1);
  border: 1px solid rgba(241, 70, 104, 0.2);
  color: #f14668;
}
```

### 6.9 Info Notice

```css
.info-notice {
  background: rgba(var(--accent-color-rgb), 0.08);
  border: 1px solid rgba(var(--accent-color-rgb), 0.2);
  border-radius: 10px;
  padding: 1rem;
  display: flex;
  align-items: center;
  gap: 1rem;
  color: rgba(255, 255, 255, 0.9);
}
```

### 6.10 Toggle / Switch

```css
.toggle-slider {
  width: 50px;
  height: 24px;
  border-radius: 24px;
  background-color: rgba(255, 255, 255, 0.1);
  transition: 0.4s;
}
.toggle-slider::before {
  width: 18px;
  height: 18px;
  left: 3px;
  bottom: 3px;
  background-color: white;
  border-radius: 50%;
  transition: 0.4s;
}
input:checked + .toggle-slider {
  background-color: var(--accent-color);
}
input:checked + .toggle-slider::before {
  transform: translateX(26px);
}
```

### 6.11 Pagination

```css
.pagination-link, .pagination-previous, .pagination-next {
  background: rgba(var(--accent-color-rgb), 0.1);
  border: 1px solid rgba(var(--accent-color-rgb), 0.2);
  color: rgba(255, 255, 255, 0.8);
  border-radius: 6px;  /* links */ or 8px /* prev/next */
  font-weight: 600;
  transition: all 0.3s ease;
}
/* Hover */
  background: rgba(var(--accent-color-rgb), 0.2);
  color: #ffffff;
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(var(--accent-color-rgb), 0.2);

/* Active/Current */
.pagination-link.is-current {
  background: var(--accent-color);
  border-color: var(--accent-color);
  box-shadow: 0 4px 10px rgba(var(--accent-color-rgb), 0.3);
}

/* Disabled */
.pagination-previous.is-disabled, .pagination-next.is-disabled {
  background: rgba(255, 255, 255, 0.05);
  color: rgba(255, 255, 255, 0.3);
  border-color: rgba(255, 255, 255, 0.1);
  pointer-events: none;
}
```

### 6.12 Empty State

```css
.empty-state {
  padding: 4rem 2rem;
  text-align: center;
  background: rgba(30, 27, 38, 0.3);
  border-radius: 12px;
  border: 1px dashed rgba(var(--accent-color-rgb), 0.2);
}
.empty-state i {
  font-size: 3rem;
  color: rgba(var(--accent-color-rgb), 0.3);
  margin-bottom: 1.5rem;
}
.empty-state-title {
  color: rgba(255, 255, 255, 0.9);
  font-size: 1.2rem;
  font-weight: 600;
}
.empty-state-text {
  color: rgba(255, 255, 255, 0.6);
  max-width: 400px;
}
```

### 6.13 Footer

```css
.modern-footer {
  background: #1a1a2e;
  backdrop-filter: blur(10px);
  border-top: 1px solid rgba(var(--accent-color-rgb), 0.5);
  padding: 1rem 0;
  margin-top: auto;
}
.footer-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.7);
}
/* Footer link — animated underline */
.plex-staff-link {
  color: var(--accent-color);
  font-weight: 500;
  transition: all 0.3s ease;
  position: relative;
  padding: 0.2rem 0.4rem;
  border-radius: 4px;
}
.plex-staff-link:hover {
  color: #ffffff;
  background: rgba(var(--accent-color-rgb), 0.1);
}
.plex-staff-link::before {
  /* Animated underline that scales from right to left */
  content: '';
  position: absolute;
  bottom: 0; left: 0;
  width: 100%; height: 1px;
  background: var(--accent-color);
  transform: scaleX(0);
  transform-origin: right;
  transition: transform 0.3s ease;
}
.plex-staff-link:hover::before {
  transform: scaleX(1);
  transform-origin: left;
}
```

### 6.14 Scrollbar

```css
/* Global scrollbar (from navbar partial) */
::-webkit-scrollbar { width: 10px; height: 10px; }
::-webkit-scrollbar-track {
  background: rgba(19, 17, 26, 0.8);
  border-radius: 8px;
}
::-webkit-scrollbar-thumb {
  background: rgba(var(--accent-color-rgb), 0.3);
  border: 2px solid rgba(19, 17, 26, 0.8);
  border-radius: 8px;
}
::-webkit-scrollbar-thumb:hover {
  background: rgba(var(--accent-color-rgb), 0.5);
}

/* Compact scrollbar (home page, inner panels) */
::-webkit-scrollbar { width: 6px; }
::-webkit-scrollbar-track { background: rgba(255,255,255,0.02); border-radius: 3px; }
::-webkit-scrollbar-thumb { background: var(--accent-color); border-radius: 3px; }

/* Tiny scrollbar (report reason) */
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-thumb { background: rgba(var(--accent-color-rgb), 0.5); border-radius: 2px; }
```

### 6.15 Settings Card (Icon Grid)

```css
.settings-card {
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(var(--accent-color-rgb), 0.1);
  border-radius: 12px;
  padding: 1.5rem;
  cursor: pointer;
  transition: all 0.3s ease;
  /* Staggered fade-in animation */
  opacity: 0;
  animation: fadeIn 0.3s ease forwards;
  animation-delay: calc(var(--index) * 0.1s); /* nth-child based */
}
.settings-card:hover {
  background: rgba(255, 255, 255, 0.04);
  transform: translateY(-5px);
  border-color: rgba(var(--accent-color-rgb), 0.3);
  box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
}
.settings-card-icon {
  width: 50px;
  height: 50px;
  background: rgba(var(--accent-color-rgb), 0.1);
  border-radius: 12px;
  font-size: 1.5rem;
  color: var(--accent-color);
}
.settings-card:hover .settings-card-icon {
  background: rgba(var(--accent-color-rgb), 0.2);
  transform: scale(1.05);
}
```

### 6.16 File Upload

```css
.file-input-label {
  background: rgba(30, 27, 38, 0.6);
  border: 1px dashed rgba(var(--accent-color-rgb), 0.3);
  border-radius: 8px;
  padding: 1.25rem;
  text-align: center;
  cursor: pointer;
  color: rgba(255, 255, 255, 0.7);
}
.file-input-label:hover {
  background: rgba(var(--accent-color-rgb), 0.05);
  border-color: var(--accent-color);
}
.file-input-label i {
  font-size: 2rem;
  color: var(--accent-color);
}
.file-preview {
  background: rgba(30, 27, 38, 0.4);
  border-radius: 8px;
  padding: 0.75rem;
}
```

### 6.17 Time Selector (Tab-style)

```css
.time-selector {
  background: #1a1a2e;
  border-radius: 12px;
  padding: 0.75rem;
  width: fit-content;
  margin: 0 auto;
}
.time-option {
  padding: 0.5rem 1rem;
  border-radius: 8px;
  color: rgba(255, 255, 255, 0.7);
  font-weight: 500;
  min-width: 80px;
  text-align: center;
}
.time-option:hover {
  color: #ffffff;
  background: rgba(var(--accent-color-rgb), 0.1);
}
.time-option.active {
  color: #ffffff;
  background: rgba(var(--accent-color-rgb), 0.2);
}
```

---

## 7. Effects & Transitions

### 7.1 Transitions

```css
/* Standard — used on almost everything */
transition: all 0.3s ease;

/* Quick — buttons, small interactive elements */
transition: all 0.2s ease;

/* Specific property transitions */
transition: transform 0.3s ease;    /* icons, nav arrows */
transition: opacity 0.3s ease;      /* fade effects */
transition: 0.4s;                   /* toggle switches */

/* Shimmer effect on login button */
transition: 0.5s;  /* the ::before pseudo-element sweep */
```

### 7.2 Hover Transforms

```css
/* Card lift */
transform: translateY(-5px);    /* glass cards, settings cards, report cards */
transform: translateY(-3px);    /* action buttons (large), error buttons */
transform: translateY(-2px);    /* buttons, stat boxes, member cards, pagination */
transform: translateY(-1px);    /* compact buttons, staff cards */

/* Slide effects */
transform: translateX(5px);     /* punishment items, member cards, appeal cards (hover) */
transform: translateX(-5px);    /* back button (hover) */
transform: translateX(-3px);    /* back button icon (hover), pagination prev icon */
transform: translateX(3px);     /* pagination next icon */

/* Scale */
transform: scale(1.05);         /* avatars, settings icons, color preview */
transform: scale(1.1);          /* color presets */

/* Icon rotation */
transform: rotate(20deg);       /* nav item icons */
transform: rotate(30deg);       /* settings gear icon */

/* 3D perspective (login/error cards) */
transform: perspective(1000px) rotateX(Xdeg) rotateY(Ydeg);
/* X = (mouseY - centerY) / 40, Y = (centerX - mouseX) / 40 */

/* Brightness on hover */
filter: brightness(120%);       /* action buttons */
```

### 7.3 Keyframe Animations

```css
/* Fade in (staggered card entrance, alert appearance) */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(-10px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* Fade out (alert dismissal) */
@keyframes fadeOut {
  from { opacity: 1; transform: translateY(0); }
  to   { opacity: 0; transform: translateY(-10px); }
}

/* Pulse (loading, error icon, login glow) */
@keyframes pulse {
  0%   { transform: scale(1); }
  50%  { transform: scale(1.05); }  /* or scale(1.1) for error icon */
  100% { transform: scale(1); }
}

/* Float (login page background stars) */
@keyframes float {
  0%, 100% { transform: translateY(0) translateX(0); }
  50%      { transform: translateY(-20px) translateX(10px); }
}

/* Bounce (Discord icon in login button) */
@keyframes bounce {
  from { transform: translateY(0); }
  to   { transform: translateY(-4px); }
}

/* Badge glow (staff badge) */
@keyframes badge-glow {
  0%   { box-shadow: 0 2px 6px rgba(var(--accent-color-rgb), 0.2); }
  100% { box-shadow: 0 2px 12px rgba(var(--accent-color-rgb), 0.5); }
}

/* Status dot pulse (online/idle/dnd indicators) */
@keyframes pulse-green {
  0%   { box-shadow: 0 0 0 0 rgba(67, 181, 129, 0.4); }
  70%  { box-shadow: 0 0 0 6px rgba(67, 181, 129, 0); }
  100% { box-shadow: 0 0 0 0 rgba(67, 181, 129, 0); }
}
@keyframes pulse-yellow {
  0%   { box-shadow: 0 0 0 0 rgba(250, 166, 26, 0.4); }
  70%  { box-shadow: 0 0 0 6px rgba(250, 166, 26, 0); }
  100% { box-shadow: 0 0 0 0 rgba(250, 166, 26, 0); }
}
@keyframes pulse-red {
  0%   { box-shadow: 0 0 0 0 rgba(240, 71, 71, 0.4); }
  70%  { box-shadow: 0 0 0 6px rgba(240, 71, 71, 0); }
  100% { box-shadow: 0 0 0 0 rgba(240, 71, 71, 0); }
}
```

### 7.4 Glassmorphism / Blur

```css
/* Primary surface blur */
backdrop-filter: blur(10px);   /* glass cards, navbar, footer, modal-card, login container */

/* Overlay blur */
backdrop-filter: blur(8px);    /* modal background, back button, search input, mobile menu */

/* Lighter blur */
backdrop-filter: blur(4px);    /* action button.view */
```

### 7.5 Gradients

```css
/* Page background */
radial-gradient(circle at top left, rgba(accent, 0.2) 0%, rgba(accent, 0.15) 50%, rgba(accent, 0.1) 100%), #0f0f13

/* Stat card overlay */
linear-gradient(45deg, transparent, rgba(accent, 0.03))

/* Member card left border (hover reveal) */
linear-gradient(to bottom, var(--accent-color), transparent)

/* Report card top bar */
linear-gradient(to right, var(--accent-color), rgba(accent, 0.5))

/* Staff badge */
linear-gradient(135deg, rgba(accent, 0.3) 0%, rgba(accent, 0.15) 100%)

/* Login button shimmer (pseudo ::before) */
linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent)

/* Decorative shapes */
radial-gradient(circle, rgba(accent, 0.1-0.2) 0%, rgba(accent, 0) 70%)
```

### 7.6 Decorative Elements

```css
/* Login page floating stars */
.star {
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  width: 5–15px (random);
  opacity: 0–0.5 (random);
  animation: float 8s infinite ease-in-out;
  animation-delay: 0–8s (random);
}

/* Login page decorative shapes */
.circle: 150px, border-radius: 50%, radial-gradient accent glow
.square: 100px, border-radius: 16px, rgba(accent, 0.08), rotated 20deg
.dots: 180px, dot grid pattern via background-image radial-gradient, 18px spacing

/* Login page glow follower */
.glow: 150px circle, radial-gradient accent, follows cursor, pulses when idle
```

---

## 8. Chart.js Theme (Data Visualization)

```javascript
// Chart background
backgroundColor: 'rgba(26, 26, 46, 0.9)'  // tooltip bg

// Grid lines
gridColor: 'rgba(255, 255, 255, 0.05)'

// Tick labels
tickColor: 'rgba(255, 255, 255, 0.7)'
tickFontSize: 11

// Legend labels
legendColor: 'rgba(255, 255, 255, 0.8)'
legendFontSize: 11

// Tooltip
tooltipBg: 'rgba(26, 26, 46, 0.9)'
tooltipBorder: 'rgba(var(--accent-color-rgb), 0.3)'
tooltipBorderWidth: 1
tooltipCornerRadius: 8
tooltipPadding: 10
tooltipTextColor: 'rgba(255, 255, 255, 0.9)'

// Line chart elements
lineTension: 0.4
lineBorderWidth: 3
linePointRadius: 3
linePointHoverRadius: 5
linePointBorderWidth: 2
lineFill: 'start'  // area fill under lines
```

---

## 9. Dark/Light Mode

**This theme is dark-mode only.** There is no light mode palette. The entire design system assumes a dark background. If you need a light mode, you would need to invert the background layers and adjust text/surface opacity values accordingly.

---

## 10. Tailwind CSS Config Snippet

```js
// tailwind.config.js
const config = {
  theme: {
    extend: {
      colors: {
        // Page backgrounds
        'page': '#0f0f13',
        'surface': {
          DEFAULT: '#1a1a2e',
          secondary: '#18151f',
          tertiary: '#1e1b26',
          input: 'rgba(24, 21, 31, 0.6)',
        },
        // Accent (use CSS variable for dynamic theming)
        'accent': {
          DEFAULT: '#7060be',
          blue: '#3498db',
          green: '#2ecc71',
          red: '#e74c3c',
          orange: '#f39c12',
          violet: '#9b59b6',
          teal: '#1abc9c',
          pink: '#e91e63',
        },
        // Semantic
        'success': '#48c774',
        'danger': '#f14668',
        'warning': '#ffd700',
        'info': '#ffa500',
        // Punishment
        'ban': '#ff6b6b',
        'kick': '#5bc0de',
        'warn': '#ffc107',
        // Discord status
        'online': '#43b581',
        'idle': '#faa61a',
        'dnd': '#f04747',
        'offline': '#747f8d',
      },
      fontFamily: {
        sans: ['Rubik', 'Inter', 'sans-serif'],
        mono: ['Roboto Mono', 'monospace'],
      },
      fontSize: {
        'stat-value': ['2.5rem', { fontWeight: '700' }],
        'section-title': ['1.25rem', { fontWeight: '600' }],
        'card-title': ['1.1rem', { fontWeight: '600' }],
        'badge': ['0.8rem', { fontWeight: '600', letterSpacing: '0.5px' }],
        'tag': ['0.7rem', { fontWeight: '600', letterSpacing: '0.5px' }],
      },
      borderRadius: {
        'card': '16px',
        'card-md': '12px',
        'card-sm': '8px',
        'badge': '6px',
        'pill': '24px',
      },
      backdropBlur: {
        'card': '10px',
        'overlay': '8px',
        'subtle': '4px',
      },
      boxShadow: {
        'card-hover': '0 8px 32px rgba(112, 96, 190, 0.15)',
        'card-rest': '0 8px 32px rgba(0, 0, 0, 0.2)',
        'card-sm': '0 4px 12px rgba(0, 0, 0, 0.1)',
        'button': '0 4px 6px rgba(0, 0, 0, 0.1)',
        'button-hover': '0 6px 8px rgba(0, 0, 0, 0.15)',
        'glow': '0 0 10px rgba(112, 96, 190, 0.2)',
        'glow-hover': '0 0 15px rgba(112, 96, 190, 0.3)',
        'modal': '0 8px 32px rgba(0, 0, 0, 0.4)',
        'input-focus': '0 0 15px rgba(112, 96, 190, 0.15)',
        'pagination-active': '0 4px 10px rgba(112, 96, 190, 0.3)',
      },
      animation: {
        'fade-in': 'fadeIn 0.3s ease forwards',
        'fade-out': 'fadeOut 0.3s ease forwards',
        'pulse': 'pulse 2s infinite',
        'float': 'float 8s infinite ease-in-out',
        'bounce-sm': 'bounce 1s infinite alternate',
        'badge-glow': 'badge-glow 3s infinite alternate',
        'pulse-green': 'pulse-green 2s infinite',
        'pulse-yellow': 'pulse-yellow 2s infinite',
        'pulse-red': 'pulse-red 2s infinite',
      },
      keyframes: {
        fadeIn: {
          from: { opacity: '0', transform: 'translateY(-10px)' },
          to: { opacity: '1', transform: 'translateY(0)' },
        },
        fadeOut: {
          from: { opacity: '1', transform: 'translateY(0)' },
          to: { opacity: '0', transform: 'translateY(-10px)' },
        },
        pulse: {
          '0%': { transform: 'scale(1)' },
          '50%': { transform: 'scale(1.05)' },
          '100%': { transform: 'scale(1)' },
        },
        float: {
          '0%, 100%': { transform: 'translateY(0) translateX(0)' },
          '50%': { transform: 'translateY(-20px) translateX(10px)' },
        },
        bounce: {
          from: { transform: 'translateY(0)' },
          to: { transform: 'translateY(-4px)' },
        },
        'badge-glow': {
          '0%': { boxShadow: '0 2px 6px rgba(112, 96, 190, 0.2)' },
          '100%': { boxShadow: '0 2px 12px rgba(112, 96, 190, 0.5)' },
        },
        'pulse-green': {
          '0%': { boxShadow: '0 0 0 0 rgba(67, 181, 129, 0.4)' },
          '70%': { boxShadow: '0 0 0 6px rgba(67, 181, 129, 0)' },
          '100%': { boxShadow: '0 0 0 0 rgba(67, 181, 129, 0)' },
        },
        'pulse-yellow': {
          '0%': { boxShadow: '0 0 0 0 rgba(250, 166, 26, 0.4)' },
          '70%': { boxShadow: '0 0 0 6px rgba(250, 166, 26, 0)' },
          '100%': { boxShadow: '0 0 0 0 rgba(250, 166, 26, 0)' },
        },
        'pulse-red': {
          '0%': { boxShadow: '0 0 0 0 rgba(240, 71, 71, 0.4)' },
          '70%': { boxShadow: '0 0 0 6px rgba(240, 71, 71, 0)' },
          '100%': { boxShadow: '0 0 0 0 rgba(240, 71, 71, 0)' },
        },
      },
      transitionTimingFunction: {
        'ease': 'ease',
      },
      transitionDuration: {
        '200': '200ms',
        '300': '300ms',
        '400': '400ms',
        '500': '500ms',
      },
    },
  },
};

export default config;
```

---

## 11. CSS Variable Definitions (Copy-Paste Ready)

```css
:root {
  /* ── Accent (dynamic) ──────────────────────── */
  --accent-color: #7060be;
  --accent-color-rgb: 112, 96, 190;

  /* ── Backgrounds ────────────────────────────── */
  --bg-page: #0f0f13;
  --bg-surface: #1a1a2e;
  --bg-surface-secondary: rgba(24, 21, 31, 0.6);
  --bg-surface-tertiary: rgba(30, 27, 38, 0.6);
  --bg-surface-modal-header: rgba(35, 32, 44, 0.6);
  --bg-surface-subtle: rgba(255, 255, 255, 0.02);
  --bg-surface-subtle-hover: rgba(255, 255, 255, 0.04);
  --bg-surface-hover: rgba(255, 255, 255, 0.05);
  --bg-input: rgba(24, 21, 31, 0.6);
  --bg-input-focus: rgba(30, 27, 38, 0.8);
  --bg-modal-overlay: rgba(19, 17, 26, 0.8);
  --bg-scrollbar-track: rgba(19, 17, 26, 0.8);

  /* ── Text ───────────────────────────────────── */
  --text-primary: #ffffff;
  --text-secondary: rgba(255, 255, 255, 0.9);
  --text-body: rgba(255, 255, 255, 0.85);
  --text-muted: rgba(255, 255, 255, 0.7);
  --text-subtle: rgba(255, 255, 255, 0.6);
  --text-faint: rgba(255, 255, 255, 0.5);
  --text-placeholder: rgba(255, 255, 255, 0.4);
  --text-disabled: rgba(255, 255, 255, 0.3);

  /* ── Borders ────────────────────────────────── */
  --border-default: rgba(var(--accent-color-rgb), 0.1);
  --border-input: rgba(var(--accent-color-rgb), 0.2);
  --border-hover: rgba(var(--accent-color-rgb), 0.3);
  --border-prominent: rgba(var(--accent-color-rgb), 0.5);
  --border-muted: rgba(255, 255, 255, 0.1);

  /* ── Semantic Colors ────────────────────────── */
  --color-success: #48c774;
  --color-danger: #f14668;
  --color-danger-alt: #d9534f;
  --color-warning: #ffd700;
  --color-info: #ffa500;

  /* ── Punishment Colors ──────────────────────── */
  --color-ban: #ff6b6b;
  --color-kick: #5bc0de;
  --color-warn: #ffc107;

  /* ── Discord Status ─────────────────────────── */
  --color-online: #43b581;
  --color-idle: #faa61a;
  --color-dnd: #f04747;
  --color-offline: #747f8d;

  /* ── Radius ─────────────────────────────────── */
  --radius-sm: 4px;
  --radius-badge: 6px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;
  --radius-pill: 24px;
  --radius-circle: 50%;

  /* ── Shadows ────────────────────────────────── */
  --shadow-card-hover: 0 8px 32px rgba(var(--accent-color-rgb), 0.15);
  --shadow-card-rest: 0 8px 32px rgba(0, 0, 0, 0.2);
  --shadow-sm: 0 4px 12px rgba(0, 0, 0, 0.1);
  --shadow-md: 0 4px 15px rgba(0, 0, 0, 0.15);
  --shadow-modal: 0 8px 32px rgba(0, 0, 0, 0.4);
  --shadow-input-focus: 0 0 15px rgba(var(--accent-color-rgb), 0.15);
  --shadow-glow: 0 0 10px rgba(var(--accent-color-rgb), 0.2);
  --shadow-glow-hover: 0 0 15px rgba(var(--accent-color-rgb), 0.3);

  /* ── Transitions ────────────────────────────── */
  --transition-fast: all 0.2s ease;
  --transition-base: all 0.3s ease;
  --transition-slow: all 0.5s ease;

  /* ── Blur ───────────────────────────────────── */
  --blur-card: blur(10px);
  --blur-overlay: blur(8px);
  --blur-subtle: blur(4px);
}
```

---

## 12. Icon Library

**Font Awesome 6.4.0** (Free, solid + brands)

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
```

Common icons used:
- `fa-home`, `fa-users`, `fa-chart-bar`, `fa-gavel`, `fa-flag`, `fa-search`, `fa-id-card`, `fa-cog`
- `fa-ban`, `fa-shoe-prints`, `fa-exclamation-triangle`, `fa-clock`, `fa-comment-alt`
- `fa-save`, `fa-paint-brush`, `fa-palette`, `fa-arrow-left`, `fa-trash-alt`
- `fa-cloud-upload-alt`, `fa-check-circle`, `fa-exclamation-circle`
- `fa-history`, `fa-hashtag`, `fa-hourglass-start`, `fa-sign-out-alt`
- `fab fa-discord`

---

## 13. Quick Reference: Component Patterns

| Pattern | Background | Border | Radius | Padding | Hover |
|---|---|---|---|---|---|
| Glass Card | `#1a1a2e` | `accent/0.1` | 16px | 1.5rem | lift -5px, glow shadow, border → accent |
| Settings Card | `white/0.02` | `accent/0.1` | 12px | 1.5rem | lift -5px, bg → white/0.04 |
| List Item | `white/0.02` | `accent/0.1` | 12px | 1rem | slide +5px, bg → white/0.04, border → accent |
| Button (accent ghost) | `accent/0.15` | none | 8px | 0.6rem 1.25rem | bg → accent/0.25, lift -2px |
| Button (accent solid) | `accent` | none | 12px | 1.25rem 2rem | bg → accent/0.9, lift -2px, glow |
| Button (outline) | `accent/0.1` | `accent/0.2` | 8px | 0.5rem 1.25rem | bg → accent solid, color → white |
| Nav Item | transparent | none | 8px | 0.5rem 1rem | bg → accent/0.1, color → white |
| Form Input | `rgba(24,21,31,0.6)` | `accent/0.2` | 8px | 0.75rem 1rem | border → accent, glow shadow |
| Badge | `status-color/0.2` | sometimes `status/0.3` | 6px | 0.35rem 0.75rem | — |
| Modal | `rgba(30,27,38,0.95)` | `accent/0.2` | 16px | — | — |
| Alert | `status/0.1` | `status/0.2` | 8px | 0.75rem 1.25rem | — |
