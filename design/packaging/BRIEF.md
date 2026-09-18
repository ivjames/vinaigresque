# Vinaigresque — packaging art brief (round 1)

Context: the site's design brief is `design/BRIEF.md`; its product facts,
brand tokens, voice and "what is NOT known" section all apply here and are
not repeated. This brief adds what packaging needs: the container options
under consideration, what goes on a pack, and the deliverable shape for a
round of art directions. Round 1 is exploration: nothing here is production
artwork, and no pack size is settled.

## Containers under consideration

Two sources. The owner's own plan (project packet, 2026-09-16) is blank
stand-up pouches plus sheet labels for testing, then printed high-barrier
pouches for retail; two Pouch House samples are on order, 4.375 × 6 × 2 in
and 5 × 6.5 × 2.5 in. The second source is Vann's Spices' private-label
container sheet (`private-label-spices-container-options-vanns-spices.pdf`,
versions dated 2025-08-26/27), which lists what Vann's fills and labels:

| Vann's option | Size | Label / print area |
|---|---|---|
| Glass round, 4 oz | 4 in H × 1.75 in dia | 4.5 × 2.5 in |
| Glass square, 4 oz | 4 in H × 1.5 in sides | 4.5 × 2.5 in |
| Glass square, 4 oz, grinder top | 4 in H × 1.5 in sides | 4.5 × 2.5 in |
| Plastic, 1 oz | 2.047 in H × 1.775 in dia | 4 × 0.875 in |
| Plastic, 3.75 oz | 4.75 in H × 1.75 in dia | 5 × 3 in |
| Plastic, 5.5 oz | 4.75 in H × 2 in dia | 5 × 3 in |
| Plastic, 8 oz | 5 in H × 2.25 in dia | 6 × 3 in |
| Plastic, 16 oz | 5.75 in H × 2.5 in dia | 6.75 × 3.5 in |
| PET food service, 32 oz | 2.75 × 3.25 × 8.25 in | 2.179 × 3.8875 in |
| PET food service, 160 oz | 5 × 7.25 × 10.5 in | 3.5 × 3.5 in |
| Pillow pouch | 3.5 or 5.5 in wide, height adjustable | full wrap; full ink or transparent |
| Stand-up pouch | 5 or 6.125 in wide × 8 in high × 3 in base | full wrap; full ink or with transparent window |

Vann's label-content list (same sheet, page 3): a story paragraph, social
and URL, a usage paragraph, ingredients, "distributed by" with city, state,
zip, net weight in oz and g, UPC, nutrition panel as needed. Allowed phrases
include Non-GMO (written, uncertified), Vegan, Made in the USA; Kosher and
Organic need applications. None of these claims is decided for this product;
none goes on the art except as a bracketed slot.

### Fit

Facts: one pouch is 42 g of dry mix making about eight servings, and the
packet's provisional bulk volume for that fill is about 124 mL, to be
measured. Vann's jar "ounces" are capacity, not weight: a 4 in × 1.75 in
cylinder is roughly 158 mL gross, consistent with a 4 fl oz (118 mL) nominal.

Inferences from that, all to be checked against a real 42 g fill:

- The 4 oz glass jars (118 mL) are too small for a full eight-serving fill
  with any headspace. Glass at this fill would mean a smaller jar product
  (about four servings) or a jar Vann's does not list.
- The 5.5 oz plastic (about 163 mL) is the smallest listed container that
  takes 124 mL with headspace; the 8 oz (237 mL) takes it at about half full.
- The grinder top does not apply: the blend is leafy herbs and powders.
- Vann's stand-up pouch (5 × 8 × 3 in) is larger than both Pouch House
  samples; 42 g would sit in its lower third. The pillow pouch, at 3.5 in
  wide and a chosen height, is the closer Vann's fit for this fill; the
  stand-up buys shelf presence at the cost of fill proportion.

