# Section Pattern: Numbered Process Cards (01-04)

**Source:** Julian Vance Law Offices (prime-legal-grid.base44.app)
**Best for:** Service businesses, professional services, agencies
**Vibe:** Organized, clear, step-by-step

## Description
Horizontal row of 4 cards, each with a large background number (01, 02, 03, 04), small colored circle with number, title, and description. Clean process visualization.

## Layout Structure
```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   [◉01]        [◉02]        [◉03]        [◉04]                  │
│    01           02           03           04        ← bg numbers│
│                                                                 │
│   Title        Title        Title        Title                  │
│   Desc         Desc         Desc         Desc                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## Visual Specs

**Card Structure (each):**
- Large faint background number (01, 02, 03, 04) — decorative, low opacity
- Small colored circle with white number inside (◉ 01)
- Title: Bold, clear
- Description: Regular weight, 2-3 lines

**Background Numbers:**
- Very large (filling top portion of card)
- Low opacity (5-10%)
- Light gray or brand color tint
- Positioned top-right or centered-top of card

**Circle Indicators:**
- Small circle (24-32px)
- Brand color fill
- White number inside
- Positioned top-left of content area

**Cards:**
- White or off-white background
- Subtle shadow or border
- Equal width, consistent height
- Gap between cards: 16-24px

**Container:**
- Max-width container (1200px)
- Horizontal on desktop
- Stack 2x2 or 1x4 on mobile

## When to Use
- Law firms (case process)
- Agencies (workflow)
- Service businesses (how it works)
- Any business with clear steps

## Variations
- **2 steps:** Larger cards, more detail
- **3 steps:** Balanced, common for simple processes
- **4 steps:** As shown — detailed but scannable
- **Vertical:** Stack on desktop for longer descriptions

## Prompt Snippet
```
Process Section: Numbered step cards (01-04)
- Layout: 4-column grid on desktop, responsive stack on mobile
- Each card:
  * Large background number: "01", "02", "03", "04" — faint opacity (5%), {BRAND_COLOR} tint
  * Small circle indicator: {BRAND_COLOR} background, white number
  * Title: Bold, "{STEP_1_TITLE}", "{STEP_2_TITLE}" etc.
  * Description: Regular text, 2-3 lines explaining the step
- Card styling: White background, subtle shadow, {BORDER_RADIUS}px radius
- Gap: 20px between cards
- Section padding: 80px top/bottom
- Background: {SECTION_BG_COLOR} (light/off-white typical)
```

## Notes
- Background numbers add visual interest without clutter
- Keep descriptions concise — this is overview, not detail
- Circle color should be brand color for consistency
- 4 steps is max for horizontal layout — more steps should go vertical
