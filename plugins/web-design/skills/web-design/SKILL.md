---
name: web-design
description: Routes one brief to one of 40 named web design aesthetics against one of 9 site contexts and returns copy-paste design tokens, component CSS, and a preview page. Use when the user is starting the visual direction for a new site, page, or app UI, or asks to restyle one wholesale, or names a visual style (brutalist, glassmorphism, Swiss, retro), a decade, or a reference company (Linear, Stripe, Vercel, Muji, Duolingo). Do not use for single-component edits, for repos that already have a tokens file or design system, for logos, print, or icons, or for building many sites at once (that is the showcase skill).
---

# Web Design Router

One skill, two axes. A **context** is what the site is for (dashboard, blog, store). An **aesthetic** is how it looks (Swiss, neo-brutalism, dark SaaS). The router picks one of each and loads exactly two reference files. The combination happens at build time; nothing here is pre-combined.

**Neighbors:** `showcase` builds a portfolio of many sites, one per design language; this skill routes one brief to one aesthetic. `frontend-design` is the polish pass this skill hands off to at the end. If the repo already has a tokens file or design system, stop and use that instead of this skill.

## Workflow

1. **Read the brief.** Extract: site type, named reference companies, era words (80s, Y2K, retro), tone words (loud, calm, premium, playful), banned words ("not another dark SaaS site"), supplied brand assets (logo, hex colors, fonts), and stack (Tailwind, plain CSS, React, etc.).
2. **Pick a context** from the 9 below. If none fits, use `marketing`.
3. **Load** `references/contexts/{context}.md`. Take its `Allowed` list.
4. **Pick one aesthetic** from the allowed list using the index and the Router Rules. If the user named an aesthetic that the context bans, use it anyway and say in one line why the context file would normally exclude it.
5. **Load** `references/aesthetics/{slug}.md`. Seven are researched with measured tokens: `swiss`, `dark-saas`, `gradient-mesh`, `mono-editorial`, `editorial`, `scandinavian`, `motion-first` (every context default is covered). If the file does not exist yet, load `references/aesthetics/_template.md` and the `_index.md` entry for that slug, then build tokens from the fingerprint and the listed reference sites. Say in one line that this aesthetic is not yet fully researched.
6. **Apply brand overrides** (below).
7. **Build** using the recipe's tokens verbatim. Do not invent colors, fonts, radii, or shadows that are not in the token block.
8. **Deliver the output contract** (below).
9. **Polish pass:** if the `frontend-design` skill is available, load it last and apply its guidance to typography and spacing without changing any token values.

## Contexts

| slug | What it is | Default aesthetic if brief is silent |
|---|---|---|
| `dashboard` | logged-in data views, tables, charts, filters | `swiss` |
| `saas-app` | logged-in product UI, forms, settings | `dark-saas` |
| `marketing` | landing pages, pricing, feature tours | `gradient-mesh` |
| `blog` | reading-first, articles, index, author | `editorial` |
| `docs` | sidebar tree, code blocks, search | `mono-editorial` |
| `ecommerce` | product grid, PDP, cart | `scandinavian` |
| `portfolio` | work grid, case studies | `swiss` |
| `local-business` | hours, map, services, phone CTA | `scandinavian` |
| `agency` | showcase, manifesto, team | `motion-first` |

## Aesthetic index

Full index with fingerprints and discriminators: `references/aesthetics/_index.md`. Read it when two or more candidates seem to fit. Slugs only, grouped by family:

- **Rational:** `swiss` `bauhaus` `minimalism` `flat` `material` `bento` `enterprise`
- **Product / SaaS:** `dark-saas` `gradient-mesh` `glass` `neumorphism` `claymorphism` `skeuomorphism` `mono-editorial`
- **Raw:** `brutalism` `neo-brutalism` `grunge` `collage`
- **Editorial / Print:** `editorial` `art-deco` `luxury` `scandinavian` `japanese-minimal`
- **Retro:** `y2k-aero` `vaporwave` `retro-futurism` `memphis` `pixel` `lo-fi-riso`
- **Tech / Dark:** `cyberpunk` `terminal` `sci-fi-hud`
- **Illustrated / Human:** `alegria` `hand-drawn` `playful` `isometric` `organic`
- **Immersive:** `maximalism` `photo-led` `motion-first`

## Router rules

