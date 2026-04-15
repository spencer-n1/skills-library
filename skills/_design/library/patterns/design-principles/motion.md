# Motion & Animation Principles

## Intensity: Keep It Subtle

For trades/service business websites, motion should enhance — not distract.

**Level 1-3 (Recommended):**
- Simple hover states
- Fade-in on scroll
- Subtle scale on active states

**❌ Avoid Level 8-10:**
- No magnetic buttons
- No perpetual looping animations
- No scroll hijacking
- No 3D transforms

## Scroll Entry Animations

**Standard Fade-Up:**
```
Initial: opacity: 0, translateY(12px)
Animate to: opacity: 1, translateY(0)
Duration: 600ms
Easing: cubic-bezier(0.16, 1, 0.3, 1)
```

**Use for:**
- Section content on first appearance
- Staggered list/grid items
- Testimonial cards

**Performance:**
- Use IntersectionObserver (not scroll events)
- Animate only `transform` and `opacity`
- Never animate `width`, `height`, `top`, `left`

## Hover States

**Buttons:**
- Background color shift (subtle)
- OR `scale-[0.98]` on active (physical push feel)
- Duration: 200ms

**Cards:**
- Ultra-subtle lift: `shadow-[0_2px_8px_rgba(0,0,0,0.04)]`
- Duration: 200ms
- No dramatic transforms

**Links:**
- Underline animation (left-to-right reveal)
- OR opacity shift: `hover:opacity-70`

## Staggered Reveals

For lists and grids:
```
animation-delay: calc(var(--index) * 80ms)
```

**Use for:**
- Service cards
- Review/testimonial lists
- Portfolio items

Creates a polished "waterfall" effect without being flashy.

## What to Avoid

**❌ Banned Patterns:**
- Perpetual motion (constant looping animations)
- Parallax scrolling
- Scroll-triggered complex sequences
- 3D card tilts on hover
- Custom mouse cursors
- Particle effects
- Page transition animations

**Why:** These distract from the goal (contact form submission) and can feel unprofessional for trades.

## Performance Guardrails

- Use `will-change: transform` sparingly
- Isolate animations in their own components
- Never apply motion to scrolling containers
- Test on mobile devices

## Easing Functions

**Standard:**
```
cubic-bezier(0.16, 1, 0.3, 1)  /* Ease-out-expo feel */
```

**Spring (buttons/interactive):**
```
type: "spring",
stiffness: 100,
damping: 20
```

## Loading States

**Skeleton Screens:**
- Match layout sizes exactly
- Shimmer effect acceptable
- Avoid generic spinners

**Form Submission:**
- Button loading state (spinner inside button)
- Disable form during submission
- Clear error/success states

## Scroll Behavior

- Smooth scroll for anchor links: `scroll-behavior: smooth`
- No scroll hijacking
- No scroll progress indicators
- Navigation should scroll smoothly to sections
