# Mercado Negro — brand unification notes

Working notes from the brand consolidation pass across:

- `tarjeta-martha-mn.html` (digital card, in the `tarjeta-martha` repo)
- `mercado-negro/index.html` (website, this repo)

Both now share `css/mn-brand-tokens.css`, kept byte-identical in each
repo since GitHub Pages serves them as two separate static sites with
no cross-repo includes possible.

## What changed

- Replaced the bright magenta (`#8B2252`) that previously dominated
  nav, hero CTA, section labels, buttons and form UI on both
  properties with a restrained palette derived from the approved
  Mercado Negro card on the Martha Domínguez hub (see "Palette
  derivation" below). Magenta is gone entirely; dusty rose now
  appears only on the two or three primary call-to-action buttons.
- Replaced the large handwritten `Alex Brush` script "Mercado Negro"
  title (previously the dominant brand mark on both properties) with
  an elegant uppercase serif `MERCADO NEGRO` wordmark in EB Garamond,
  matching the treatment on the approved hub card.
- Demoted the legacy circular mark (`img/logo.png` /
  `images/mercado-negro-logo.png` — dark circle, "MERCADO · NEGRO"
  ring text, script "Martha Domínguez" center) from the dominant
  hero/card visual to a small secondary badge (64–76px). The file was
  not deleted; it's kept as the legacy mark per the brief.
- Introduced a shared functional/UI type layer (Arial/Helvetica) for
  nav, buttons, form fields and contact rows, separate from the serif
  brand layer and the italic serif used for the tagline.
- Rebuilt the website hero as a composed, framed section (gold corner
  framing, ornamental rule, legacy badge, serif wordmark, descriptor,
  italic tagline, CTA) instead of plain centered text on flat black.
- Unified button hierarchy: primary actions use dusty rose + cream
  text; secondary actions use charcoal surfaces with a thin gold
  border, consistent radius and hover states, on both properties.
- Preserved all existing functional content and behavior — see
  "Functionality preserved" below.

## Palette derivation

Values were sampled directly from `hub-assets/cards/mercado-negro.png`
in the `tarjeta-martha` repo (the approved hub artwork), not invented:

| Token | Hex | Sampled from |
|---|---|---|
| `--mn-charcoal` | `#121210` | Clean dark background area, sampled directly |
| `--mn-chocolate` | `#1c1712` | Cake-stand / plate shadow tones |
| `--mn-gold` | `#c9a876` | Averaged across crest ring + descriptor band + arrow-button ring pixels (raw average ≈ `#a18a68` in shadow, highlight peaks ≈ `#c7b28d`; picked a usable UI mid-tone in that range) |
| `--mn-cream` | `#f5f0e6` | "MERCADO NEGRO" headline text, near-white, warmed slightly to match the cream already used on the Martha hub (`#F4EEE3`/`#F5F0E8`) for cross-property consistency |
| `--mn-rose` | `#8b6b6a` | Flower/floral shadow tones in the card photography — these read as deep muted plum/wine, not a bright rose, which is consistent with "restrained... only when useful"; brightened from the raw photographic shadow sample to be usable as a UI accent |

See `css/mn-brand-tokens.css` for the full token list.

## ⚠️ Missing production assets — action needed

Two assets referenced or implied by the brand direction do not exist
anywhere in either project and were **not** created as substitutes,
per instruction:

### 1. Standalone MN crest

The ornamental gold "MN" circular crest (fine ring, dotted texture,
botanical flourish) visible on the approved Mercado Negro hub card
**only exists baked into that composite card image**
(`tarjeta-martha/hub-assets/cards/mercado-negro.png` /
`.webp`). There is no standalone crest file — vector or raster,
transparent or otherwise — anywhere in `tarjeta-martha`,
`mercado-negro`, or `mercado-negro-app`.

I did not crop it out of the composite card for production use (it
would carry JPEG/WebP compression artifacts, an arbitrary crop
boundary, and no transparency — not something to ship as a logo
file), and did not redraw/trace/reinterpret it as a new SVG.

**What's needed:** a standalone crest file — ideally a vector (SVG)
or a high-resolution PNG with transparency — matching the mark shown
on the hub card, sized with safe padding around the ring and
botanical branch so it can be dropped into both the card header and
the website hero without repeating this audit.

Until it's supplied, both properties use the legacy circular mark as
a small secondary badge plus the typographic `MERCADO NEGRO` serif
wordmark as the primary brand treatment, per the brief's fallback
guidance.

### 2. Dark dessert photography

The brief's photography direction (dark, editorial, chocolate,
berries, controlled highlights) references the hub card's dessert
photography as the reference *style*, but no dedicated photography
asset — of that dish or any other — exists in either project to
place in the website hero or elsewhere. `mercado-negro-app/src/assets/hero.png`
is unrelated generic app illustration art from a different product
and was not used.

Rather than substitute generic stock food photography (explicitly
discouraged in the brief) or fabricate an image, the website hero was
composed with layered charcoal/chocolate tone, gold framing and
typography to avoid the "empty black hero" problem without
photography. **If real product photography becomes available, it
should replace the current tone-only hero background** — the CSS is
structured (`.hero` background layer) to make that a contained swap.

## Functionality preserved

Verified unchanged on both properties:

- WhatsApp deep links (card: `+52 55 1728 4050`; website: `+52 56 5791 7967`
  — these were already two different numbers in the original files;
  not something introduced or "fixed" here, flagging in case it's an
  existing data error worth checking)
- Instagram handle: `@mercadonegrobymarthadominguez`
- CLABE interbancaria (card only): `012180015019864949`, with its
  copy-to-clipboard behavior
- "Guardar contacto" vCard download (card), same fields as before
- Website contact form (Web3Forms endpoint + access key), success/error
  messaging, same field set and options
- All internal nav anchors (`#nosotros`, `#servicios`, `#menu`, `#contacto`)
- Menu content: Pasteles / Postres / Antipastos / Charcutería, same
  descriptions (icons changed from emoji to line-art SVG for visual
  consistency with the new serif/gold system; no content change)

No Firebase files, hosting config, or new dependencies were
introduced. Both properties remain plain static HTML/CSS/JS on
GitHub Pages, relative paths preserved.
