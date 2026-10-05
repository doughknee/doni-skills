# Swiss / International Style

**Slug:** `swiss` · **Family:** Rational / Structural · **Lineage:** 1950s Basel and Zürich (Müller-Brockmann, Vignelli), carried today by U.S. Graphics Co., Vitra, Braun
**Fingerprint:** A visible grid, one grotesk typeface at two weights, black on white with a single signal color, 1px rules instead of boxes, flush-left ragged-right, zero radius, zero shadow, photography treated as evidence.

## Choose when
- Context is `dashboard`, `portfolio`, or `docs` and the brief is silent on style
- Brief says: grid, structured, objective, editorial-but-not-magazine, Helvetica, Vignelli, "like a transit map"
- Subject is design, architecture, type, data, or anything where the content should carry the page

## Avoid when
- Brief wants warmth, texture, or personality
- Consumer product with no editorial content
- **vs minimalism:** Swiss has structure you can see; Minimalism has almost nothing to see.
- **vs bauhaus:** Swiss is type-first; Bauhaus is shapes-first.
- **vs mono-editorial:** Swiss uses one grotesk throughout; mono-editorial adds a monospace voice.

## Tokens

Measured from usgraphics.com and vitra.com (Oct 2026, computed styles). Do not substitute.

```css
:root {
  /* color: usgraphics is pure black on white; vitra softens to #333 on white. Both use one signal. */
  --bg: #ffffff;
  --surface: #f7f7f7;        /* vitra section tint; usgraphics uses #eeeeee */
  --text: #000000;           /* usgraphics. Use #101010 (vitra) if pure black feels harsh on large screens */
  --text-muted: #333333;
  --text-subtle: #767676;    /* vitra tertiary */
  --accent: #ff4136;         /* usgraphics signal red. Classic Swiss alternates: #0000ee (vitra link blue), #ffb700 (usgraphics yellow) */
  --accent-2: #002dce;       /* usgraphics link blue */
  --border: #bfbfbf;         /* usgraphics hairline */
  --border-strong: #000000;  /* structural rules */
  --border-soft: #aaaaaa;

  /* type: one grotesk, two weights. Univers (usgraphics) and Futura (vitra) are the originals. */
  --font-display: "Univers", "Helvetica Neue", "Neue Haas Grotesk", "Inter", Helvetica, Arial, sans-serif;
  --font-body: var(--font-display);
  --font-mono: "Berkeley Mono", "JetBrains Mono", ui-monospace, monospace;
  --text-xs: 12px; --text-sm: 13px; --text-base: 15px;
  --text-lg: 18px; --text-xl: 30px; --text-2xl: 48px;
  --weight-body: 400; --weight-display: 700;
  --tracking-display: 0;     /* Swiss does not track display type. Vitra: normal. Usgraphics: normal. */
  --tracking-caps: 0.14em;   /* vitra uppercase buttons: 2.1px at 14px */
  --leading-body: 1.4;       /* usgraphics 18/12 = 1.5, vitra 25.2/18 = 1.4 */

  /* shape: none */
  --radius-sm: 0; --radius-md: 0; --radius-lg: 0; --radius-full: 0;
  --border-w: 1px;

  /* depth: none. Usgraphics' one shadow is a 2px hard offset on buttons, a print metaphor. */
  --shadow-sm: none;
  --shadow-md: none;
  --shadow-lg: none;
  --shadow-print: 2px 2px 0 0 #bbbbbb;

  /* rhythm: the grid is the design */
  --space: 8px;
  --cols: 12;
  --gutter: 24px;
  --section-y: 96px;
  --max-w: 1280px;

  /* motion: none by default */
  --dur: 0ms; --ease: linear;
}
```

Free substitutes: Inter (closest to Univers), Jost or Futura PT (for the Vitra flavor). Never Roboto or Open Sans; their rounded forms are not Swiss.

Tailwind v4: prefix each with `--color-`, `--font-`, `--radius-` inside `@theme {}`. Set `--radius-*` to `0` explicitly so Tailwind's defaults do not leak.

## Layout rules
- 12-column grid, 24px gutter, 1280px max. Draw the grid: columns and rows separated by 1px `--border` rules, not gaps. Usgraphics does this on every page.
- Text sits flush-left on a column edge. Nothing is centered. Nothing is justified.
- Hierarchy by size and weight only: 48 / 30 / 18 / 15 / 13. No color changes for headings.
- Asymmetry is intentional: a headline in columns 1-5, body in 7-12, empty space in 6.
- Images are rectangular, uncropped, no radius, no border, placed on grid lines. Captions in `--text-xs` below.
- Tables are the native component. Every data display is a table with 1px rules.
- Section separators are a single `--border-strong` rule at full width.
- Whitespace is structural, not decorative: an empty column is a decision.

## Components

