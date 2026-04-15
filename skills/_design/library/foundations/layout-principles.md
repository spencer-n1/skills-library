# Layout Principles

## Rating
- **Status**: foundational
- **Preferred contexts**: all
- **Avoid contexts**: none

---

## Core Layouts

**Single Column (Mobile-First):**
- Stack all content vertically
- Full-width sections
- Centered text

**Two Column:**
- Split: 50/50, 60/40, or 40/60
- Common: Text left, image right (or reverse)
- Gap: 32-64px

**Three Column:**
- Equal thirds for features/services
- Use sparingly (gets crowded on tablet)
- Gap: 24-32px

---

## Hero Layouts

**Full-Bleed Image:**
- Image covers 100% viewport
- Text overlaid with gradient
- Nav transparent over image

**Split Layout:**
- Left: Headline + CTA
- Right: Image or form
- 50/50 or 60/40 split

**Centered:**
- All content centered
- Max-width container
- Minimal, focused

---

## Section Patterns

**Alternating:**
- Section 1: Image left, text right
- Section 2: Text left, image right
- Creates visual rhythm

**Cards Grid:**
- 3 cards max per row
- Equal height cards
- Consistent padding

**Full-Width Band:**
- Breaks up alternating sections
- Stats bar, testimonials, CTA
- Contrasting background

---

## Z-Index Scale

- Background patterns: `z-0`
- Content: `z-10`
- Floating elements: `z-20`
- Navigation: `z-30`
- Modals/overlays: `z-40`
- Toasts/notifications: `z-50`

---

## Responsive Breakpoints

**Mobile:** < 640px
- Single column
- Stacked navigation
- Reduced spacing

**Tablet:** 640px - 1024px
- 2 columns where appropriate
- Simplified layouts

**Desktop:** > 1024px
- Full layouts
- Multi-column grids
- Hover states active