Not known: Vann's terms (minimums, whether they blend and fill or only
supply), whether the owner intends to co-pack at all, and the shelf-life
target that decides clear, white or metallized. Nothing in this round
depends on those answers; the art is drawn for the surfaces above so it
can be judged on any of them.

## What goes on a pack

Front, per the packet's front-of-pack direction, kept unusually simple:

1. `Vinaigresque.` with the sage period.
2. The flavor name. Classic Italian Herb is the base; the family for this
   round is the six on the site: Classic Italian Herb, Lemon Herb, Garlic &
   Herb, Greek Herb, Roasted Red Pepper, Ginger Citrus.
3. `A mustard-free vinaigrette mix.`
4. The bottle mark, one static frame of the site's cruet (its inline SVG in
   `index.html` is the no-JS frame: taupe glass, gold oil, four burgundy
   globs, sage herb flecks). Extend it; do not redraw it.
5. The add-oil-and-vinegar cue, e.g. `Add oil and vinegar. Shake.` and
   `Makes about eight servings.`
6. Net weight as a slot: `NET WT [__ g / __ oz]`. No number.

Back: mixing directions (3 : 1 oil to vinegar; ¾ cup oil and ¼ cup vinegar
per pouch, 1½ tablespoons and ½ tablespoon per salad), ingredients at the
name level only (dried oregano, parsley and basil, garlic and onion powder,
black pepper, salt, sugar), the pairing guide, and bracketed slots for
`[Nutrition Facts]`, `[Distributed by]`, `[Lot / best by]`, `[UPC]`,
`[vinaigresque.com]`. Slots are drawn as labelled boxes at plausible size,
never filled with invented text, figures or a fake barcode.

Nothing else. No claims (no "all natural", "non-GMO", "gluten free",
"allergen-free", "safe for"), no origin story on the front, no "in
development" language on the pack.

## Brand system on pack

The tokens, faces and voice in `design/BRIEF.md` apply. Specifics for print:

- Cream ground is the default. A direction may put one other token on a
  field, but sage (`#6B7F4E`) never sits behind or as small text; on a
  sage-ink, burgundy or ink field, text is cream.
- Flavor is told by name and by an ingredient image or icon, never by colour
  alone. Colour may assist.
- Type: system stacks as the site uses them (`--serif` and `--sans` in
  `index.html`). Do not load a webfont.
- Minimum type on pack: 6 pt equivalent for slot text; the name, flavor,
  descriptor and net weight larger.
- Images: the cutouts in `assets/img/` (referenced from the round files as
  `../../../assets/img/…`). Do not add images to the repo this round.

## Deliverable per direction

One file at `design/packaging/round-1/<slug>.html`, self-contained (inline
CSS, no script needed, nothing loaded from another host), drawing these
surfaces at true proportion on a common scale of **1 in = 96 CSS px**, each
labelled with its name and dimensions:

1. Stand-up pouch front, 5 × 8 in (Vann's). Mark the printable safe area and
   the 3 in gusset zone at the base as light guides.
2. Pillow pouch front, 3.5 in wide × 6 in high (height is adjustable; 6 in
   is this round's working assumption).
3. Jar label, 5 × 3 in, flat (fits the 3.75 oz and 5.5 oz plastic).
4. Stand-up pouch back, 5 × 8 in, with the back content above.
5. The flavor family: fronts of the stand-up pouch for Classic Italian Herb,
   Lemon Herb and Ginger Citrus side by side at half scale, showing how a
   flavor changes the front.

Then screenshots to `design/packaging/round-1/shots/<slug>-<surface>.png`
via Playwright with the pre-installed Chromium (`/opt/pw-browsers`; do not
run `playwright install`), at device scale 2. Look at them; fix what is
wrong; repeat. Compute the contrast ratios of your actual text and field
pairs. Report back: the hypothesis, what each surface does, the ratios, and
anything you could not resolve. No file dumps.

Round files are exploration and are not linked from the site.
