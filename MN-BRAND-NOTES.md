# Mercado Negro — brand unification notes

Working notes from the brand consolidation pass across:

- `tarjeta-martha-mn.html` (digital card, in the `tarjeta-martha` repo)
- `mercado-negro/index.html` (website, this repo)

Both now share `css/mn-brand-tokens.css`, kept byte-identical in each
repo since GitHub Pages serves them as two separate static sites with
no cross-repo includes possible.

## Brand direction history (important for future work)

There have been **four** brand-direction passes on this project.
**The fourth (Option 1 logo + Option C UI palette) is current and
locked.** Check with the client before assuming any earlier direction
still applies if this comes up again — it has changed multiple times.

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
3. **Third pass — "Option 1"** — assets under `brand-option1/`. Same
   seal + script + byline identity, but supplied as one flattened
   lockup image, black/near-black dominant background
   (`--mn-black: #090908`), gold restrained to accents. Buttons still
   used a filled dusty-rose primary CTA (`--mn-rose: #8B6B6A`).
   **Superseded — the client felt this still read as "too brown" in
   places and rejected the rose CTA.**
4. **Fourth pass — APPROVED: Option 1 logo + Option C UI palette
   (current, locked)** — assets under `brand-optionc/`. Logo is
   byte-identical to the third pass (confirmed via `cmp`) — only the
   UI palette and button treatment changed:
   - New token names: `--mn-black`, `--mn-charcoal`, `--mn-panel`,
     `--mn-panel-2`, `--mn-ivory`, `--mn-champagne` (`#D8C79E`,
     paler/more desaturated than the old `--mn-gold: #C9A876`),
     `--mn-champagne-soft`, `--mn-divider`
   - **No `--mn-rose` token at all** — the filled dusty-rose primary
     CTA is explicitly rejected for this pass
   - Primary CTA is now an **outline treatment**: `--mn-button-fill`
     (`#101010` near-black) + `--mn-button-border` (`#D8C79E`
     champagne) + `--mn-button-text` (`#F5F0E6` ivory) — not a filled
     color block
   - Source of truth: `brand-optionc/reference/APPROVED_OPTION_1_SOURCE_OF_TRUTH.png`
     (logo) + `brand-optionc/reference/SELECTED_OPTION_C_CARD_STYLE_REFERENCE.png`
     (UI mood/card styling)

`css/mn-brand-tokens.css` keeps backward-compatible aliases
(`--mn-cream` → `--mn-ivory`, `--mn-gold` → `--mn-champagne`,
`--mn-charcoal-2` → `--mn-panel-2`, etc.) so that any markup still
using the older variable names resolves to current Option C values
rather than silently reverting to a superseded palette. New CSS should
prefer the direct Option C names (`--mn-ivory`, `--mn-champagne`,
`--mn-panel`) going forward.

Earlier `brand/` and `brand-option1/` folders were **not deleted** —
kept as legacy per instruction not to remove assets unnecessarily —
but are no longer referenced by either live HTML file. `brand-optionc/`
is what's actually wired into both properties now.

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
- Unified button hierarchy: primary actions use the Option C outline
  treatment (near-black fill, champagne border, ivory text — no
  filled color block); secondary actions use black/charcoal surfaces
  with a thin champagne/divider border, consistent radius and hover
  states, on both properties.
- Visually-hidden `<h1>` on the website hero (the visible brand name
  is an image) to keep a real heading in the accessibility/SEO outline.
- Preserved all existing functional content and behavior — see
  "Functionality preserved" below.

## Brand assets (current, approved — Option 1 logo + Option C palette)

All under `brand-optionc/` in both repos (copied from the
client-supplied `Mercado_Negro_OptionC_Black_Champagne_Pack_for_Claude`
pack). Logo files are byte-identical to the earlier `brand-option1/`
pack — only the tokens/reference are new for this pass:

- `brand-optionc/logo/mercado-negro-option1-full-lockup-transparent.*`
  — primary full lockup, dark backgrounds. **Primary mark.**
- `brand-optionc/logo/mercado-negro-option1-full-lockup-black.*` —
  exact black-background safety master
- `brand-optionc/logo/mercado-negro-option1-seal-transparent.*` /
  `-black.*` — seal alone, for favicon/compact nav/social/badge use.
  **Do not shrink the full lockup into small icon slots — use the seal.**
- `brand-optionc/favicon/` — 32/48/64/128/180/192/512px + `favicon.ico`
- `brand-optionc/social/mercado-negro-social-avatar-1024.*` — square
  social avatar
- `brand-optionc/social/mercado-negro-social-share-1200x630.*` —
  OG/Twitter share image
- `brand-optionc/tokens/mn-brand-tokens.json`,
  `brand-optionc/tokens/mn-brand-tokens.css` — client-supplied color
  source of truth (values match `css/mn-brand-tokens.css` exactly)
- `brand-optionc/reference/APPROVED_OPTION_1_SOURCE_OF_TRUTH.png` —
  logo reference (unchanged from prior pass)
- `brand-optionc/reference/SELECTED_OPTION_C_CARD_STYLE_REFERENCE.png`
  — UI mood/card-styling reference for this pass specifically

None of these were redrawn, traced, simplified, or reinterpreted —
used exactly as supplied.

## Palette (current)

| Token | Hex | Role |
|---|---|---|
| `--mn-black` | `#090908` | deepest background tier |
| `--mn-charcoal` | `#121210` | primary background |
| `--mn-panel` | `#0D0D0D` | card/panel surface |
| `--mn-panel-2` | `#111111` | slightly elevated panel surface |
| `--mn-ivory` | `#F5F0E6` | primary text/logo color |
| `--mn-champagne` | `#D8C79E` | restrained accent — borders, rules, labels |
| `--mn-champagne-soft` | `#C9B88B` | secondary/muted champagne |
| `--mn-button-fill` | `#101010` | primary CTA fill |
| `--mn-button-border` | `#D8C79E` (champagne) | primary CTA border |
| `--mn-button-text` | `#F5F0E6` (ivory) | primary CTA text |

These match `brand-optionc/tokens/mn-brand-tokens.json` exactly (the
supplied source of truth). **There is no `--mn-chocolate` and no
`--mn-rose` token anymore** — chocolate was second-pass only, and the
filled dusty-rose CTA was third-pass only. Both are explicitly
rejected by the current (Option C) direction.

## Explicitly out of scope for this pass

Per the Option C brief:
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
