# Layout Patterns Library
## Extracted from The First The Last Agency Research

---

## Pattern 1: Asymmetric Two-Column (Jesko Jets, YODEZEEN)

### Description
Two-column layout with unequal widths, creating visual tension and hierarchy.

### Visual Structure
```
┌─────────────────────────────────────────┐
│                                         │
│  ┌──────────────────┐ ┌──────────────┐  │
│  │                  │ │              │  │
│  │   HEADLINE       │ │   [IMAGE]    │  │
│  │   Large text     │ │              │  │
│  │   content here   │ │              │  │
│  │                  │ │              │  │
│  │                  │ │              │  │
│  └──────────────────┘ └──────────────┘  │
│         60%                40%          │
│                                         │
└─────────────────────────────────────────┘
```

### Variations
| Ratio | Use Case | Visual Effect |
|-------|----------|---------------|
| 60/40 | Standard content | Balanced asymmetry |
| 70/30 | Text-heavy | Content dominance |
| 50/50 | Equal pairing | Balance with tension |
| 40/60 | Image-forward | Visual emphasis |

### Implementation
```css
.asymmetric-layout {
  display: grid;
  grid-template-columns: 6fr 4fr;
  gap: 60px;
  align-items: center;
  padding: 120px 40px;
}

/* Variant: Image left */
.asymmetric-layout--reverse {
  grid-template-columns: 4fr 6fr;
}

/* Responsive */
@media (max-width: 768px) {
  .asymmetric-layout {
    grid-template-columns: 1fr;
    gap: 40px;
  }
}
```

### Base44 Implementation
```
Create an asymmetric two-column layout:
- Grid: 60% text / 40% image (or reverse)
- Large gap (60px) between columns
- Vertical center alignment
- Full-bleed section padding (120px vertical)
- Responsive: Stack on tablet/mobile
- Apply to: About sections, features, product showcases
```

---

## Pattern 2: Full-Bleed Image with Overlaid Text (All Sites)

### Description
Edge-to-edge imagery with text positioned strategically over the image, creating depth and immersion.

### Visual Structure
```
┌─────────────────────────────────────────┐
│ ██████████████████████████████████████ │
│ ██████████████████████████████████████ │
│ ████                             █████ │
│ ████  HEADLINE                   █████ │
│ ████  Subtext here               █████ │
│ ████                             █████ │
│ ████                    [CTA]    █████ │
│ ██████████████████████████████████████ │
│ ██████████████████████████████████████ │
└─────────────────────────────────────────┘
        [FULL-BLEED BACKGROUND IMAGE]
```

### Positioning Variants
| Position | Best For | Readability |
|----------|----------|-------------|
| Center | Hero statements | High (needs overlay) |
| Bottom-left | CTAs | High |
| Top-left | Editorial | Medium |
| Mixed | Complex layouts | Careful contrast needed |

### Implementation
```css
.full-bleed-section {
  position: relative;
  min-height: 80vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.full-bleed-section img {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 0;
}

.full-bleed-section .overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.4);
  z-index: 1;
}

.full-bleed-section .content {
  position: relative;
  z-index: 2;
  color: white;
  text-align: center;
  max-width: 800px;
  padding: 40px;
}
```

### Base44 Implementation
```
Design a full-bleed image section with overlaid text:
- Full viewport width, 80vh minimum height
- Background image with object-fit: cover
- Semi-transparent overlay (rgba(0,0,0,0.4))
- Centered text content
- Large headline with supporting copy
- CTA button
- Responsive: Adjust height on mobile
```

---

## Pattern 3: Masonry/Waterfall Grid (Bottega 53)

### Description
Pinterest-style grid with items of varying heights, creating organic visual rhythm.

### Visual Structure
```
┌─────────────────────────────────────────┐
│ ┌──────┐ ┌──────────┐ ┌──────┐         │
│ │      │ │          │ │      │ ┌──────┐│
│ │      │ │          │ │      │ │      ││
│ │  A   │ │    B     │ │  C   │ │  D   ││
│ │      │ │          │ │      │ │      ││
│ │      │ │          │ └──────┘ │      ││
│ │      │ │          │ ┌──────┐ └──────┘│
│ └──────┘ │          │ │  E   │ ┌──────┐│
│ ┌──────┐ │          │ │      │ │      ││
│ │  F   │ └──────────┘ └──────┘ │  G   ││
│ │      │ ┌──────────┐          │      ││
│ └──────┘ │    H     │          └──────┘│
│          └──────────┘                   │
└─────────────────────────────────────────┘
```

### Implementation
```css
/* CSS Columns approach */
.masonry-grid {
  column-count: 4;
  column-gap: 20px;
  padding: 40px;
}

.masonry-item {
  break-inside: avoid;
  margin-bottom: 20px;
}

/* Alternative: CSS Grid with span */
.masonry-grid-alt {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 20px;
  gap: 20px;
}

.masonry-item-alt {
  grid-row: span 10; /* Base height */
}

.masonry-item-alt.tall {
  grid-row: span 15;
}
```

