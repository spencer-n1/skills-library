# CTA Pattern: Chat Bubble Floating CTA

**Source:** Summit HVAC Solutions (summit-comfort-crew.base44.app)
**Best for:** Sites without hero form, clean designs, any business type
**Vibe:** Helpful, non-intrusive, always available

## Description
Circular chat/message icon button fixed to bottom-right corner. Opens chat, scrolls to contact, or opens contact page. Non-intrusive alternative to in-your-face CTAs.

## Layout Structure
```
┌─────────────────────────────────────────────┐
│                                             │
│                                             │
│                                    ┌─────┐  │
│                                    │ 💬 │  │  ← fixed bottom-right
│                                    └─────┘  │
└─────────────────────────────────────────────┘
```

## Visual Specs

**Button:**
- Circular, 56-64px diameter
- Position: Fixed, bottom-right corner (20-24px from edges)
- Background: Brand color or dark (high contrast)
- Icon: Chat bubble, message, or question mark
- Icon color: White or light
- Shadow: Subtle drop shadow for depth

**Behavior:**
- Always visible on scroll
- Smooth hover animation (scale up slightly)
- Click action: Scroll to contact section OR open contact page
- Optional: Tooltip on hover "Have questions?"

**Mobile:**
- Same position (bottom-right)
- Ensure doesn't overlap with critical content
- Tap target: Full button area

## When to Use
- Hero doesn't have contact form (clean image approach)
- Want CTA available without being pushy
- Multi-page sites (navigates to contact page)
- Single-page sites (smooth scroll to contact)
- Any business where questions are common

## When NOT to Use
- Hero already has prominent form (redundant)
- Very simple sites with obvious contact
- When it would overlap important mobile elements

## Variations
- **Chat icon:** Opens live chat widget
- **Message icon:** Opens contact form modal
- **Phone icon:** Tap-to-call on mobile
- **Arrow icon:** Scrolls to top (different purpose)

## Prompt Snippet
```
Floating CTA: Chat bubble button
- Position: Fixed, bottom-right corner (24px from edges)
- Button:
  * Shape: Circular, {BUTTON_SIZE}px (56-64px typical)
  * Background: {BRAND_COLOR} or dark
  * Icon: Chat/message icon, white, 24px
  * Shadow: Subtle drop shadow (0 4px 12px rgba(0,0,0,0.15))
- Behavior:
  * Click: {ACTION} (scroll to contact / open contact page / open chat)
  * Hover: Scale 1.1, smooth transition
  * Optional tooltip: "Have questions?" on hover
- Mobile:
  * Same position
  * Ensure no overlap with nav or critical content
  * Tap target: Full 56-64px area
- Z-index: High (above content, below modals)
```

## Notes
- This is Spencer's "sick idea" — non-intrusive but always available
- Works especially well with clean hero (no form) approach
- Alternative to aggressive popups
- Keep icon simple and recognizable
