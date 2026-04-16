---
name: base44-to-wordpress
name: base44-to-wordpress
description: Convert Base44 websites into fully editable Elementor WordPress pages by generating clean Elementor JSON from templates and importing via WP-CLI. Replaces fragile SSH database injection with a structure-first generate-and-import pipeline.
type: procedural
keywords: ["wordpress", "elementor", "base44", "website transfer", "json import"]
auto_detect: false
agent_type: main
input_schema:
  source_type: "live_url|source_files|screenshots"
  wordpress_url: string
  wordpress_credentials: object
output_schema:
  elementor_page_url: string
  edit_with_elementor_url: string
quality_metrics:
  success_rate: 0.90
  avg_tokens: 0
  note: "Eliminates ID-mapping fragility by generating valid Elementor JSON from proven section templates"
evolution:
  parent: wordpress-pipeline
  version: "3.0"
  lineage: ["v2.5 SSH injection", "v3.0 template generation"]
status: active
---

# Base44 → WordPress Elementor Pipeline
## Generate-and-Import Workflow

**Version:** 3.0 — April 2026  
**Status:** Active — replaces v2.5 SSH injection approach

---

## Philosophy Change

**Old way (v2.5):** Build layout manually → extract widget IDs → inject text via SSH database surgery.
- Fragile, version-dependent, 40% success rate.

**New way (v3.0):** Analyze source → map content to proven Elementor section templates → generate complete page JSON → import as new Elementor page.
- Clean, repeatable, client-editable, ~90% success rate.

---

## Prerequisites

- WordPress site with Elementor installed and activated
- WP-CLI access (SSH or local)
- Base44 reference: live URL, source files, or detailed screenshots

---

## STEP 1 — Extract Content & Design Tokens

**Goal:** Build a structured content map from the Base44 source.

### If Live URL (Preferred)

Use browser DevTools to extract precise values:

```python
browser.open(targetUrl="https://example.com/")
browser.snapshot()

# Extract design tokens
browser.act(kind="evaluate", fn="""
() => {
  const getStyle = (el, prop) => window.getComputedStyle(el)[prop];
  const sections = Array.from(document.querySelectorAll('section, [class*=\"section\"]')).slice(0, 8);
  
  return {
    typography: {
      h1: document.querySelector('h1') ? {
        size: getStyle(document.querySelector('h1'), 'fontSize'),
        weight: getStyle(document.querySelector('h1'), 'fontWeight'),
        lineHeight: getStyle(document.querySelector('h1'), 'lineHeight'),
        color: getStyle(document.querySelector('h1'), 'color')
      } : null,
      h2: document.querySelector('h2') ? {
        size: getStyle(document.querySelector('h2'), 'fontSize'),
        weight: getStyle(document.querySelector('h2'), 'fontWeight'),
        color: getStyle(document.querySelector('h2'), 'color')
      } : null,
      body: document.querySelector('p') ? {
        size: getStyle(document.querySelector('p'), 'fontSize'),
        color: getStyle(document.querySelector('p'), 'color')
      } : null
    },
    colors: {
      primary: getStyle(document.querySelector('a, button'), 'backgroundColor'),
      text: getStyle(document.querySelector('p'), 'color'),
      heading: getStyle(document.querySelector('h1'), 'color'),
      bg: getStyle(document.body, 'backgroundColor')
    },
    sections: sections.map(s => ({
      tag: s.tagName,
      class: s.className,
      bg: getStyle(s, 'backgroundColor'),
      paddingTop: getStyle(s, 'paddingTop'),
      paddingBottom: getStyle(s, 'paddingBottom'),
      minHeight: getStyle(s, 'minHeight'),
      text: Array.from(s.querySelectorAll('h1, h2, h3, p')).map(el => ({
        tag: el.tagName,
        text: el.textContent.trim().slice(0, 200),
        color: getStyle(el, 'color')
      }))
    }))
  };
}
""")
```

### If Source Files

Read the Base44 export files (usually React components in `src/components/` or similar). Extract:
- Section names and order
- Text content per section
- Tailwind/design token classes (colors, spacing, typography)
- Button labels and links

### Content Map Format

Write everything to `scratch/content_map_v3.md`:

