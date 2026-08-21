# Mercado Negro — brand unification notes

Working notes from the brand consolidation pass across:

- `tarjeta-martha-mn.html` (digital card, in the `tarjeta-martha` repo)
- `mercado-negro/index.html` (website, this repo)
- `tarjeta-martha/index.html` — the Martha Domínguez hub's Mercado
  Negro tile (now up to date — see "Hub tile — resolved" below)

Both HTML files share `css/mn-brand-tokens.css`, kept byte-identical
in each repo since GitHub Pages serves them as two separate static
sites with no cross-repo includes possible.

## ✅ Hub tile — resolved

Earlier notes here flagged that the Martha hub's Mercado Negro tile
(`tarjeta-martha/hub-assets/cards/mercado-negro.webp`/`.png`) was a
flat photo composite with the *old* monogram/wordmark baked into its
pixels, and that there was no way to update "just the branding"
without either regenerating the composite or overlaying new elements —
so it was intentionally left alone in the Final Locked Brand Pack
pass.

That gap is now closed: the client supplied a freshly regenerated hub
tile (`Martha_FINAL_Hub_Card_and_Transparent_Favicon_for_Claude` pack)
with the current locked monogram + Option 4 serif wordmark baked in by
whoever produced the source art — option (a) from the note below,
resolved as expected. Same photo composition, cake, tart, plate, arrow
button, and gold border as before; only the branding inside the tile
changed. Delivered pre-sized at 879×380 (the tile's existing shared
aspect ratio), so the old CSS crop-compensation hack
(`object-position: center bottom` working around ~22px of extra cream
canvas in the old export) was removed — the image now renders at its
native ratio with no special-casing.

At the same time, a new **transparent-background** Martha MD monogram
favicon was supplied (`martha-favicon/`), replacing the earlier
favicon derivation that had padded the monogram onto its own opaque
cream background — that version was showing a visible box behind the
mark in some browser chrome. Now under
`tarjeta-martha/images/md-icons-v2/`, referenced from `index.html`'s
`<head>` only. The Coordenada card and Mercado Negro card keep their
own separate, already-correct favicons — verified neither was
incorrectly inheriting the hub's.

The old `images/md-icons/` folder (opaque-background version) and old
hub tile bytes are gone from active use but not force-deleted from
git history — only the in-place files were overwritten per the
brief's "replace" instruction, which is different from the
brand-token folders in earlier passes that were deliberately kept
side-by-side as legacy references.

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
card and the website display it inside an `overflow:hidden` frame
sized to `aspect-ratio: 728/136` — that boundary was found by scanning
the alpha channel row-by-row: the "Mercado Negro" text and its full
divider render completely intact through y≈136, and only the already-
truncated byline pixels below that row are cut. The `<img>` itself
uses plain `width:100%; height:auto` with no `object-fit`/
`object-position` — since the frame's aspect ratio matches the image's
true rendered proportions at that crop line, the browser reveals
exactly the intended region with no distortion. The divider and "BY
MARTHA DOMÍNGUEZ" byline are then recreated as real HTML/CSS (a thin
champagne rule + dot, and a text line), matching
`LOCKED_OPTION4_FULL_STACK_CARD_REFERENCE.png`. The source PNG/WebP
files on disk are byte-for-byte what was delivered — only how much of
them is *displayed* is constrained via CSS.

**Correction (2026-08-21):** an earlier version of this fix used
`aspect-ratio: 728/105` with `object-fit: cover; object-position: top`
— that boundary was a guess, not measured from the actual pixels, and
it cut into the middle of the "Mercado Negro" glyphs and the divider
line, which read as clipped letters plus a visible dark rectangular
matte (the crop frame's own bounding box against the panel/hero
background). The `728/136` boundary above is the corrected, verified
value — confirmed by compositing the crop against the actual panel
background color and checking no glyph or divider pixel is cut.

If a corrected wordmark export (with the byline fully visible, no
truncation) is supplied later, this workaround can be removed
entirely and the image shown at full natural height instead.

**Resolved (2026-08-21):** the client supplied a corrected export,
`mercado-negro-wordmark-option4-CLEAN-transparent.png` (1673×324),
containing only the "Mercado Negro" mark itself — no baked byline, no
truncation, generous transparent padding on all sides (verified via
alpha-channel bbox: content sits at (92,55)–(1587,269) inside the
1673×324 canvas, corners fully transparent). This supersedes
`mercado-negro-wordmark-option4-transparent.*` and the crop-frame
workaround above entirely. Both the card and the website now render
this file directly with plain `display:block; width:100%; height:auto`
— no `aspect-ratio`, no `overflow:hidden` frame, no `object-fit`/
`object-position`. The divider and "BY MARTHA DOMÍNGUEZ" byline remain
real HTML/CSS underneath, unchanged. The old
`mercado-negro-wordmark-option4-transparent.png/.webp` files are left
on disk (not deleted) but are no longer referenced by either live HTML
file — see "Brand assets" below.

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
- `brand-final/logo/mercado-negro-wordmark-option4-CLEAN-transparent.png`
  — upright Didot-serif "Mercado Negro" wordmark, **current/active**.
  Clean export containing only the wordmark, no baked byline, no crop
  needed — rendered directly at natural proportions. Supersedes
  `mercado-negro-wordmark-option4-transparent.*` (kept on disk, no
  longer referenced) — see "Known issue" / "Resolved" above.
- `brand-final/favicon-transparent/` — 32/48/64/180/192/512px +
  `favicon.ico`, **current/active**. Genuinely transparent PNGs
  (verified corner-pixel alpha = 0) from the client-supplied
  `Mercado_Negro_Transparent_Favicon_Set`. Supersedes
  `brand-final/favicon/`, whose PNGs had an opaque black
  (`#0B0B0B`-ish) background baked in — confirmed via corner-pixel
  check (`(11,11,11,255)`). The old `brand-final/favicon/` folder is
  kept on disk (not deleted) but is no longer referenced by either
  live HTML file.
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
