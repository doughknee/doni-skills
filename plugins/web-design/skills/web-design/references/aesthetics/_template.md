# {Name}

**Slug:** `{slug}` · **Family:** {family} · **Lineage:** {era or reference brand}
**Fingerprint:** {one sentence an AI can match against a brief}

## Choose when
- {brief signal}
- {brief signal}
- {brief signal}

## Avoid when
- {brief signal}
- {brief signal}
- **vs {neighbor}:** {discriminator line, copied from _index.md}

## Tokens

Every value below was measured from the reference sites listed at the bottom. Do not substitute.

```css
:root {
  /* color */
  --bg: #;
  --surface: #;
  --surface-2: #;
  --text: #;
  --text-muted: #;
  --accent: #;
  --accent-2: #;        /* omit if the aesthetic has one accent */
  --border: #;
  --border-strong: #;

  /* type */
  --font-display: ;
  --font-body: ;
  --font-mono: ;
  --text-xs: 12px; --text-sm: 14px; --text-base: 16px;
  --text-lg: 20px; --text-xl: 32px; --text-2xl: 48px;
  --weight-body: 400; --weight-display: ;
  --tracking-display: ;

  /* shape */
  --radius-sm: ; --radius-md: ; --radius-lg: ; --radius-full: 9999px;
  --border-w: 1px;

  /* depth */
  --shadow-sm: ;
  --shadow-md: ;
  --shadow-lg: ;

  /* rhythm */
  --space: 4px;
  --section-y: ;
  --max-w: ;

  /* motion */
  --dur: ; --ease: ;
}
```

Tailwind v4 mapping: prefix each with `--color-`, `--font-`, `--radius-`, `--shadow-` inside `@theme {}`.

## Layout rules
- Max width and gutter
- Column behavior
- Hero pattern
- Section rhythm
- Alignment
- Image treatment

## Components

```css
.btn { }
.btn-primary { }
.card { }
.nav { }
.input { }
.hero h1 { }
```

## Motion
- What moves
- How much
- What never moves

## Do
- 
- 
- 
- 
- 

## Don't
- 
- 
- 
- 
- 

## A11y
- Contrast check result for text on bg and accent on bg.
- Focus ring spec.
- Known failure and the fix, if any.

## Accent-compatible
`{slug}`, `{slug}`, `{slug}` (one accent layer at a time)

## Reference sites
- {url} (measured: {what})
- {url}
- {url}

## Variants
(none yet)
