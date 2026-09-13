# Aayushi Fab — Design System

Extracted from the live `index.html` build. This is the single source of truth for every additional page (About Us, Capabilities, Certifications, Featured Fabrics, Contact). Do not introduce new colors, fonts, radii, or spacing values outside what's documented here.

## 1. Visual Theme & Atmosphere

A quiet, editorial, natural-materials aesthetic for a 75+ year old sustainable polyester fabric manufacturer. Deep sage greens and soft off-whites read as "green manufacturing" without being literal or cheap-looking. Full-bleed photography carries the storytelling — the brief is explicit that this is an image-led, low-text site, closer to a lookbook than a corporate brochure. Fraunces (a warm, slightly quirky serif) is reserved for headlines to add craft and warmth; Work Sans carries everything else with restraint. Borders are hairline, shadows are almost absent, and the one deliberately decorative flourish — the pinking-shear zigzag border on fabric swatches — is the brand's signature device and should not be diluted elsewhere.

**Key characteristics**
- Natural, muted sage-green palette over warm off-white — never pure white-on-white
- Full-bleed photography as the primary storytelling tool, text kept brief and supporting
- Fraunces serif (light/regular weights, occasionally italic) for all headlines, Work Sans for everything else
- Pill-shaped buttons only; no sharp-cornered CTAs
- Hairline borders (1px) instead of shadows to separate sections; the one exception is the soft shadow under the About/Story image
- Uppercase, wide-tracked micro-labels (eyebrows, pillar labels, stat labels) as a recurring rhythm device
- The zigzag-edged fabric swatch card is the brand's signature UI element — reuse it verbatim wherever fabric imagery appears

## 2. Color Palette & Roles

| Token | Hex | Role |
|---|---|---|
| `--color-bg` | `#FFFFFF` | Default page background |
| `--color-bg-soft` | `#F1F5EE` | Soft section backgrounds (e.g. Pillars band) |
| `--color-sage` | `#6F8F63` | Mid-tone accent, rarely used directly |
| `--color-sage-deep` | `#4E6B45` | Primary accent — icons, eyebrow labels, link hover, button hover fill |
| `--color-sage-pale` | `#DCE7D6` | Pale accent fills |
| `--color-ink` | `#1C2420` | Primary text, default button fill/border color |
| `--color-ink-soft` | `#4A544C` | Secondary/body text |
| `--color-line` | `#D8E2D2` | Hairline dividers and borders on light backgrounds |
| `--color-stats-bg` | `#3B5434` | Dark green banner background (stats section) |
| `--color-footer-bg` | `#1C2A18` | Footer background, darkest green |

No pure black is used anywhere. No new hues (no blue, purple, red, etc.) should be introduced — certification badges and buyer logos will bring their own color and should sit on white/pale cards to stay neutral.

## 3. Typography

**Fonts:** `Fraunces` (display/serif, weights 300/400/500, italic 300/400) for headlines only. `Work Sans` (400/500/600) for everything else. Loaded via Google Fonts, already linked in `<head>`.

| Role | Font | Size (clamp/fixed) | Weight | Notes |
|---|---|---|---|---|
| H1 / Hero heading | Fraunces | `clamp(2.2rem, 5vw, 3.9rem)` | 300 | line-height 1.1, max-width 800px |
| H2 / Section heading | Fraunces | `clamp(1.8rem, 3.5vw, 2.7rem)` | 400 | line-height ~1.18 |
| Eyebrow / micro-label | Work Sans | `0.7rem` | 600 | uppercase, letter-spacing 0.18–0.22em, color `--color-sage-deep` |
| Body / paragraph | Work Sans | `0.92–0.94rem` | 400 | line-height 1.7–1.8, color `--color-ink-soft`, max-width capped (~430–500px) to keep line length readable |
| Button/CTA label | Work Sans | `0.8rem` | 600 | uppercase, letter-spacing 0.05–0.06em |
| Nav link | Work Sans | `0.83rem` | 500 | color `--color-ink-soft`, underline-on-hover via `::after` |
| Stat number | Fraunces | `clamp(2rem, 3.5vw, 2.9rem)` | 300 | tabular, tight line-height |
| Stat label | Work Sans | `0.82rem` | 500 | color rgba white 0.78 (on dark bg) |

Base body font-size is 16px, line-height 1.5.

## 4. Components

### Buttons (all pill-shaped, `border-radius: 999px`)
- **Solid (on photo/dark):** white background, ink text, 1.5px white border → hover: transparent bg, white text/border
- **Outline (on photo/dark):** transparent bg, white text, 1.5px `rgba(255,255,255,0.5)` border → hover: border solid white, bg `rgba(255,255,255,0.1)`
- **Outline (on light bg, e.g. "Get in Touch", "Discover Our Story"):** transparent bg, ink text, 1.5px ink border → hover: fills solid ink bg, white text
- **Solid dark (e.g. "Explore All Fabrics"):** ink bg, white text → hover: `--color-sage-deep` bg
- Padding: `13px 30px` (hero CTAs) or `12px 28px` (secondary) or `15px 40px` (primary solid); all uppercase, 0.8rem, weight 600, letter-spacing 0.05–0.06em

