---
name: identity-proposal
description: Use when designing, proposing, or revising a logo/brand mark for Craig Earley Software, LLC — building an Artifact "spec sheet" that presents SVG mark concepts with revision history, light/dark previews, in-context mockups, favicon-legibility testing, and a recommendation section. Covers the reusable page structure, the shared SVG symbol/gradient library technique, and the currentColor/custom-property gotcha with `<use>`.
---

# Identity Proposal

Recipe for building and iterating on the brand-identity Artifact used to pitch
logo concepts for this site (navy `#3b4a8f`, accent `#79bcff`, Inter). Built
across five real revisions (A–E) exploring blueprint/bracket marks, CE
monograms, and abstract gradient-shaded forms — every convention below earned
its place by catching a real problem in that process, not a hypothetical one.

## Pull the real brand tokens from the live site first

Don't guess colors from theme SCSS files or old screenshots — read them off
the live site's computed styles, which is the actual source of truth:

```js
() => {
  const root = getComputedStyle(document.documentElement);
  const vars = {};
  for (const prop of root) if (prop.startsWith('--')) vars[prop] = root.getPropertyValue(prop);
  return vars;
}
```

Run via Playwright's `browser_evaluate` against `https://craigearley.software`.
This is how `--color-primary: #3b4a8f` and `--color-primary-text-offset:
#79bcff` were confirmed as the real brand blue/accent, not assumed.

## Page structure: a blueprint "spec sheet," not a mood board

Structure the Artifact like an engineering drawing sheet — it fits the site's
own blueprint/steel-structure visual language and gives every revision a
consistent frame:

- **Title block**: eyebrow ("Identity Proposal"), `<h1>` company name, and a
  meta row with `Sheet`, `Rev` (e.g. "C — abstract / dimensional"), `Date`,
  `Drawn`. Bump the `Rev` letter every time the doc is substantially
  restructured, not on every tiny tweak.
- **Intro paragraph**: one paragraph stating what changed this revision and
  why, in plain language — this is what the user reads first on every
  republish, so it has to stand alone without them re-reading prior rounds.
- **Numbered sections** (`01`, `02`, ...) via a `.section-label` row (number +
  uppercase label + a flex-grow divider line), not `<h2>` alone — keeps the
  drafting-sheet feel and makes the doc scannable when it gets long.
- **Concept panel** per mark: name, one-line rationale, a `.plate` showing the
  mark large, a `.specs` grid (construction / core / palette / min-size), an
  in-context row (browser-tab mockup + site-header mockup), and a note
  (amber `.note` for a caveat, green `.note.good` for a validated result).
- **Recommendation section**: state an actual position, not just a
  side-by-side. If the honest answer is "here's the real tradeoff, you
  decide" (see Rev C's "The Real Fork"), say that explicitly instead of
  forcing a false consensus.

## Carry-forward / retired pattern across revisions

