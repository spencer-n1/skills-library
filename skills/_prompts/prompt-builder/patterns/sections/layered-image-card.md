# Pattern: Layered Image Card with Text Overlay

**File:** `sections/layered-image-card.md`  
**Use case:** Hero sections, feature highlights, showcase areas

---

## Description

Full-bleed background image with a content card positioned over it. The card contains text content and sits on top of a darkened image area for readability.

---

## Visual Structure

```
┌─────────────────────────────────────────┐
│                                         │
│     [BACKGROUND IMAGE - full bleed]     │
│                                         │
│   ┌─────────────────────────┐           │
│   │                         │           │
│   │   Headline              │           │
│   │   Subtext description   │           │
│   │   [CTA Button]          │           │
│   │                         │           │
│   └─────────────────────────┘           │
│                                         │
└─────────────────────────────────────────┘
```

---

## Critical Rules

### Equal Heights (CRITICAL)
- **All cards in a row must be the same height**
- Content should fill space properly — NO excessive blank space below text
- If cards are in a grid, they align at top and bottom

### Card Positioning
- Card sits on top of the background image
- Usually positioned at bottom-left, bottom-center, or offset
- Card should NOT float randomly — anchor it to an edge

### Overlay Opacity
- Dark gradient overlay (40-60% opacity) behind the card area
- White text on dark background must pass contrast checks
- Image should still be visible but not competing with text

### Card Sizing
- Consistent padding: 24-32px
- Card should not cover more than 40% of the image
- Leave breathing room around the card

---

## Common Mistakes

❌ **Cards with tiny text and massive empty space below**  
✅ Content fills the card vertically — text + button distributed properly

❌ **Unequal card heights in the same row**  
✅ All cards match height — use flexbox/grid align-items: stretch

❌ **Overlay too light** (text unreadable) or **too dark** (image invisible)  
✅ Test contrast — aim for 4.5:1 minimum, image still visible

❌ **Card floating in random spot**  
✅ Anchor to edges — bottom-left, centered bottom, or offset with purpose

---

## Variations

### Direct Text Overlay (No Card)
- Text sits directly on image with overlay
- No separate card container
- Simpler, cleaner look

### Flush Bottom Card
- Card touches bottom edge of section
- No gap between card and container edge
- Grounded, stable feeling

### Centered Card
- Card positioned in center of image
- Works for symmetrical/balanced compositions
- Risk: Can obscure important image content

---

## Example Usage

```
Section: Services Showcase
- 3 layered image cards in a row
- Each shows a different service type
- Cards positioned at bottom-left
- Equal heights, consistent padding
- CTA button in each card
```

---

## Technical Notes

```css
/* Card container */
.layered-card {
  position: relative;
  min-height: 400px; /* or 100vh for hero */
}

/* Background image with overlay */
.layered-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to right,
    rgba(0,0,0,0.6) 0%,
    rgba(0,0,0,0.3) 50%,
    rgba(0,0,0,0) 100%
  );
}

/* Content card */
.card-content {
  position: absolute;
  bottom: 40px;
  left: 40px;
  max-width: 400px;
  background: rgba(0,0,0,0.7);
  padding: 32px;
  border-radius: 12px;
}

/* Equal heights for row */
.card-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

.card-row .layered-card {
  height: 100%; /* fills grid cell */
}
```

---

## When to Use

✅ **Use for:**
- Hero sections with impactful imagery
- Service/feature highlights
- Portfolio/showcase sections
- Anywhere you want imagery + readable text

❌ **Avoid when:**
- Image content is critical (card obscures it)
- You have lots of text (card gets too tall)
- Mobile-first priority (can stack awkwardly on small screens)