### Fabric swatch card — signature component, reuse exactly
```
.fabric-card > .fabric-ph (aspect-ratio 3/4, gradient/photo fill)
  > .zigzag-overlay (15px border-image using zigzag.png, pinking-shear effect, pointer-events:none)
.fabric-card-label (0.7rem, 600, uppercase, letter-spacing 0.1em)
.fabric-card-link ("View Fabrics" + arrow SVG, color shifts to sage-deep + arrow slides 3px on hover)
```
Hover lifts the whole swatch `translateY(-6px)`. This exact structure is what the Featured Fabrics page should repeat 30–40 times in a flat grid — do not restyle, resize the border weight, or change the hover behavior.

### Cards / sections generally
- No visible shadows except the About/Story image wrap: `box-shadow: 0 28px 72px rgba(28,36,32,0.14)`, `border-radius: 14px`
- Section dividers are hairline borders (`1px solid var(--color-line)` on light, `1px solid rgba(255,255,255,0.15)` on dark), not cards-in-boxes
- Icons: inline SVG, 24×24 viewBox, `stroke-width: 1.4`, color `--color-sage-deep` on light backgrounds or `rgba(255,255,255,0.65)` on dark

### Navigation
- Fixed header, 72px height, white bg, border-bottom appears only after scroll (`.is-scrolled`)
- Links get a 1px underline that grows from left on hover/active (`::after` transform scaleX)
- Desktop (>760px): inline horizontal links + "Get in Touch" pill button on the right
- Mobile (≤760px): top-level "Get in Touch" button in header bar is hidden; hamburger toggles a full-width sliding dropdown panel containing the 5 navigation links and an integrated full-width "Get in Touch" pill button (`.nav-mobile-cta`) at the bottom of the list. Auto-closes on link click.

### Footer
- Dark (`--color-footer-bg`), 4-column grid (`1.9fr 1fr 1fr 1.55fr`) → 2 cols @1100px → 1 col @760px
- Column headings: 0.68rem, 600, uppercase, letter-spacing 0.14em
- Links at 0.5 white opacity, hover to full/near-full opacity
- Circular social icons: 36px, 1px border at 0.18 opacity, hover brightens border+icon

## 5. Layout, Section Rhythm & Card Plating

- **Max content width:** 1440px, centered
- **Container padding:** 52px desktop → 36px @1100px → 24px @760px → 16px @500px
- **Section vertical padding:** large sections run 90–124px top/bottom on desktop, roughly halving on mobile (80–90px)
- **Alternating Section Rhythm:** Every page alternates between `--color-bg` (pure white for breathing room, hero copy, fabric swatches) and `--color-bg-soft` (`#F1F5EE` for warm sage grounding) rather than long stretches of plain white.
- **Card Plating:** Grouped cards (certifications, buyer logos, focus pillars, pillar icons) sit on `--color-bg-soft` backgrounds as white/tinted cards (`background: var(--color-bg)` with `border: 1px solid var(--color-line)`), separating cleanly without heavy shadows.
- **Dark Green Banners (`--color-stats-bg`, `#3B5434`):** High-impact conversion and legacy bands (homepage stats, About legacy strip, Capabilities CTA, Fabrics inquiry CTA, Certifications verification CTA) all share this authoritative deep-sage background with white typography and pill buttons.
- **Grids:** Pillars 3-col → 1-col @900px · Fabrics teaser 5-col → 2-col @760px · Stats 4-col → 2-col @900px → 1-col @500px · Footer 4-col → 2-col @1100px → 1-col @760px
- **Breakpoints:** 1100px, 900px, 760px, 500px (match these exactly — don't add new ones)

## 6. Do's and Don'ts

**Do**
- Keep every new page inside the same fixed header / footer already built, unchanged
- Alternate section backgrounds so the sage-green brand identity is felt structurally throughout the page
- Keep copy short — one or two sentences per section max, per the client's explicit "not text-heavy" instruction
- Let photography carry each section; use the same `fabric-ph`-style gradient placeholders only until real photos are supplied
- Reuse the eyebrow + Fraunces-heading + Work-Sans-subtext pattern for every new section header
- Keep all buttons pill-shaped and match one of the four documented button styles — no new button style

**Don't**
- Don't leave long consecutive stretches of pure white sections
- Don't introduce a new accent color for a "special" page (e.g. Certifications badges should sit neutrally on white/pale cards, not get a new brand color)
- Don't add drop shadows to cards/sections beyond the one documented exception
- Don't change the zigzag swatch card's structure, proportions, or hover behavior
- Don't add a contact form or social-follow section — the client explicitly ruled both out
- Don't add sharp-cornered buttons or non-pill CTAs

## 7. Reference Implementation

`index.html` is the canonical implementation of all tokens above. When building a new page, copy its `<head>` (fonts, meta), header, and footer markup verbatim, and build the new page's `<main>` content using only the components and tokens documented here.