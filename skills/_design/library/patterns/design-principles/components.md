# Component Principles

## Buttons

**Primary CTA:**
- Background: Solid dark (`#111111` or accent color)
- Text: White
- Border-radius: `4px` to `6px` (subtle, not pill)
- Padding: `px-6 py-3` or `px-8 py-4`
- No box-shadow by default

**Hover:**
- Background shift to lighter/darker shade
- OR `scale-[0.98]` on active for tactile feel

**Secondary/Button Outline:**
- Transparent background
- Border: `1px solid`
- Text: Same as border color

**❌ Avoid:**
- Pill shapes (`rounded-full`) for primary actions
- Heavy drop shadows
- Gradient backgrounds

## Cards

**Structure:**
- Border: `1px solid #EAEAEA` (light) or `#27272a` (dark)
- Border-radius: `8px` or `12px` maximum
- Background: White or subtle off-white
- Padding: `p-6` or `p-8`

**Elevation:**
- Default: No shadow, use border only
- Hover: Ultra-subtle shadow `shadow-[0_2px_8px_rgba(0,0,0,0.04)]`

**Bento Grid Cards:**
- Asymmetric sizing
- Generous internal padding
- Clean borders, no shadows

## Forms

**Input Fields:**
- Label ABOVE input (never inline)
- Gap between label and input: `gap-1.5`
- Border: `1px solid` subtle gray
- Border-radius: `4px` to `6px`
- Padding: `px-4 py-3`

**Focus States:**
- Ring or border color change
- No default browser outline

**Error States:**
- Red border
- Error text below input
- Clear, specific messaging

**Form Layout:**
- Stack fields vertically: `gap-4` or `gap-6`
- Full width on mobile
- Max-width container on desktop

## Navigation

**Desktop:**
- Logo left OR centered
- Links: Home, Services, About, Location/Contact
- CTA button on right
- Clean, minimal styling

**Mobile:**
- Hamburger menu
- Full-screen overlay OR slide-out drawer
- Large touch targets (min 44px)

**Rules:**
- No duplicate links
- Cross-page links must land at top of destination
- Sticky nav on scroll (optional)

## Tags & Badges

**Pill Style:**
- `rounded-full`
- Small text: `text-xs`
- Uppercase: `uppercase tracking-wider`
- Background: Muted pastel colors

**Usage:**
- Service categories
- Status indicators
- Feature highlights

## Accordions (FAQ)

**Structure:**
- No container boxes
- Items separated by `border-bottom: 1px solid`
- Toggle icon: Clean `+` and `-` (not chevrons)
- Generous padding per item

## Dividers

- Use `border-t` or `border-b` with subtle gray
- OR generous whitespace instead of visible lines
- Never heavy visible dividers between every section

### Wave Shape Dividers

**Usage:** Transition between hero and content sections
- SVG wave at bottom of section
- Wave color should flow INTO next section (no white gap)
- Subtle, decorative only
- Works well for coastal/surfacing businesses

**Alternative:** Geometric shape dividers (diagonal, curved)

---

## Between-Section CTA Banners

**Purpose:** Conversion point between content sections

**Rules:**
- Use sparingly — every other section max
- Keep text concise and punchy
- Match section background or use subtle gradient
- Don't interrupt visual flow

**Style:**
- Background: Subtle dark or contrasting accent
- Text: White or high-contrast
- Accent: Arrow or icon pointing direction
- Padding: `py-12` or `py-16`

**Examples:**
- "Ready to get started? Call now →"
- "24/7 Emergency Service Available"
- "Get Your Free Quote Today →"

---

## Icons

**Recommended Sets:**
- Phosphor Icons (Bold or Fill weights)
- Radix UI Icons
- Lucide (acceptable but overused)

**Rules:**
- Standardize stroke width across all icons
- Use consistent icon style (don't mix filled and outline)
- Icon size should match text line-height

## Images

**Hero/Background:**
- High quality, desaturated preferred
- Subtle overlay to ensure text legibility
- `object-cover` for full-bleed

**Content Images:**
- Consistent aspect ratios within sections
- Border-radius matching cards (`8px` or `12px`)
- Lazy loading for below-fold images

**Placeholders:**
- Use reliable sources: `https://picsum.photos/seed/{context}/800/600`
- Avoid broken Unsplash links
