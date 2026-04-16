---
name: schema-markup
description: Implement structured data (Schema.org) to enhance search visibility
type: procedural
keywords: ["schema markup", "structured data", "Schema.org", "rich snippets", "SEO markup"]
auto_detect: true
agent_type: sub
---

# Schema Markup

Implement structured data to enhance search visibility with rich snippets and improved understanding.

## When to Use
- Product pages (ecommerce)
- Review/Rating content
- Articles and blog posts
- Local business pages
- Events, courses, recipes
- FAQ pages

## Don't Use When
- The markup doesn't match visible content
- You're using it to manipulate rankings
- The page type doesn't have appropriate schema

## Schema Types by Use Case

### Organization / LocalBusiness
**Best for:** Company info, local SEO

**Properties:**
- name, url, logo
- address, telephone
- sameAs (social profiles)
- openingHours (LocalBusiness)
- geo coordinates (LocalBusiness)

### Product
**Best for:** Ecommerce product pages

**Properties:**
- name, description, image
- brand
- offers (price, availability, currency)
- aggregateRating
- review

### Article / BlogPosting
**Best for:** Blog posts, news articles

**Properties:**
- headline, description
- author (name, url)
- datePublished, dateModified
- image
- publisher (Organization)

### Review / AggregateRating
**Best for:** Review content, testimonials

**Properties:**
- itemReviewed
- reviewRating (ratingValue, bestRating)
- author
- reviewBody
- aggregateRating (ratingValue, reviewCount)

### FAQPage
**Best for:** FAQ sections

**Properties:**
- mainEntity (Question)
  - name (the question)
  - acceptedAnswer (Answer)
    - text (the answer)

### HowTo
**Best for:** Step-by-step guides

**Properties:**
- name, description, image
- totalTime
- estimatedCost
- step (HowToStep)
  - name, text, url, image

### BreadcrumbList
**Best for:** Navigation breadcrumbs

**Properties:**
- itemListElement
  - position, name, item (URL)

### VideoObject
**Best for:** Video content

**Properties:**
- name, description
- thumbnailUrl
- uploadDate
- duration
- contentUrl (actual video file)

## Implementation Methods

### JSON-LD (Recommended)
Place in `<head>` or `<body>`:

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Product Name",
  "description": "Product description",
  "image": "https://example.com/image.jpg",
  "brand": {
    "@type": "Brand",
    "name": "Brand Name"
  },
  "offers": {
    "@type": "Offer",
    "price": "99.99",
    "priceCurrency": "USD",
    "availability": "https://schema.org/InStock"
  }
}
```

### Microdata
Inline HTML attributes (more complex, harder to maintain).

### RDFa
Another inline method, less common.

## Testing & Validation

**Google Tools:**
- Rich Results Test: Test specific pages
- Schema Markup Validator: General validation
- URL Inspection Tool: See indexed structured data

**Third-party:**
- Schema.org validator
- Chrome extensions (Structured Data Testing Tool alternatives)

## Common Mistakes

1. **Mismatch** — Markup doesn't match visible content
2. **Incomplete** — Required properties missing
3. **Spam** — Fake reviews, incorrect markup
4. **Conflicts** — Multiple schemas for same content
5. **Syntax errors** — Invalid JSON

## Best Practices

- Use JSON-LD for easier maintenance
- Test every implementation
- Keep markup updated with content changes
- Don't mark up hidden/irrelevant content
- Use specific types over generic ones
- Include all required properties

## Tools & Generators

- Google's Structured Data Markup Helper
- Schema App
- Merkle's Schema Markup Generator
- TechnicalSEO.com Tools

## Related Skills

- **seo-audit** — Technical SEO foundation
- **ai-seo** — AI-assisted optimization