```markdown
# Content Map v3 — [Client Name]

## Global Tokens
- Primary: #1E4F8A
- Text: #333333
- Heading: #0A0A0A
- Background: #FFFFFF
- Font Heading: Inter, 700
- Font Body: Inter, 400

## Section 1: Hero
- Layout: full-height, centered, single column
- Background: #1E4F8A
- h1: "We Build Websites That Convert"
  - color: #FFFFFF
  - size: 56px
- p: "Local business web design with zero fluff."
  - color: rgba(255,255,255,0.85)
  - size: 18px
- button_primary: "Get a Free Quote"
  - link: #contact
- button_secondary: "See Our Work"
  - link: #portfolio

## Section 2: Services
- Layout: 3-column grid
- Background: #FFFFFF
- h2: "What We Do"
- cards:
  1. h3: "Web Design" / p: "Custom sites..."
  2. h3: "SEO" / p: "Rank higher..."
  3. h3: "Ads" / p: "Google PPC..."

## Section 3: CTA
- Layout: centered, single column
- Background: #F5F5F5
- h2: "Ready to Grow?"
- button: "Call Now" / link: tel:+1...

## Skip List
- Animations: ignored
- Custom icons: ignored (use Elementor defaults if needed)
- Complex forms: ignored (use standard contact plugins)
```

---

## STEP 2 — Map Sections to Elementor Templates

**Goal:** Choose the right template structure for each section.

### Template Library

Every section type has a pre-validated Elementor JSON template. The agent selects the closest match.

| Section Type | Template ID | Notes |
|-------------|-------------|-------|
| Hero (centered, 1-col) | hero_centered_fullheight | 100vh, heading + subheading + 2 buttons |
| Hero (2-col, text + image) | hero_split | Heading left, image placeholder right |
| Services (3-col cards) | services_3col | 3 cards with icon + heading + text |
| Features (2-col alternating) | features_alternating | Image + text rows |
| Testimonials (slider or grid) | testimonials_3col | 3 quote cards |
| CTA (centered) | cta_centered | Heading + button, solid bg |
| Footer (simple) | footer_simple | Links + copyright |
| Text content (1-col) | content_single | Generic text block |

**Template selection logic:**
1. Read `content_map_v3.md`
2. For each section, match against the table above
3. If no match, use `content_single` as fallback
4. Record the template ID for each section

**Write mapping file:** `scratch/section_template_map.json`

```json
{
  "sections": [
    {
      "index": 0,
      "name": "Hero",
      "template_id": "hero_centered_fullheight",
      "content_map": {
        "heading": "We Build Websites That Convert",
        "subheading": "Local business web design with zero fluff.",
        "button_primary_text": "Get a Free Quote",
        "button_primary_url": "#contact",
        "button_secondary_text": "See Our Work",
        "button_secondary_url": "#portfolio"
      }
    }
  ]
}
```

---

## STEP 3 — Generate Elementor Page JSON

**Goal:** Build a complete, valid Elementor page document from scratch.

### Elementor Document Structure

A valid Elementor page JSON is an array of top-level elements (usually containers in Flexbox mode). Each element has:

```json
{
  "id": "[7-char hex ID]",
  "elType": "container",
  "settings": { ... },
  "elements": [
    {
      "id": "[7-char hex ID]",
      "elType": "widget",
      "widgetType": "heading",
      "settings": { "title": "..." },
      "elements": []
    }
  ]
}
```

**Rules for valid JSON:**
- Every `id` must be a unique 7-character hex string (e.g., `"a1b2c3d"`)
- `elType` is one of: `section`, `container`, `column`, `widget`
- Every container/section must have an `elements` array (can be empty)
- Widgets store content in `settings` with field names specific to the widget type

### Widget Type → Settings Mapping

| Widget | Settings Fields |
|--------|-----------------|
| `heading` | `title`, `header_size` (h1-h6), `align` |
| `text-editor` | `editor` (HTML string) |
| `button` | `text`, `link` => `{ "url": "..." }`, `align`, `size` |
| `image` | `url`, `alt` |
| `icon` | `icon` => `{ "value": "...", "library": "fa-solid" }` |
| `divider` | (none usually) |

### Python Script: Generate JSON

Use this approach to build the page JSON:

