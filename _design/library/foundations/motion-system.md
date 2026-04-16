# Motion System

## Rating
- **Status**: foundational
- **Preferred contexts**: all
- **Avoid contexts**: none

---

## Animation Timing

**Standard Durations:**
- Micro-interactions: `150ms`
- Hover states: `200-300ms`
- Page transitions: `300-400ms`
- Complex sequences: `500-800ms`

**Easing Functions:**
- Standard: `ease-out` or `cubic-bezier(0, 0, 0.2, 1)`
- Enter: `ease-out`
- Exit: `ease-in`
- Bounce: `cubic-bezier(0.34, 1.56, 0.64, 1)`

---

## Scroll Behaviors

**Smooth Scroll:**
- Enable: `scroll-behavior: smooth`
- Duration: Browser default (usually 300ms)

**Scroll-Triggered Animations:**
- Trigger point: 20% from bottom of viewport
- Stagger delay: `100ms` between elements
- Duration: `600ms` per element

---

## Hover Patterns

**Buttons:**
- Scale: `transform: scale(1.02)` or `scale(1.05)`
- Shadow increase
- Background darken/lighten
- Duration: `200ms`

**Cards:**
- Lift: `transform: translateY(-4px)`
- Shadow increase
- Duration: `300ms`

**Links:**
- Underline animation (left to right)
- Color shift
- Duration: `200ms`

---

## Performance Rules

**Always Use:**
- `transform` instead of `top/left`
- `opacity` for fade effects
- `will-change` sparingly

**Never Use:**
- Animating `width`, `height`, `margin`, `padding`
- `box-shadow` animations (expensive)
- Unthrottled scroll events

**Accessibility:**
- Respect `prefers-reduced-motion`
- Keep animations subtle
- Avoid flashing/strobing
