# Editorial / Magazine

**Slug:** `editorial` · **Family:** Editorial / Print · **Lineage:** The New York Times (web, 2014 redesign onward), The New Yorker, The Atlantic
**Fingerprint:** A multi-family newsroom type stack (display serif, text serif, label sans), 1px hairlines and gray tints instead of shadows, near-square 3px corners, uppercase tracked eyebrows above every section, chromatic color used as signal (breaking, developing, live) and never as button fill, dense columns.

## Choose when
- Context is `blog` and the brief is silent on style
- Brief names NYT, The Atlantic, New Yorker, a newspaper, a magazine, "long-form," or "journalism"
- Site publishes articles with bylines, sections, and dates
- Tone words: serious, literary, authoritative, reported

## Avoid when
- Site has fewer than 20 articles or no regular publishing cadence (go `minimalism` or `scandinavian`)
- Brief wants playful, startup, or product-led
- **vs luxury:** Editorial is dense; Luxury is empty.
- **vs swiss:** Editorial mixes serif and sans across families; Swiss is one grotesk.
- **vs mono-editorial:** no monospace; the eyebrow is a tracked sans, not mono.

## Tokens

Measured from nytimes.com (May 2026 capture via shadcn.io DESIGN.md). Do not substitute.

```css
:root {
  /* color: a six-step ink ladder on white; hairlines carry all elevation */
  --bg: #ffffff;
  --surface: #ebebeb;         /* surface tint: section backgrounds, quote blocks */
  --text: #121212;            /* ink primary */
  --text-2: #363636;          /* ink secondary: body */
  --text-3: #5a5a5a;          /* ink tertiary: bylines, dates */
  --text-4: #727272;          /* ink quaternary: captions */
  --text-5: #8b8b8b;          /* ink quintary: timestamps, metadata */
  --text-disabled: #666666;
  --border: #dfdfdf;          /* stroke quaternary: hairlines */
  --border-strong: #c7c7c7;   /* stroke strong: section rules */
  --link: #326891;            /* editorial blue: inline links and section nav */
  --link-soft: #567b95;
  --accent: #326891;          /* the brand accent IS the editorial blue */
  --accent-2: #2671dc;        /* interactive blue: buttons, focus */
  --signal-breaking: #d0021b;
  --signal-developing: #e6540a;
  --signal-negative: #a61b1e;
  --signal-positive: #267c30;
  --highlight: #fefad1;       /* reader highlight yellow */

  /* type: four families. Free substitutes in the stacks. */
  --font-display: "nyt-cheltenham", "Playfair Display", "Libre Caslon Display", Georgia, serif;
  --font-body: "nyt-imperial", "Source Serif 4", "Newsreader", Georgia, serif;
  --font-label: "nyt-franklin", "Libre Franklin", "Inter", Helvetica, Arial, sans-serif;
  --font-mono: ui-monospace, monospace;
  --text-xs: 10px; --text-sm: 12px; --text-base: 14px;    /* NYT body is 14px imperial at 19px leading on index; 18-20px on article */
  --text-lg: 20px; --text-xl: 32px; --text-2xl: 48px;
  --text-article: 20px; --leading-article: 1.55;
  --weight-body: 400; --weight-display: 700;
  --tracking-display: -0.01em;
  --tracking-label: 0.1em;    /* 1px at 10px uppercase */

  /* shape: square by default */
  --radius-sm: 3px; --radius-md: 3px; --radius-lg: 3px; --radius-full: 50%;   /* 50% only for avatars */
  --border-w: 1px;

  /* depth: zero drop shadows measured on the homepage */
  --shadow-sm: none;
  --shadow-md: none;
  --shadow-lg: none;

  /* rhythm: 4px base, 10px workhorse */
  --space: 4px;
  --gap: 10px;
  --section-y: 48px;
  --max-w: 1200px;
  --measure: 680px;           /* article column */

  /* motion */
  --dur: 150ms; --ease: ease;
}
```

