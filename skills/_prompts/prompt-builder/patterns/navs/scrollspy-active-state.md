---
type: reference
---

# Nav Scrollspy (Active State Follows Scroll)

**File:** `library/navs/scrollspy-active-state.md`

---

## Concept
As the user scrolls through the page, the active/highlighted state in the navigation moves to match the current section. "Home" highlighted when at top, "Services" when in services section, etc.

---

## Best For
- Single-page landing pages
- Long-scrolling sites with clear sections
- Improving user orientation
- Adding polish to navigation

---

## How It Works
1. Each section has an ID (e.g., `#services`, `#about`, `#contact`)
2. Nav links point to those IDs
3. JavaScript detects which section is in viewport
4. Active class applied to corresponding nav link
5. Visual highlight moves as user scrolls

---

## Base44 Implementation
- Built-in scroll behavior for anchor links
- May need custom CSS for active state styling
- Smooth scroll to sections

---

## WordPress/Elementor Implementation
```javascript
// Intersection Observer approach
const sections = document.querySelectorAll('section[id]');
const navLinks = document.querySelectorAll('.nav-link');

const observerOptions = {
  root: null,
  rootMargin: '-50% 0px -50% 0px',
  threshold: 0
};

const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const id = entry.target.getAttribute('id');
      navLinks.forEach(link => {
        link.classList.remove('active');
        if (link.getAttribute('href') === `#${id}`) {
          link.classList.add('active');
        }
      });
    }
  });
}, observerOptions);

sections.forEach(section => observer.observe(section));
```

---

## Visual Styling

**Active State Options:**
- Underline
- Background pill/highlight
- Color change
- Bold weight
- Dot indicator

**Evergreen Example:**
- Light sage background pill
- Dark text
- Rounded corners
- Subtle but clear

---

## Prompt Snippet

```
Navigation:
- Sticky nav with anchor links: Hero, Services, About, Testimonials, Contact
- Scrollspy behavior: active highlight moves as user scrolls through sections
- Smooth scroll to sections on click
- Active state style: [choose - underline/pill background/color change]
```

---

## When to Use
- Single-page designs
- Clear section breaks
- Want to orient users as they scroll
- Adding premium polish
- Long pages with 5+ sections

---

## When NOT to Use
- Multi-page sites (different paradigm)
- Short pages (no scroll needed)
- Complex nested sections (hard to track)
- If it conflicts with sticky CTA placement