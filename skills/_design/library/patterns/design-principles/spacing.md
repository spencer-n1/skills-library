# Spacing & Layout Principles

## Macro Whitespace

**Section Spacing:**
- Default: `py-20 md:py-24 lg:py-32` between sections
- Tighter for dense pages: `py-16`
- Luxury feel: `py-24 md:py-32`

**Container Width:**
- Default: `max-w-7xl mx-auto px-4 sm:px-6 lg:px-8`
- Wide: `max-w-[1400px]` for expansive layouts
- Narrow (text-heavy): `max-w-4xl` for readability

## Layout Patterns

### Anti-Center Bias
Default LLMs center everything. Force asymmetric layouts:

**Split Screen (50/50):**
```
[Text Left] [Image Right]
```
- Hero: Content left-aligned, image/asset right
- Alternating: Section 1 text left, Section 2 text right

**Left-Aligned Content:**
- Hero headline and subtext aligned left
- CTA buttons left-aligned under text
- Works especially well for trades/professional services

**Asymmetric White Space:**
- Use `margin-top: -2rem` for overlapping elements
- Vary image aspect ratios (4:3 next to 16:9)
- Empty zones create breathing room

### Bento Grid Layouts

**Structure:**
- Asymmetrical CSS Grid
- Cards with `border: 1px solid` (subtle)
- Border-radius: `8px` or `12px` (crisp, not pill)
- Generous internal padding: `p-6` or `p-8`

**Example Patterns:**
```
Row 1: [Wide Card] [Square Card]
Row 2: [Square] [Wide Card]
```

**Use for:**
- Services sections
- Feature highlights
- Stats/dashboard-style displays

### Asymmetric Two-Column (60/40 or 70/30)

**Layout:**
```
[60% Content] [40% Image]
[40% Image] [60% Content]  /* Alternating */
```

- Creates visual tension
- Avoids "blocky" equal-column look
- Good for About, Services, Why Choose Us sections
- **Mobile:** Stack vertically, 100% width each

### Background Variety Pattern

**Mix background types to create visual interest without chaos:**

1. **Solid color sections** — Clean, professional
2. **Full-bleed image sections** — Visual impact
3. **Geometrical shapes** — Subtle depth

**Rules:**
- Never same background type on adjacent sections
- Wave/divider shapes should flow into next section color (no white gaps)
- Alternating: solid → image → solid → geometrical → image

### Grid Over Flex-Math

**❌ Never:**
```
w-[calc(33%-1rem)] /* Fragile flex math */
```

**✅ Always:**
```
grid grid-cols-1 md:grid-cols-3 gap-6
```

## Hero Section Rules

**Critical: No h-screen**
```
/* ❌ Causes mobile Safari bugs */
h-screen

/* ✅ Use this instead */
min-h-[100dvh]
```

**Hero Structure:**
- Full viewport height: `min-h-[100dvh]`
- Content centered vertically
- Asymmetric content placement (not dead center)
- Background: Full-bleed image with overlay OR solid color

## Component Spacing

**Cards:**
- Padding: `p-6` default, `p-8` for emphasis
- Gap between cards: `gap-4` or `gap-6`

**Buttons:**
- Internal padding: `px-6 py-3` or `px-8 py-4`
- Gap between button groups: `gap-4`

**Form Inputs:**
- Label above input (not inline)
- Gap between label and input: `gap-1.5` or `gap-2`
- Gap between form fields: `gap-4` or `gap-6`

## Responsive Breakpoints

**Standard:**
- `sm:` — 640px+
- `md:` — 768px+  
- `lg:` — 1024px+
- `xl:` — 1280px+

**Mobile-First Rule:**
- Design for mobile first
- Add complexity at `md:` and up
- High-variance layouts MUST collapse gracefully on mobile