Free substitute stack that reads as newsroom: Playfair Display (headlines), Source Serif 4 (body), Libre Franklin (labels). All on Google Fonts.

Tailwind v4: prefix each with `--color-`, `--font-`, `--radius-` inside `@theme {}`.

## Layout rules
- Index page: 12-column grid, 10px gutters, 1200px max. A lead story spans 6-8 columns; secondary stories 3-4; a rail column of 3 with hairline separation.
- Article page: single column at `--measure` 680px, body at 20px/1.55 in the text serif, headline at 48px in the display serif, byline and date in the label sans at 12px.
- Every section starts with an eyebrow: label sans, 10-11px, uppercase, `--tracking-label`, `--text`, followed by a `--border-strong` rule.
- Separation is always a hairline (`--border`) or a tint (`--surface`), never a shadow or a card edge.
- Images: full column width, 3px radius, caption and credit below in `--text-4` at 12px.
- Pull quotes: display serif at 28-32px, `--border-strong` rule above and below, inset into the measure.
- Drop cap on article first paragraph: display serif, 3 lines tall, `--text`.
- Link color is `--link` only inline; nav links are `--text` with underline on hover.
- Dense is correct. Index pages carry 30+ headlines above the fold.

## Components

```css
.eyebrow {
  font: 500 var(--text-xs)/1 var(--font-label);
  text-transform: uppercase; letter-spacing: var(--tracking-label);
  color: var(--text); padding-bottom: 6px;
  border-bottom: var(--border-w) solid var(--border-strong);
  margin-bottom: 12px;
}

.btn {
  font: 700 var(--text-sm)/1 var(--font-label);
  height: 36px; padding: 0 16px;
  border-radius: var(--radius-sm);
  border: var(--border-w) solid var(--border-strong);
  background: var(--bg); color: var(--text);
  transition: background var(--dur) var(--ease);
}
.btn:hover { background: var(--surface); }
.btn-primary { background: var(--accent-2); border-color: var(--accent-2); color: #fff; }
.btn-primary:hover { background: #1d5fb8; }

.card {              /* a story card: no box, hairline below */
  padding: 0 0 16px;
  border-bottom: var(--border-w) solid var(--border);
}
.card h3 { font: 700 var(--text-lg)/1.2 var(--font-display); margin: 0 0 6px; letter-spacing: var(--tracking-display); }
.card p  { font: 400 var(--text-base)/1.4 var(--font-body); color: var(--text-2); margin: 0 0 6px; }
.card .meta { font: 400 var(--text-sm) var(--font-label); color: var(--text-5); }

.nav {
  height: 48px; display: flex; align-items: center; gap: 20px; padding: 0 20px;
  border-bottom: var(--border-w) solid var(--border-strong);
  font: 500 var(--text-sm) var(--font-label);
}
.nav a { color: var(--text); text-decoration: none; }
.nav a:hover { text-decoration: underline; }
.masthead { font: 700 var(--text-xl) var(--font-display); text-align: center; padding: 16px 0; border-bottom: 2px solid var(--text); }

.input {
  height: 36px; padding: 0 10px;
  border: var(--border-w) solid var(--border-strong);
  border-radius: var(--radius-sm);
  background: var(--bg); color: var(--text);
  font: var(--text-base) var(--font-label);
}
.input:focus { outline: none; border-color: var(--accent-2); box-shadow: 0 0 0 1px var(--accent-2); }

.article { max-width: var(--measure); margin: 0 auto; }
.article h1 {
  font: var(--weight-display) clamp(32px, 4.5vw, 48px)/1.1 var(--font-display);
  letter-spacing: var(--tracking-display); color: var(--text); margin: 0 0 16px;
}
.article .byline { font: 400 var(--text-sm) var(--font-label); color: var(--text-3); margin-bottom: 24px; }
.article p { font: 400 var(--text-article)/var(--leading-article) var(--font-body); color: var(--text); margin: 0 0 1.4em; }
.article p:first-of-type::first-letter {
  font: 700 3.6em/0.85 var(--font-display); float: left; margin: 0.08em 0.08em 0 0; color: var(--text);
}
.pullquote {
  font: 400 28px/1.3 var(--font-display); color: var(--text);
  border-top: var(--border-w) solid var(--border-strong); border-bottom: var(--border-w) solid var(--border-strong);
  padding: 20px 0; margin: 32px 0;
}
figcaption { font: 400 var(--text-sm)/1.4 var(--font-label); color: var(--text-4); margin-top: 6px; }

.signal { font: 700 var(--text-xs) var(--font-label); text-transform: uppercase; letter-spacing: var(--tracking-label); }
.signal-breaking { color: var(--signal-breaking); }
.signal-live::before { content: ""; display: inline-block; width: 6px; height: 6px; border-radius: 50%; background: var(--signal-breaking); margin-right: 6px; }
```

