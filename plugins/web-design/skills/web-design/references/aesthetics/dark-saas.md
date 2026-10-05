# Dark SaaS

**Slug:** `dark-saas` · **Family:** Product / SaaS · **Lineage:** Linear (2019 onward), Raycast, Resend
**Fingerprint:** Near-black canvas with a faint blue cast, a four-step surface ladder instead of drop shadows, hairline borders, one lavender or blue accent used sparingly, product screenshot as the hero, negative letter-spacing on display type.

## Choose when
- Brief names Linear, Raycast, Resend, Cal.com, or "modern dev tool"
- Product is software with a UI worth screenshotting
- Tone words: precise, fast, craft, engineered, serious

## Avoid when
- Context is `blog`, `docs` (unless user asks), `local-business`, `ecommerce`
- Brief says warm, friendly, approachable, playful
- **vs cyberpunk:** no neon, no glitch, restrained.
- **vs terminal:** proportional type, real UI, not a CLI.

## Tokens

Measured from linear.app (May 2026 capture via shadcn.io DESIGN.md). Do not substitute.

```css
:root {
  /* color */
  --bg: #010102;            /* canvas: near-black with blue cast, never #000 */
  --surface: #0f1011;       /* surface-1: cards */
  --surface-2: #141516;     /* surface-2: hovered card */
  --surface-3: #18191a;     /* surface-3: dropdowns, popovers */
  --surface-4: #191a1b;     /* surface-4: lifted modal */
  --text: #f7f8f8;          /* ink */
  --text-muted: #d0d6e0;    /* ink-muted: body on dark */
  --text-subtle: #8a8f98;   /* ink-subtle: captions, labels */
  --text-tertiary: #62666d; /* placeholders, disabled */
  --accent: #5e6ad2;        /* lavender-blue: brand mark, focus ring, one CTA per section */
  --accent-hover: #828fff;
  --border: #23252a;        /* hairline */
  --border-strong: #34343a;
  --border-tertiary: #3e3e44;
  --success: #27a644;

  /* type */
  --font-display: "Inter Display", "Inter", "Geist", system-ui, sans-serif;
  --font-body: "Inter", "Geist", system-ui, sans-serif;
  --font-mono: "Geist Mono", "JetBrains Mono", ui-monospace, monospace;
  --text-xs: 12px; --text-sm: 14px; --text-base: 16px;
  --text-lg: 20px; --text-xl: 32px; --text-2xl: 48px; --text-3xl: 80px;
  --weight-body: 400; --weight-display: 500;
  /* tracking scales with size: -3.0px at 80px, -1.2px at 48px, -0.5px at 32px, -0.05px at 16px */
  --tracking-display: -0.0375em;
  --tracking-body: -0.003em;

  /* shape */
  --radius-sm: 4px; --radius-md: 8px; --radius-lg: 12px; --radius-xl: 24px; --radius-full: 9999px;
  --border-w: 1px;

  /* depth: surface ladder replaces shadows. Use shadows only on floating overlays. */
  --shadow-sm: none;
  --shadow-md: none;
  --shadow-lg: 0 16px 40px rgba(0,0,0,0.5);

  /* rhythm: 4px base, 9 steps to 96px */
  --space: 4px;
  --section-y: 96px;
  --max-w: 1200px;

  /* motion */
  --dur: 160ms; --ease: cubic-bezier(0.25, 0.1, 0.25, 1);
}
```

Linear's own display face is "Linear Display"; Inter Display at weight 500 with the tracking above is the closest open substitute.

Tailwind v4: prefix each with `--color-`, `--font-`, `--radius-`, `--shadow-` inside `@theme {}`.

## Layout rules
- Max width 1200px, 24px gutter on mobile, 32px desktop.
- Hero: headline left or centered at 48-80px, one line of muted body, one accent button plus one ghost button, then a full-width product screenshot in a `--surface` frame with `--border` 1px and `--radius-lg`.
- Sections alternate between full-bleed `--bg` and contained `--surface` panels. Never a third background.
- Feature grids are 3-up on desktop, 1-up mobile, each cell a `--surface` card with 24px padding.
- Hierarchy comes from surface step and text tier, never from shadow or size jumps beyond the scale.
- Nav is 56px tall, `--bg` with bottom `--border`, logo left, links center at `--text-sm`, CTA right.
- Dense is fine. Linear's pages carry a lot of text at 14-16px.

## Components

