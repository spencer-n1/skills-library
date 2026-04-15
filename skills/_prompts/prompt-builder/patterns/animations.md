# Animation Patterns Library
## Extracted from The First The Last Agency Research

---

## Pattern 1: Scroll-Triggered Reveal (All Sites)

### Description
Content fades and slides into view as user scrolls, creating a narrative flow and progressive disclosure.

### Animation Details
```css
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(40px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.reveal-element {
  animation: fadeInUp 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
```

### Timing Specifications
| Property | Value | Notes |
|----------|-------|-------|
| Duration | 0.6-0.8s | Fast enough to feel responsive |
| Easing | `cubic-bezier(0.16, 1, 0.3, 1)` | Smooth deceleration |
| Delay | 0-0.2s | Stagger for multiple elements |
| Distance | 30-50px | Visible but not jarring |

### JavaScript Implementation
```javascript
const observerOptions = {
  threshold: 0.2,
  rootMargin: '0px 0px -50px 0px'
};

const revealObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('revealed');
      revealObserver.unobserve(entry.target);
    }
  });
}, observerOptions);

document.querySelectorAll('.reveal').forEach(el => {
  revealObserver.observe(el);
});
```

### Base44 Implementation
```
Add scroll-triggered reveal animations:
- Elements fade in and translate up (40px)
- Duration: 0.8s with smooth deceleration easing
- Trigger at 20% visibility
- Stagger delays: 0.1s, 0.2s, 0.3s for grouped elements
- Apply to: headings, paragraphs, images, cards
```

---

## Pattern 2: Text Character Animation (Jesko Jets)

### Description
Text reveals character by character or word by word, creating a typing or cinematic effect.

### Animation Details
```css
@keyframes charReveal {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.char {
  display: inline-block;
  animation: charReveal 0.4s ease forwards;
  animation-delay: calc(var(--char-index) * 0.03s);
}
```

### Variants
| Variant | Use Case | Timing |
|---------|----------|--------|
| Character by character | Dramatic headlines | 30ms per char |
| Word by word | Subheadings, descriptions | 80ms per word |
| Line by line | Paragraphs, statements | 150ms per line |

### JavaScript Implementation
```javascript
function splitText(element) {
  const text = element.textContent;
  element.innerHTML = text
    .split('')
    .map((char, i) => 
      `<span class="char" style="--char-index: ${i}">${char}</span>`
    )
    .join('');
}

// Word variant
function splitWords(element) {
  const text = element.textContent;
  element.innerHTML = text
    .split(' ')
    .map((word, i) => 
      `<span class="word" style="--word-index: ${i}">${word}</span>`
    )
    .join(' ');
}
```

### Base44 Implementation
```
Create character-by-character text reveal:
- Split headline into individual characters
- Each character fades up with 30ms stagger
- Total animation time scales with text length
- Use for: main headlines, CTAs
- Combine with scroll trigger for reveal timing
```

---

## Pattern 3: Accordion Expand/Collapse (Jesko Jets)

### Description
Smooth height animation for expandable content sections, revealing full content with elegant motion.

### Animation Details
```css
.accordion-content {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.accordion-item.active .accordion-content {
  max-height: 800px; /* Or use JS for dynamic height */
}

.accordion-icon {
  transition: transform 0.3s ease;
}

.accordion-item.active .accordion-icon {
  transform: rotate(45deg);
}
```

### Smooth Height Solution (JavaScript)
```javascript
class Accordion {
  constructor(element) {
    this.element = element;
    this.content = element.querySelector('.accordion-content');
    this.isOpen = false;
    element.addEventListener('click', () => this.toggle());
  }
  
  toggle() {
    this.isOpen = !this.isOpen;
    
    if (this.isOpen) {
      const height = this.content.scrollHeight;
      this.content.style.maxHeight = height + 'px';
      this.element.classList.add('active');
    } else {
      this.content.style.maxHeight = '0';
      this.element.classList.remove('active');
    }
  }
}
```

### Base44 Implementation
```
Design expanding accordion sections:
- Header row with title and plus/minus icon
- Smooth height transition (0.4s) on click
- Icon rotates 45° to become X when open
- Content reveals with fade effect
- Full-bleed image support in expanded state
- Only one item open at a time (optional)
```

---

## Pattern 4: Sticky/Floating Element (Jesko Jets)

### Description
Element remains fixed in viewport while content scrolls past, creating layered depth and focus.

### Animation Details
```css
.floating-element {
  position: sticky;
  top: 50%;
  transform: translateY(-50%);
  z-index: 10;
}

/* Or fixed with scroll-linked animation */
.floating-scroll {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

### Scroll-Linked Movement
```javascript
window.addEventListener('scroll', () => {
  const scrollY = window.scrollY;
  const element = document.querySelector('.floating-element');
  
  // Subtle rotation based on scroll
  const rotation = scrollY * 0.02;
  element.style.transform = `translateY(-50%) rotate(${rotation}deg)`;
  
  // Or vertical movement
  const offset = scrollY * 0.1;
  element.style.transform = `translateY(calc(-50% + ${offset}px))`;
});
```

### Base44 Implementation
```
Create a floating product showcase:
- Center-positioned image that stays sticky on scroll
- Content scrolls around/behind the image
- Subtle scroll-linked rotation (0-15 degrees)
- Z-index layering for depth
- Smooth transitions between sections
```

---

## Pattern 5: Marquee/Infinite Scroll (Gifford Hill)

### Description
Continuous horizontal scrolling animation for statistics, logos, or content that loops infinitely.

### Animation Details
```css
@keyframes marquee {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-50%);
  }
}

