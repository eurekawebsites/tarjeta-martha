# Mercado Negro — brand unification notes

Working notes from the brand consolidation pass across:

- `tarjeta-martha-mn.html` (digital card, in the `tarjeta-martha` repo)
- `mercado-negro/index.html` (website, this repo)

Both now share `css/mn-brand-tokens.css`, kept byte-identical in each
repo since GitHub Pages serves them as two separate static sites with
no cross-repo includes possible.

## Brand direction history (important for future work)

There have been **three** brand-direction passes on this project.
**The third (Option 1) is current and locked.** Check with the client
before assuming any earlier direction still applies if this comes up
again.

1. **First pass** — an ornamental gold "MN" crest concept (fine ring,
   dotted texture, botanical flourish) inspired by artwork glimpsed on
   a Martha Domínguez hub card mockup. No standalone file for that
   crest ever existed; it was only visible baked into a composite card
   image. Used an all-caps serif "MERCADO NEGRO" wordmark as primary.
   **Superseded — do not reintroduce.**
2. **Second pass** — client-approved seal + script wordmark direction,
   assets under `brand/`: round seal + script "Mercado Negro" + gold
   "BY MARTHA DOMÍNGUEZ" byline as separate composable pieces, on a
   charcoal/chocolate-forward palette (`--mn-chocolate: #1C1712` used
   as a visible secondary surface color throughout).
   **Superseded — do not reintroduce the chocolate/brown surfaces.**
3. **Third pass — APPROVED OPTION 1 (current, locked)** — assets under
   `brand-option1/`. Same seal + script + byline identity, but:
   - Supplied as **one flattened lockup image** (not separate pieces)
   - Background must be **black/near-black dominant**
     (`--mn-black: #090908` / `--mn-charcoal: #121210`)
   - **No brown/chocolate-forward surfaces** — `--mn-chocolate` is
     removed from the token file entirely
   - Gold is a restrained accent/detail only, not a surface color
   - Source of truth image: `brand-option1/reference/APPROVED_OPTION_1_SOURCE_OF_TRUTH.png`

The `brand/` folder (second pass) was **not deleted** — kept as legacy
per instruction not to remove assets unnecessarily — but is no longer
referenced by either live HTML file. `brand-option1/` is what's
actually wired into both properties now.

## What changed (current implementation)

- Removed the bright magenta (`#8B2252`) that originally dominated
  nav, hero CTA, section labels, buttons and form UI on both
  properties. Palette is black/charcoal/gold/cream with restrained
  dusty rose on primary CTAs only — no chocolate/brown surfaces.
- Primary brand mark on both properties is the supplied Option 1 full
  lockup (`brand-option1/logo/mercado-negro-option1-full-lockup-transparent.webp`):
  seal + script "Mercado Negro" + fine gold divider + "BY MARTHA
  DOMÍNGUEZ" byline, used as one flattened image exactly as delivered.
- Compact/secondary uses (nav bar, favicon, social) use the Option 1
  seal alone (`brand-option1/logo/mercado-negro-option1-seal-transparent.webp`).
- Shared functional/UI type layer (Arial/Helvetica) for nav, buttons,
  form fields and contact rows, separate from the serif editorial
  layer and the script brand wordmark (baked into the logo image).
- Website hero is a composed, framed section (gold corner framing,
  primary lockup, descriptor, italic tagline, CTA) on a black→charcoal
  gradient — not plain centered text on flat black, and not
  chocolate-tinted.
- Unified button hierarchy: primary actions use dusty rose + cream
  text; secondary actions use charcoal/black surfaces with a thin gold
  border, consistent radius and hover states, on both properties.
- Visually-hidden `<h1>` on the website hero (the visible brand name
  is an image) to keep a real heading in the accessibility/SEO outline.
- Preserved all existing functional content and behavior — see
  "Functionality preserved" below.

## Brand assets (current, approved — Option 1)

All under `brand-option1/` in both repos (copied from the
client-supplied `Mercado_Negro_OPTION_1_APPROVED_Assets_for_Claude`
pack):

- `brand-option1/logo/mercado-negro-option1-full-lockup-transparent.*`
  — primary full lockup, dark backgrounds. **Primary mark.**
- `brand-option1/logo/mercado-negro-option1-full-lockup-black.*` —
  exact black-background safety master (use if the transparent
  version ever shows edge artifacts on a non-solid background)
- `brand-option1/logo/mercado-negro-option1-seal-transparent.*` /
  `-black.*` — seal alone, for favicon/compact nav/social/badge use.
  **Do not shrink the full lockup into small icon slots — use the seal.**
- `brand-option1/favicon/` — 32/48/64/128/180/192/512px + `favicon.ico`
- `brand-option1/social/mercado-negro-social-avatar-1024.*` — square
  social avatar
- `brand-option1/social/mercado-negro-social-share-1200x630.*` —
  OG/Twitter share image
- `brand-option1/tokens/mn-brand-tokens.json`,
  `brand-option1/tokens/mn-brand-tokens.css` — client-supplied color
  source of truth (values match `css/mn-brand-tokens.css` exactly)
- `brand-option1/reference/APPROVED_OPTION_1_SOURCE_OF_TRUTH.png` —
  locked visual reference

None of these were redrawn, traced, simplified, or reinterpreted —
used exactly as supplied.

## Palette (current)

| Token | Hex | Role |
|---|---|---|
| `--mn-black` | `#090908` | deepest background tier |
| `--mn-charcoal` | `#121210` | primary background |
| `--mn-gold` | `#C9A876` | restrained accent/detail only — not a surface color |
| `--mn-cream` | `#F5F0E6` | dominant logo/text color |
| `--mn-rose` (dusty rose) | `#8B6B6A` | primary CTA accent only, used sparingly |

These match `brand-option1/tokens/mn-brand-tokens.json` exactly (the
supplied source of truth). **There is no `--mn-chocolate` token
anymore** — that was second-pass only and is explicitly rejected by
the Option 1 direction.

## Explicitly out of scope for this pass

Per the Option 1 brief:
- The Martha Domínguez hub (`tarjeta-martha/index.html`) and its
  Mercado Negro hub tile artwork were **not touched** — that's a
  separate future pass.
- Coordenada Viajes branding/pages were **not touched**.

## Remaining gap

No dedicated dark dessert photography asset exists in either project.
The website hero is composed with layered black/charcoal tone, gold
framing and the logo lockup to avoid an empty hero without
substituting stock photography. **If real product photography becomes
available,** it can be added as a hero background layer — the CSS
`.hero` background is structured to make that a contained change.

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
