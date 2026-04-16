# Section Pattern: Services Grid (3-Card Equal)

**Source:** General pattern — standard services display
**Best for:** Service businesses with 3 distinct offerings
**Vibe:** Clear, organized, scannable

## Description
Three equal cards in a row, each representing a service. Icon or number at top, title, description, and optional link/button.

## Layout Structure
```
┌─────────────────────────────────────────────────────────────┐
│                     [Section Header]                        │
│                                                             │
│   ┌─────────┐    ┌─────────┐    ┌─────────┐                 │
│   │  [Icon] │    │  [Icon] │    │  [Icon] │                 │
│   │  Title  │    │  Title  │    │  Title  │                 │
│   │  Desc   │    │  Desc   │    │  Desc   │                 │
│   │ [Link]  │    │ [Link]  │    │ [Link]  │                 │
│   └─────────┘    └─────────┘    └─────────┘                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## Visual Specs

**Cards:**
- Equal width (33% each)
- Consistent height (can use flexbox stretch)
- White or subtle background
- Border or shadow for definition
- Rounded corners (12-16px)

**Card Content:**
- Icon at top (optional): Brand color, 40-48px
- Title: Bold, medium size
- Description: 2-3 lines, regular weight
- Link/button: "Learn More" or arrow

**Section Header:**
- Small label: "OUR SERVICES" (optional)
- Headline: "What We Offer" or similar
- Subheadline: Brief description (optional)

**Grid:**
- Gap: 24-32px between cards
- Responsive: Stack on mobile

## When to Use
- HVAC (Install, Repair, Maintenance)
- Law (Personal Injury, Family Law, Criminal Defense)
- Dental (Cleanings, Cosmetic, Restorative)
- Any business with 3 core services

## Variations
- **With images:** Photo at top of each card
- **Featured middle:** Middle card elevated/larger
- **Horizontal:** Side-by-side with image left
- **Icon only:** No description, just icon + title

## Prompt Snippet
```
Services Section: 3-card equal grid
- Section header:
  * Label: "OUR SERVICES" — small, uppercase, {BRAND_COLOR}
  * Headline: "{SECTION_HEADLINE}"
  * Subheadline (optional): "{SECTION_SUBHEADLINE}"
- Layout: 3-column grid, equal width
- Gap: 24px between cards
- Cards:
  * Background: {CARD_BG_COLOR}
  * Border-radius: {BORDER_RADIUS}px
  * Padding: 32px
  * Icon: {ICON_STYLE} at top, {ICON_SIZE}px, {ICON_COLOR}
  * Title: "{SERVICE_1_NAME}", "{SERVICE_2_NAME}", "{SERVICE_3_NAME}" — bold
  * Description: 2-3 lines explaining service
  * Link: "Learn More →" or similar
- Background: {SECTION_BG_COLOR}
- Padding: 80px top/bottom
- Mobile: Stack vertically
```

## Notes
- 3 is the sweet spot — more than 3 should use different pattern
- Cards should feel equal in importance
- Icons help visual scanning but aren't required
- Descriptions should be benefit-focused, not feature lists