.marquee-container {
  overflow: hidden;
  white-space: nowrap;
}

.marquee-content {
  display: inline-flex;
  animation: marquee 30s linear infinite;
}

.marquee-content:hover {
  animation-play-state: paused;
}
```

### HTML Structure
```html
<div class="marquee-container">
  <div class="marquee-content">
    <!-- Duplicate content for seamless loop -->
    <div class="marquee-items">
      <span>$7.5 Billion</span>
      <span>7,210 Jobs</span>
      <span>44,000 Residents</span>
    </div>
    <div class="marquee-items">
      <span>$7.5 Billion</span>
      <span>7,210 Jobs</span>
      <span>44,000 Residents</span>
    </div>
  </div>
</div>
```

### Base44 Implementation
```
Create an infinite scrolling statistics bar:
- Horizontal continuous scroll
- Duration: 30s for full cycle
- Pause on hover
- Duplicate content for seamless loop
- Large numbers with supporting labels
- Smooth linear animation
```

---

## Pattern 6: Image Hover Zoom (Bottega 53)

### Description
Subtle scale increase on image hover, creating depth and interactivity without overwhelming.

### Animation Details
```css
.image-container {
  overflow: hidden;
}

.image-container img {
  transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
}

.image-container:hover img {
  transform: scale(1.05);
}
```

### Advanced Variant with Overlay
```css
.portfolio-item {
  position: relative;
  overflow: hidden;
}

.portfolio-item img {
  transition: transform 0.6s ease;
}

.portfolio-item:hover img {
  transform: scale(1.05);
}

.portfolio-item .overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.3);
  opacity: 0;
  transition: opacity 0.4s ease;
}

.portfolio-item:hover .overlay {
  opacity: 1;
}

.portfolio-item .info {
  position: absolute;
  bottom: 20px;
  left: 20px;
  color: white;
  transform: translateY(20px);
  opacity: 0;
  transition: all 0.4s ease;
}

.portfolio-item:hover .info {
  transform: translateY(0);
  opacity: 1;
}
```

### Base44 Implementation
```
Add image hover zoom effect:
- Scale from 1.0 to 1.05 on hover
- Duration: 0.6s with smooth easing
- Container overflow: hidden to clip zoom
- Optional: Dark overlay fade-in
- Optional: Info text slide-up reveal
- Use for: portfolio grids, galleries, cards
```

---

## Pattern 7: Clip-Path Text Reveal (YODEZEEN)

### Description
Text reveals using clip-path animation, creating a wiping or masking effect.

### Animation Details
```css
@keyframes clipReveal {
  from {
    clip-path: inset(0 100% 0 0);
  }
  to {
    clip-path: inset(0 0 0 0);
  }
}

.text-reveal {
  animation: clipReveal 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

/* Bottom-up variant */
@keyframes clipRevealUp {
  from {
    clip-path: inset(100% 0 0 0);
  }
  to {
    clip-path: inset(0 0 0 0);
  }
}

/* Center-out variant */
@keyframes clipRevealCenter {
  from {
    clip-path: inset(50% 50% 50% 50%);
  }
  to {
    clip-path: inset(0 0 0 0);
  }
}
```

### Base44 Implementation
```
Create clip-path text reveal animations:
- Left-to-right wipe for headlines
- Bottom-to-top for descriptions
- Center-out for dramatic statements
- Duration: 0.8s with smooth deceleration
- Trigger on scroll into view
```

---

## Pattern 8: Staggered Grid Load (Bottega 53)

### Description
Grid items animate in with incremental delays, creating a wave or cascade effect.

### Animation Details
```css
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px) scale(0.95);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.grid-item {
  opacity: 0;
  animation: fadeInUp 0.6s ease forwards;
  animation-delay: calc(var(--index) * 0.1s);
}
```

### JavaScript for Dynamic Index
```javascript
document.querySelectorAll('.grid-item').forEach((item, index) => {
  item.style.setProperty('--index', index);
});
```

### Base44 Implementation
```
Add staggered grid load animation:
- Each grid item fades up with increasing delay
- Delay increment: 0.1s per item
- Include subtle scale (0.95 → 1.0)
- Duration: 0.6s per item
- Apply to: portfolio grids, team members, features
```

---

## Quick Reference: Animation Timing

| Animation Type | Duration | Easing |
|----------------|----------|--------|
| Hover effects | 0.3-0.4s | ease |
| Scroll reveals | 0.6-0.8s | cubic-bezier(0.16, 1, 0.3, 1) |
| Page transitions | 0.5-0.6s | cubic-bezier(0.4, 0, 0.2, 1) |
| Accordion | 0.4s | cubic-bezier(0.4, 0, 0.2, 1) |
| Marquee | 30s | linear |
| Character reveal | 0.4s total | ease |

## Performance Guidelines

1. **Use `transform` and `opacity`** - GPU accelerated
2. **Add `will-change`** - For heavy animations
3. **Use Intersection Observer** - Don't animate off-screen
4. **Debounce scroll events** - Or use `passive: true`
5. **Respect `prefers-reduced-motion`** - Accessibility

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```