## Motion
- Underline on hover, 150ms.
- Nothing else. News sites do not animate content.
- Allowed: a sticky masthead that collapses from 2-line to 1-line on scroll.

## Do
- Use three type families with distinct jobs: display serif for headlines, text serif for body, sans for every label and byline.
- Start every section with a tracked uppercase eyebrow and a rule.
- Separate with hairlines and tints, never cards or shadows.
- Keep corners at 3px. Round only avatars.
- Reserve red and orange for editorial signals (breaking, live, developing). They never fill a button.

## Don't
- No drop shadows anywhere.
- No chromatic color as a button fill except `--accent-2` blue.
- No centered body text. Headlines may center on the article page only.
- No sans-serif body copy. If the client insists, the article still uses the serif.
- No radius above 3px except circles.

## A11y
- `--text` #121212 on white: 18.1:1. `--text-2` #363636: 11.5:1. `--text-3` #5a5a5a: 6.9:1. `--text-4` #727272: 4.8:1, passes. `--text-5` #8b8b8b: 3.4:1, fails body; keep it for 12px metadata only and never for anything the reader needs.
- `--link` #326891 on white: 5.5:1, passes. `--accent-2` #2671dc: 4.6:1, passes. White on `--accent-2`: 4.6:1.
- `--signal-breaking` #d0021b on white: 5.4:1, passes.
- Focus ring: `outline: 2px solid var(--accent-2); outline-offset: 2px`.
- Drop caps: wrap in a span with `aria-hidden` and keep the full first word in the paragraph text for screen readers, or skip the drop cap.

## Accent-compatible
`hand-drawn` (illustrated spot art in the rail), `photo-led` (one full-bleed lead photograph on the index), `swiss` (data tables for a stats section). No textures, no dark mode by default.

## Reference sites
- https://www.nytimes.com (measured: ink ladder #121212 through #8b8b8b, strokes #dfdfdf and #c7c7c7, surface tint #ebebeb, editorial blue #326891, interactive blue #2671dc, signal red #d0021b, four-family stack with cheltenham 700 headlines and franklin 10px/500 uppercase labels at 1px tracking, 3px radius, zero shadows)
- https://www.shadcn.io/design/nytimes (source of the measured capture, May 2026)
- https://www.theatlantic.com (secondary: same family, warmer ink, wider measure)

## Variants

### Variant: new-yorker
Overrides: `--font-display: "Irvin", "Playfair Display SC", serif;` masthead and section heads set in the display face with tighter tracking; body measure widens to 720px; `--text` becomes `#000000`. Spot illustrations expected in the rail.
Use when: brief names The New Yorker, or wants literary and illustrated over news-dense.

### Variant: atlantic
Overrides: `--text: #000000; --bg: #ffffff; --accent: #cd2c2c;` (Atlantic red) used on the masthead rule and eyebrow underlines only; display serif tightens to `--tracking-display: -0.02em`; body at 19px.
Use when: brief names The Atlantic, or wants essays and long reads over daily news.
