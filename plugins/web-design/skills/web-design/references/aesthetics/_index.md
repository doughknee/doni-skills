# Aesthetic Index

40 base aesthetics. Each entry: slug, family, era or lineage, fingerprint (concrete signifiers to match against a brief), and a `vs` line naming the nearest neighbor. When two candidates fit, the `vs` line is the tie-breaker.

Recipe status: `[R]` researched with measured tokens, `[T]` template only (build from fingerprint and reference sites, flag it).

---

## Rational / Structural

### swiss [R]
International Typographic Style, 1950s Switzerland. Visible modular grid, Helvetica/Inter/Neue Haas, flush-left ragged-right, one accent color, no ornament, photography as objective document.
Refs: swissted.com, massimovignelli-style work, usgraphics.com
**vs minimalism:** Swiss has structure you can see; Minimalism has almost nothing to see.

### bauhaus [T]
1919-1933 German school. Primary red/yellow/blue plus black on cream, circles/squares/triangles used as the content not decoration, Futura-class geometric sans, poster composition.
Refs: bauhaus-dessau.de, Bauhaus Movement poster archives
**vs swiss:** Bauhaus is shapes-first; Swiss is type-first.

### minimalism [T]
Black, white, one gray. One typeface. Zero or one image. Page is mostly empty. Absorbs Barely-There UI.
Refs: minimal.gallery, brutalistwebsites.com minimal section, Dieter Rams
**vs japanese-minimal:** Minimalism is achromatic and cold; Japanese Minimal is warm paper tones and asymmetric.

### flat [T]
2012-2016 Metro/Windows 8 lineage. Saturated solid color tiles, zero shadows or gradients, simple glyph icons, bold sans.
Refs: Microsoft Metro, early Windows Phone, flatuicolors.com
**vs material:** Flat has no depth at all; Material adds elevation.

### material [T]
Google's system. Cards with 1dp-8dp elevation shadows, FAB, ripple feedback, Roboto, tonal color roles. Absorbs Fluent (Microsoft's cousin).
Refs: m3.material.io, Google Workspace
**vs flat:** shadows and motion exist and mean something.

### bento [T]
Apple keynote lineage, 2022 onward. Page is a grid of rounded tiles of varying sizes; each tile is one feature or stat; tiles mix text, image, and number.
Refs: apple.com product pages, bentogrids.com
**vs material:** Bento is a layout pattern; Material is a component system. Bento can wear several surface styles.

### enterprise [T]
Safe B2B conventions. Navy or corporate blue, hero plus logo bar plus three-column features plus testimonials, trust badges, stock photography, generous but unremarkable.
Refs: salesforce.com, workday.com, servicenow.com
**vs material:** Enterprise is about page conventions, not a rendering rule.

---

## Product / SaaS

### dark-saas [R]
Linear and Raycast lineage. Near-black canvas with a faint blue cast, four-step surface ladder instead of shadows, hairline borders, one lavender or blue accent, product screenshot as hero, aggressive negative tracking on display type.
Refs: linear.app, raycast.com, resend.com
**vs cyberpunk:** no neon, no glitch, restrained.

### gradient-mesh [R]
Stripe lineage. White page, aurora or mesh gradient in the hero, light-weight type, pastel-to-saturated blends, "tech bro gradients."
Refs: stripe.com, mercury.com
**vs dark-saas:** light background; color comes from gradients, not glow.

### glass [T]
Frosted translucent panels, backdrop-filter blur, 1px light border at 20-30% white, vivid gradient behind the glass. Absorbs Apple Liquid Glass (2025-26).
Refs: Apple visionOS and iOS 26 UI, hype4.academy glassmorphism
**vs neumorphism:** glass is translucent; neumorphism is opaque.

### neumorphism [T]
2020 Dribbble wave. Monochrome, elements extruded with paired light and dark shadows, soft, low contrast, pressed and raised states.
Refs: neumorphism.io, dribbble neumorphism tag
**vs claymorphism:** mono and subtle vs pastel and puffy.

### claymorphism [T]
2021-22. Puffy rounded 3D shapes, pastel fills, inner shadow plus outer shadow, big radius, friendly.
Refs: hype4.academy claymorphism, clay.css
**vs playful:** Clay is a surface treatment; Playful is a shape language and tone.