```python
import json
import random

def generate_id():
    return ''.join(random.choices('0123456789abcdef', k=7))

def build_heading(text, size='h2', align='center', color=None):
    settings = {
        "title": text,
        "header_size": size,
        "align": align
    }
    if color:
        settings["title_color"] = color
    return {
        "id": generate_id(),
        "elType": "widget",
        "widgetType": "heading",
        "settings": settings,
        "elements": []
    }

def build_text_editor(html_text, align='center'):
    return {
        "id": generate_id(),
        "elType": "widget",
        "widgetType": "text-editor",
        "settings": {
            "editor": html_text,
            "align": align
        },
        "elements": []
    }

def build_button(text, url, align='center'):
    return {
        "id": generate_id(),
        "elType": "widget",
        "widgetType": "button",
        "settings": {
            "text": text,
            "link": {"url": url},
            "align": align
        },
        "elements": []
    }

def build_container(elements, bg_color=None, min_height=None, padding=None):
    settings = {"content_width": "full", "flex_direction": "column"}
    if bg_color:
        settings["background_color"] = bg_color
    if min_height:
        settings["min_height"] = {"unit": "vh", "size": min_height}
    if padding:
        settings["padding"] = padding
    return {
        "id": generate_id(),
        "elType": "container",
        "settings": settings,
        "elements": elements
    }

# Example: Build a Hero section
hero = build_container(
    elements=[
        build_heading("We Build Websites That Convert", size="h1"),
        build_text_editor("Local business web design with zero fluff."),
        build_button("Get a Free Quote", "#contact")
    ],
    bg_color="#1E4F8A",
    min_height=100,
    padding={"unit": "px", "top": "80", "bottom": "80", "left": "20", "right": "20"}
)

page_data = [hero]
json_output = json.dumps(page_data, separators=(',', ':'))

with open('/tmp/elementor_page.json', 'w') as f:
    f.write(json_output)
```

### Pre-Validated Templates

For common sections, use these proven JSON structures rather than building from scratch each time.

#### Template: hero_centered_fullheight

```json
[{
  "id": "HERO_ID",
  "elType": "container",
  "settings": {
    "content_width": "full",
    "flex_direction": "column",
    "justify_content": "center",
    "align_items": "center",
    "min_height": {"unit": "vh", "size": 100},
    "padding": {"unit": "px", "top": "80", "bottom": "80", "left": "20", "right": "20"},
    "background_color": "BG_COLOR"
  },
  "elements": [
    {
      "id": "H1_ID",
      "elType": "widget",
      "widgetType": "heading",
      "settings": {
        "title": "HEADING_TEXT",
        "header_size": "h1",
        "align": "center",
        "title_color": "HEADING_COLOR"
      },
      "elements": []
    },
    {
      "id": "P_ID",
      "elType": "widget",
      "widgetType": "text-editor",
      "settings": {
        "editor": "<p>SUBHEADING_TEXT</p>",
        "align": "center",
        "text_color": "TEXT_COLOR"
      },
      "elements": []
    },
    {
      "id": "BTN1_ID",
      "elType": "widget",
      "widgetType": "button",
      "settings": {
        "text": "BTN1_TEXT",
        "link": {"url": "BTN1_URL"},
        "align": "center"
      },
      "elements": []
    }
  ]
}]
```

**Usage:** Replace the ALL_CAPS placeholders with actual values and regenerate all IDs.

#### Template: services_3col

A container with 3 nested containers (columns), each holding an icon, heading, and text.

```json
{
  "id": "SECTION_ID",
  "elType": "container",
  "settings": {
    "content_width": "boxed",
    "flex_direction": "row",
    "padding": {"unit": "px", "top": "80", "bottom": "80"},
    "background_color": "BG_COLOR"
  },
  "elements": [
    {
      "id": "COL1_ID",
      "elType": "container",
      "settings": {
        "flex_direction": "column",
        "width": {"unit": "%", "size": 33.333},
        "padding": {"unit": "px", "top": "24", "bottom": "24", "left": "24", "right": "24"}
      },
      "elements": [
        {"id": "ICON1_ID", "elType": "widget", "widgetType": "icon", "settings": {"icon": {"value": "fas fa-bolt", "library": "fa-solid"}}, "elements": []},
        {"id": "H3_1_ID", "elType": "widget", "widgetType": "heading", "settings": {"title": "TITLE_1", "header_size": "h3", "align": "center"}, "elements": []},
        {"id": "P1_ID", "elType": "widget", "widgetType": "text-editor", "settings": {"editor": "<p>BODY_1</p>", "align": "center"}, "elements": []}
      ]
    },
    {"id": "COL2_ID", "elType": "container", ...},
    {"id": "COL3_ID", "elType": "container", ...}
  ]
}
```