```css
.btn {
  font: var(--weight-display) var(--text-sm)/1 var(--font-body);
  letter-spacing: var(--tracking-body);
  padding: 0 16px; height: 36px;
  border-radius: var(--radius-md);
  border: var(--border-w) solid var(--border-strong);
  background: var(--surface-2); color: var(--text);
  transition: background var(--dur) var(--ease), border-color var(--dur) var(--ease);
}
.btn:hover { background: var(--surface-3); border-color: var(--border-tertiary); }
.btn-primary { background: var(--accent); border-color: var(--accent); color: #fff; }
.btn-primary:hover { background: var(--accent-hover); border-color: var(--accent-hover); }

.card {
  background: var(--surface);
  border: var(--border-w) solid var(--border);
  border-radius: var(--radius-lg);
  padding: 24px;
  transition: background var(--dur) var(--ease);
}
.card:hover { background: var(--surface-2); }

.nav {
  height: 56px; display: flex; align-items: center; gap: 32px;
  padding: 0 32px;
  background: var(--bg);
  border-bottom: var(--border-w) solid var(--border);
}
.nav a { color: var(--text-subtle); font-size: var(--text-sm); }
.nav a:hover { color: var(--text); }

.input {
  height: 36px; padding: 0 12px;
  background: var(--surface); color: var(--text);
  border: var(--border-w) solid var(--border-strong);
  border-radius: var(--radius-md);
  font: var(--text-sm) var(--font-body);
}
.input:focus { outline: none; border-color: var(--accent); box-shadow: 0 0 0 1px var(--accent); }

.hero h1 {
  font: var(--weight-display) clamp(40px, 7vw, 80px)/1.05 var(--font-display);
  letter-spacing: var(--tracking-display);
  color: var(--text);
}
.hero p { font-size: var(--text-lg); color: var(--text-subtle); max-width: 560px; }

.screenshot-frame {
  background: var(--surface);
  border: var(--border-w) solid var(--border);
  border-radius: var(--radius-lg);
  padding: 8px;
  overflow: hidden;
}
```

## Motion
- Surface and border color on hover, 160ms.
- Fade-up on scroll for sections: 12px translate, 300ms, once.
- Product screenshots may do a slow parallax (max 20px) on scroll.
- Never: bounce, spring overshoot, glow pulses, gradient animation.

## Do
- Keep one accent instance per viewport: the CTA, or the focus ring, not both plus the logo.
- Use the surface ladder for every hierarchy decision.
- Set display type at weight 500 with negative tracking; it looks heavier than it is.
- Put a real product screenshot in the hero. Without one, this aesthetic has no protagonist.
- Keep body copy at `--text-muted` (#d0d6e0), not pure `--text`, so headlines pop.

## Don't
- No #000000 canvas. The blue cast is the signature.
- No gradients in the background. Linear has none. (Raycast variant allows one radial spotlight.)
- No second chromatic color anywhere.
- No display weight above 600.
- No drop shadows on cards. Shadows only on true overlays (modals, dropdowns).

## A11y
- `--text` on `--bg`: 19.4:1. `--text-muted` on `--bg`: 14.8:1. `--text-subtle` on `--bg`: 6.7:1. `--text-tertiary` on `--bg`: 3.9:1, so tertiary is for placeholders and disabled only, never body.
- `--accent` #5e6ad2 on `--bg`: 4.1:1 as text. Use accent as a fill with white text (6.1:1), or on borders. For accent-colored links, lighten to `--accent-hover` #828fff (7.2:1).
- Focus ring: `box-shadow: 0 0 0 2px var(--bg), 0 0 0 4px var(--accent)`.

## Accent-compatible
`hand-drawn` (annotations over screenshots), `mono-editorial` (mono labels and tables), `terminal` (a single code block in CLI style). Nothing else.

## Reference sites
- https://linear.app (measured: all color and radius values, tracking scale, surface ladder)
- https://www.shadcn.io/design/linear (source of the measured capture, May 2026)
- https://raycast.com (variant reference)

## Variants

### Variant: raycast
Overrides: add `--spotlight: radial-gradient(600px circle at 50% 0%, rgba(94,106,210,0.15), transparent 70%)` on the hero background only. `--accent` becomes `#ff6363` (Raycast red). Everything else unchanged.
Use when: brief names Raycast, or asks for "a bit of glow" or "a spotlight."

### Variant: oled
Overrides: `--bg: #000000; --surface: #0a0a0a; --surface-2: #111111; --surface-3: #161616; --surface-4: #1a1a1a;` border steps shift to `#1f1f1f`, `#2a2a2a`, `#333333`. Drop the blue cast entirely.
Use when: mobile-first, battery, or "true black" is in the brief. Linear itself does not do this; this variant is the generic OLED look that Vercel's dark mode uses (#0a0a0a).
