# Mercado Negro — brand unification notes

Working notes from the brand consolidation pass across:

- `tarjeta-martha-mn.html` (digital card, in the `tarjeta-martha` repo)
- `mercado-negro/index.html` (website, this repo)

Both now share `css/mn-brand-tokens.css`, kept byte-identical in each
repo since GitHub Pages serves them as two separate static sites with
no cross-repo includes possible.

## Brand direction history (important for future work)

There were **two** brand-direction passes on this project. The second
supersedes the first:

1. **First pass** — an ornamental gold "MN" crest concept (fine ring,
   dotted texture, botanical flourish) inspired by artwork glimpsed on
   a Martha Domínguez hub card mockup. No standalone file for that
   crest ever existed; it was only visible baked into a composite card
   image. That direction used an all-caps serif "MERCADO NEGRO"
   wordmark as the primary mark.
2. **Approved/current pass** — the client confirmed they prefer the
   **classic round Mercado Negro seal + script "Mercado Negro"
   wordmark + "BY MARTHA DOMÍNGUEZ" byline** — i.e. a cleaned-up,
   properly-exported version of the pre-existing legacy circular logo,
   not the ornate MN crest. This is what's implemented now. **Do not
   reintroduce the all-caps serif wordmark or the MN-crest concept as
   the primary mark** — that direction was explicitly rejected.

If a fresh brand pass is ever requested again, check with the client
which of these directions (or a new one) is current before assuming.

## What changed (both passes combined)

- Removed the bright magenta (`#8B2252`) that originally dominated
  nav, hero CTA, section labels, buttons and form UI on both
  properties. Palette is now charcoal/chocolate/gold/cream with
  restrained dusty rose on primary CTAs only.
- Primary brand mark on both properties is now the supplied lockup
  image (`brand/logo/mercado-negro-primary-lockup-cream-gold-transparent-1600.webp`):
  round seal + script "Mercado Negro" + gold "BY MARTHA DOMÍNGUEZ"
  byline, used as one image exactly as delivered — not redrawn,
  not reconstructed from separate elements.
- Compact/secondary uses (nav bar, favicon) use the seal alone
  (`brand/logo/mercado-negro-seal-*-transparent-1024.webp`).
- Introduced a shared functional/UI type layer (Arial/Helvetica) for
  nav, buttons, form fields and contact rows, separate from the serif
  editorial layer and the script brand wordmark.
- Rebuilt the website hero as a composed, framed section (gold corner
  framing, primary lockup, descriptor, italic tagline, CTA) instead of
  plain centered text on flat black.
- Unified button hierarchy: primary actions use dusty rose + cream
  text; secondary actions use charcoal surfaces with a thin gold
  border, consistent radius and hover states, on both properties.
- Added a visually-hidden `<h1>` on the website hero (the visible
  brand name is now an image) to keep a real heading in the
  accessibility tree/SEO outline.
- Preserved all existing functional content and behavior — see
  "Functionality preserved" below.

## Brand assets (current, approved)

All under `brand/` in both repos (copied from the client-supplied
`Mercado_Negro_Approved_Brand_Assets_for_Claude` pack):

- `brand/logo/mercado-negro-primary-lockup-cream-gold-transparent-1600.*`
  — primary lockup, dark backgrounds. **Preferred primary mark.**
- `brand/logo/mercado-negro-lockup-gold-transparent-1600.*` — all-gold variant
- `brand/logo/mercado-negro-lockup-charcoal-gold-transparent-1600.*` — light-background variant
- `brand/logo/mercado-negro-seal-{cream,gold,charcoal}-transparent-1024.*`
  — seal alone, for favicons/compact/secondary use
- `brand/favicon/` — 32/64/180/192/512px + `favicon.ico`
- `brand/social/mercado-negro-social-avatar-1024.*` — OG/Twitter/social image
- `brand/mn-brand-tokens.json`, `brand/mn-brand-tokens-approved.css` —
  client-supplied color source of truth (values match
  `css/mn-brand-tokens.css` exactly)
- `brand/reference/` — approved direction board + original logo/seal
  references, kept for history

None of these were redrawn, traced, or reinterpreted — used exactly
as supplied.

## Palette

| Token | Hex |
|---|---|
| `--mn-charcoal` | `#121210` |
| `--mn-chocolate` | `#1C1712` |
| `--mn-gold` | `#C9A876` |
| `--mn-cream` | `#F5F0E6` |
| `--mn-rose` (dusty rose) | `#8B6B6A` — primary CTA accent only, used sparingly |

These match `brand/mn-brand-tokens.json` exactly (the supplied source
of truth).

## Remaining gap

No dedicated dark dessert photography asset exists in either project
(the earlier note about this still applies). The website hero is
composed with layered charcoal/chocolate tone, gold framing and the
logo lockup to avoid an empty hero without substituting stock
photography. **If real product photography becomes available,** it
can be added as a hero background layer — the CSS `.hero` background
is structured to make that a contained change.

## Functionality preserved

Verified unchanged on both properties:

- WhatsApp deep links (card: `+52 55 1728 4050`; website: `+52 56 5791 7967`
  — these are two different numbers in the original source files, not
  something introduced or changed here; flagging in case it's worth
  checking which is correct)
- Instagram handle: `@mercadonegrobymarthadominguez`
- CLABE interbancaria (card only): `012180015019864949`, with its
  copy-to-clipboard behavior
- "Guardar contacto" vCard download (card), same fields as before
- Website contact form (Web3Forms endpoint + access key), success/error
  messaging, same field set and options
- All internal nav anchors (`#nosotros`, `#servicios`, `#menu`, `#contacto`)
- Menu content: Pasteles / Postres / Antipastos / Charcutería, same
  descriptions

No Firebase files, hosting config, or new dependencies were
introduced. Both properties remain plain static HTML/CSS/JS on
GitHub Pages, relative paths preserved.
