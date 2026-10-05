# Monospace Editorial

**Slug:** `mono-editorial` · **Family:** Product / SaaS · **Lineage:** Vercel Geist (2023 onward), PlanetScale, Resend docs
**Fingerprint:** Near-white page, ink near-black type, monospace eyebrows and labels above a geometric sans body, hairline rules, dense tables and numbered sections, no brand color (the ink is the brand), a single mesh gradient allowed only at hero scale.

## Choose when
- Brief names Vercel, Geist, Next.js, PlanetScale, or "developer docs"
- Context is `docs`, or `marketing` for an infrastructure or API product
- Tone words: precise, technical, documentation, engineered, clean

## Avoid when
- Brief says warm, playful, consumer, friendly
- Product has no technical audience
- **vs terminal:** light, calm, typeset; not a CLI.
- **vs swiss:** mono is the voice; Swiss uses a grotesk throughout and has no mono.
- **vs dark-saas:** light canvas; if the brief wants dark, go there instead.

## Tokens

Measured from vercel.com (May 2026 capture via shadcn.io DESIGN.md) and vercel.com/geist/colors. Do not substitute.

```css
:root {
  /* color */
  --bg: #ffffff;            /* canvas */
  --bg-soft: #fafafa;       /* canvas-soft: page body on marketing */
  --surface: #f5f5f5;       /* canvas-soft-2: card fill, code block bg */
  --text: #171717;          /* ink: the primary. There is no brand blue. */
  --text-muted: #4d4d4d;    /* body */
  --text-subtle: #888888;   /* mute: captions, mono labels */
  --accent: #171717;        /* ink IS the accent. CTAs are black. */
  --link: #0070f3;          /* inline links only */
  --link-deep: #0761d1;
  --border: #ebebeb;        /* hairline */
  --border-strong: #a1a1a1;
  --error: #ee0000; --warning: #f5a623; --success: #0070f3;

  /* the one gradient, hero scale only */
  --mesh: linear-gradient(90deg, #50e3c2, #007cf0, #ff0080, #f9cb28);

  /* type */
  --font-display: "Geist", "Inter", system-ui, sans-serif;
  --font-body: "Geist", "Inter", system-ui, sans-serif;
  --font-mono: "Geist Mono", "JetBrains Mono", ui-monospace, monospace;
  --text-xs: 12px; --text-sm: 14px; --text-base: 16px;
  --text-lg: 20px; --text-xl: 32px; --text-2xl: 48px;
  --weight-body: 400; --weight-display: 600;   /* 600 is the hard cap */
  --tracking-display: -0.05em;                  /* -2.4px at 48px */
  --tracking-mono: 0.02em;

  /* shape: two pill scales, never mixed in one view */
  --radius-sm: 4px; --radius-md: 6px; --radius-lg: 8px; --radius-xl: 12px;
  --radius-pill: 100px;    /* marketing CTAs */
  --radius-full: 9999px;
  --border-w: 1px;

  /* depth: stacked small shadows plus an inset hairline ring, never one heavy drop */
  --shadow-sm: 0 0 0 1px rgba(0,0,0,0.08);
  --shadow-md: 0 0 0 1px rgba(0,0,0,0.08), 0 2px 4px rgba(0,0,0,0.04), 0 4px 8px rgba(0,0,0,0.04);
  --shadow-lg: 0 0 0 1px rgba(0,0,0,0.08), 0 4px 8px rgba(0,0,0,0.06), 0 12px 24px rgba(0,0,0,0.12);

  /* rhythm: 4px base, 12 steps to 192px section gap */
  --space: 4px;
  --section-y: 128px;
  --max-w: 1080px;

  /* motion */
  --dur: 150ms; --ease: ease;
}

@media (prefers-color-scheme: dark) {
  :root {
    --bg: #0a0a0a; --bg-soft: #0a0a0a; --surface: #111111;
    --text: #ededed; --text-muted: #a1a1a1; --text-subtle: #888888;
    --accent: #ededed;
    --border: #1f1f1f; --border-strong: #333333;
    --shadow-sm: 0 0 0 1px rgba(255,255,255,0.08);
    --shadow-md: 0 0 0 1px rgba(255,255,255,0.08), 0 2px 4px rgba(0,0,0,0.4);
    --shadow-lg: 0 0 0 1px rgba(255,255,255,0.08), 0 12px 24px rgba(0,0,0,0.6);
  }
}
```

Geist Sans and Geist Mono are free (Vercel, SIL OFL) and on Google Fonts.

Tailwind v4: prefix each with `--color-`, `--font-`, `--radius-`, `--shadow-` inside `@theme {}`.

## Layout rules
- Max width 1080px, 24px gutter. Vercel's grid is a visible part of the look: use 1px `--border` rules between columns and rows, not gaps.
- Hero: mono eyebrow (12px, uppercase, `--text-subtle`), sentence-case headline at 48px weight 600 tracking -0.05em, one body line, pill CTA in ink.
- Every section gets a numbered or mono label above its heading. This is the signature.
- Tables are first-class. Use them for comparisons and specs with 1px rules and 12px padding.
- Code blocks: `--surface` bg, 1px `--border`, `--radius-lg`, mono at 14px.
- Dark bands: a polarity-flipped section (ink bg, white text) is allowed once per page for showcase or conversion.
- The mesh gradient appears once, in the hero, as a text fill or a thin band. Never on buttons, never shrunk.

