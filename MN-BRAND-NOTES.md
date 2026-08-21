# Mercado Negro — brand unification notes

Working notes from the brand consolidation pass across:

- `tarjeta-martha-mn.html` (digital card, in the `tarjeta-martha` repo)
- `mercado-negro/index.html` (website, this repo)
- The Martha Domínguez hub's Mercado Negro tile — **NOT yet updated,
  see "Hub tile — pending" below.**

Both HTML files share `css/mn-brand-tokens.css`, kept byte-identical
in each repo since GitHub Pages serves them as two separate static
sites with no cross-repo includes possible.

## ⚠️ Hub tile — pending (not done in this pass)

The Martha hub (`tarjeta-martha/index.html`) shows Mercado Negro as
one flat photo composite: `hub-assets/cards/mercado-negro.webp` /
`.png`. The old monogram, old wordmark, flowers, cake, plate, arrow
button and gold border are all baked into the same image pixels —
there is no way to swap "just the branding" without either
regenerating that composite (explicitly against instructions — no
redrawing) or overlaying new elements on top of the existing photo.

When the Final Locked Brand Pack asked to update "the Mercado Negro
tile only" on the hub, this was surfaced to the user as a real
constraint rather than guessed at, and **the user's direction was to
leave the hub tile alone for this pass.** The website and digital card
were updated to the final locked brand; the hub tile still shows the
old monogram/wordmark baked into its photo.

**Next time this comes up:** either (a) get a freshly regenerated hub
tile composite image with the new monogram/wordmark already baked in
by whoever produces the source art, or (b) explicitly authorize an
HTML/CSS overlay approach (new monogram + wordmark images
absolutely-positioned on top of the existing photo, covering the old
branding, exact composition/size/corners/border/arrow otherwise
untouched).

## Brand direction history (important for future work)

There have been **five** brand-direction passes on this project.
**The fifth ("FINAL LOCKED BRAND PACK") is current and locked** — note
the pack's own filename says "final," but so did earlier ones in
spirit; check with the client before assuming any direction still
applies if this comes up again.

1. **First pass** — an ornamental gold "MN" crest concept (fine ring,
   dotted texture, botanical flourish) inspired by artwork glimpsed on
   a Martha Domínguez hub card mockup. No standalone file for that
   crest ever existed; it was only visible baked into a composite card
   image. Used an all-caps serif "MERCADO NEGRO" wordmark as primary.
   **Superseded.**
2. **Second pass** — seal + script wordmark, assets under `brand/`:
   round seal + script "Mercado Negro" + gold "BY MARTHA DOMÍNGUEZ"
   byline as separate composable pieces, on a charcoal/chocolate-forward
   palette. **Superseded.**
3. **Third pass — "Option 1"** — assets under `brand-option1/`. Same
   seal + script + byline identity, supplied as one flattened lockup
   image, black/near-black background, filled dusty-rose primary CTA.
   **Superseded — client felt it still read "too brown."**
4. **Fourth pass — "Option C"** — assets under `brand-optionc/`. Same
   logo as pass 3 (confirmed byte-identical via `cmp`), only the UI
   palette/button treatment changed: outline-style CTAs, no filled
   rose. **Superseded — client moved on from the seal+script identity
   entirely, see pass 5.**
