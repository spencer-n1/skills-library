# Hero Pattern: Mixed Typography (Serif + Sans-Serif)

**Source:** PureGlow Med Spa (curvy-pure-glow-path.base44.app)
**Best for:** Med spas, luxury brands, feminine aesthetics, high-end services
**Vibe:** Elegant, sophisticated, editorial

## Description
Hero headline using two complementary fonts — typically a serif for key words (elegance/tradition) and sans-serif for supporting text (modern/clean). Creates visual hierarchy and premium feel.

## Layout Structure
```
┌─────────────────────────────────────────────┐
│                                             │
│     ╔═══════════════════════════════════╗   │
│     ║  Serene   (serif, italic)         ║   │
│     ║  BEAUTY  (serif, bold)            ║   │
│     ║  for the modern world             ║   │
│     ║           (sans-serif)            ║   │
│     ╚═══════════════════════════════════╝   │
│                                             │
│     [Subheadline in clean sans-serif]       │
│     [CTA Button]                            │
│                                             │
└─────────────────────────────────────────────┘
```

## Visual Specs

**Typography Mix:**
- **Primary word(s):** Serif font, often italic or script
  - Examples: Playfair Display, Cormorant Garamond, Great Vibes
  - Use for: Emotional keywords, brand essence words
  - Style: Often larger, more decorative

- **Supporting words:** Sans-serif font
  - Examples: Inter, Source Sans Pro, Lato
  - Use for: Functional text, locations, descriptors
  - Style: Clean, readable, neutral

**Common Combinations:**
- Serif italic + Sans-serif regular
- Serif bold + Sans-serif light
- Script accent + Sans-serif body

**Hierarchy:**
- Mixed headline: Largest text on page
- Subheadline: Sans-serif, smaller
- CTAs: Sans-serif for consistency

**Example Structures:**
```
"Refined" (serif script) + "BEAUTY" (serif bold) + "in Miami" (sans)
"Discover" (sans) + "Serenity" (serif italic)
"Your" (sans) + "Glow" (serif bold) + "Awaits" (sans)
```

## When to Use
- Med spas (luxury, feminine, beauty)
- High-end wellness
- Wedding services
- Premium hospitality
- Editorial-style brands

## When NOT to Use
- Ultra-modern tech (too soft)
- Industrial/construction (mismatch)
- Budget-focused services (too premium-feeling)

## Variations
- **Serif + Serif:** Different weights/styles of same serif family
- **Script + Sans:** Handwritten feel for personal brands
- **Bold + Light:** Same family, extreme weight contrast
- **Stacked:** Words on separate lines for dramatic effect

## Prompt Snippet
```
Hero Section: Mixed typography headline
- Layout: Centered or left-aligned headline area
- Headline structure:
  * "{WORD_1}" — {SERIF_FONT}, {STYLE_1} (e.g., italic, 64px)
  * "{WORD_2}" — {SERIF_FONT}, {STYLE_2} (e.g., bold, 72px)
  * "{WORD_3}" — {SANS_FONT}, {STYLE_3} (e.g., regular, 48px)
- Example: "Refined" (Playfair Display, italic) + "BEAUTY" (Playfair Display, bold) + "in Orange County" (Inter, regular)
- Subheadline: {SANS_FONT}, 18-20px, regular weight
- CTAs: {SANS_FONT} for consistency
- Colors: Headline in {HEADLINE_COLOR}, subheadline in {SUBHEADLINE_COLOR}
- Spacing: Generous line-height (1.2-1.4) between headline lines
- Background: {BACKGROUND} (often white/light for this style)
```

## Notes
- Font pairing is critical — must complement, not compete
- Don't overdo it — 2-3 font styles max in headline
- Serif adds elegance, sans-serif adds readability
- Works best with clean, minimal backgrounds
- This is Spencer's "mixed fonts in hero" pattern for elegant sites
