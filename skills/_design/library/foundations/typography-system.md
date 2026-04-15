# Typography System

## Rating
- **Status**: foundational
- **Preferred contexts**: all
- **Avoid contexts**: none

---

## Font Selection Rules

### Better Than Inter
Avoid Inter, Roboto, Open Sans — these are LLM defaults that look generic.

**Primary Sans-Serif (Body, UI, Buttons):**
- `Geist` — Modern, clean, technical feel
- `Satoshi` — Slightly warmer, professional
- `Cabinet Grotesk` — Editorial, premium
- `Outfit` — Friendly but professional

**Editorial Serif (Hero Headlines Only):**
- `Playfair Display` — Classic, trustworthy
- `Newsreader` — Editorial, warm
- `Instrument Serif` — Modern editorial

**Monospace (Numbers, Labels, Technical):**
- `JetBrains Mono` — Clean technical
- `Geist Mono` — Modern, matches Geist sans

---

## Typography Hierarchy

**Display/Headlines:**
- Size: `text-4xl md:text-5xl lg:text-6xl` (standard)
- Size: `text-6xl md:text-7xl lg:text-8xl` (hero impact — use sparingly)
- Tracking: `tracking-tight` or `tracking-tighter`
- Line-height: `leading-none` or `leading-tight`
- Weight: `font-bold` or `font-semibold`

**Split Typography Pattern:**
- Large text split across viewport: "We Build" (left) + "Trust" (right)
- Creates visual tension and modern feel
- Requires careful responsive handling

**Body Text:**
- Size: `text-base` or `text-lg`
- Line-height: `leading-relaxed` (1.625)
- Max-width: `max-w-[65ch]` for readability
- Color: Off-black, never pure `#000000`

**Secondary/Meta:**
- Size: `text-sm`
- Color: Muted gray (`text-gray-500` or `text-gray-600`)
- Uppercase with tracking for labels: `uppercase tracking-wider text-xs`

---

## Anti-Patterns to Avoid

- ❌ Giant screaming H1s that take up half the viewport
- ❌ Inter font (overused AI default)
- ❌ Thin font weights on small text (poor readability)
- ❌ All caps body text
- ❌ More than 2 font families per site

---

## Serif Usage Rules

**Use Serif for:**
- Hero headlines on premium/luxury sites
- Quote blocks for testimonials
- Section headers on editorial-style sites

**Never Use Serif for:**
- Dashboard/admin interfaces
- Service business sites targeting older demographics
- Navigation, buttons, or small text
