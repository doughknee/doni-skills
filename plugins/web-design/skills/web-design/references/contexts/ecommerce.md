# E-commerce

**Slug:** `ecommerce`
**What it is:** Product grid, product detail, cart, checkout, trust signals.
**Default aesthetic (brief is silent):** `scandinavian`

## Allowed aesthetics
- scandinavian
- luxury
- photo-led
- playful
- flat
- material
- bento
- japanese-minimal
- y2k-aero (youth and streetwear)
- neo-brutalism (indie and DTC)
- organic (food, skincare, wellness)

## Banned aesthetics
- Raw family except neo-brutalism
- terminal
- cyberpunk
- sci-fi-hud
- brutalism
- maximalism
- motion-first

## Must-have sections
- Announcement bar
- Nav with search, account, cart
- Hero or featured collection
- Product grid with filters
- PDP: gallery, title, price, variants, add-to-cart, details accordion
- Cart drawer
- Trust row: shipping, returns, payment icons
- Footer with policies

## Layout skeleton
- Product grid 4-up desktop, 2-up mobile
- PDP: gallery 60% left, buy box 40% right sticky
- Product images on a consistent background (white or the recipe's `--surface`)
- Price in the recipe's display face at `--text-lg`

## Component list
- Product card (image, name, price, quick-add)
- Variant selector (swatch, size pills)
- Add-to-cart button (the one accent instance)
- Cart drawer
- Filter sidebar
- Review stars
- Trust badge row

## Notes
- Photography quality decides the aesthetic: strong photos → photo-led or luxury; weak photos → scandinavian or flat with illustration
- The add-to-cart button is the only place the accent must appear on a PDP
