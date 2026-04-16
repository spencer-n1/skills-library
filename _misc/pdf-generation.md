# PDF Generation with ReportLab

Reference for generating professional, branded PDFs from scratch using Python's ReportLab library. Use this for client deliverables, research reports, proposals, and any document that needs consistent formatting.

---

## When to Use

- Client research reports (branded, professional formatting)
- Proposals and quotes
- Contracts and agreements
- Any deliverable that needs to look polished and consistent

---

## Basic Setup

```python
from reportlab.lib.pagesizes import letter
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer, PageBreak
from reportlab.lib.styles import getSampleStyleSheet

# Create document
doc = SimpleDocTemplate("output.pdf", pagesize=letter)
styles = getSampleStyleSheet()
story = []
```

---

## Common Elements

### Title and Headings
```python
# Title
title = Paragraph("Report Title", styles['Title'])
story.append(title)
story.append(Spacer(1, 12))

# Heading
story.append(Paragraph("Section Header", styles['Heading1']))
```

### Body Text
```python
body = Paragraph("Your content here... " * 20, styles['Normal'])
story.append(body)
story.append(Spacer(1, 12))
```

### Page Breaks
```python
story.append(PageBreak())
```

### Build the PDF
```python
doc.build(story)
```

---

## ⚠️ Critical: Unicode Subscript/Superscript

**DO NOT use Unicode characters** like ₀₁₂₃₄₅₆₇₈₉ or ⁰¹²³⁴⁵⁶⁷⁸⁹ — they render as black boxes.

**USE XML tags instead:**

```python
# Subscripts: <sub> tag
chemical = Paragraph("H<sub>2</sub>O", styles['Normal'])

# Superscripts: <super> tag  
squared = Paragraph("x<super>2</super> + y<super>2</super>", styles['Normal'])
```

---

## Advanced: Custom Styles

```python
from reportlab.lib.styles import ParagraphStyle
from reportlab.lib.enums import TA_CENTER, TA_LEFT

# Custom title style
custom_title = ParagraphStyle(
    'CustomTitle',
    parent=styles['Heading1'],
    fontSize=24,
    textColor='#0a0a0a',
    spaceAfter=30,
    alignment=TA_CENTER
)
```

---

## Canvas Approach (for simple docs)

```python
from reportlab.pdfgen import canvas

c = canvas.Canvas("hello.pdf", pagesize=letter)
width, height = letter

# Add text
c.drawString(100, height - 100, "Hello World!")

# Add a line
c.line(100, height - 140, 400, height - 140)

c.save()
```

---

## Quick Reference

| Task | Method |
|------|--------|
| Multi-page structured doc | Platypus (SimpleDocTemplate) |
| Single page, simple layout | Canvas |
| Subscripts | `<sub>` tag in Paragraph |
| Superscripts | `<super>` tag in Paragraph |
| Page break | `PageBreak()` element |
| Spacing | `Spacer(1, height)` |

---

## Related

- For extracting text/tables from existing PDFs: use `pdfplumber`
- For OCR on scanned PDFs: `pytesseract` + `pdf2image`
- For merging/splitting: `pypdf`

---

*Source: Anthropic PDF Skill (skills/pdf)*  
*Saved for future agency deliverables*
