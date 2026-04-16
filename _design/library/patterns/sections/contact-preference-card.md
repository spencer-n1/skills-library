# Section Pattern: Contact Preference Card ("Prefer to Call?")

**Source:** ClearView Orthodontics (smile-view-flow.base44.app)
**Best for:** Healthcare, professional services, any business where phone is primary CTA
**Vibe:** Helpful, non-pushy, gives options

## Description
Alternative contact option card that presents phone/online choice without being aggressive. Shows "Prefer to call?" with phone number as secondary option to forms.

## Layout Structure
```
┌─────────────────────────────────────────┐
│  Have questions?                        │
│                                         │
│  ┌─────────────────────────────────┐    │
│  │  📞  Prefer to call?            │    │
│  │      Our team is ready to help  │    │
│  │      (555) 123-4567             │    │
│  └─────────────────────────────────┘    │
│                                         │
│  [Or fill out the form below]           │
│                                         │
└─────────────────────────────────────────┘
```

## Visual Specs

**Card Container:**
- Light background (slightly different from section bg)
- Border or subtle shadow
- Rounded corners (12-16px)
- Padding: 24-32px

**Icon:**
- Phone icon or headset icon
- Brand color or neutral
- Size: 24-32px

**Headline:**
- "Prefer to call?" or "Rather talk to someone?"
- Friendly, not salesy
- Medium weight

**Supporting text:**
- "Our team is ready to help"
- "Speak with a specialist"
- "We're here to answer your questions"

**Phone Number:**
- Large, bold, clickable
- Brand color or dark
- Click-to-call on mobile

**Form reference:**
- "Or fill out the form below"
- "Or request a callback online"
- Small, subtle text

## When to Use
- Healthcare (patients may prefer phone)
- High-ticket services (consultation calls)
- Older demographics who prefer phone
- Complex services that need explanation

## When NOT to Use
- Pure e-commerce (checkout focused)
- Very simple inquiries
- When phone is NOT a primary channel

## Variations
- **Simple card:** Just phone number with icon
- **Split choice:** Phone on left, form on right
- **Floating:** Sticky phone button on mobile
- **Modal:** "Need help? Call us" popup

## Prompt Snippet
```
Contact Preference Card: "Prefer to call?" option
- Position: Above or alongside contact form
- Card styling:
  * Background: {CARD_BG_COLOR} (slightly contrasting)
  * Border-radius: {BORDER_RADIUS}px
  * Padding: 24px
  * Optional: subtle border or shadow
- Content:
  * Icon: Phone/headset icon, {ICON_COLOR}, 24px
  * Headline: "Prefer to call?" — medium weight
  * Subtext: "{SUPPORT_TEXT}" (e.g., "Our team is ready to help")
  * Phone: "{PHONE_NUMBER}" — large, bold, {PHONE_COLOR}, clickable
- Form reference: "Or fill out the form below" — small, subtle
- Mobile: Tap-to-call functionality essential
- Behavior: Collapsible or always visible based on context
```

## Notes
- This reduces form anxiety by giving an escape hatch
- Works well for older demographics
- Keep phone number prominent — don't hide it
- Good for healthcare where personal connection matters
