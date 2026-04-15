# Section Pattern: Why Choose Us (Professional/Healthcare)

**Source:** General pattern — healthcare/professional variant
**Best for:** Healthcare, professional services, attorneys, financial advisors
**Vibe:** Trust, credentials, expertise

## Description
Two-column layout: Professional image on left (doctor, team, office), 3-4 trust differentiators on right with icons. Clean, authoritative feel.

## Layout Structure
```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   [Professional Image]         ✦ Point One                  │
│                                Description                  │
│                                ✦ Point Two                  │
│                                Description                  │
│                                ✦ Point Three                │
│                                Description                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## Visual Specs

**Left Column (Image):**
- Professional photo (doctor, team, clean office)
- Rounded corners (12-16px)
- Optional: Subtle shadow
- Aspect ratio: 4:3 or 3:4 (portrait)

**Right Column (Content):**
- Section label (optional): "WHY CHOOSE US" — small, uppercase, brand color
- Headline: Large, bold
- 3-4 bullet points with ✦ symbol or icons
- Each point: Bold title + description

**Bullet Points:**
- ✦ Symbol or simple icon
- Short bold title
- 1-2 line description
- Consistent spacing between points

## When to Use
- Healthcare (dental, med spa, therapy)
- Attorneys (experience, credentials)
- Financial advisors (trust, expertise)
- Any credibility-focused business

## Variations
- **With stats bar:** Stats above this section
- **Image right:** Flip layout
- **More points:** 4-5 with smaller text
- **With CTA:** Button after bullet points

## Prompt Snippet
```
Why Choose Us Section: Professional split layout
- Layout: 2-column (image left, content right) — 50/50 split
- Left: Professional image of {IMAGE_SUBJECT}
  * Rounded corners ({BORDER_RADIUS}px)
  * Object-fit: cover
- Right:
  * Small label: "WHY CHOOSE US" — uppercase, {BRAND_COLOR}, small
  * Headline: "{HEADLINE_TEXT}" — large, bold
  * 3-4 bullet points:
    - Symbol: ✦ or {ICON_STYLE}
    - Title: Bold, "{POINT_1_TITLE}"
    - Description: Regular, 1-2 lines
  * Points: {POINT_1}, {POINT_2}, {POINT_3}
- Background: {BG_COLOR}
- Padding: 80px top/bottom
- Gap between columns: 40-60px
```

## Notes
- Image quality critical — professional photography, not stock-looking
- Points should be REAL differentiators, not generic claims
- ✦ symbol is Spencer's preference for inline trust markers