Every mark from a prior revision gets one compact card in this revision —
never silently drop it and never re-run its full concept panel again (that's
already in the Artifact's version history). Two states:

- **Carried forward** (`.carried-card`): still valid, one line saying why
  it's still on the table (e.g. "No letters — no collision risk").
- **Retired** (`.retired-card`): grayscale + `opacity: .45` icon,
  strikethrough name, and a stated reason — not just removed from the page.
  Rev E retired three CE-lettered marks in one round after the CE
  regulatory-marking collision was raised; each card says *why*, so the
  document is still legible as a decision record months later.

```css
.retired-card .mark { filter: grayscale(1); opacity: .45; }
.retired-card .rc-name { text-decoration: line-through; text-decoration-color: var(--bad); }
```

## Build marks as a shared `<symbol>` library, not inline duplicates

Every mark gets defined once in a hidden `<svg style="position:absolute">` at
the top of the document, then referenced everywhere (plate, favicon test,
browser-tab mockup, nav mockup, wordmark lockup) via `<use href="#mark-id"/>`.
Without this, five marks × six contexts each is 30 copies of near-identical
path data to keep in sync.

```html
<svg width="0" height="0" style="position:absolute">
  <symbol id="mark-focus" viewBox="0 0 100 100">
    <path d="..." fill="none" stroke="currentColor" stroke-width="7"/>
    <circle cx="50" cy="50" r="5.5" fill="var(--accent)"/>
  </symbol>
</svg>
<svg class="mark mark--navy"><use href="#mark-focus"/></svg>
```

Recolor per context with `color` (drives `currentColor` on strokes) and a
locally-overridden `--accent` custom property, not separate symbol variants:

```css
.mark--navy { color: var(--navy); }
.mark--onNavy { color: #fff; --accent: #8fc3ff; }
```

## The `<use>` + CSS class gotcha (this bit us once — Rev C)

**A class selector defined on the page never reaches into a `<symbol>`
cloned by `<use>`.** `.node { fill: var(--accent); }` targeting a class on
the symbol's `<circle>` silently does nothing — the accent dots rendered
solid black instead of accent-blue, and it looked fine in the code, so it
only showed up on screenshot review. Only **inherited custom properties**
cross the `<use>` shadow boundary; direct selector matching does not.

Fix: put the color directly on the symbol as a presentation attribute
referencing the custom property, and override the property (not a class) per
context:

```html
<!-- WRONG: .node CSS rule never applies inside <use> -->
<circle class="node" cx="50" cy="50" r="5.5"/>
<style>.node { fill: var(--accent); }</style>

<!-- RIGHT: presentation attribute + inherited custom property -->
<circle cx="50" cy="50" r="5.5" fill="var(--accent)"/>
```

If this bites again, it'll look exactly the same way: a color that's clearly
set in a stylesheet rule but silently doesn't apply only on `<use>`-cloned
content.

## Test every mark at favicon scale before calling it a finalist

Every mark that made it to "finalist" status was checked at 16/24/32/48px in
a dedicated throwaway test page — this is what caught real, non-obvious
problems that were invisible at normal preview size:

- Truss Mark (Rev A) loses its corner nodes below 16px and reads as a
  generic △.
- Chip Monogram / Chip Facet Mark (Rev B/D) crowd their detail below 24–32px.
- Focus Monogram and Beacon Mark held up fine down to 16–24px.

Build the size test as its own scratch HTML page (see
[[design-preview-loop]]) with the mark rendered at each target size on both
a light and a dark plate — some techniques (gradient/glow especially) read
differently depending on the ground color.

## Mock the mark in its real contexts, not floating alone

A mark on a blank plate is not how anyone will see it. Every finalist gets
two in-context mockups matching the real site chrome:

- **Browser tab**: a small rounded rect styled like a tab, `14×14`–`18×18`px
  mark + truncated title text.
- **Site header**: reproduces the real nav bar — white background, mark +
  "Craig Earley Software, LLC" in `var(--navy)`, "ABOUT" link — because the
  real site header is white regardless of page theme, so a dark-hero-styled
  mockup here would misrepresent how it actually looks.

## Check letter-based marks against real-world collisions before finalizing

Before finalizing any monogram, check whether the letters collide with an
existing trademark, regulatory mark, or well-known symbol. "CE" specifically
collides with the mandatory Conformité Européenne marking required on
electronics sold in the EU/EEA — a real risk for a software/electronics-
adjacent brand, not just an aesthetic nitpick, and it retired three otherwise
solid concepts (Focus Monogram, Chip Monogram, Chip Facet Mark) in Rev E.

## Republish to the same Artifact URL across revisions

Pass the same `url` param to the `Artifact` tool on every revision instead of
letting it mint a new link — the user gets one bookmark that always shows the
latest round, and prior revisions stay reachable through the Artifact's own
version picker (no need to duplicate old content into the new page). Full
`Write` of the file per revision (not incremental `Edit`) was easier to
reason about than diffing when whole sections get restructured, retired, or
promoted between rounds.

## Common Mistakes

| Mistake | Fix |
|---|---|
| Guessing brand colors from theme source or memory | Pull `--color-*` custom properties off the live site via `browser_evaluate` |
| Styling `<use>`-referenced symbol content with a class selector | Set the color as a presentation attribute (`fill="var(--accent)"`) and override the custom property per context instead |
| Judging a mark's legibility only at large preview size | Render it at 16/24/32/48px on both light and dark plates before calling it a finalist |
| Showing a mark floating alone as the only "proof" | Mock it in a browser-tab chrome and the site's real (white) nav bar |
| Silently dropping a superseded mark from the next revision | Give it a `.retired-card` with a stated reason, or a `.carried-card` if it's still valid |
| Forcing a single winner when the honest answer is a real tradeoff | State the tradeoff explicitly (e.g. "The Real Fork") instead of a false recommendation |
| Finalizing a lettered mark without a collision check | Check the letter combination against known trademarks/regulatory marks (e.g. CE marking) first |
| Minting a new Artifact URL each revision | Pass the same `url` to `Artifact` so one link always shows the latest round |
