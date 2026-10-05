# Gradient Mesh

**Slug:** `gradient-mesh` · **Family:** Product / SaaS · **Lineage:** Stripe (2018 onward), Mercury, Ramp
**Fingerprint:** White canvas, a multi-color mesh gradient washing the upper third of the hero and nowhere else, light-weight display type with negative tracking, one indigo CTA per section, tabular figures on every number, dark navy app mockups composited over the white page.

## Choose when
- Context is `marketing` and the brief is silent on style
- Brief names Stripe, Mercury, Ramp, Brex, or "fintech"
- Product handles money, data, or infrastructure and wants to feel trustworthy and modern at once
- Tone words: polished, premium, confident, financial

## Avoid when
- Brief says dark, moody, edgy, or developer-first (go `dark-saas`)
- Brief says warm, handmade, small, local
- **vs dark-saas:** light background; color comes from gradients, not glow.
- **vs glass:** the gradient sits behind opaque content, not behind frosted panels.

## Tokens

Measured from stripe.com (May 2026 capture via shadcn.io DESIGN.md). Do not substitute.

```css
:root {
  /* color */
  --bg: #ffffff;             /* canvas */
  --bg-soft: #f6f9fc;        /* canvas-soft: alternating sections, cool white */
  --surface: #ffffff;        /* cards sit on bg-soft */
  --text: #0d253d;           /* ink: navy, never pure black */
  --text-muted: #273951;     /* ink-secondary */
  --text-subtle: #64748d;    /* ink-mute: captions */
  --accent: #533afd;         /* indigo: the one filled button per band */
  --accent-deep: #4434d4;    /* hover */
  --accent-press: #2e2b8c;
  --accent-soft: #665efd;
  --accent-bg: #b9b9f9;      /* subdued hover bg */
  --navy: #1c1e54;           /* dark app mockup frames and dark bands */
  --border: #e3e8ee;         /* hairline */
  --border-input: #a8c3de;
  --ruby: #ea2261; --magenta: #f96bee; --cream: #f5e9d4; --lemon: #9b6829;
  --shadow-tint: #003770;    /* shadows are tinted navy, never gray */

  /* the mesh: five stops, hero only, upper third of the viewport */
  --mesh:
    radial-gradient(at 10% 10%, var(--cream) 0, transparent 50%),
    radial-gradient(at 90% 0%, #ffd4a3 0, transparent 45%),
    radial-gradient(at 60% 30%, #c4b5fd 0, transparent 50%),
    radial-gradient(at 30% 60%, var(--accent) 0, transparent 55%),
    radial-gradient(at 85% 70%, var(--ruby) 0, transparent 50%);

  /* type: Söhne at weight 300 for display. Inter 300 with ss01 is the open substitute. */
  --font-display: "Söhne", "Inter", system-ui, sans-serif;
  --font-body: "Söhne", "Inter", system-ui, sans-serif;
  --font-mono: "Söhne Mono", "JetBrains Mono", ui-monospace, monospace;
  --text-xs: 12px; --text-sm: 14px; --text-base: 16px;
  --text-lg: 20px; --text-xl: 32px; --text-2xl: 56px;
  --weight-body: 400; --weight-display: 300;
  /* tracking: -1.4px at 56px, -0.2px at 20px */
  --tracking-display: -0.025em;
  --font-features: "ss01", "tnum";   /* tabular numerals on every figure */

  /* shape */
  --radius-sm: 4px; --radius-md: 8px; --radius-lg: 16px; --radius-full: 9999px;
  --border-w: 1px;

  /* depth: navy-tinted, soft, multi-layer */
  --shadow-sm: 0 2px 5px -1px rgba(0,55,112,0.08), 0 1px 3px -1px rgba(0,0,0,0.05);
  --shadow-md: 0 6px 12px -2px rgba(0,55,112,0.12), 0 3px 7px -3px rgba(0,0,0,0.1);
  --shadow-lg: 0 13px 27px -5px rgba(0,55,112,0.18), 0 8px 16px -8px rgba(0,0,0,0.15);

  /* rhythm */
  --space: 4px;
  --section-y: 112px;
  --max-w: 1080px;

  /* motion */
  --dur: 200ms; --ease: cubic-bezier(0.25, 0.1, 0.25, 1);
}
```

Tailwind v4: prefix each with `--color-`, `--font-`, `--radius-`, `--shadow-` inside `@theme {}`. Put `--mesh` on a `.hero-mesh` utility, not in the theme.

## Layout rules
- Max width 1080px, 24px gutter. Stripe's content column is narrow; whitespace does the premium work.
- Hero: mesh gradient fills the top 60-70vh, skewed 6-8° on its bottom edge (`clip-path` or `transform: skewY(-6deg)` on the background layer only). Headline at 56px weight 300, subhead at 20px, one indigo CTA plus one text link with arrow.
- A dark navy app mockup (`--navy` frame, `--radius-lg`, `--shadow-lg`) sits at the hero's right or overlaps its bottom edge.
- Sections alternate `--bg` and `--bg-soft`. The skewed divider may repeat once more mid-page.
- Feature sections: text left (max 440px), illustration or mockup right. Alternate.
- Every number uses tabular figures. Pricing, stats, and tables set `font-feature-settings: "tnum"`.
- One filled indigo button per section. Secondary actions are text links with a trailing arrow.
- Logo bar in grayscale at 60% opacity.

## Components

