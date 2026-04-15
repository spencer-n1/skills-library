# Section Pattern: Reviews/Testimonials Carousel

**Source:** General pattern — standard testimonial display
**Best for:** All local service businesses
**Vibe:** Social proof, trust, community

## Description
Carousel or grid of customer reviews. Star rating, quote, customer name/info, optionally photos. Clean, trustworthy presentation.

## Layout Structure
```
┌─────────────────────────────────────────────────────────────┐
│                    [Section Header]                         │
│                                                             │
│   ┌─────────────────────────────────────────────────────┐   │
│   │  ★★★★★                                              │   │
│   │  "Quote text here from a satisfied customer..."      │   │
│   │                                                      │   │
│   │  [Photo]  Customer Name                              │   │
│   │           Business/Location                          │   │
│   └─────────────────────────────────────────────────────┘   │
│                                                             │
│                    [←  ● ● ●  →]                            │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## Visual Specs

**Section Header:**
- Label: "TESTIMONIALS" or "WHAT CLIENTS SAY"
- Headline: "Trusted by {NUMBER} Happy Customers"
- Optional: Overall rating (4.9/5 from 100+ reviews)

**Review Card:**
- Star rating: 5 stars, brand color or gold
- Quote: Large text, in quotes or styled block
- Attribution: Customer photo (circle), name, location/service
- Optional: Company name if B2B

**Carousel Controls:**
- Arrows: Left/right navigation
- Dots: Current slide indicator
- Auto-play: Optional, slow (5-7 seconds)

**Grid Alternative:**
- 2-3 cards visible at once
- No carousel, just static grid
- Good for fewer reviews

## When to Use
- All local service businesses
- After services section (proof they deliver)
- Before contact/CTA (final trust push)

## Variations
- **Single large:** One featured review, big
- **Grid:** 3 cards side by side, static
- **With photos:** Customer photos included
- **Video:** Video testimonials (advanced)

## Prompt Snippet
```
Reviews Section: Testimonial carousel
- Section header:
  * Label: "TESTIMONIALS" — small, uppercase, {BRAND_COLOR}
  * Headline: "{HEADLINE_TEXT}"
  * Optional: Overall rating display
- Carousel:
  * Navigation arrows: Left/right, subtle
  * Dots: Bottom center, active dot highlighted
  * Auto-play: {YES/NO}, 6 second interval
- Review cards:
  * Star rating: ★★★★★ in {STAR_COLOR}
  * Quote: Large text (20-24px), in quotation marks
  * Attribution:
    - Photo: Circular, 48-64px
    - Name: Bold
    - Detail: Location or service type
  * Card background: {CARD_BG_COLOR}
  * Card padding: 32-40px
- Number of reviews: {NUMBER}
- Background: {SECTION_BG_COLOR}
- Padding: 80px top/bottom
```

## Notes
- Real reviews only — fake testimonials are obvious and hurt trust
- Photos add credibility significantly
- Carousel should be swipeable on mobile
- Consider highlighting 1-2 best reviews as featured
