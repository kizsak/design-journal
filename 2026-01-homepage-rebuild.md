# Homepage Rebuild – Light Leaks, Card Grid, and CSS Simplification
Date: 2026-01-07

## Context
I was rebuilding the front page of my *Digital & Computational Arts* portfolio after a series of layout and interaction issues. The page uses a grid of image-based cards with text overlays and a neon/light-leak aesthetic. Over time, incremental CSS changes made the layout fragile and difficult to debug.

This journal documents how I diagnosed the problems, simplified the structure, and rebuilt the homepage to be more stable while preserving the visual identity.

---

## Goals
- Restore the light-leak visual atmosphere across pages
- Ensure all homepage cards are fully clickable
- Align four cards horizontally on desktop
- Reduce CSS fragility and interaction bugs
- Separate visual effects from layout logic

---

## What Was Broken

### HTML Structure Issues
- `<header>` and `<section>` elements were accidentally placed inside `<head>`
- `<body>` opening tag was missing
- Browser auto-correction caused unpredictable layout behavior

### CSS Interaction Bugs
- `pointer-events: none` on `.card__content` prevented text hover and click behavior
- Absolutely positioned background layers sometimes intercepted clicks
- `height: 100%` on anchors relied on parent height instead of explicit positioning
- Excessive nesting increased z-index and stacking-context complexity

### Design-Level Problems
- Cards appeared clickable but did not behave reliably
- Debugging required tracking too many overlapping layers
- Visual effects were tightly coupled to layout mechanics

---

## Key Decisions

### 1. Simplify the Card Structure
Each card was reduced to a single `<a>` element that:
- holds the background image
- contains the text overlay
- uses a `::after` pseudo-element for shading

This eliminated unnecessary wrapper elements and reduced z-index conflicts.

---

### 2. Make the Entire Card Clickable by Construction
Instead of relying on inherited height, links were made structurally responsible for interaction by positioning them explicitly.

```css
.card__link {
  position: absolute;
  inset: 0;
}