5. **Fifth pass — FINAL LOCKED BRAND PACK (current, locked)** — assets
   under `brand-final/`. This is a genuine identity change, not just a
   palette tweak:
   - **Monogram** = "Option 2" — an ornate circular gold-frame "MN"
     monogram with a richer 3D gold finish (fleur-de-lis flourishes,
     scrollwork), noticeably more elaborate than any earlier mark.
     File: `mercado-negro-monogram-option2-locked-transparent.webp`
   - **Wordmark** = "Option 4" from an 8-option comparison board — a
     clean **upright Didot-style serif** "Mercado Negro". This is a
     hard departure from every earlier pass, which all used a script/
     cursive wordmark (Alex Brush). The script font is no longer used
     anywhere in either property.
     File: `mercado-negro-wordmark-option4-transparent.webp`
   - Monogram and wordmark are two **separate image files**, not one
     fused lockup — stack them with visible breathing room between
     (the brief explicitly called this out).
   - Palette tokens shifted slightly from pass 4's Option C values:
     `--mn-black: #0B0B0B` (was `#090908`), `--mn-near-black: #121212`
     (was `#121210`), `--mn-ivory: #F4F1EA` (was `--mn-cream: #F5F0E6`),
     `--mn-champagne: #D4B98A` (was `#D8C79E`). Same spirit
     (black/near-black + ivory + restrained champagne, no chocolate,
     no filled rose), just refined hex values — treat pass 4's values
     as fully superseded, not "close enough."
   - Source of truth: `brand-final/reference/LOCKED_OPTION2_MONOGRAM_SOURCE.png`,
     `brand-final/reference/LOCKED_OPTION4_WORDMARK_SOURCE.png`,
     `brand-final/reference/LOCKED_OPTION4_FULL_STACK_CARD_REFERENCE.png`

### Known issue in the delivered wordmark asset

`mercado-negro-wordmark-option4-transparent.png` (728×155) has its own
"BY MARTHA DOMÍNGUEZ" byline text baked in below the "Mercado Negro"
line and a divider — but the export is **cut off mid-letter at the
bottom edge of the file itself** (confirmed by inspecting the alpha
channel row-by-row). This isn't something introduced here; it's how
the file was delivered.

Rather than stretch, redraw, or otherwise modify that asset, both the
card and the website display it inside a `overflow:hidden` frame at a
fixed `aspect-ratio: 728/105` (`object-fit: cover; object-position:
top`) — this shows only the clean "Mercado Negro" text and cuts off
above where the truncation starts. The divider and "BY MARTHA
DOMÍNGUEZ" byline are then recreated as real HTML/CSS (a thin
champagne rule + dot, and a text line), matching
`LOCKED_OPTION4_FULL_STACK_CARD_REFERENCE.png`. The source PNG/WebP
files on disk are byte-for-byte what was delivered — only how much of
them is *displayed* is constrained via CSS. If a corrected export
(with the byline fully visible) is supplied later, this workaround can
be removed and the image shown at full height instead.

`css/mn-brand-tokens.css` keeps backward-compatible aliases
(`--mn-cream` → `--mn-ivory`, `--mn-gold` → `--mn-champagne`,
`--mn-charcoal` → `--mn-near-black`, `--mn-panel` → `--mn-near-black`,
etc.) so that any markup still using older variable names resolves to
the current locked values rather than silently reverting to a
superseded palette. New CSS should prefer the direct current names
(`--mn-ivory`, `--mn-champagne`, `--mn-near-black`, `--mn-black`)
going forward.

Earlier `brand/`, `brand-option1/`, and `brand-optionc/` folders were
**not deleted** — kept as legacy per instruction not to remove assets
unnecessarily — but are no longer referenced by either live HTML file.
`brand-final/` is what's actually wired into both properties now.

## What changed (current implementation)

- Removed the bright magenta (`#8B2252`) that originally dominated
  nav, hero CTA, section labels, buttons and form UI on both
  properties. Palette is black/near-black/ivory with champagne as a
  restrained accent only — no chocolate/brown, no filled rose.
- Primary brand marks on both properties are now the supplied Option 2
  monogram + Option 4 wordmark, used as two separate images stacked
  with breathing room, not one fused lockup.
- Compact/secondary uses (nav bar, favicon, social) use the monogram
  alone.
- Shared functional/UI type layer (Arial/Helvetica) for nav, buttons,
  form fields and contact rows, separate from the serif editorial
  layer. The script (Alex Brush) font is gone entirely — the wordmark
  is now the upright Didot-style serif image, and the `Alex Brush`
  Google Fonts import was removed from both files.
- Website hero is a composed, framed section (gold corner framing,
  monogram, wordmark, divider, byline, descriptor, italic tagline,
  outline CTA) on a black→near-black gradient.