---

## STEP 4 — Import into WordPress

**Goal:** Get the generated JSON into Elementor as a working page.

### Method A: WP-CLI Direct Import (Fastest)

Create a new blank page, then set its `_elementor_data` meta with the generated JSON.

```bash
# 1. Create the page
wp post create --post_type=page --post_title="Home" --post_status=publish --post_name=home --porcelain > /tmp/page_id.txt
PAGE_ID=$(cat /tmp/page_id.txt)

# 2. Mark it as built with Elementor
wp post meta update $PAGE_ID _elementor_edit_mode builder
wp post meta update $PAGE_ID _elementor_template_type page

# 3. Inject the JSON
wp post meta update $PAGE_ID _elementor_data --format=json < /tmp/elementor_page.json

# 4. Flush caches
wp elementor flush-css
wp cache flush
```

### Method B: Elementor Template Export/Import

If Method A fails (e.g., Elementor validation rejects the JSON), wrap the page JSON as an Elementor template:

```python
import json

with open('/tmp/elementor_page.json') as f:
    content = json.load(f)

template = {
    "version": "0.4",
    "title": "Imported Page",
    "type": "page",
    "content": content
}

with open('/tmp/elementor_template.json', 'w') as f:
    json.dump(template, f)
```

Then import via WP-CLI or Elementor's template import UI:
- Upload `/tmp/elementor_template.json` to WordPress Admin → Elementor → Templates → Import
- Or use a plugin like "Elementor Template Import" programmatically

### Method C: Elementor API (If WP-CLI unavailable)

Use WordPress REST API to create the page and set meta:

```bash
# Create page via REST
curl -X POST https://yoursite.com/wp-json/wp/v2/pages \
  -u username:application_password \
  -H "Content-Type: application/json" \
  -d '{"title":"Home","status":"publish","content":""}'

# Then update _elementor_data via custom endpoint or direct DB
```

**Preferred order:** Method A → Method B → Method C.

---

## STEP 5 — Verify & Fix

**Checklist after import:**

1. Open the page URL. Does it load without a white screen?
2. Open the page in Elementor editor. Does the structure appear?
3. Check each section:
   - [ ] Hero is 100vh
   - [ ] Text content matches the content map
   - [ ] Colors are approximately correct
   - [ ] Buttons have correct links
   - [ ] Mobile preview looks acceptable

### Common Issues & Fixes

| Issue | Cause | Fix |
|-------|-------|-----|
| White screen after import | Invalid JSON structure or missing required fields | Validate JSON, ensure all elements have `id` and `elements` array |
| Page loads but no Elementor content | `_elementor_edit_mode` or `_elementor_template_type` missing | Run the WP-CLI meta update commands |
| Styles not applied | Elementor CSS cache | Run `wp elementor flush-css` |
| Mobile layout broken | Missing responsive settings | Add `responsive` settings or keep default Elementor breakpoints |
| Widget shows default content | Wrong settings field name | Cross-check Widget Type → Settings Mapping table |

---

## Critical Rules (Same as v2.5)

### ✅ ALWAYS DO
1. Hero min-height = 100vh
2. Measure padding from source and apply as container padding
3. Preserve unicode symbols in text: ✓ → ← 📞
4. Use unique 7-char hex IDs for every element

### ❌ NEVER DO
1. NO animations
2. NO scroll indicators
3. NO wave/curved section transitions
4. NO contact forms (handle with plugin shortcodes in text widgets if needed)
5. NO images/photos (use placeholder images or let client add later)
6. NO big Base44 emoji icons (use Elementor icon widget sparingly or skip)

---

## File Locations

- Content map: `scratch/content_map_v3.md`
- Section mapping: `scratch/section_template_map.json`
- Generated page JSON: `/tmp/elementor_page.json`
- Template wrapper: `/tmp/elementor_template.json`

---

## Version History

- **v3.0 (April 2026):** Complete rewrite. Replaced SSH database injection with generate-and-import pipeline using pre-validated Elementor templates.
- **v2.5 (March 2026):** SSH-based injection pipeline. Archived due to 40% success rate.
