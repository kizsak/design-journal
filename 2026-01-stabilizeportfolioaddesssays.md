# Design Journal — Stabilizing the Portfolio Architecture & Introducing Essay-Length Process Notes  
**Date:** 2026-01-07

## Context
Today’s work focused on stabilizing my portfolio’s underlying architecture after a series of cascading layout issues introduced during iterative visual refinement. While the neon/light-leak aesthetic was largely successful, structural fragility in the HTML, CSS, and JavaScript began to surface—especially as individual projects accumulated longer descriptions and more complex interactions.

This session became less about surface polish and more about **re-establishing a clear separation between layout, interaction, and content**.

---

## Problems Identified

### 1. Content Density vs. Visual Containers
Several computational image design pieces required extended process explanations that exceeded the height and visual logic of their background image panels. Attempts to “shrink to fit” via font size felt conceptually wrong and reduced readability.

**Insight:** The issue wasn’t typography—it was content architecture.

---

### 2. Carousel Image Cropping
Carousel images were being unintentionally cropped or stretched due to shared CSS rules with card layouts. While cards benefit from aggressive `object-fit: cover`, this behavior is counterproductive for artwork viewing.

**Resolution:** I separated styling logic for:
- **Cards** (aesthetic cropping acceptable)
- **Carousel images** (integrity and aspect ratio prioritized)

This reinforced the principle that **display intent should drive CSS decisions**, not visual reuse.

---

### 3. Caption & Process Notes Fragility
Captions and descriptions intermittently failed to display due to:
- Overloaded containers
- Hidden overflow rules
- Implicit height assumptions
- JavaScript attempting to manage both short and long content in the same region

This revealed a deeper structural flaw: **multiple semantic roles were being forced into a single UI area**.

---

## Key Design Decisions

### 1. Introducing a Dedicated Essay Panel
Rather than compressing complex explanations into the carousel sidebar, I introduced a persistent, page-level **“Process Notes” essay panel** below the gallery.

Each image now:
- Displays a **short caption + tools list** near the image
- Maps to a **separate essay template** for long-form process writing

This mirrors how physical exhibitions often separate wall labels from catalogs or essays.

---

### 2. Template-Driven Content Mapping
Each artwork now uses explicit data attributes:
- `data-desc` → short description template
- `data-essay` → long-form essay template

JavaScript swaps content dynamically based on the active image. This:
- Eliminates duplicated markup
- Reduces error risk
- Scales cleanly as projects are added

---

### 3. Visual Priority Corrections
On the About page, the profile image was visually underweighted relative to the surrounding gradients and navigation elements. Rather than restructuring the grid, I adjusted the image’s size constraints to restore balance.

**Takeaway:** Sometimes hierarchy problems are solved by *proportion*, not layout.

---

## Outcomes
- The portfolio is now **structurally more resilient**
- Long process narratives are readable without compromising visual clarity
- The carousel behaves predictably across aspect ratios
- The site now supports both **quick browsing** and **deep reading**
- CSS and JavaScript responsibilities are more clearly separated

---

## Reflections
This work reinforced an important lesson:  
> Visual complexity demands architectural simplicity.

As the portfolio matures, the primary challenge is no longer “making things look right,” but ensuring that **design intent, technical structure, and content scale together**. Today’s refactor creates space for future work without requiring constant repair.

---

## Next Steps
- Final pass on carousel image scaling across breakpoints
- Light accessibility audit (focus order, ARIA roles)
- Optional micro-interactions for essay transitions
- Continue migrating older pages to the essay-panel model
