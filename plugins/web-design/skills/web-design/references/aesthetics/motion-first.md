# Motion-First / Awwwards

**Slug:** `motion-first` · **Family:** Immersive / Expressive · **Lineage:** Lusion, Active Theory, Framer (marketing), Awwwards Site of the Day
**Fingerprint:** The animation is the identity. A WebGL or canvas layer under the DOM, scroll-driven section transitions, kinetic display type at 80-120px with heavy negative tracking, one electric accent on black or white, pill buttons, custom easing curves (never `ease`), and a page that is mostly empty when still.

## Choose when
- Context is `agency` and the brief is silent on style
- Brief names Awwwards, Lusion, Active Theory, Framer, or says "immersive," "3D," "WebGL," "scroll experience," "showcase"
- The site exists to prove the maker's craft
- The budget covers custom animation work; this aesthetic is expensive to build well

## Avoid when
- Any context other than `agency`, `portfolio`, or a product launch microsite
- Content-heavy sites; motion fights reading
- Brief mentions performance, accessibility-first, SEO, or "fast"
- **vs everything:** choose only when the brief asks for motion or an agency showcase. Never a fallback.
- **vs dark-saas:** dark-saas is static chrome around a product; motion-first is the chrome moving.

## Tokens

Measured from lusion.co (Oct 2026, computed styles) and framer.com (May 2026 capture via shadcn.io DESIGN.md). Lusion scales every size by viewport width; the tokens below are normalized to a 1440px viewport.

```css
:root {
  /* color: two canvases, both measured. Pick one per site, never mix. */
  --bg: #ffffff;              /* lusion default: white with a WebGL layer */
  --bg-dark: #090909;         /* framer: pure black canvas, no light interludes */
  --surface: #f0f1fa;         /* lusion cool tint: 55 uses */
  --surface-dark: #141414;    /* framer surface-1 */
  --surface-dark-2: #1c1c1c;
  --text: #000000;            /* lusion: pure black, 1100 uses */
  --text-dark: #ffffff;
  --text-muted: #2b2e3a;      /* lusion slate */
  --text-muted-dark: #999999; /* framer ink-muted */
  --accent: #0016ec;          /* lusion electric blue: the single chromatic */
  --accent-2: #1a2ffb;        /* lusion hover blue */
  --accent-framer: #0099ff;   /* framer signal blue: links, focus, selected only, never a fill */
  --border: #e4e6ef;          /* lusion */
  --border-dark: #262626;     /* framer hairline */
  --gradient-a: #d44df0; --gradient-b: #6a4cf5; --gradient-c: #ff7a3d; --gradient-d: #ff5577;  /* framer spotlight cards: atmosphere, not section grounds */

  /* type: one grotesk, display at extreme scale */
  --font-display: "Aeonik", "GT Walsheim", "Inter Display", "Inter", system-ui, sans-serif;
  --font-body: "Aeonik", "Inter", system-ui, sans-serif;
  --font-mono: ui-monospace, monospace;
  --text-xs: 12px; --text-sm: 14px; --text-base: 16px;
  --text-lg: 20px; --text-xl: 32px; --text-2xl: 56px; --text-3xl: 85px; --text-4xl: 110px;
  --weight-body: 400; --weight-display: 500;
  /* framer: -5.5px at 110px, -4.25px at 85px. That is -0.05em. */
  --tracking-display: -0.05em;
  --tracking-caps: 0.08em;    /* lusion uppercase labels */

  /* shape: pills and soft cards */
  --radius-sm: 4px; --radius-md: 10px; --radius-lg: 15px; --radius-xl: 45px; --radius-pill: 100px; --radius-full: 9999px;
  --border-w: 1px;

  /* depth: none. Depth comes from the canvas layer and from scale transforms. */
  --shadow-sm: none;
  --shadow-md: none;
  --shadow-lg: none;

  /* rhythm: lusion uses a 5px base; framer 5px. Sections are viewport-height. */
  --space: 5px;
  --section-y: 100vh;
  --max-w: none;              /* edge to edge */
  --gutter: 5vw;

  /* motion: measured easings from lusion. These are the aesthetic. */
  --ease-out: cubic-bezier(0.4, 0, 0.1, 1);     /* 32 uses: hover, reveal */
  --ease-expo: cubic-bezier(0.35, 0, 0, 1);     /* 14 uses: page transitions, big moves */
  --ease-spring: cubic-bezier(0.16, 1, 0.3, 1); /* overshoot on enter */
  --dur-fast: 200ms; --dur: 400ms; --dur-slow: 500ms; --dur-page: 1200ms;
}
```