### skeuomorphism [T]
Pre-2013 iOS lineage, subtler return in 2026. Real materials (leather, wood, brushed metal, paper), realistic lighting, physical controls (dials, switches, stitched edges).
Refs: iOS 6 archives, Things 3 (restrained), Panic apps
**vs claymorphism:** Skeuo imitates real objects; Clay imitates nothing.

### mono-editorial [R]
Vercel Geist lineage. Near-white page, ink near-black type, monospace eyebrows and labels, hairline rules, dense tables, numbered sections, single ink accent, pill CTAs.
Refs: vercel.com, vercel.com/geist, planetscale.com
**vs terminal:** light, calm, typeset; not a CLI.

---

## Raw / Anti-design

### brutalism [T]
Unstyled or near-default HTML. Times or Arial, underlined blue links, harsh 1px borders, no responsive polish, visible structure. Absorbs Geocities / early-web nostalgia.
Refs: brutalistwebsites.com, craigslist.org, berkshirehathaway.com
**vs neo-brutalism:** Brutalism is undesigned; Neo-Brutalism is designed to look rough.

### neo-brutalism [T]
2-4px black outlines on everything, hard offset box-shadow (4px 4px 0 #000), saturated flat fills, chunky rounded or grotesk type, no gradients. Absorbs Cute-alism.
Refs: gumroad.com, figma.com/community, neobrutalism.dev
**vs brutalism:** polished and intentional.

### grunge [T]
1990s alt lineage. Noise, scratches, torn edges, overprinted and distressed type, dark and dirty, photocopied textures. The mechanism is surface damage.
Refs: Ray Gun magazine archives, Nine Inch Nails site history, modern indie wrestling and metal band sites
**vs collage:** Grunge is surface damage; Collage is composition.

### collage [T]
Zine and cut-paper. Torn paper edges, tape, scanned photos, type pasted at angles, layered stacks, mixed media. The mechanism is composition.
Refs: are.na collage tag, indie publisher sites
**vs lo-fi-riso:** Collage layers objects; Riso layers inks.

---

## Editorial / Print

### editorial [R]
Magazine lineage. Large serif display headlines, multi-column text, pull quotes, drop caps, bylines and datelines, dense and typeset.
Refs: nytimes.com/section/magazine, theatlantic.com, newyorker.com
**vs luxury:** Editorial is dense; Luxury is empty.

### art-deco [T]
1920s-30s. Gold on black (or black on cream), sunburst and chevron ornament, mirrored symmetry, tall condensed serifs and sans, geometric frames.
Refs: Great Gatsby film site archives, The Peninsula hotels, Chrysler Building motifs
**vs luxury:** Deco is ornamental; Luxury is bare.

### luxury [T]
Fashion house lineage. Hairline serifs, enormous whitespace, one large photograph, almost no visible UI, muted palette, centered type, uppercase tracking.
Refs: celine.com, therow.com, aesop.com
**vs editorial:** no columns, no density.

### scandinavian [R]
Nordic product lineage. Warm neutrals (oat, sand, sage, clay), friendly geometric sans, product photography on natural backgrounds, rounded and practical, light wood tones.
Refs: ikea.com, hay.dk, muuto.com, normann-copenhagen.com
**vs japanese-minimal:** cozier, more color, product-led.

### japanese-minimal [T]
Muji lineage. Off-white paper tones, generous negative space, slight asymmetry, thin type, restraint as warmth, natural materials. Absorbs wabi-sabi.
Refs: muji.com, ryohin-keikaku.jp, kenyahara.com
**vs scandinavian:** austere, not cozy.

---

## Retro / Nostalgia

Era anchor is the discriminator for this whole family.

### y2k-aero [T]
2000-2008. Glossy bubbles, aqua and sky gradients, lens flares, chrome text, water and glass, Frutiger-class humanist sans.
Refs: Windows Vista and XP archives, early iTunes, Frutiger Aero wiki
**vs vaporwave:** earnest optimism, not irony.

### vaporwave [T]
Ironic 80s-90s internet. Pastel pink and cyan, marble busts, checkerboard floors, Windows 95 chrome, Japanese katakana, VHS glitch, palm trees.
Refs: Vaporwave aesthetic wiki, Macintosh Plus cover, poolsuite.net
**vs y2k-aero:** ironic, not earnest.

### retro-futurism [T]
1950s-70s atomic age. Rounded chrome, orange and teal, starbursts, boomerang shapes, Space Age geometric sans, Jetsons and Eames.
Refs: Googie architecture, Space Age design archives, 2001 film typography
**vs memphis:** mid-century optimism, not postmodern clash.

### memphis [T]
1980s Italian postmodern. Squiggles, confetti, terrazzo, pastel plus primary clash, playful asymmetry, bold outlined shapes.
Refs: memphis-milano.com, Ettore Sottsass archives
**vs retro-futurism:** postmodern clash, not mid-century optimism.

### pixel [T]
8-bit and 16-bit games. Pixel fonts (Press Start 2P, Silkscreen), hard edges, limited palettes, sprite-style icons, dithering.
Refs: itch.io game pages, NES.css, pixel art communities
**vs terminal:** color and sprites, not green text.

### lo-fi-riso [T]
Risograph print imitation. Two or three ink colors (fluorescent pink, blue, yellow), grain, misregistration, halftone, cream paper.
Refs: risomania, independent print studios, risograph zine sites
**vs grunge:** clean and cheerful, not dirty.

---

## Tech / Dark

### cyberpunk [T]
Neon magenta and cyan on black, scanlines, glitch, HUD corner brackets, monospace, dirty and loud.
Refs: Cyberpunk 2077 site, Blade Runner 2049 UI, cyberpunk-ui on Dribbble
**vs sci-fi-hud:** grime and neon vs clean and cool.

### terminal [T]
Monospace everything, green or amber on black, blinking cursor, ASCII art, prompt-style navigation, CLI metaphors.
Refs: terminal.sexy, hacker-news clones, warp.dev marketing
**vs cyberpunk:** one color, no glitch, CLI metaphor.

### sci-fi-hud [T]
Thin-line interface frames, corner brackets, cool blue and white on dark, data readouts, clean. Apple TV+ title and Expanse lineage.
Refs: Territory Studio work, Expanse UI, Apple TV+ title sequences
**vs cyberpunk:** no neon, no grime, no glitch.

---

## Illustrated / Human

### alegria [T]
Corporate Memphis. Flat illustrated people with oversized limbs and small heads, muted pastels, big-tech explainer look.
Refs: Facebook Alegria system, early Airbnb illustration, humaaans.com
**vs hand-drawn:** characters are the mechanism.

### hand-drawn [T]
Marker underlines, doodle arrows, handwriting fonts (Caveat, Kalam), imperfect strokes over otherwise clean layouts. Rising in 2026 as pushback against AI polish.
Refs: notion.so marketing, excalidraw.com, tldraw.com
**vs alegria:** no characters required; the mark is the imperfection.

### playful [T]
Duolingo lineage. Fat rounded shapes, primaries, mascots, bouncy motion, big friendly buttons with bottom-edge 3D.
Refs: duolingo.com, headspace.com, lego.com
**vs claymorphism:** shape and tone, not surface.

### isometric [T]
Fixed-angle 3D scenes, floating objects, Spline-style renders, soft lighting.
Refs: spline.design, dribbble isometric tag
**vs claymorphism:** full scenes, not UI surfaces.

### organic [T]
Blob shapes, flowing curves, earth tones, leaf and water motifs, slow easing. Absorbs botanical.
Refs: blobmaker.app, organic SaaS marketing (Oatly, Allbirds)
**vs scandinavian:** curves and nature, not products and grids.

---

## Immersive / Expressive

### maximalism [T]
Dense layering everywhere, clashing patterns, three-plus typefaces, saturated color, intentional overload. Absorbs dopamine design.
Refs: gucci.com campaigns, Pinterest maximalism tag
**vs collage:** no paper metaphor; just more of everything.

### photo-led [T]
Full-bleed photography is the layout, type overlaid, every section is an image. Travel, real estate, food, vehicles.
Refs: airbnb.com, nationalgeographic.com, rivian.com
**vs luxury:** photo fills the frame rather than sits in whitespace.

### motion-first [R]
Scroll-driven transitions, kinetic type, WebGL scenes, the animation is the identity. Awwwards agency lineage.
Refs: awwwards.com SOTD, active-theory.com, lusion.co
**vs everything:** choose only when the brief asks for motion or an agency showcase.