### Base44 Implementation
```
Create a masonry portfolio grid:
- 4 columns on desktop, 2 on tablet, 1 on mobile
- Mixed aspect ratios for visual interest
- 20px gap between items
- Items break inside avoided
- Images load lazily
- Hover: Scale + info reveal
- Optional: Category filters
```

### JavaScript Library Alternative
```javascript
// Using Masonry.js
var msnry = new Masonry('.masonry-grid', {
  itemSelector: '.masonry-item',
  columnWidth: '.masonry-sizer',
  gutter: 20,
  percentPosition: true
});
```

---

## Pattern 4: Sticky Side Panel (Jesko Jets)

### Description
One panel scrolls while the other stays fixed, creating a storytelling effect.

### Visual Structure
```
Initial State:
┌──────────────────┬──────────────────────┐
│                  │                      │
│  [STICKY IMAGE]  │   Content block 1    │
│                  │                      │
│                  │                      │
│                  ├──────────────────────┤
│                  │                      │
│                  │   Content block 2    │
│                  │                      │
└──────────────────┴──────────────────────┘

Scrolled State:
┌──────────────────┬──────────────────────┐
│                  │                      │
│  [STICKY IMAGE]  │   Content block 3    │
│                  │                      │
│                  │                      │
│                  ├──────────────────────┤
│                  │                      │
│                  │   Content block 4    │
│                  │                      │
└──────────────────┴──────────────────────┘
     ↑ Stays in view   ↑ Scrolls past
```

### Implementation
```css
.sticky-layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
}

.sticky-panel {
  position: sticky;
  top: 50%;
  transform: translateY(-50%);
  height: fit-content;
}

.scrolling-panel {
  /* Normal scrolling content */
}

.scrolling-panel section {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 60px 0;
}
```

### Base44 Implementation
```
Create a sticky side panel layout:
- Two-column layout
- Left panel: Sticky image/product
- Right panel: Scrolling content sections
- Each content section: min-height 100vh
- Smooth scroll snapping (optional)
- Product subtly rotates/moves on scroll
- Use for: Product showcases, storytelling
```

---

## Pattern 5: Grid Break / Overlap (YODEZEEN)

### Description
Elements intentionally break out of their containers or overlap, creating dynamic tension.

### Visual Structure
```
┌─────────────────────────────────────────┐
│                                         │
│  ┌─────────────────────────┐            │
│  │                         │            │
│  │    TEXT CONTENT         │            │
│  │                         │            │
│  └─────────────────────────┘            │
│            │                            │
│            ▼                            │
│       ┌──────────────┐                  │
│       │              │                  │
│       │    IMAGE     │  ← Breaks out    │
│       │   (offset)   │    of container  │
│       │              │                  │
│       └──────────────┘                  │
│                                         │
└─────────────────────────────────────────┘
```

### Implementation
```css
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 40px;
}

.breakout-image {
  width: 60vw;
  margin-left: -10vw; /* Breaks left edge */
  max-width: none;
}

.breakout-image--right {
  margin-left: auto;
  margin-right: -10vw;
}

/* Full-bleed utility */
.full-bleed {
  width: 100vw;
  margin-left: calc(-50vw + 50%);
}
```

### Base44 Implementation
```
Design a grid-breaking layout:
- Container: max-width 1200px, centered
- Breakout image: 60vw width, offset left/right
- Image overlaps between sections
- Creates depth and visual interest
- Use sparingly for maximum impact
```

---

## Pattern 6: Specifications/Data Grid (Jesko Jets)

### Description
Structured data display in an asymmetric grid, perfect for technical specs, stats, or features.

### Visual Structure
```
┌─────────────────────────────────────────┐
│                                         │
│  Gulfstream 650ER                       │
│  ═══════════════════════════            │
│                                         │
│  ┌─────────────┐ ┌─────────────┐        │
│  │ Range       │ │ Speed       │        │
│  │ 11,263 km   │ │ 480 knots   │        │
│  └─────────────┘ └─────────────┘        │
│  ┌─────────────┐ ┌─────────────┐        │
│  │ Passengers  │ │ Endurance   │        │
│  │ Up to 12    │ │ 14 hrs      │        │
│  └─────────────┘ └─────────────┘        │
│                                         │
│  SPECIFICATION                          │
│  ┌─────────────┐ ┌─────────────┐        │
│  │ Cabin Length│ │ Cabin Width │        │
│  │ 14.05 m²    │ │ 2.49 m²     │        │
│  └─────────────┘ └─────────────┘        │
│                                         │
└─────────────────────────────────────────┘
```

### Implementation
```css
.specs-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 40px 60px;
}

.spec-item {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.spec-label {
  font-size: 14px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: #666;
}

.spec-value {
  font-size: 32px;
  font-weight: 700;
  font-variant-numeric: tabular-nums;
}

/* Section divider */
.spec-section {
  grid-column: 1 / -1;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 0.2em;
  margin-top: 20px;
  padding-top: 20px;
  border-top: 1px solid #e5e5e5;
}
```

