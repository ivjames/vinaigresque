# Vinaigresque — landing page design brief

Context: vinaigresque.com is one static `index.html` served by nginx from this
checkout. No build step, no backend, no forms that post anywhere. The current
page (`/index.html`, PR #5) is the light-mode landing page: hero with the
animated bottle, how it works, why mustard-free, a flavor lineup, oil and
vinegar pairings, and an under-development panel.

Round 1 (the four directions in `design/round-1/`) was briefed before the
product packet existed and treated the product's form, ingredients and
palette as unknown. They are not unknown any more. This brief replaces that
one; the round-1 files stay as a record of what was explored and should not
be read as current on any point where they disagree with what follows.

## Source of truth

The owner's project packet (September 16, 2026) settles the product and the
brand. It is **not in this repo and is not to be committed**: the checkout is
the web root, and the packet holds the recipe, sourcing and nutrition work.
What follows is the part of it a landing page needs. Anything a page would
need beyond this, ask for; do not infer it from the round-1 files, and never
from the packet's AI-generated concept boards, whose nutrition panels,
ingredient lists, dates, barcodes and net weights are placeholder art.

## What is known about the product (use only this)

- Name: **Vinaigresque**. Domain: vinaigresque.com. The wordmark keeps its
  green period.
- It is a **dry vinaigrette seasoning mix**, sold as a pouch. The buyer adds
  their own oil and vinegar, then shakes or whisks. It is a pantry mix, not a
  bottled dressing.
- **Mustard-free** is the defining constraint and the positioning hook.
  Mustard is the usual emulsifier; without it the dressing separates as it
  sits, and that is accepted: it is made fresh and shaken before serving.
  Say that plainly. Do not claim it is emulsifier-free, gum-free, or
  anything-else-free, and do not frame it as a health product.
- **Origin:** the creator had a bad reaction to mustard, and that is why the
  mix exists. Mustard is one of Health Canada's priority food allergens, on
  the enhanced-labelling list since 2012, and the page may say so. This is a
  selling point and may lead the "why" section. State it as a fact about
  the recipe — there is no mustard in it — never as a safety promise: no
  "safe for", "allergen-free" or cross-contact claims, because those depend
  on how and where it is made, which is not settled.
- **3 : 1 oil to vinegar**, three parts oil to one part vinegar. One pouch
  makes about **eight servings**. For a whole pouch that is ¾ cup oil and
  ¼ cup vinegar; for one salad, 1½ tablespoons oil and ½ tablespoon vinegar.
- The mix is dried oregano, parsley and basil, garlic and onion powder,
  black pepper, salt and a little sugar: the packet's ingredient list at the
  name level, which the page may show. Never weights or proportions. The
  bottle animation shows the herbs, the powders and the pepper; salt and
  sugar dissolve, nothing else belongs in it, and no mustard seed ever.
- Extra-virgin olive oil and red wine vinegar are the house pairing. The
  pairing guide on the page (red wine, white wine or champagne, balsamic,
  apple cider, sherry, rice; olive oil, mild olive oil, avocado, neutral) is
  the customer-choice guide from the packet and may be reused as is.
- Flavors: **Classic Italian Herb** is the base blend. Lemon Herb, Garlic &
  Herb, Greek Herb and Roasted Red Pepper are the starter extensions, all in
  development. Say so; a flavor's status is text, not a colour.
- Positioning: a specialty pantry product for everyday salads. Refined,
  approachable, food-first. Culinary, not rustic; premium pantry, not
  luxury; fresh and ingredient-forward, not wellness-branded.
- Voice: simple, clean, food-first, slightly witty when useful, never
  precious. Directional lines, usable verbatim: "A mustard-free vinaigrette
  mix." "Simple ingredients. Remarkable salads." "Good ingredients go
  further." "Same salad. A more interesting story."

## What is NOT known — do not invent it

No price, no launch date, no shipping, no stockists, no testimonials, no
founder story beyond the origin above (no name, no date, no medical detail),
no ingredient weights, no nutrition figures, no cross-contact or "safe for"
language, no claims beyond mustard-free. Pouch size and
artwork are not settled, so **no packaging imagery** until they are. The
exact prepared volume per pouch is not measured, so keep serving language at
"about eight servings" and the ratio above.

Where a page structurally needs one of these, write bracketed placeholder
copy, e.g. `[price]`, so a reader can see what is real and what is a slot.
Never write plausible-sounding fake specifics.

## Brand system

Light mode only. The dark holding page this site opened with is kept as a
family reference (`design/round-1/shots/holding-*-dark.png`) and nothing more.

Tokens, as `/index.html` now names them:

| token | hex | role |
|---|---|---|
| `--cream` | `#FAF6EC` | background |
| `--ink` | `#2E2A1F` | olive brown: text and line work |
| `--sage` | `#6B7F4E` | the period and thin accents only |
| `--sage-ink` | `#5A6C40` | buttons, links, numerals on a fill |
| `--gold` | `#D4B04C` | the oil |
| `--burgundy` | `#7A2E34` | the vinegar, and one accent |
| `--taupe` | `#D8CDBA` | rules, the bottle's glass, structure |
| `--muted` | `#5E5849` | secondary copy |
| `--panel` | `#F3EDDE` | one step below cream, for cards |

Measured, not estimated: sage on cream is 4.08 : 1, so it never sits behind
or as text at body size; `--sage-ink` is 5.33 : 1 and does. `--muted` is
6.6 : 1 on cream. Taupe is never text.

Type: an editorial serif for display and ledes, a clean sans for body and
UI. The packet's reference faces are Tiempos Headline / Tiempos Text Italic
and Inter, "or a close licensed equivalent". No licence is on record, so the
page uses system stacks; do not load a webfont without one.

The bottle mark is the canvas simulation in `/index.html`: an open bottle,
golden oil, burgundy globules rising and falling, the mix falling in through
the neck. Motion is calm and ambient, holds still under reduced motion, and
degrades to the inline SVG without JS. Print and static uses take one frame
of it. Do not redraw the bottle from scratch; extend what is there.

## Hard constraints (every page)

1. One HTML file with inline CSS and inline script, plus images under
   `assets/` in this repo. Nothing loads from another host: no frameworks,
   no external scripts, no webfont CDN. JavaScript optional and
   progressive: the page must be complete with JS off. (Round 1's drafts
   were single files with no images; the shipped page has an `assets/`
   directory beside it, served by the same vhost.)
2. Works at 360px wide (16px side gutters, no horizontal scroll) through
   1440px. Test both. Write section padding as longhands (`padding-top`,
   `padding-bottom`): the shorthand on a `.wrap` element zeroes its gutter,
   which is how the first draft of the landing page lost it on phones.
3. Light only. Body has an explicit background, colours are the custom
   properties above. No `prefers-color-scheme` block.
4. Accessibility: body text ≥ 4.5 : 1, large text ≥ 3 : 1, control edges
   ≥ 3 : 1 against what they sit on; visible focus styles;
   `prefers-reduced-motion` honoured; semantic landmarks; one `h1`;
   images and SVG have alt text or `aria-hidden`. Compute the ratios.
5. The call to action: there is no backend, and the list is not open.
   While it is closed the form is `hidden` in the HTML, the panel says the
   list is not open, and the hero button reads "Coming soon". Opening it is
   an HTML edit, not a script: set the form's `action`, remove `hidden`,
   drop the closed line, relabel the button. A reader without JavaScript
   must see the same state as everyone else, so no toggle that only a
   script can flip. Do not wire it to a real service without being told
   which, and do not invent a `mailto:` address.
6. `<meta name="robots" content="noindex">` stays until told otherwise.
7. The HTML under ~60KB; images shown below their native pixel size and
   kept small (the current eleven total about 350KB). Keep the inline
   data-URI favicon.
8. No build stamp on the page (see `DEPLOY.md`).

## Process

- Write the page, then open it in Chromium via Playwright (pre-installed at
  `/opt/pw-browsers/chromium`; do NOT run `playwright install`) and take
  screenshots at 360×800 and 1440×900. Look at them. Fix what is wrong.
  Repeat until the page matches your intent.
- Check contrast ratios of your actual text/background pairs (compute them;
  don't estimate).
- Land it as a PR against `main`; the conventions in
  `.claude/rules/lab980-conventions.md` say how. Merging does not deploy.
- Your report back: what changed, which copy is placeholder, the ratios you
  measured, and anything you could not resolve. No file dumps.

---

# Round 2 (2026-09-17)

Decisions taken on 2026-09-17, on top of the packet brief above. Where the
two differ, this section wins; where it is silent, the packet brief stands.

1. **The shipped `index.html` is the direction.** Round 2 iterates on it.
   The round-1 files in `design/round-1/` are retired as directions and stay
   only as a record; nothing is carried forward from them except by
   deliberate choice.
2. **The packet's brand system stands as written**: cream ground, gold is
   the oil and not the page, light mode only. (An "own the yellow" override
   was considered and withdrawn the same day.)
3. **No call to action for now.** The hero "Coming soon" button and the
   waitlist panel are removed, along with their nav and footer links. The
   under-development line stays, as text. The packet brief's closed-waitlist
   shape (hidden form, HTML edit to open) is set aside until there is a list
   to open; do not reintroduce a button, form or `mailto:` without being
   told.
4. **Round-2 variants** are full alternative treatments of `index.html`,
   one file each at `design/round-2/<slug>.html`, screenshots in
   `design/round-2/shots/`. Each starts from the shipped page after the
   CTA removal, keeps its content and facts, and changes what its stated
   hypothesis calls for. Image paths from there are `../../assets/img/…`.
   Every hard constraint and the process in the packet brief apply.

---

# Round 3 (2026-09-17)

Decision on round 2: **`scale` is the base**, and three moves from the other
variants fold into it. Round 3 produces the new `index.html`, landed by PR;
it goes live at the next deploy.

1. From `edit`: the copy cuts. The hero kicker, the strip's fourth line, the
   how-it-works lede, step 3's repeat of the mustard explanation, the why
   section's ingredient repeat and third paragraph, and the flavours lede go.
   Every fact stays; only restatements leave.
2. From `food`: the three step renders at native size on panel plates as the
   how-it-works row's main event, with the numeral in the plate corner and
   never over the picture.
3. From `food`: five flavour cards in one row from 1000px, icons heading
   each card, so there is no 3 + 2 hole.
4. Everything else is `scale` as merged in #10: 7rem name capped beside the
   bottle, the why section on the panel field, the between-section air, the
   display numerals where they remain. The status heading comes down to the
   ordinary h2 size; the round-2 review found 88px gave the least important
   section the loudest voice.

Image paths in `index.html` are `assets/img/…`. All hard constraints in the
packet brief apply; the round-2 section's decisions (no CTA, cream ground,
light only) still stand.
