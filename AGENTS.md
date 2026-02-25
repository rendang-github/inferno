# AGENTS.md - Call of the Inferno

This document provides guidance for AI coding agents working in this repository.

## Project Overview

This is a static HTML website for a D&D 5E campaign supplement called "Call of the Inferno". The site is a single-page document with embedded CSS, custom fonts, and images, designed for both web viewing and print.

## Build/Lint/Test Commands

This project has **no build system, test framework, or linting tools**. It is a static HTML site.

### Preview the site locally

```bash
# Using Python's built-in server
python3 -m http.server 8000

# Using Node.js (if available)
npx serve .

# Using PHP (if available)
php -S localhost:8000
```

Then open http://localhost:8000 in a browser.

### Validation

```bash
# Validate HTML using the W3C validator (requires curl)
curl -H "Content-Type: text/html; charset=utf-8" --data-binary @index.html https://validator.w3.org/nu/?out=json

# Check for broken links in images (manual inspection)
grep -o 'src="img/[^"]*"' index.html | sort -u
```

## Project Structure

```
inferno/
├── index.html      # Main HTML file (single-page application)
├── CNAME           # GitHub Pages custom domain (inferno.warlordsofbeer.com)
├── font/           # Custom fonts
│   ├── MoriaCitadel.TTF    # Decorative header font
│   └── konquer-Regular.ttf # Body text font
└── img/            # Campaign images (PNG, JPG)
```

## Code Style Guidelines

### HTML

- Use semantic HTML5 elements where appropriate
- Maintain consistent 4-space indentation
- Use lowercase for element and attribute names
- Always close tags properly
- Use `&amp;`, `&lt;`, `&gt;` for special characters

### CSS (embedded in `<style>` tag)

- All CSS is embedded in the `<head>` within a single `<style>` block
- Use lowercase class names with underscores or no separators (e.g., `.inline99`, `.stylecap`)
- Group related styles together
- Use RGBA for colors with transparency: `rgba(122, 32, 13, 0.3)`
- Use hex colors for solid colors: `#7a200d`, `#750800`
- Maintain the existing selector ordering: base styles → layout → typography → components

### Typography

The project uses a specific typography hierarchy:

- **H1**: Moria Citadel font, 60px, centered, dark red (#750800)
- **H2**: Palatino, 38px, small-caps, bordered top
- **H3**: Palatino, 30px, small-caps, dark red (#7a200d)
- **H4**: Palatino, 20px, small-caps, bordered bottom
- **H5**: Small-caps, 18px
- **Body**: Georgia/serif

### Color Palette

Primary colors used throughout:

- Dark red/brown: `#750800`, `#7a200d`, `#551609`
- Green accent (tables, flavour boxes): `#cfe7ce`
- Paper background: `img/paper.jpg`

### Layout Classes

Key CSS classes and their purposes:

| Class | Purpose |
|-------|---------|
| `.page` | Two-column layout container with `column-count: 2` |
| `.background` | Main content wrapper with paper texture |
| `.flavour` | Green highlighted example/narrative boxes |
| `.green` | Striped table styling |
| `.tcenterN` | Center-align table column N |
| `.tleftN` | Left-align table column N |
| `.trightN` | Right-align table column N |
| `.hero` | Full-width banner image |
| `.inline`, `.inline97-99` | Inline images with text wrap |
| `.portrait` | Character portrait container |
| `.stylecap` | Large decorative drop cap |
| `.spoiler` | Hidden text (reveals on hover) |
| `.break` | Section break with border |

### Images

- Store all images in `img/` directory
- Use PNG for images with transparency
- Use JPG for photographs
- Reference images relative to root: `src="img/filename.png"`
- Use appropriate class for layout (`.hero`, `.inline`, `.portrait`, `.illustration`)

### Tables

Tables follow a consistent pattern:

```html
<table class="green tcenter1 tcenter2 tleft3">
    <tr><th>Header 1</th><th>Header 2</th><th>Header 3</th></tr>
    <tr><td>Value 1</td><td>Value 2</td><td>Value 3</td></tr>
</table>
```

### Flavour Text Boxes

Example boxes use this structure:

```html
<div class="flavour">
    <strong>Character Name</strong> descriptive text here...
</div>
```

### Page Breaks

For print layout, pages use:

```html
<div class="page">
    <!-- page content -->
</div>
```

Each `.page` div creates a new two-column section with a page break after.

### Drop Caps

Large decorative first letters:

```html
<div class="stylecap"><span>T</span></div>ext continues here...
```

## Print Considerations

The CSS includes `@media print` rules for printing. When making changes:

- Test print styles using browser print preview
- Maintain `break-after: always` on `.page` divs
- Keep margins and backgrounds print-friendly

## Deployment

This site is deployed to GitHub Pages with a custom domain. To deploy:

1. Push changes to the main branch
2. GitHub Pages will automatically rebuild the site
3. The site is served at https://inferno.warlordsofbeer.com

## Common Tasks

### Adding a new section

1. Create a new `<div class="page">` container
2. Add appropriate heading (h2 for major sections, h3 for subsections)
3. Include images with proper classes
4. Close the div properly

### Adding a new image

1. Place image file in `img/` directory
2. Choose appropriate class (hero, inline, portrait, illustration)
3. For text-wrap images, use the div wrapper pattern:

```html
<div class="portrait"><img class="portrait" src="img/filename.png"></div>
```

### Adding a table

1. Use the `.green` class for styling
2. Add alignment classes as needed
3. Include `<th>` for header rows

## Notes

- This is a single-page document with no JavaScript
- All content is in index.html
- No external dependencies or CDNs
- Fonts are self-hosted in the `font/` directory