### Base44 Implementation
```
Create a specifications grid layout:
- 2-column grid for data pairs
- Large gaps (40px vertical, 60px horizontal)
- Label: small uppercase, letter-spacing
- Value: large (32px), bold, tabular numbers
- Section headers: full width, border-top
- Clean, technical aesthetic
- Use for: Product specs, stats, features
```

---

## Pattern 7: Accordion Content Sections (Jesko Jets)

### Description
Expandable content sections that reveal full content on interaction, keeping initial view minimal.

### Visual Structure
```
Collapsed:
┌─────────────────────────────────────────┐
│ Pets                          [+]       │
├─────────────────────────────────────────┤
│ 24/7 availability             [+]       │
├─────────────────────────────────────────┤
│ Onboard services              [+]       │
├─────────────────────────────────────────┤
│ Efficient                     [+]       │
└─────────────────────────────────────────┘

Expanded:
┌─────────────────────────────────────────┐
│ Pets                          [−]       │
│                                         │
│ [FULL-BLEED IMAGE]                      │
│                                         │
│ Description text here spanning the      │
│ full width of the container...          │
│                                         │
├─────────────────────────────────────────┤
│ 24/7 availability             [+]       │
└─────────────────────────────────────────┘
```

### Implementation
```css
.accordion-list {
  border-top: 1px solid #e5e5e5;
}

.accordion-item {
  border-bottom: 1px solid #e5e5e5;
}

.accordion-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 24px 0;
  cursor: pointer;
}

.accordion-content {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.4s ease;
}

.accordion-item.active .accordion-content {
  max-height: 1000px;
}

.accordion-image {
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  margin-bottom: 24px;
}
```

### Base44 Implementation
```
Design expanding accordion sections:
- Border-top/bottom separators
- Header: Title left, icon right
- Content: Full-bleed image + description
- Smooth height animation (0.4s)
- Icon rotation on expand (45deg)
- Only one open at a time (optional)
- Use for: Services, FAQ, features
```

---

## Pattern 8: Offset/Alternating Layout (All Sites)

### Description
Content blocks alternate between image-left and image-right, creating visual rhythm through a page.

### Visual Structure
```
Section 1:
┌─────────────────────────────────────────┐
│ ┌──────────────┐ ┌──────────────────┐   │
│ │              │ │                  │   │
│ │    IMAGE     │ │   TEXT CONTENT   │   │
│ │              │ │                  │   │
│ └──────────────┘ └──────────────────┘   │
└─────────────────────────────────────────┘

Section 2:
┌─────────────────────────────────────────┐
│ ┌──────────────────┐ ┌──────────────┐   │
│ │                  │ │              │   │
│ │   TEXT CONTENT   │ │    IMAGE     │   │
│ │                  │ │              │   │
│ └──────────────────┘ └──────────────┘   │
└─────────────────────────────────────────┘

Section 3:
┌─────────────────────────────────────────┐
│ ┌──────────────┐ ┌──────────────────┐   │
│ │              │ │                  │   │
│ │    IMAGE     │ │   TEXT CONTENT   │   │
│ │              │ │                  │   │
│ └──────────────┘ └──────────────────┘   │
└─────────────────────────────────────────┘
```

### Implementation
```css
.content-block {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: center;
  padding: 120px 40px;
}

.content-block:nth-child(even) {
  direction: rtl;
}

.content-block:nth-child(even) > * {
  direction: ltr;
}

/* Alternative with explicit classes */
.content-block--image-left {
  /* Default */
}

.content-block--image-right {
  grid-template-columns: 1fr 1fr;
}

.content-block--image-right .content-block__image {
  order: 2;
}
```

### Base44 Implementation
```
Create alternating content sections:
- Two-column grid (image + text)
- Alternate image left/right per section
- Consistent 120px vertical padding
- 60px gap between columns
- Responsive: Stack on mobile (image always first)
- Use for: About sections, features, storytelling
```

---

## Quick Reference: Layout Selection Guide

| Pattern | Best For | Complexity |
|---------|----------|------------|
| Asymmetric Two-Column | Content + image pairs | Low |
| Full-Bleed Image | Hero sections, impact | Low |
| Masonry Grid | Portfolios, galleries | Medium |
| Sticky Side Panel | Product showcases | Medium |
| Grid Break/Overlap | Editorial, artistic | Medium |
| Specs/Data Grid | Technical content | Low |
| Accordion | FAQ, services | Medium |
| Alternating | Long-form content | Low |

## Responsive Breakpoints

```css
/* Desktop */
@media (min-width: 1200px) {
  .container { max-width: 1400px; }
}

/* Tablet */
@media (max-width: 991px) {
  .two-column { grid-template-columns: 1fr; }
  .masonry { column-count: 2; }
}

/* Mobile */
@media (max-width: 767px) {
  .masonry { column-count: 1; }
  .sticky-panel { position: relative; }
  .full-bleed { min-height: 60vh; }
}
```