```css
.btn {
  font: var(--weight-body) var(--text-sm)/1 var(--font-body);
  padding: 8px 14px;
  border: var(--border-w) solid var(--border-strong);
  border-radius: 0;
  background: var(--bg); color: var(--text);
  box-shadow: var(--shadow-print);
}
.btn:hover { background: var(--text); color: var(--bg); box-shadow: none; }
.btn-primary { background: var(--accent); border-color: var(--accent); color: #fff; box-shadow: none; }
.btn-caps { text-transform: uppercase; letter-spacing: var(--tracking-caps); font-weight: 600; }

.card {
  background: var(--bg);
  border-top: var(--border-w) solid var(--border-strong);
  padding: 16px 0 24px;
}
.card h3 { font-size: var(--text-lg); font-weight: var(--weight-display); margin: 0 0 8px; }

.nav {
  display: grid; grid-template-columns: repeat(var(--cols), 1fr); gap: 0 var(--gutter);
  height: 48px; align-items: center;
  border-bottom: var(--border-w) solid var(--border-strong);
  font-size: var(--text-sm); font-weight: var(--weight-display);
}
.nav a { color: var(--text); text-decoration: none; }
.nav a:hover { color: var(--accent); }

.input {
  height: 36px; padding: 0 10px;
  border: var(--border-w) solid var(--border-strong);
  border-radius: 0;
  background: var(--bg); color: var(--text);
  font: var(--text-sm) var(--font-body);
}
.input:focus { outline: 2px solid var(--accent); outline-offset: -2px; }

.hero { display: grid; grid-template-columns: repeat(var(--cols), 1fr); gap: 0 var(--gutter); }
.hero h1 {
  grid-column: 1 / 8;
  font: var(--weight-display) clamp(32px, 4.5vw, 48px)/1.1 var(--font-display);
  letter-spacing: 0; margin: 0;
}
.hero p { grid-column: 8 / 13; font-size: var(--text-lg); line-height: var(--leading-body); }

.grid-rules { display: grid; grid-template-columns: repeat(3, 1fr); }
.grid-rules > * { padding: 16px; border-right: 1px solid var(--border); border-bottom: 1px solid var(--border); }
.grid-rules > *:nth-child(3n) { border-right: 0; }

table { width: 100%; border-collapse: collapse; font-size: var(--text-sm); }
th { text-align: left; font-weight: var(--weight-display); padding: 8px 0; border-bottom: 1px solid var(--border-strong); }
td { padding: 8px 0; border-bottom: 1px solid var(--border); }
```

## Motion
- None by default. Hover states switch instantly (usgraphics: no transitions at all).
- If the context needs feedback (dashboard), allow 100ms linear on background and color only.
- Never: easing curves, fades, parallax, transforms.

## Do
- Draw the grid with 1px rules so the structure is visible.
- Use exactly one typeface at two weights (400, 700).
- Put the accent on one element per view: a rule, a button, a word.
- Set every radius to 0 and every shadow to none. Check Tailwind defaults.
- Let a column sit empty when the content does not need it.

## Don't
- No centered text. Flush-left is the rule.
- No second typeface, no serif, no script.
- No radius, no gradient, no shadow (except the 2px print offset on buttons).
- No icons where a word will do. Swiss sites use words.
- No tracking on display type. Only uppercase labels get letter-spacing.

## A11y
- `--text` #000 on #fff: 21:1. `--text-muted` #333: 12.6:1. `--text-subtle` #767676: 4.5:1, passes at body size exactly; keep it for captions only.
- `--accent` #ff4136 on white: 3.6:1 as text, fails body; use as fill with white text (3.6:1, fails AA for small text; use 18px+ bold on it or switch to `--accent-2` #002dce, 9.6:1).
- Focus: `outline: 2px solid var(--accent); outline-offset: 2px`. The hard outline matches the aesthetic.
- Grid rules at #bfbfbf are decorative; mark grid containers `role="presentation"` when they are not tables.

## Accent-compatible
`mono-editorial` (mono for data tables), `photo-led` (one full-width photograph treated as document), `hand-drawn` (a single marker annotation on a diagram). Nothing textured or rounded.

## Reference sites
- https://usgraphics.com (measured: Univers LT Pro 12/13.2/14/15px at 400/700, 1px rules #bfbfbf and #000, signal colors #ff4136 #ffb700 #00794c, button shadow 2px 2px 0 #bbb, radius 0)
- https://www.vitra.com/en-us/home (measured: vitraFutura 14-32px at 400-600, text #333 and #101010, link #0000ee, surface #f7f7f7, uppercase buttons at 2.1px tracking, radius 0, no borders)
- https://www.swissted.com (poster reference for color and composition)

## Variants

### Variant: vitra
Overrides: `--font-display: "Futura PT", "Jost", sans-serif; --text: #333333; --accent: #0000ee;` buttons become uppercase with `--tracking-caps` and a solid `--text` fill. Softer, more editorial, product-photography-friendly.
Use when: brief names Vitra, Braun, or a furniture or product brand that wants Swiss but not stark.

### Variant: color-field
Overrides: one section per page gets `background: var(--accent)` with white type at display scale. Everything else unchanged.
Use when: brief says "poster-like," "bold," or "Müller-Brockmann."
