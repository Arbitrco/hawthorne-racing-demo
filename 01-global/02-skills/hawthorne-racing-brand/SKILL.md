---
name: hawthorne-racing-brand
description: "Hawthorne Racing brand design system. ALWAYS use this skill whenever asked to create any document, presentation, slide deck, PDF, report, sponsorship deck, one-pager, media kit, proposal, memo, or any downloadable/shareable deliverable for Hawthorne Racing. Also trigger when asked to create Word documents, PowerPoint presentations, branded content, or any visual deliverable in the Hawthorne Racing scenario or demo context. This skill contains all brand rules, colors, fonts, logo usage, layout patterns, and format-specific implementation notes. Use it even if the user doesn't mention 'brand'; any document creation for Hawthorne Racing should follow these rules."
---

# Hawthorne Racing Brand Design System

This skill defines the complete visual identity for Hawthorne Racing. Every document, presentation, and PDF must follow these rules. No exceptions.

## Brand Overview

**Company:** Hawthorne Racing
**Positioning:** Precision motorsport team built on data, engineering, and racecraft. "Precision Drives Victory."
**Tagline:** Engineered. Focused. Relentless.
**Website:** hawthorneracing.com
**Contact:** info@hawthorneracing.com
**Phone (placeholder):** +44 1234 567890

Note: Hawthorne Racing is a demo/scenario brand. Contact details on the brand boards are placeholders; use the values above unless told otherwise.

---

## Color Palette

| Role | Color | Hex | Usage |
|------|-------|-----|-------|
| Racing Green | Bright green | #0B8E3E | Primary accent: section labels, headline underscores, links, CTAs, stat highlights, logo accent |
| Dark Green | Deep green | #05642B | Secondary accent: hover states, chart secondary series, depth fills on green surfaces |
| Charcoal | Near-black | #1C1F23 | Header bands, table headers, cover and closing backgrounds, primary headings, dark UI |
| Silver | Cool gray | #B6BCC3 | Secondary strokes in the track-line motif, muted meta text on dark backgrounds, chart gridlines |
| Off-White | Pale gray | #F2F4F5 | Alternating table rows, light page backgrounds, cards on charcoal |
| White | Pure white | #FFFFFF | Content page backgrounds, card bodies, text on dark |
| Body Text | Dark gray | #2B3038 | Body copy on white (derived from charcoal, softened for reading) |
| Border | Light gray | #E2E6E9 | Table borders, card borders, divider lines |
| Text Muted | Gray | #6B7280 | Stat descriptions, secondary text |
| Text Hint | Light gray | #8D939C | Footers, metadata, captions |
| Tint | Pale green | #EDF7F1 | Callout box background on white pages |

