# Vinaigresque — landing page design brief (round 1)

Context: vinaigresque.com is one static `index.html` served by nginx from this
checkout. No build step, no backend, no forms that post anywhere. The current
page is a holding page (see `/index.html`): name, tagline, an animated cruet,
"Under development".

Goal of round 1: **basic landing pages**, several distinct directions, so one
can be picked and developed in later rounds. Each direction is one
self-contained HTML file in `design/round-1/`.

## What is known about the product (use only this)

- Name: **Vinaigresque**. Domain: vinaigresque.com.
- It is a **mustard-free vinaigrette mix**. Mustard is the usual emulsifier in
  vinaigrette; this product does without it. That is the whole pitch so far.
- The holding page encodes a **3 : 1 oil-to-vinegar** ratio (three parts oil,
  one part vinegar) and shows oregano, parsley, rosemary, chilli, black pepper
  and garlic suspended in the bottle. Treat the ratio as the product's
  instruction and the herbs as *illustrative*, not a confirmed ingredient list.
- Existing palette tokens (from `/index.html`): cream `#f6f1e4`, ink
  `#2e2a20`, muted `#6f6452`, oil `#c8a227`, vinegar `#6b3b3b`, herb
  `#6b7f4e`, rule `#d9cfb8`, with a dark-scheme set. A direction may keep,
  adapt or replace these — say which in your notes.

## What is NOT known — do not invent it

No price, no pack size, no ingredient list, no allergen or health claims, no
shipping, no stockists, no testimonials, no founder story, no launch date.
**Not the product's physical form either**: a mix the buyer adds to their own
oil and vinegar, or a bottled dressing at 3 : 1. The holding page's bottle
suggests the latter; the 3 : 1 instruction reads as the former. Nor what holds
it together: only that mustard, the usual emulsifier, is absent. Do not assert
an emulsifier-free dressing, or a shake that follows from one.
Where a landing page structurally needs one of these, write **bracketed
placeholder copy** — e.g. `[price]`, `[ingredient list]`, `[quote from a
customer]` — so a reader can see at a glance what is real and what is a slot.
Never write plausible-sounding fake specifics.

## Hard constraints (every direction)

1. One file, `design/round-1/<slug>.html`, self-contained. Inline CSS.
   JavaScript optional and progressive: the page must be complete with JS off.
   No frameworks, no external scripts. Fonts: system stacks preferred; a
   Google Fonts `<link>` is allowed only if the typeface *is* the direction.
2. Works at 360px wide (16px side gutters, no horizontal scroll) through
   1440px. Test both.
3. Light and dark: `prefers-color-scheme: dark` handled, body has an explicit
   background, colours as custom properties on `:root`.
4. Accessibility: body text ≥ 4.5:1 contrast in both schemes, large text
   ≥ 3:1; visible focus styles; `prefers-reduced-motion` honoured; semantic
   landmarks; one `h1`; images/SVG have alt text or `aria-hidden`.
5. Sections a basic landing page needs, in whatever order the direction
   argues for: a hero (name + one line + one call to action), what it is and
   why mustard-free matters, how to use it (the 3 : 1 ratio), and a closing
   call to action. Keep it to those; no fake extra sections.
6. The call to action: this is a static site with no backend. Use either a
   "notify me" email form with `action="#"` and a visible `[form target]`
   placeholder note, or a `mailto:` link, or a `[buy link]` placeholder
   button. Do not wire it to any real third-party service.
7. `<meta name="robots" content="noindex">` for now, as the holding page has.
8. Under ~60KB. Keep the existing `<link rel="icon" …>` data-URI favicon or
   supply your own inline one.
9. Do not touch `/index.html` or any file outside `design/round-1/`.

## Process

- Write the page, then open it in Chromium via Playwright (pre-installed at
  `/opt/pw-browsers/chromium`; do NOT run `playwright install`) and take
  screenshots at 360×800 and 1440×900, light and dark, into
  `design/round-1/shots/<slug>-{mobile,desktop}-{light,dark}.png`. Look at
  them. Fix what is wrong. Repeat until the page matches your intent.
- Check contrast ratios of your actual text/background pairs (compute them;
  don't estimate).
- Your report back: the slug, the direction in two sentences, what palette
  and type you used and why, which copy is placeholder, and anything you
  could not resolve. No file dumps.