Free substitutes: Inter Display or Inter at weight 500 with -0.05em tracking. Aeonik and GT Walsheim are commercial.

Tailwind v4: prefix colors with `--color-`, fonts with `--font-`, radii with `--radius-`, and expose easings as `--ease-*` inside `@theme {}`.

## Layout rules
- Edge to edge. No max-width container; use `--gutter` 5vw on each side.
- Every section is at least 100vh and pinned or scroll-driven. Content enters, transforms, and exits inside its section.
- Hero: one line of display type at 85-110px, weight 500, -0.05em, taking 60-80% of viewport width. Below it a 14px uppercase label and one pill button. Behind it, the canvas layer.
- Work section: one project per viewport, full-bleed image or video, title overlaid at display scale, horizontal scroll or scroll-snap.
- Navigation is a pill or a single word in a corner. It may hide on scroll and return on scroll-up.
- Type sizes scale with viewport: `clamp(40px, 7.6vw, 110px)` for hero.
- The page is nearly empty when static. The motion fills it.
- A loader (0-100 counter or wordmark reveal) is expected on first visit and must not exceed 1.5s.

## Components

```css
.btn {
  font: 500 var(--text-sm)/1 var(--font-body);
  text-transform: uppercase; letter-spacing: var(--tracking-caps);
  height: 48px; padding: 0 28px;
  border-radius: var(--radius-pill);
  border: var(--border-w) solid var(--text);
  background: transparent; color: var(--text);
  transition: background var(--dur) var(--ease-out), color var(--dur) var(--ease-out), transform var(--dur) var(--ease-spring);
}
.btn:hover { background: var(--text); color: var(--bg); transform: scale(1.04); }
.btn-primary { background: var(--accent); border-color: var(--accent); color: #fff; }
.btn-primary:hover { background: var(--accent-2); border-color: var(--accent-2); }

.card {              /* project tile */
  position: relative; overflow: hidden;
  border-radius: var(--radius-lg);
  aspect-ratio: 4 / 3;
}
.card img, .card video { width: 100%; height: 100%; object-fit: cover; transition: transform var(--dur-slow) var(--ease-expo); }
.card:hover img, .card:hover video { transform: scale(1.06); }
.card .title {
  position: absolute; left: 24px; bottom: 24px;
  font: 500 var(--text-xl)/1 var(--font-display); letter-spacing: var(--tracking-display); color: #fff;
  transform: translateY(8px); opacity: 0;
  transition: transform var(--dur) var(--ease-out), opacity var(--dur) var(--ease-out);
}
.card:hover .title { transform: none; opacity: 1; }

.nav {
  position: fixed; top: 20px; left: var(--gutter); right: var(--gutter);
  display: flex; justify-content: space-between; align-items: center;
  font: 500 var(--text-sm) var(--font-body); text-transform: uppercase; letter-spacing: var(--tracking-caps);
  mix-blend-mode: difference; color: #fff;
  transition: transform var(--dur) var(--ease-expo);
}
.nav.hidden { transform: translateY(-120%); }

.input {
  height: 48px; padding: 0 0 0 0;
  border: 0; border-bottom: var(--border-w) solid var(--text);
  background: transparent; color: var(--text);
  font: var(--text-lg) var(--font-body);
}
.input:focus { outline: none; border-bottom-width: 2px; }

.hero { min-height: 100vh; display: grid; align-content: end; padding: 0 var(--gutter) 10vh; }
.hero h1 {
  font: var(--weight-display) clamp(40px, 7.6vw, 110px)/0.95 var(--font-display);
  letter-spacing: var(--tracking-display); color: var(--text); margin: 0;
  overflow: hidden;
}
.hero h1 .line { display: block; transform: translateY(110%); animation: rise var(--dur-page) var(--ease-expo) forwards; }
.hero h1 .line:nth-child(2) { animation-delay: 80ms; }
.hero h1 .line:nth-child(3) { animation-delay: 160ms; }
@keyframes rise { to { transform: none; } }

.canvas-layer { position: fixed; inset: 0; z-index: -1; pointer-events: none; }

.marquee { overflow: hidden; white-space: nowrap; font: 500 var(--text-2xl) var(--font-display); letter-spacing: var(--tracking-display); }
.marquee span { display: inline-block; padding-right: 2em; animation: scroll-x 20s linear infinite; }
@keyframes scroll-x { to { transform: translateX(-100%); } }

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation-duration: 0.01ms !important; animation-iteration-count: 1 !important; transition-duration: 0.01ms !important; scroll-behavior: auto !important; }
  .hero h1 .line { transform: none; }
  .canvas-layer { display: none; }
}
```

