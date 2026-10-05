# Scandinavian / Nordic

**Slug:** `scandinavian` · **Family:** Editorial / Print · **Lineage:** IKEA, Muuto, HAY, Normann Copenhagen, Marimekko
**Fingerprint:** White canvas with one warm stone or sage block color per page, a friendly geometric sans at two weights, pill buttons, product photography on natural backgrounds, 1px rules, generous padding, practical and warm rather than austere.

## Choose when
- Context is `ecommerce` or `local-business` and the brief is silent on style
- Brief names IKEA, HAY, Muuto, Marimekko, or says Nordic, Danish, hygge, cozy-but-clean
- Physical products, home goods, cafes, makers, family services
- Tone words: warm, practical, honest, calm, approachable

## Avoid when
- Brief wants luxury, exclusivity, or drama (go `luxury`)
- Brief wants stark, austere, meditative (go `japanese-minimal`)
- Technical product with no photography
- **vs japanese-minimal:** cozier, more color, product-led.
- **vs minimalism:** has warmth, color blocks, and rounded buttons; minimalism has none.
- **vs organic:** grids and rectangles, not blobs.

## Tokens

Measured from ikea.com/us and muuto.com (Oct 2026, computed styles). Two reference points: IKEA is the mass-market end, Muuto the design-house end. Default tokens blend them; variants push to each end.

```css
:root {
  /* color: white canvas, near-black ink, one warm neutral and one muted nature tone */
  --bg: #ffffff;
  --surface: #f5f5f5;         /* ikea: 61 uses. neutral card and section bg */
  --surface-warm: #e9e7e4;    /* muuto stone: 14 uses. the warm alternative */
  --text: #111111;            /* ikea and muuto both: rgb(17,17,17) */
  --text-muted: #484848;      /* ikea body: rgb(72,72,72), 2896 uses */
  --text-subtle: #767676;     /* muuto tertiary */
  --accent: #27455c;          /* muuto slate blue: CTAs and links. ikea alternative: #0058a3 */
  --accent-2: #b7d692;        /* muuto sage: 26 uses, the one block color */
  --accent-earth: #4f3d3a;    /* muuto bark brown */
  --border: #dfdfdf;          /* ikea: 196 uses, the hairline */
  --border-strong: #111111;
  --success: #0a8a00;         /* ikea in-stock green */
  --link: #007cc1;            /* ikea link blue */

  /* type: one geometric sans. IKEA uses Noto IKEA; Muuto uses Euclid Flex (with Spectral serif for quotes). */
  --font-display: "Euclid Flex", "Noto Sans", "Plus Jakarta Sans", "DM Sans", system-ui, sans-serif;
  --font-body: var(--font-display);
  --font-serif: "Spectral", "Source Serif 4", Georgia, serif;   /* quotes and editorial moments only */
  --font-mono: ui-monospace, monospace;
  --text-xs: 12px; --text-sm: 14px; --text-base: 16px;
  --text-lg: 20px; --text-xl: 32px; --text-2xl: 40px; --text-3xl: 70px;
  --weight-body: 400; --weight-display: 700;    /* ikea 700; muuto 500 (see variant) */
  --tracking-display: -0.035em;                  /* ikea h1: -1.39px at 40px. muuto h2: -2.8px at 70px (-0.04em) */
  --tracking-body: -0.02em;                      /* muuto body: -0.32px at 16px */
  --leading-body: 1.45;                          /* muuto 23/16; ikea 21/14 = 1.5 */

  /* shape: pills for buttons, small radius for cards */
  --radius-sm: 4px;           /* ikea: 46 uses */
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-pill: 64px;        /* ikea: 274 uses on buttons and chips. muuto: 60px */
  --radius-full: 50%;
  --border-w: 1px;

  /* depth: none on both sites */
  --shadow-sm: none;
  --shadow-md: none;
  --shadow-lg: 0 8px 24px rgba(17,17,17,0.08);   /* overlays and cart drawer only */

  /* rhythm */
  --space: 8px;
  --section-y: 80px;
  --max-w: 1280px;

  /* motion */
  --dur: 200ms; --ease: ease-out;
}
```

