# Footer Pattern: Standard Multi-Column

**Source:** General pattern — standard site footer
**Best for:** Multi-page sites, established businesses
**Vibe:** Complete, professional

## Description
Multi-column footer with logo/about, quick links, services, and contact info. Copyright bar at bottom.

## Layout Structure
```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  LOGO         Quick Links    Services       Contact         │
│  Brief about  - Link 1       - Service 1    Phone           │
│  text here    - Link 2       - Service 2    Email           │
│               - Link 3       - Service 3    Address         │
│               - Link 4                      Social Icons    │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│  © 2026 Business Name. All rights reserved.    [Privacy]   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## Visual Specs

**Main Footer:**
- Dark background (default) or light
- 4 columns: About, Links, Services, Contact
- Consistent spacing
- Padding: 60-80px top, 40px bottom

**Column 1 (About):**
- Logo
- Brief tagline or description (2 lines max)
- Optional: Social icons

**Column 2 (Quick Links):**
- Header: "Quick Links"
- Links: Home, About, Services, Contact, etc.

**Column 3 (Services):**
- Header: "Services"
- Links to individual service pages

**Column 4 (Contact):**
- Header: "Contact Us"
- Phone, email, address
- Optional: Hours

**Bottom Bar:**
- Copyright text
- Privacy Policy, Terms links
- Subtle divider above

## When to Use
- Multi-page sites
- When SEO matters (internal linking)
- Established businesses

## Variations
- **Minimal:** Logo + copyright only
- **With map:** Embedded map in contact column
- **With form:** Newsletter signup
- **Large:** Full-width sections instead of columns

## Prompt Snippet
```
Footer: Standard multi-column
- Background: {BG_COLOR} (dark typical: #0a0a0a, #1a1a1a)
- Layout: 4-column grid on desktop, stack on mobile
- Column 1 (About):
  * Logo
  * Tagline: "{TAGLINE}"
  * Social icons: {SOCIAL_LINKS}
- Column 2 (Quick Links):
  * Header: "Quick Links"
  * Links: {LINK_1}, {LINK_2}, {LINK_3}, {LINK_4}
- Column 3 (Services):
  * Header: "Services"
  * Links: {SERVICE_1}, {SERVICE_2}, {SERVICE_3}
- Column 4 (Contact):
  * Header: "Contact Us"
  * Phone: {PHONE}
  * Email: {EMAIL}
  * Address: {ADDRESS}
- Bottom bar:
  * Copyright: "© {YEAR} {BUSINESS_NAME}. All rights reserved."
  * Links: Privacy Policy, Terms of Service
- Text color: White or light gray on dark bg
- Padding: 60px top, 40px bottom main; 20px bottom bar
```

## Notes
- Footer is for navigation and trust — keep it organized
- Don't overload with content
- Ensure all links work
- Social icons only if business actively uses them
