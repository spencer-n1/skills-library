---
type: reference
---

# Full-Bleed Hero with Gradient Overlay

**File:** `library/heroes/full-bleed-gradient-overlay.md`

---

## Concept
Hero image takes up full viewport (including nav area), then transitions into a solid color or gradient where text lives. Creates seamless blend from image to content.

---

## Layout Structure

```
┌─────────────────────────────┐
│                             │
│      FULL-BLEED IMAGE       │
│      (includes nav)         │
│                             │
│                             │
├─────────────────────────────┤
│  GRADIENT OVERLAY (1/3)     │
│  ┌─────────────────────┐    │
│  │   HERO TEXT         │    │
│  │   Headline          │    │
│  │   Subheadline       │    │
│  │   CTAs              │    │
│  └─────────────────────┘    │
└─────────────────────────────┘
```

---

## Visual Specs

**Image:**
- Full viewport height (100vh)
- Extends under navigation
- High quality, on-brand

**Gradient Overlay:**
- Starts at ~60-70% down image
- Fades to theme color
- Covering ~1/3 to 1/2 of bottom
- Direction: bottom-to-top fade or diagonal

**Text placement:**
- On gradient area (high contrast)
- Left-aligned or centered
- Large, readable

---

## Prompt Snippet

```
Hero section:
- Full-viewport background image (100vh)
- Image extends under navigation
- Bottom 1/3 has gradient overlay fading to [theme color]
- Hero text (headline, subheadline, CTAs) positioned on gradient area
- Smooth transition from image to solid color
- Navigation transparent over image, solid on scroll
```

---

## When to Use
- Strong hero imagery available
- Want immersive first impression
- Image + color theme blend
- Premium/luxury positioning

---

## When NOT to Use
- Weak imagery
- Text-heavy heroes
- Mobile-first (can work but needs care)
- Fast conversion needed (image can slow perceived speed)