Free substitutes: Plus Jakarta Sans (closest to Euclid Flex), DM Sans, Noto Sans (IKEA's base). Spectral is free on Google Fonts.

Tailwind v4: prefix each with `--color-`, `--font-`, `--radius-`, `--shadow-` inside `@theme {}`.

## Layout rules
- Max width 1280px, 24px gutter on mobile, 40px desktop.
- Hero: a full-width photograph on a natural background (wood, linen, daylight) with a headline overlaid or below, one pill CTA. Or a split: headline left on `--surface-warm`, photo right.
- One block-color section per page in `--accent-2` (sage) or `--surface-warm` (stone). Never two block colors on one page.
- Product grid: 4-up desktop, 2-up mobile, 16px gap, images on `--surface` with 4px radius, name in `--text`, price in `--text` bold.
- Every section is separated by `--section-y` padding or a 1px `--border` rule. No cards with edges; content sits on the canvas or on a tint.
- Buttons are pills. Chips and filters are pills. Inputs are not.
- Headlines at 40px (IKEA) to 70px (Muuto) depending on how editorial the page is. Tracking tightens with size.
- Pull quotes and story sections may switch to `--font-serif`.
- Photography rule: natural light, real rooms, no studio white unless it is a product thumbnail.

## Components

```css
.btn {
  font: 700 var(--text-sm)/1 var(--font-body);
  height: 48px; padding: 0 24px;
  border-radius: var(--radius-pill);
  border: var(--border-w) solid var(--border-strong);
  background: var(--bg); color: var(--text);
  transition: background var(--dur) var(--ease), color var(--dur) var(--ease);
}
.btn:hover { background: var(--text); color: var(--bg); }
.btn-primary { background: var(--text); border-color: var(--text); color: var(--bg); }
.btn-primary:hover { background: var(--text-muted); border-color: var(--text-muted); }
.btn-accent { background: var(--accent); border-color: var(--accent); color: #fff; }
.chip { height: 36px; padding: 0 16px; border-radius: var(--radius-pill); border: 1px solid var(--border); background: var(--bg); font-size: var(--text-sm); }
.chip[aria-pressed="true"] { background: var(--text); color: var(--bg); border-color: var(--text); }

.card {              /* product card: no box */
  display: grid; gap: 8px;
}
.card img { aspect-ratio: 1; object-fit: cover; background: var(--surface); border-radius: var(--radius-sm); }
.card h3 { font: 700 var(--text-base)/1.3 var(--font-body); margin: 0; letter-spacing: var(--tracking-body); }
.card .price { font: 700 var(--text-base) var(--font-body); }
.card .meta { font: 400 var(--text-sm) var(--font-body); color: var(--text-muted); }

.nav {
  height: 72px; display: flex; align-items: center; gap: 32px; padding: 0 40px;
  background: var(--bg);
  border-bottom: var(--border-w) solid var(--border);
  font: 400 var(--text-base) var(--font-body); letter-spacing: var(--tracking-body);
}
.nav a { color: var(--text); text-decoration: none; }
.nav a:hover { text-decoration: underline; text-underline-offset: 4px; }

.input {
  height: 48px; padding: 0 16px;
  border: var(--border-w) solid var(--border);
  border-radius: var(--radius-sm);
  background: var(--bg); color: var(--text);
  font: var(--text-base) var(--font-body);
}
.input:focus { outline: none; border-color: var(--text); box-shadow: 0 0 0 1px var(--text); }

.hero h1 {
  font: var(--weight-display) clamp(32px, 5vw, 56px)/1.1 var(--font-display);
  letter-spacing: var(--tracking-display); color: var(--text); margin: 0;
}
.hero p { font-size: var(--text-lg); line-height: var(--leading-body); color: var(--text-muted); max-width: 520px; }

.block { background: var(--accent-2); padding: var(--section-y) 40px; }
.block-warm { background: var(--surface-warm); }
.block h2 { font: 500 clamp(32px, 5vw, 70px)/1 var(--font-display); letter-spacing: -0.04em; }

.quote { font: 400 var(--text-xl)/1.3 var(--font-serif); color: var(--text); max-width: 720px; }
```

## Motion
- Background and color on hover, 200ms ease-out.
- Product images: scale 1.03 on hover, 300ms. That is the only transform.
- Sections do not animate on scroll. The calm is the point.
- Cart drawer slides from the right, 250ms.

## Do
- Pick one block color per page and use it for one section.
- Put products on `--surface` thumbnails and lifestyle shots in natural light.
- Use pills for every button and chip.
- Keep body at 16px with -0.02em tracking; it reads tidy without being tight.
- Switch to the serif for one quote or story moment per page.

## Don't
- No shadows on cards. Hairlines and tints only.
- No saturated accent. The sage and slate are muted on purpose.
- No more than two neutrals plus one nature tone on a page.
- No stock photography of people pointing at laptops. Real rooms, real objects.
- No rounded inputs. Pills are for actions, not fields.

## A11y
- `--text` #111 on white: 19.3:1. `--text-muted` #484848: 9.0:1. `--text-subtle` #767676: 4.5:1, passes at the line.
- `--text` on `--accent-2` sage #b7d692: 12.4:1, passes. `--text` on `--surface-warm` #e9e7e4: 16.1:1.
- `--accent` #27455c on white: 9.3:1 as text; white on `--accent`: 9.3:1. Both pass.
- `--link` #007cc1 on white: 4.5:1, passes at the line.
- Focus ring: `outline: 2px solid var(--text); outline-offset: 2px`. On pills, the ring follows the radius automatically.

## Accent-compatible
`hand-drawn` (a doodle arrow or underline on the hero), `photo-led` (one full-bleed room shot), `organic` (one blob-masked image). Nothing dark, nothing techy.

## Reference sites
- https://www.ikea.com/us/en/ (measured: text #111111 and #484848, hairline #dfdfdf, surface #f5f5f5, link #007cc1, in-stock #0a8a00, h1 40px/700 at -1.39px tracking, body 14px/21px, pill radius 64px on 274 elements, 4px on cards, no shadows)
- https://www.muuto.com (measured: Euclid Flex 16px/400 at -0.32px, h2 70px/500 at -2.8px, sage #b7d692, stone #e9e7e4, slate #27455c, bark #4f3d3a, Spectral serif for quotes, pill radius 60px, no shadows)
- https://www.hay.dk (visual reference; blocks the headless browser)

## Variants

### Variant: ikea
Overrides: `--accent: #0058a3; --accent-2: #ffdb00;` (Swedish blue and yellow, the yellow only on one promo band or the CTA), `--weight-display: 700`, `--font-display: "Noto Sans"`, body 14px. Denser grids, 6-up product rows, price in 20px bold.
Use when: brief names IKEA, or is mass-market retail with many SKUs.

### Variant: design-house
Overrides: `--weight-display: 500; --text-3xl: 70px;` headlines at 70px with -0.04em; `--accent-2` stays sage; add `--font-serif` quotes on every story section; product grid loosens to 3-up with 32px gaps.
Use when: brief names Muuto, HAY, Normann, or says "design studio," "gallery," "considered."