1. **Named reference company wins.** Linear, Raycast → `dark-saas`. Vercel, Geist → `mono-editorial`. Stripe → `gradient-mesh`. Apple → `bento` (marketing) or `glass` (UI). Duolingo → `playful`. Muji → `japanese-minimal`. IKEA → `scandinavian`. NYT, The Atlantic → `editorial`. Gumroad, Figma community → `neo-brutalism`.
2. **Decade word → Retro family.** 50s-70s → `retro-futurism`. 80s → `memphis` (print) or `vaporwave` (digital). 90s → `brutalism` geocities variant or `vaporwave`. 2000s → `y2k-aero`. "Arcade", "8-bit" → `pixel`.
3. **Tie-break by discriminator.** When two candidates remain, read both entries in `_index.md`. Pick the one whose `vs` line names the other; that line was written for this collision.
4. **Never default to the loud four.** `brutalism`, `maximalism`, `cyberpunk`, `motion-first` are chosen only when the brief signals them. They are never a fallback.
5. **Density follows subject.** If the subject itself is visual (type foundry, photographer, architect), prefer the less dense candidate so the work carries the page.
6. **Reading contexts stay light.** `blog` and `docs` never take a dark aesthetic except `dark-saas` and `terminal` when the user asks.

## Brand overrides

When the user supplies brand assets, the aesthetic is the system and the brand is two variables inside it.

- Supplied primary color → replaces `--accent`. Keep the recipe's `--bg`, `--surface`, `--text`, `--border`.
- Supplied secondary color → replaces `--accent-2` if the recipe has one; otherwise ignore.
- Supplied display font → replaces the display stack only. Body and mono stacks stay.
- Supplied logo → place it; never recolor it to match tokens.
- Check contrast after substitution. If the supplied accent fails 4.5:1 against `--bg` as text, use it only on surfaces and buttons, and say so.

## Blends

Briefs say "Swiss but warmer" or "dark SaaS with hand-drawn touches." Rule: **one base, one accent, never two bases.**

- Base supplies every token and all layout rules.
- Accent supplies exactly one thing: a texture, a type choice for display only, or an illustration treatment.
- Each recipe's `## Accent-compatible` line lists what can layer on it. If the requested accent is not listed, say so and offer the closest listed one.
- If the brief asks for two bases, pick the one the context allows and say which one you dropped.

## Variants

Variants live inside the parent recipe under `## Variants`, never as separate files. Cap three per aesthetic. Apply a variant when its `Use when` line matches the brief. A variant is an override block: it changes named tokens and nothing else.

## Accessibility floor

Every build, regardless of aesthetic:
- Body text at or above 4.5:1 against its background.
- Interactive elements at or above 3:1.
- Visible focus ring on every interactive element. Four aesthetics (`neumorphism`, `glass`, `luxury`, `vaporwave`) fail this by default; their recipes carry the fix in `## A11y`. Apply it even though it breaks the look slightly.
- Decorative elements are exempt and must be `aria-hidden`.

## Stack detection

Look at the project before asking. `tailwind.config.*` or `@import "tailwindcss"` in CSS → Tailwind. `package.json` with `react` → React components. Nothing → plain HTML and CSS. Never ask which stack when the repo answers it.

- **Tailwind v4:** emit tokens as `@theme { --color-bg: ...; }` in the global CSS.
- **Tailwind v3:** emit `theme.extend` in `tailwind.config.ts` mapping to CSS vars.
- **Plain CSS:** emit `:root { }` block.

## Output contract

Always return the same three things, in this order:

1. **Tokens file.** `tokens.css` (or the Tailwind equivalent per stack) containing the recipe's full token block with brand overrides applied and a `prefers-color-scheme` block when the recipe defines a dark counterpart.
2. **Component CSS.** The recipe's `## Components` blocks, adapted to the stack. Button, card, nav, input, hero at minimum.
3. **Preview page.** One self-contained `preview.html`: nav, hero, three cards, a form, a footer, rendered in the chosen aesthetic with the user's actual copy if supplied. This is the yes/no artifact. Publish it as an artifact if the Artifact tool is available; otherwise send the file.

State the chosen context and aesthetic in one line at the top of the reply. Do not explain the routing beyond that line.

## Evals

`evals/briefs.json` holds 17 test briefs with expected `context` and `slug`; five of them are silent briefs that must fall to a context default. Run them when editing `_index.md` or any context file. If fewer than 15 route correctly, or any silent brief misses, the index descriptions or the defaults table need sharpening, not the recipes.