## Motion
This section is the recipe.
- **Easing:** `--ease-expo` for anything larger than 100px of travel. `--ease-out` for hover and reveals. `--ease-spring` only on enter, never on exit. Never `ease`, `ease-in-out`, or `linear` except marquees.
- **Durations:** hover 200-400ms, reveals 400-500ms, page and section transitions 1200ms. Longer reads as slow, shorter reads as cheap.
- **Text reveal:** lines masked with `overflow: hidden` and translated up 110%, staggered 80ms. Words may split; letters should not unless the headline is under 12 characters.
- **Scroll:** use the native Scroll-driven Animations API (`animation-timeline: scroll()` / `view()`) or GSAP ScrollTrigger. Pin sections, scrub transforms, snap between projects. Lenis or similar for smooth scroll is standard in this aesthetic.
- **Canvas layer:** Three.js or OGL scene behind the DOM. Mouse-reactive, low-poly, one material. It must degrade to a static image on low-end devices and under reduced motion.
- **Cursor:** a custom cursor (dot plus ring, or a label that follows) is allowed. It must not replace the native cursor on interactive elements for keyboard users.
- **Loader:** counter or wordmark, under 1.5s, then a `--ease-expo` wipe.
- **Never:** motion on body text, motion without a reduced-motion fallback, more than one thing moving per viewport at rest.

## Do
- Set one display headline per viewport at 85px or larger.
- Use the measured easings. They are the difference between craft and template.
- Stagger reveals by 80ms. Lower feels mechanical, higher feels laggy.
- Ship the `prefers-reduced-motion` block. Awwwards judges check it now.
- Keep the DOM nearly empty; let the canvas and transforms carry the page.

## Don't
- No shadows. Depth comes from scale and the canvas.
- No `ease` or `ease-in-out`. Ever.
- No two accents. One electric color on black or white.
- No motion on paragraphs or lists.
- No autoplay audio. (Lusion-style sites that do it get muted and closed.)

## A11y
- `--text` #000 on white: 21:1. White on `--bg-dark` #090909: 19.6:1. `--text-muted-dark` #999 on #090909: 7.4:1, passes.
- `--accent` #0016ec on white: 8.6:1 as text, passes. White on `--accent`: 8.6:1.
- `mix-blend-mode: difference` on the nav is unreliable for contrast over images; add a `text-shadow: 0 0 1px rgba(0,0,0,0.5)` fallback or a backdrop pill.
- Every animation and the canvas layer must honor `prefers-reduced-motion`. The CSS block above does it; the JS layer must check `matchMedia('(prefers-reduced-motion: reduce)')` before initializing.
- Scroll-jacking must leave keyboard scroll (Space, PageDown, arrows) working and must not trap focus.
- Focus ring: `outline: 2px solid var(--accent); outline-offset: 4px`. Custom cursors do not replace focus indicators.

## Accent-compatible
`swiss` (a grid for the work index), `neo-brutalism` (hard outlines on the pill buttons), `grunge` (a single noise overlay on the canvas). One at a time.

## Reference sites
- https://lusion.co (measured: Aeonik at 400/500, pure black text on white, electric blue #0016ec and #1a2ffb, cool tint #f0f1fa, slate #2b2e3a, pill radius 100px, 15px cards, easings cubic-bezier(0.4,0,0.1,1) ×32 and cubic-bezier(0.35,0,0,1) ×14, durations 0.3-0.5s, WebGL canvas present, no shadows)
- https://www.framer.com (measured via shadcn.io capture: canvas #090909, surfaces #141414 and #1c1c1c, hairline #262626, signal blue #0099ff, GT Walsheim display 12-110px at -5.5px tracking, Inter Variable body with cv01/05/09/11 and ss03/ss07, 10px base radius, 5px spacing base, gradient spotlight stops)
- https://activetheory.net (pure WebGL, no DOM to measure; visual reference for canvas-first sites)
- https://www.awwwards.com/websites/sites_of_the_day/ (ongoing reference pool)

## Variants

### Variant: framer-dark
Overrides: `--bg: var(--bg-dark); --surface: var(--surface-dark); --text: var(--text-dark); --text-muted: var(--text-muted-dark); --border: var(--border-dark); --accent: var(--accent-framer);` accent never fills a button (white pill on black instead); gradient spotlight cards using `--gradient-*` as radial glows inside cards only.
Use when: brief names Framer, or wants motion-first on black.

### Variant: canvas-only
Overrides: the hero has no DOM content except the nav; the WebGL scene is the hero. First DOM headline appears at 100vh. `--text-4xl` drops to 85px.
Use when: brief names Active Theory, or the client has a 3D asset to feature.