```css
.btn {
  font: 500 var(--text-sm)/1 var(--font-body);
  height: 40px; padding: 0 16px;
  border-radius: var(--radius-full);
  border: var(--border-w) solid var(--border);
  background: var(--bg); color: var(--text);
  transition: all var(--dur) var(--ease);
}
.btn:hover { border-color: var(--text-subtle); }
.btn-primary { background: var(--accent); border-color: var(--accent); color: #fff; box-shadow: var(--shadow-sm); }
.btn-primary:hover { background: var(--accent-deep); border-color: var(--accent-deep); }
.btn-primary:active { background: var(--accent-press); }
.link-arrow { color: var(--accent); font-weight: 500; }
.link-arrow::after { content: " →"; display: inline-block; transition: transform var(--dur) var(--ease); }
.link-arrow:hover::after { transform: translateX(4px); }

.card {
  background: var(--surface);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
  padding: 32px;
  transition: transform var(--dur) var(--ease), box-shadow var(--dur) var(--ease);
}
.card:hover { transform: translateY(-2px); box-shadow: var(--shadow-lg); }

.nav {
  height: 64px; display: flex; align-items: center; gap: 32px; padding: 0 24px;
  background: transparent;   /* sits on the mesh */
}
.nav a { color: var(--text); font-size: var(--text-sm); font-weight: 500; opacity: 0.85; }
.nav a:hover { opacity: 1; }

.input {
  height: 40px; padding: 0 12px;
  border: var(--border-w) solid var(--border-input);
  border-radius: var(--radius-md);
  background: var(--bg); color: var(--text);
  font: var(--text-sm) var(--font-body);
  box-shadow: inset 0 1px 2px rgba(0,55,112,0.06);
}
.input:focus { outline: none; border-color: var(--accent); box-shadow: 0 0 0 3px var(--accent-bg); }

.hero { position: relative; overflow: hidden; }
.hero-mesh {
  position: absolute; inset: 0 0 20% 0;
  background: var(--mesh); background-color: var(--bg-soft);
  transform: skewY(-6deg); transform-origin: top left;
  z-index: 0;
}
.hero > * { position: relative; z-index: 1; }
.hero h1 {
  font: var(--weight-display) clamp(36px, 5.5vw, 56px)/1.1 var(--font-display);
  letter-spacing: var(--tracking-display);
  color: var(--text);
  font-feature-settings: var(--font-features);
}

.mockup {
  background: var(--navy);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-lg);
  padding: 12px;
}

.stat { font-feature-settings: "tnum"; font-size: var(--text-xl); font-weight: 300; letter-spacing: -0.02em; }
```

## Motion
- Buttons and cards: 200ms, slight lift (2px) and shadow step on hover.
- Arrow links slide 4px right on hover.
- The mesh may drift slowly (60s loop, `background-position` only) if the brief wants "alive." Off by default.
- Sections fade up 16px over 400ms on scroll, once.
- Never: bounce, spin, glow pulse, gradient hue rotation.

## Do
- Keep the mesh in the hero and nowhere else. One instance per page.
- Set display at weight 300. The lightness is the signal of confidence.
- Use tabular numerals everywhere a number appears.
- Tint every shadow with navy, never neutral gray.
- Let the dark navy mockup be the only dark element on the page.

## Don't
- No mesh on buttons, cards, or badges. Stripe never shrinks it.
- No pure black text. Ink is navy.
- No second filled button color. Indigo only.
- No display weight above 400.
- No warm grays. All neutrals lean cool (`--bg-soft` #f6f9fc).

## A11y
- `--text` #0d253d on white: 15.4:1. `--text-muted` #273951: 11.6:1. `--text-subtle` #64748d: 4.9:1, passes.
- `--accent` #533afd on white: 5.8:1 as text, passes. White on `--accent`: 5.8:1, passes.
- Weight 300 at 56px passes; weight 300 below 24px does not render reliably on Windows and drops perceived contrast. Keep body at 400.
- The mesh behind nav links: ensure links sit over a region where contrast with `--text` stays at or above 4.5:1; the cream and lavender stops are safe, the ruby and indigo stops are not. Keep nav over the top-left quadrant.
- Focus ring: `box-shadow: 0 0 0 3px var(--accent-bg)`.

## Accent-compatible
`hand-drawn` (annotations on mockups), `isometric` (one 3D object in the hero instead of a mockup), `bento` (feature grid as tiles on `--bg-soft`). Nothing dark, nothing textured.

## Reference sites
- https://stripe.com (measured: ink #0d253d, indigo #533afd and its ladder, canvas-soft #f6f9fc, hairline #e3e8ee, input border #a8c3de, Söhne 300 display with -1.4px tracking at 56px, tnum figures, navy mockups #1c1e54, cream #f5e9d4, ruby #ea2261)
- https://www.shadcn.io/design/stripe (source of the measured capture, May 2026)
- https://mercury.com (secondary reference: same family, serif display variant)

## Variants

### Variant: mercury
Overrides: `--font-display: "Tiempos Headline", "Newsreader", serif; --weight-display: 400;` mesh stops shift to `#e8e4f5`, `#dbe9f6`, `#f5e9d4` (quieter). Ink stays navy.
Use when: brief names Mercury, or wants gradient-mesh with a serif and less saturation.

### Variant: aurora
Overrides: mesh stops become `#a5f3fc`, `#c4b5fd`, `#fbcfe8`, `#fde68a` on `#ffffff`; hero gets a 90s `background-position` drift animation. Display weight 400.
Use when: brief says "aurora," "northern lights," or asks for the gradient to move.