### Rules
- **No gradients in documents.** The badge artwork has depth but all document surfaces are flat color.
- Charcoal (#1C1F23) plays the structural role: header bands, table headers, cover/closing pages. Content pages are white.
- Racing Green (#0B8E3E) is the accent on white/light backgrounds and the label color on charcoal.
- Racing Green on charcoal passes contrast only for bold text at 9pt or larger. Small text on charcoal uses white or Silver (#B6BCC3), never green.
- Dark Green (#05642B) never carries text on dark backgrounds. It is a fill/depth color only.
- Silver is never used for body text on white (insufficient contrast). Meta/hint text on white uses #8D939C at minimum sizes only.
- The two brand boards list Racing Green as #0B8E3E and #0B8F3E. #0B8E3E is canonical. Always use #0B8E3E.

---

## Typography

The brand voice is condensed, italic, motorsport-industrial. Headlines lean forward.

| Element | Font | Weight/Style | Size | Case | Spacing |
|---------|------|--------------|------|------|---------|
| Page title | Barlow Condensed (PDF) / Arial Narrow (PPTX/DOCX) | 800 Italic / Bold Italic | 32-38pt | ALL CAPS | 1px letter-spacing |
| Section heading | Barlow Condensed / Arial Narrow | 800 Italic / Bold Italic | 16-24pt | ALL CAPS | 1px letter-spacing |
| Section label | Barlow / Calibri | 700 Bold (not italic) | 9-10pt | ALL CAPS | 2.5px letter-spacing, Racing Green |
| Group heading | Barlow / Calibri | 700 Bold | 10pt | ALL CAPS | 2px letter-spacing, Racing Green, underline border |
| Body text | Barlow (PDF) / Calibri (DOCX/PPTX) | 400 Regular | 10.5-11pt | Sentence case | Normal |
| Caption/footer | Barlow / Calibri | 500 Medium | 8.5-9pt | Sentence case | Normal, #8D939C |
| Stat number | Barlow Condensed / Arial Narrow | 800 Italic | 24-32pt | | |

### Font Sources
- **PDF (weasyprint):** Use Barlow Condensed + Barlow via `@font-face` with woff2 files from the `@fontsource/barlow-condensed` and `@fontsource/barlow` npm packages. Google Fonts import URLs are blocked in sandboxed environments.
- **PPTX/DOCX:** Arial Narrow Bold Italic for headings and stat numbers, Calibri for body (both universally installed). If Arial Narrow is unavailable, fall back to Arial Bold Italic.

### Rules
- ALL headings are uppercase, bold, and italic. Italic is part of the brand; do not straighten headings.
- Section labels and group headings are NOT italic. Only headings and stat numbers lean.
- Section labels (e.g., "RACE OPERATIONS") are Racing Green, 9pt, bold, all caps, 2.5px spacing. They sit above the section heading.
- Group headings (e.g., "AERO", "POWERTRAIN", "PARTNERS") are Racing Green, 10pt, bold, all caps, 2px spacing, with a bottom border in #E2E6E9. Used to separate grouped cards within a page.
- Body text is always left-aligned. Never center body text.
- Line height for body text: 1.5-1.65.

---

## Logo Files

Logos are in the `assets/` directory of this skill. All PNGs already have transparent backgrounds; no background-stripping step is required. Trim transparent padding before placement so the logo's left edge aligns with content, then record exact output pixel dimensions.

| File | Description | Use On |
|------|-------------|--------|
| `logo-primary-horizontal.png` (916x178) | Full-color horizontal lockup: eagle + HR mark + wordmark | Light content pages, DOCX headers, PPTX content slides, business docs |
| `logo-stacked.png` (416x251) | Full-color stacked lockup | Square-ish placements, cover pages where horizontal is too wide |
| `logo-icon.png` (274x160) | Eagle + HR mark only, full color | Favicons, small placements, watermarks, slide corners |
| `logo-reversed-panel.png` (1353x237) | Reversed lockup with its charcoal plate baked in | ALL dark-surface placements: covers, header bands, closing pages |
| `logo-mono-charcoal.png` (506x112) | Single-color charcoal lockup | Fax/mono contexts, subtle watermarks on light backgrounds |
| `logo-mono-green.png` (493x111) | Single-color Racing Green lockup | Green-accent contexts on white, merch mockups |

### ⚠️ Assets are used AS PROVIDED. Never edit pixels.
Do not recolor, strip backgrounds, delete the plate, or otherwise modify any logo asset. Proportional resizing and trimming fully transparent padding are the only permitted operations. The design works around the assets, not the other way round.

### The plate-blend rule (dark surfaces)
The reversed lockup ships with its charcoal plate baked in. Its flat plate field is **#1D242A**. Any document surface that hosts the reversed logo (cover pages, closing pages, content-page header bands) MUST use **#1D242A** as its background so the plate blends seamlessly and the rounded plate corners disappear. Standalone charcoal elements that carry no logo (table headers, code blocks, stat card headers) keep brand charcoal #1C1F23; the difference between the two is imperceptible but the logo surfaces must match the plate exactly.

### Logo Processing Steps
1. Load the PNG (already RGBA transparent; the reversed panel's transparency is only outside its rounded plate)
2. Find bounding box of non-transparent pixels and crop to it
3. Resize to target dimensions preserving aspect ratio (LANCZOS)
4. **Record the exact output pixel dimensions (width x height) after resizing**
5. Never alter pixel colors or alpha inside the artwork

### Logo Placement Rules
- **Cover pages (PDF/PPTX):** Reversed panel logo on a #1D242A background, top-left, aligned with heading text below. Height ~0.58in (PDF) or ~0.6in (PPTX); the plate padding means the visible mark reads slightly smaller, so size up ~15% vs a plateless logo.
- **Content pages (PDF):** Reversed panel logo, top-right inside the #1D242A header band. Height ~34px.
- **Content pages (PPTX):** Reversed panel logo, top-right in the #1D242A band. Width ~1.6in.
- **DOCX header:** Primary full-color logo on white, right-aligned, correct aspect ratio. Width 130px, height calculated from aspect ratio (130 x 178/916 ≈ 25px).
- **Closing pages:** Reversed panel logo on #1D242A, centered, larger (~0.95in height).
- **Icon watermark:** `logo-icon.png` at 8-12% opacity may sit in the bottom-right of section dividers. Nowhere else.

### ⚠️ Critical: Logo Sizing in weasyprint (PDF)

Weasyprint **ignores** HTML `width` and `height` attributes on `<img>` tags and will stretch the image to fill its container. You **must** set dimensions using inline CSS `style`.

```html
<!-- CORRECT -->
<img src="data:image/png;base64,..."
     alt="Hawthorne Racing"
     style="display:block; width:162px; height:26px; max-width:162px;" />

<!-- WRONG: weasyprint ignores these attributes -->
<img src="data:image/png;base64,..." width="162" height="26" alt="Hawthorne Racing" />
```

After processing the logo PNG, record the exact output pixel dimensions and hardcode them into the inline style. Never use `height: auto` or omit the width.

---

## Brand Motifs

### Track-Line Motif (primary decorative element)
Sweeping diagonal racing stripes: one Racing Green line, one thick charcoal line, one silver line, running parallel and kinking upward at roughly 40 degrees, with a fading dot grid to the lower right. This replaces any generic geometric pattern.

Rules:
- Use on covers, closing pages, section dividers, and stationery-style footers only. Never behind body text.
- Build as inline SVG: 2-3 `<polyline>` or `<path>` elements. Green stroke 4-6px, charcoal stroke 10-16px, silver stroke 3-4px, plus a `<pattern>` or generated grid of 2px silver dots at 25-40% opacity.
- On charcoal backgrounds, the charcoal stripe becomes off-white at 12-18% opacity so the motif reads.
- Position: lower-left sweeping to upper-right, occupying the bottom third or right half of the page. Content never overlaps the stripes.

### Dot Grid
Small dot matrix (2px dots, 10px pitch) in Silver at 25-40% opacity, used as a fade-out texture at the trailing edge of the track-line motif. Never used alone as a full-page background.

---

## Layout Components

### Stat Cards (primary card style)
Charcoal header band with Racing Green label text, white body below with an italic condensed stat number and description. Used for key metrics (lap times, points, sponsorship reach, budget figures).

```
┌─────────────────────────────┐
│ ▓▓ LABEL (green on charcoal)│  ← #1C1F23 bg, #0B8E3E text, 9pt bold, ALL CAPS, 2.5px spacing
├─────────────────────────────┤
│ 1:42.318                    │  ← Barlow Condensed/Arial Narrow 24-32pt bold italic, #1C1F23
│ Description text            │  ← 8.5-9pt, #6B7280
└─────────────────────────────┘
```
- Border: 1px #E2E6E9
- Corner radius: 6px (PDF only; PPTX uses rectangles)
- Always in rows of 3
- Always add `page-break-inside: avoid`

### Callout Box (green tint + left border)
```
┃ Callout text here in 10pt body color on #EDF7F1 background
```
- Background: #EDF7F1
- Left border: 3px solid #0B8E3E
- Border radius: 0 6px 6px 0 (PDF only)
- Padding: 14-16px
- Text: 10pt, #2B3038, line-height 1.5-1.6
- Always add `page-break-inside: avoid`

### Data Table
- Header row: #1C1F23 background, white text, 8.5pt bold, ALL CAPS, letter-spacing
- Body rows: alternating white / #F2F4F5
- Borders: 1px #E2E6E9 horizontal only
- Cell padding: 8px vertical, 12px horizontal
- Top-left header corner radius: 6px (PDF only)
- Highlight column or winning row: 3px left border in #0B8E3E, never a full green fill

### Group Heading (for grouped card sections)
Used to separate groups (departments, race weekends, sponsor tiers) across pages. Renders as a green uppercase label with a bottom border, NOT a section-level heading.

```css
.group-heading {
  font-family: 'Barlow', sans-serif;
  font-weight: 700;
  font-size: 10pt;
  color: #0B8E3E;
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-top: 0.18in;
  margin-bottom: 0.1in;
  border-bottom: 2px solid #E2E6E9;
  padding-bottom: 5px;
  page-break-after: avoid;
}
.group-heading:first-child { margin-top: 0; }
```

### Tier / Pricing Cards
Same as stat cards but with tier name, price, and period (e.g., sponsorship tiers). Featured card gets a 2px #0B8E3E border and a "LEAD PARTNER" or "RECOMMENDED" badge in green.

---

## Page Patterns

### Cover Page (PDF & PPTX)
- Background: #1D242A (matches the reversed logo's plate; see plate-blend rule)
- Track-line motif: sweeping stripes lower-left to upper-right (green + off-white at 15% + silver), dot grid fading at the trailing edge, occupying the bottom third
- Logo: `logo-reversed-panel.png`, top-left. **Use inline CSS for sizing.**
- Label: Racing Green, 10pt, bold, ALL CAPS (e.g., "SPONSORSHIP PROPOSAL")
- Title: White, 36-38pt, bold italic, ALL CAPS (e.g., "PRECISION DRIVES VICTORY")
- Subtitle: White at 60% opacity, 11-12pt, not italic
- Footer: pinned to bottom using `flex: 1` spacer + `cover-push` pattern (do NOT use `position: absolute; bottom:` on cover)
- Cover inner layout uses `display: flex; flex-direction: column` with `position: absolute; top:0; left:0; right:0; bottom:0` (explicit sides; `inset` is not supported by weasyprint)

### Content Page (PDF)
- Background: White
- Header band at top (~0.92in) in #1D242A with page title in white bold italic ALL CAPS, and reversed panel logo right-aligned
- Use named `@page content` with `@bottom-left` / `@bottom-right` margin boxes for footer
- Content area: 0.8in horizontal padding, 0.38in top padding
- Section labels → section headings → body text → components
- Footer via `@page`: "Document title - Hawthorne Racing" left, "info@hawthorneracing.com · hawthorneracing.com" right, with border-top

### Content Slide (PPTX)
- Background: White
- Header band in #1D242A: 0.95in tall, title in white 22pt bold italic ALL CAPS
- Reversed panel logo: top-right in the band
- Content: starts at y=1.05in
- Footer: divider line at y=5.3in, footer text at y=5.35in
- ALL content must end above y=5.1in

### Section Divider
- Same as cover pattern but with section title instead of report title. Optional icon watermark bottom-right at 8-12% opacity.

### Closing Page
- Background: #1D242A
- Track-line motif (same as cover)
- Reversed panel logo centered. **Use inline CSS for sizing.**
- Tagline: "ENGINEERED. FOCUSED. RELENTLESS." in Silver, letter-spaced, centered below logo
- Contact: Racing Green links centered below tagline
- Legal: white at 25% opacity below contact
- Closing inner uses `position: absolute; top:0; left:0; right:0; bottom:0` (not `inset`)

### DOCX Content Page
- Header: primary full-color logo right-aligned on white, divider line below
- Headings: Arial Narrow bold italic, ALL CAPS, with letter-spacing
- Section labels: Calibri 9pt bold, Racing Green, ALL CAPS
- Footer: divider line, "Document - Hawthorne Racing" left, "info@hawthorneracing.com · hawthorneracing.com" right (tab stops)

---

## Forbidden List

Absolute rules. Never violate them:

1. **No gradients** in documents: not in backgrounds, shapes, or text
2. **No clip art or stock illustrations**; motorsport photography only, and only where supplied
3. **No 3D chart effects**
4. **No red, yellow, or blue accents.** The palette is green/charcoal/silver only. Checkered-flag patterns are also off-brand; the track-line motif is the only pattern.
5. **No upright headings.** Headings are always bold italic. Labels and body are upright.
6. **No centered body text**; left-align all paragraphs
7. **No generic greens**; always #0B8E3E or #05642B exactly
8. **No green small text on charcoal**; green on dark is for bold labels 9pt+ only
9. **No editing of supplied logo assets.** Use them exactly as provided. On dark surfaces, use the reversed panel asset and set the surface to #1D242A so the plate blends. On light surfaces, use the full-color or mono lockups.

---

## Format-Specific Implementation

### PDF (HTML → weasyprint)

**Approach:** Build a fully styled HTML file with CSS, then convert with weasyprint.

**Named page types:**
```css
@page cover   { size: letter; margin: 0; }
@page closing { size: letter; margin: 0; }
@page content {
  size: letter;
  margin: 0;
  @bottom-left {
    content: "Sponsorship Proposal - Hawthorne Racing";
    font-family: 'Barlow', sans-serif;
    font-size: 8pt; color: #8D939C;
    padding-left: 0.8in;
    border-top: 1px solid #E2E6E9;
    padding-top: 0.1in;
  }
  @bottom-right {
    content: "info@hawthorneracing.com · hawthorneracing.com";
    font-family: 'Barlow', sans-serif;
    font-size: 8pt; color: #8D939C;
    padding-right: 0.8in;
    border-top: 1px solid #E2E6E9;
    padding-top: 0.1in;
  }
}
```

Assign pages via the CSS `page` property:
```css
.cover-page   { page: cover;   page-break-after: always; }
.closing-page { page: closing; page-break-before: always; }
.content-page { page: content; page-break-before: always; }
```

**Key CSS patterns:**
```css
/* Cover/closing: fixed full-page height, overflow hidden */
.cover-page, .closing-page {
  width: 8.5in; height: 11in;
  position: relative; overflow: hidden;
  background: #1D242A; /* matches reversed logo plate */
}

/* Inner: explicit sides, NOT inset (unsupported) */
.cover-inner, .closing-inner {
  position: absolute;
  top: 0; left: 0; right: 0; bottom: 0;
  display: flex; flex-direction: column;
  padding: 0.65in 0.8in 0.55in 0.8in;
}

.cover-push { flex: 1; }

/* Content page: flowing layout, no fixed height */
.content-page { background: #FFFFFF; }

/* Charcoal header band */
.page-header {
  background: #1D242A; /* matches reversed logo plate */
  padding: 0 0.8in; height: 0.92in;
  display: flex; align-items: center; justify-content: space-between;
  page-break-inside: avoid; page-break-after: avoid;
}
.page-header-title {
  font-family: 'Barlow Condensed', sans-serif; font-weight: 800; font-style: italic;
  font-size: 16pt; color: #FFFFFF;
  text-transform: uppercase; letter-spacing: 1.5px;
  line-height: 1.2; max-width: 5.5in;
}

/* Page body */
.page-body { padding: 0.38in 0.8in 0.3in 0.8in; }

/* Stat cards */
.stat-row { display: flex; gap: 0.16in; margin: 0.14in 0; page-break-inside: avoid; }
.stat-card { flex: 1; border: 1px solid #E2E6E9; border-radius: 6px; overflow: hidden; page-break-inside: avoid; }
.stat-card-head { background: #1C1F23; padding: 0.08in 0.14in; }
.stat-card-head span { color: #0B8E3E; font-size: 8pt; font-weight: 700; letter-spacing: 2.5px; text-transform: uppercase; display: block; }
.stat-card-num { font-family: 'Barlow Condensed', sans-serif; font-weight: 800; font-style: italic; font-size: 26pt; color: #1C1F23; }

/* Callout */
.callout { background: #EDF7F1; border-left: 3px solid #0B8E3E; border-radius: 0 6px 6px 0; padding: 0.15in 0.2in; margin: 0.16in 0; page-break-inside: avoid; }

/* Cards */
.item-card { border: 1px solid #E2E6E9; border-radius: 6px; padding: 0.11in 0.14in; display: flex; justify-content: space-between; gap: 0.12in; margin-bottom: 0.09in; page-break-inside: avoid; }
```

**Font loading:** Install `@fontsource/barlow-condensed` and `@fontsource/barlow` via npm, then use `@font-face` declarations pointing to local woff2 files (include the 800-italic weights for Barlow Condensed). Do NOT use Google Fonts `@import` URLs.

**Track-line motif on cover/closing:** Inline `<svg>` with `position:absolute; bottom:0; left:0; width:100%; height:38%`, containing 2-3 diagonal `<path>` strokes (Racing Green #0B8E3E, off-white at 15% opacity, Silver #B6BCC3 at 60%) plus a dot grid. Place the SVG as a sibling to the inner content div, not inside it.

**Logo in PDF - mandatory sizing:** process the PNG, record exact output px dimensions, hardcode into inline `style`. Never rely on HTML width/height attributes.

**weasyprint known limitations:**
- `inset` - NOT supported. Use explicit `top/left/right/bottom`.
- `box-shadow` - NOT supported. Omit.
- HTML `width`/`height` attributes on `<img>` - ignored. Always use inline CSS.

**Page overflow prevention:**
- No `height: 11in` on content pages; only cover and closing are fixed-height.
- Split long sections into multiple explicit `.content-page` divs, each with its own `page-header`. Never rely on weasyprint auto page-break to split a content div (it creates headerless pages).
- Add `page-break-inside: avoid` to every card, callout, stat row, and table.
- Add `page-break-after: avoid` to every heading and group-heading.

**Content page structure:** each `.content-page` contains a `.page-header` div then a `.page-body` div. Footer is handled by `@page content` margin boxes; no footer div in HTML.

**QA:** After generating the PDF, convert with `pdftoppm -jpeg -r 180` and inspect every page. Check for logo distortion, blank pages, missing continuation headers, content cut off at page bottom, cover footer bunched under subtitle, and closing content not vertically centered.

### PPTX (pptxgenjs)

**Setup:**
```javascript
const pptxgen = require("pptxgenjs");
let pres = new pptxgen();
pres.layout = "LAYOUT_16x9"; // 10" x 5.625"
```

**Critical spacing rules:**
- Header band (#1D242A, matches logo plate): x=0, y=0, w=10, h=0.95
- Content starts at y=1.05
- Footer line at y=5.3, footer text at y=5.35
- **All content must end above y=5.1**
- Use `margin: 0` on all text elements

**Stat cards in PPTX:**
```javascript
// Charcoal header
slide.addShape(pres.shapes.RECTANGLE, { x: cx, y: cy, w: 2.85, h: 0.32, fill: { color: "1C1F23" } });
slide.addText(label, { x: cx+0.15, y: cy, w: 2.55, h: 0.32, fontFace: "Calibri", fontSize: 8.5, bold: true, color: "0B8E3E", charSpacing: 2.5, valign: "middle", margin: 0 });
// White body with italic condensed stat
slide.addShape(pres.shapes.RECTANGLE, { x: cx, y: cy+0.32, w: 2.85, h: 0.72, fill: { color: "FFFFFF" }, line: { color: "E2E6E9", width: 0.75 } });
slide.addText(stat, { x: cx+0.15, y: cy+0.36, w: 2.55, h: 0.4, fontFace: "Arial Narrow", fontSize: 24, bold: true, italic: true, color: "1C1F23", margin: 0 });
```

**Headings on slides:** `fontFace: "Arial Narrow", bold: true, italic: true`, ALL CAPS text, `charSpacing: 1.5`.

**Common pitfalls:**
- Never use `#` prefix on hex colors (corrupts file)
- Never reuse option objects (pptxgenjs mutates them); use factory functions
- Never encode opacity in hex strings; use the `opacity` property
- Use `charSpacing` not `letterSpacing`
- Track-line motif: use `pres.shapes.LINE` elements (green, silver, white) with `transparency` 40-85 on charcoal slides

**Logo on content slides:** reversed panel logo at x=8.1, y=0.28, w=1.6 inside the #1D242A band (aspect 1353:237, so h≈0.28 at w=1.6). Band and plate blend because they share the same color.

### DOCX (docx-js)

**Setup:**
```javascript
const { Document, Packer, Paragraph, TextRun, Table, TableRow, TableCell, ImageRun, Header, Footer, ... } = require('docx');
```

**Page size:** set explicitly (docx-js defaults to A4):
```javascript
page: { size: { width: 12240, height: 15840 }, margin: { top: 1440, right: 1080, bottom: 1440, left: 1080 } }
```

**Heading styles override:**
```javascript
{ id: "Heading1", run: { size: 34, bold: true, italics: true, font: "Arial Narrow", color: "1C1F23", allCaps: true, characterSpacing: 20 } }
{ id: "Heading2", run: { size: 26, bold: true, italics: true, font: "Arial Narrow", color: "1C1F23", allCaps: true, characterSpacing: 15 } }
{ id: "Heading3", run: { size: 18, bold: true, font: "Calibri", color: "0B8E3E", allCaps: true, characterSpacing: 40 } }
```

**Logo in header:** primary full-color logo, right-aligned, correct aspect ratio:
```javascript
new Paragraph({
  alignment: AlignmentType.RIGHT,
  children: [new ImageRun({ data: logoData, transformation: { width: 130, height: 25 }, type: "png" })],
  border: { bottom: { style: BorderStyle.SINGLE, size: 4, color: "E2E6E9", space: 8 } }
})
```

**Callout box:** single-cell Table with green left border and tinted shading:
```javascript
new TableCell({
  borders: { left: { style: BorderStyle.SINGLE, size: 12, color: "0B8E3E" }, top: noBorder, bottom: noBorder, right: noBorder },
  shading: { fill: "EDF7F1", type: ShadingType.CLEAR }
})
```

**Stat cards:** two-row Table, charcoal header row with green label text, white body row with bold italic stat numbers.

**Critical rules:**
- Always `ShadingType.CLEAR`, never `SOLID`
- Always `WidthType.DXA`, never percentages
- Set both `columnWidths` on the table AND `width` on each cell
- Never use `\n`; use separate Paragraph elements
- Never use unicode bullets; use `LevelFormat.BULLET`

---

## Multi-Page Section Layout (PDF)

When a section contains many components (e.g. sponsor tiers, race calendar cards, department groups):

**Rule 1 - One logical group per page.** Split groups across multiple `.content-page` divs, each with its own `page-header`.

**Rule 2 - Group headings as visual separators.** Use `.group-heading` (Racing Green, uppercase, 10pt, bottom border) at the top of each group within a page.

**Rule 3 - Never rely on auto page-break for content pages.** Always break explicitly by closing one `.content-page` div and opening a new one with a full header.

**Rule 4 - Dense-text page pattern.** When a page has 4+ paragraphs plus a callout and a CTA block, reduce body to 10pt / line-height 1.5:
```css
.page-body.dense p { font-size: 10pt; line-height: 1.5; margin-bottom: 0.08in; }
.page-body.dense .callout { margin: 0.1in 0; padding: 0.12in 0.18in; }
.page-body.dense .cta-block { margin-top: 0.13in; }
```

---

## Footer Pattern

Content page footers via `@page content` margin boxes:

**Left:** `[Document type] - Hawthorne Racing`
**Right:** `info@hawthorneracing.com · hawthorneracing.com`

Both use `border-top: 1px solid #E2E6E9` and `padding-top: 0.1in`.

Cover page footer: `Hawthorne Racing · [Month Year] · hawthorneracing.com`, pinned to bottom with the `.cover-push` flex spacer, white at ~42% opacity, 8.5pt Barlow.

---

## Mandatory QA Step

After generating ANY asset (PDF, PPTX, or DOCX):

1. Convert to images (PDF: `pdftoppm -jpeg -r 180`; PPTX/DOCX: LibreOffice → PDF → `pdftoppm`)
2. Visually inspect every page/slide
3. Check specifically for:
   - **Logo distortion** (stretched wide = inline CSS sizing not applied)
   - **Plate seams around the reversed logo** (visible rectangle edges mean the host surface is not #1D242A; fix the surface color, never the asset)
   - **Blank or near-blank pages** (content overflow; split into explicit `.content-page` divs)
   - **Missing header on continuation pages**
   - **Content cut off at page bottom** (add `page-break-inside: avoid`)
   - **Cover footer bunched under subtitle** (ensure `.cover-push` spacer)
   - **Closing content not vertically centered**
   - **Italic headings rendering upright** (font fallback dropped italic; verify the italic woff2 is loaded / `italics: true` set)
4. Fix all issues and re-verify before delivering.

Never deliver a file without visual inspection.

---

## Accessibility

- Body text (#2B3038) on white: ratio 12.6:1 ✓
- White text on charcoal (#1C1F23): ratio 16.4:1 ✓
- Racing Green (#0B8E3E) on white: ratio 4.6:1 ✓ (fine for labels and headings)
- Racing Green on charcoal: ratio ~3.9:1; bold 9pt+ labels only, never small or regular-weight text
- Silver (#B6BCC3) on charcoal: ratio 8.7:1 ✓
- Never place text over the track-line motif or photography without a solid or heavily-scrimmed surface behind it