- Unified button hierarchy: primary actions use the outline treatment
  (near-black fill, champagne border, ivory text — no filled color
  block); secondary actions use black/near-black surfaces with a thin
  champagne/divider border, consistent radius and hover states, on
  both properties.
- Visually-hidden `<h1>` on the website hero (the visible brand name
  is images) to keep a real heading in the accessibility/SEO outline.
- Preserved all existing functional content and behavior — see
  "Functionality preserved" below.
- **Did not touch the Martha hub's Mercado Negro tile** — see
  "Hub tile — pending" at the top of this file.

## Brand assets (current, approved — Final Locked Brand Pack)

All under `brand-final/` in both repos (copied from the client-supplied
`Mercado_Negro_Final_Locked_Brand_Pack_for_Claude` pack):

- `brand-final/logo/mercado-negro-monogram-option2-locked-transparent.*`
  — ornate gold-frame "MN" monogram. **Primary compact mark** — use
  for favicon, nav, social badge, and stacked above the wordmark on
  the card/hero.
- `brand-final/logo/mercado-negro-wordmark-option4-transparent.*` —
  upright Didot-serif "Mercado Negro" wordmark. Byline text baked into
  this file is cut off at the bottom edge — see "Known issue" above;
  displayed through a cropping frame, byline recreated as HTML.
- `brand-final/favicon/` — 32/48/64/128/180/192/512px + `favicon.ico`
  (monogram-based)
- `brand-final/social/mercado-negro-social-avatar-1024.*` — square
  social avatar
- `brand-final/social/mercado-negro-social-share-1200x630.*` —
  OG/Twitter share image
- `brand-final/tokens/mn-brand-tokens.json`,
  `brand-final/tokens/mn-brand-tokens.css` — client-supplied color
  source of truth (values match `css/mn-brand-tokens.css` exactly)
- `brand-final/reference/LOCKED_OPTION2_MONOGRAM_SOURCE.png`,
  `LOCKED_OPTION4_WORDMARK_SOURCE.png`,
  `LOCKED_OPTION4_FULL_STACK_CARD_REFERENCE.png`,
  `OPTION4_BYLINE_DESCRIPTOR_REFERENCE.png`,
  `WORDMARK_OPTIONS_BOARD_CLIENT_PICKED_OPTION4.png` — reference/
  source-of-truth images

None of these were redrawn, traced, simplified, or reinterpreted —
used exactly as supplied (subject to the display-crop workaround noted
above, which does not modify the files themselves).

## Palette (current)

| Token | Hex | Role |
|---|---|---|
| `--mn-black` | `#0B0B0B` | deepest background tier |
| `--mn-near-black` | `#121212` | primary background / panel |
| `--mn-ivory` | `#F4F1EA` | primary text/logo color |
| `--mn-champagne` | `#D4B98A` | restrained accent — borders, rules, labels |
| `--mn-button-fill` | `#101010` | primary CTA fill |
| `--mn-button-border` | `#D4B98A` (champagne) | primary CTA border |
| `--mn-button-text` | `#F4F1EA` (ivory) | primary CTA text |

These match `brand-final/tokens/mn-brand-tokens.json` exactly (the
supplied source of truth). **There is no chocolate/brown token and no
filled-rose CTA token** — both were explicitly rejected in earlier
passes and remain rejected here. Note these hex values are refined
from pass 4's Option C values (e.g. `#0B0B0B` vs the old `#090908`) —
treat them as the new source of truth, not "basically the same."

## Explicitly out of scope for this pass

Per the Final Locked Brand Pack brief:
- Coordenada Viajes branding/pages were **not touched**.
- The overall Martha hub layout/shell (cream theme, Coordenada tile,
  monogram, footer) was **not touched**.
- The Martha hub's Mercado Negro tile composition (photo, cake, tart,
  arrow, size, rounded corners, layout) — **not touched at all in this
  pass**, including its branding. See "Hub tile — pending" above.

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