## Components

```css
.eyebrow {
  font: 400 var(--text-xs)/1 var(--font-mono);
  letter-spacing: var(--tracking-mono); text-transform: uppercase;
  color: var(--text-subtle); margin-bottom: 12px;
}

.btn {
  font: 500 var(--text-sm)/1 var(--font-body);
  height: 40px; padding: 0 16px;
  border-radius: var(--radius-md);
  border: var(--border-w) solid var(--border-strong);
  background: var(--bg); color: var(--text);
  transition: background var(--dur) var(--ease), border-color var(--dur) var(--ease);
}
.btn:hover { background: var(--surface); border-color: var(--text); }
.btn-primary { background: var(--accent); border-color: var(--accent); color: var(--bg); }
.btn-primary:hover { background: var(--text-muted); border-color: var(--text-muted); }
.btn-marketing { height: 48px; padding: 0 24px; border-radius: var(--radius-pill); }

.card {
  background: var(--bg);
  border-radius: var(--radius-xl);
  box-shadow: var(--shadow-md);
  padding: 24px;
}

.nav {
  height: 64px; display: flex; align-items: center; gap: 24px; padding: 0 24px;
  background: var(--bg);
  border-bottom: var(--border-w) solid var(--border);
}
.nav a { color: var(--text-muted); font-size: var(--text-sm); }
.nav a:hover { color: var(--text); }

.input {
  height: 40px; padding: 0 12px;
  background: var(--bg); color: var(--text);
  border: var(--border-w) solid var(--border-strong);
  border-radius: var(--radius-md);
  font: var(--text-sm) var(--font-body);
}
.input:focus { outline: none; border-color: var(--text); box-shadow: 0 0 0 1px var(--text); }

.hero h1 {
  font: var(--weight-display) clamp(32px, 5vw, 48px)/1.1 var(--font-display);
  letter-spacing: var(--tracking-display);
  color: var(--text);
}
.hero h1 .mesh {
  background: var(--mesh); -webkit-background-clip: text; background-clip: text; color: transparent;
}

.grid-rules { display: grid; grid-template-columns: repeat(3, 1fr); }
.grid-rules > * { padding: 24px; border-right: 1px solid var(--border); border-bottom: 1px solid var(--border); }
.grid-rules > *:nth-child(3n) { border-right: 0; }

table { width: 100%; border-collapse: collapse; font-size: var(--text-sm); }
th { font: 400 var(--text-xs) var(--font-mono); text-transform: uppercase; letter-spacing: var(--tracking-mono); color: var(--text-subtle); text-align: left; padding: 12px; border-bottom: 1px solid var(--border); }
td { padding: 12px; border-bottom: 1px solid var(--border); }
```

## Motion
- Border and background color on hover, 150ms.
- Nothing animates on scroll by default. Vercel's marketing uses subtle reveals; docs use none.
- Never: parallax, kinetic type, gradient animation.

## Do
- Put a mono eyebrow above every section heading.
- Use rules (1px lines) instead of gaps to separate grid cells.
- Keep display weight at 600; the tracking carries the voice.
- Use the pill radius (100px) only on marketing CTAs and the 6px radius on in-product buttons. Never both in one screen.
- Stack small shadows with an inset ring rather than one drop.

## Don't
- No brand color. If the client insists on one, it goes on `--link` and nowhere else.
- No display weight above 600.
- No shrunk gradient on badges or buttons. Hero only.
- No rounded corners above 12px except the pill.
- No illustration. Screenshots, diagrams, and tables only.

## A11y
- `--text` #171717 on #ffffff: 15.3:1. `--text-muted` #4d4d4d: 8.3:1. `--text-subtle` #888888: 3.5:1, so subtle is for labels at 12px uppercase mono only; never body.
- `--link` #0070f3 on white: 4.6:1, passes.
- Mesh gradient as text fill fails contrast at the yellow stop; use it on headlines at 32px+ only, and keep a solid fallback color.
- Focus ring: `box-shadow: 0 0 0 2px var(--bg), 0 0 0 4px var(--text)`.

## Accent-compatible
`hand-drawn` (annotations on diagrams), `terminal` (a single CLI block), `swiss` (a photograph treated as document). Nothing illustrated or textured.

## Reference sites
- https://vercel.com (measured: canvas, ink, hairlines, link, semantic, mesh stops, radius and shadow strategy)
- https://vercel.com/geist/colors (measured: 10-step scale semantics: 100-300 backgrounds, 400-600 borders, 700-800 high contrast, 900-1000 text)
- https://www.shadcn.io/design/vercel (source of the measured capture, May 2026)
- https://planetscale.com (secondary reference)

## Variants

### Variant: planetscale
Overrides: `--bg: #000000` default dark; `--font-display: "Inter"`; mono labels in `--text-subtle` get a leading `#` or `//` glyph. The mesh gradient becomes a single orange `#f35815` accent on CTAs.
Use when: brief names PlanetScale or wants mono-editorial but dark-first.
