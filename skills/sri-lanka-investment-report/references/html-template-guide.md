# HTML Report Design Guide

This document defines the design system for the Sri Lanka Investment Report HTML output.

## Fonts (Google Fonts CDN)
```
Playfair Display: 400, 700, 900, 400italic — headings, hero title, section titles, card titles
DM Sans: 300, 400, 500, 600 — body text, labels, navigation
DM Mono: 400, 500 — return figures, stat values, codes, dates
```

## Color System (CSS Variables)
```css
--ink: #0f1923          /* primary text */
--ink-soft: #2d3e50     /* body paragraphs */
--ink-muted: #5a6f82    /* labels, captions */
--paper: #faf8f4        /* page background */
--paper-warm: #f4efe6   /* alternate section background */
--gold: #c8922a         /* primary accent — borders, highlights */
--gold-light: #f0d89a   /* hero accent text */
--gold-pale: #fdf5e0    /* badge backgrounds */
--teal: #1a6b6b         /* return value color */
--crimson: #8b1a1a      /* very high risk */
--slate: #334766        /* nav, table headers */
--rule: #c8c0b0         /* dividers, borders */
```

## Layout Structure
```
<nav>                    — fixed, 56px, blur backdrop
<div class="hero">       — dark gradient, centered, with macro badges
<div class="macro-band"> — slate bg, 6-column stat grid
<div class="section">    — alternating paper/warm-paper, container max-width 1100px
<footer>                 — dark ink background
```

## Component Patterns

### Cards (.card)
- White background, 1px border `var(--rule)`, 12px radius, box-shadow
- Top color bar (3px) coded by risk level
- Hover: translateY(-3px) + elevated shadow
- Internal: .card-head (title + risk pill), .card-stats (2-col grid), .card-desc

### Risk Pills (.risk-pill)
- `.rp-vlow`: bg `#d4f0dc`, color `#1a6b2e`
- `.rp-low`: bg `#dff0e4`, color `#2e7a3d`
- `.rp-med`: bg `#fdf5e0`, color `#8a6200`
- `.rp-high`: bg `#ffe8d0`, color `#963d00`
- `.rp-vhigh`: bg `#fce8e8`, color `#8b1a1a`

### Tables
- thead: slate background, white text, uppercase, 0.75rem
- tbody: hover uses `var(--gold-pale)`
- Return cells: DM Mono, font-weight 600, teal color
- Wrapped in `.table-wrap` with overflow-x auto and box-shadow

### Section Headers
```html
<div class="section-header">
  <span class="section-num">01</span>  <!-- gold badge -->
  <h2>Section Title</h2>               <!-- Playfair, gold bottom border -->
</div>
```

### Card Grid
```html
<div class="card-grid">  <!-- auto-fill, minmax(280px,1fr), 1.2rem gap -->
  <div class="card risk-low"> ... </div>
```

### Investor Profile Cards
Three card types: `.conservative` (green gradient), `.moderate` (gold gradient), `.aggressive` (crimson gradient)
Each has: profile-label, profile-name, profile-desc, alloc-list with percentage alloc-pct spans.

## Animation Pattern
```javascript
// Cards animate in on scroll via IntersectionObserver
const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.style.opacity = '1';
      entry.target.style.transform = 'translateY(0)';
    }
  });
}, { threshold: 0.1 });
```
Cards start with `opacity:0; transform:translateY(16px)` and stagger with `animation-delay`.

## Macro Band
6 `.macro-item` cells inside `.macro-grid` (flex, gap 1px, slate bg):
- label (uppercase, 0.7rem, muted)
- value (Playfair Display, 1.6rem, gold-light)
- sub (0.72rem, muted)
- trend (0.8rem, `.up`=green or `.down`=red)

## Disclaimer Box
```html
<div class="disclaimer">  <!-- gold left border, pale yellow bg -->
  <strong>⚠ Disclaimer:</strong> Educational purposes only...
</div>
```

## File Structure
The HTML must be fully self-contained — no external JS dependencies except the Google Fonts CDN link. All CSS inline in `<style>` tag, all JS inline in `<script>` tag at bottom.

## Responsive
- Flex/Grid auto-fill for cards (min 280px)
- Macro band: overflow-x auto
- Tables: overflow-x auto wrapper
- Nav: can simplify on mobile (hide some links)
- Hero: clamp() on font-size for title
