---
name: design-preview-loop
description: Use when iterating on a local HTML/SVG mockup (logo concepts, OG images, layout experiments) that needs to be previewed and screenshotted with Playwright before publishing as an Artifact or committing to the site — serving scratch files locally, capturing full-page/viewport/cropped screenshots, testing light/dark and multiple sizes, and keeping scratch output out of the repo.
---

# Design Preview Loop

The generic mechanics behind every visual-design iteration round on this
project: write a scratch HTML/SVG file, serve it, screenshot it with
Playwright, `Read` the screenshot to actually look at it, adjust, repeat.
[[identity-proposal]] is the content-specific convention set built on top of
this loop for logo work specifically; this skill is the reusable plumbing
underneath it.

## The loop

1. Write the scratch mockup to the session scratchpad directory (not the
   repo), e.g. `logo-sketch3.html`.
2. Serve that directory locally — Playwright's `browser_navigate` **blocks
   `file://` URLs outright** ("Access to file: protocol is blocked"), so a
   local HTTP server is required even for a throwaway single-page mockup:
   ```bash
   cd /path/to/scratchpad && (python3 -m http.server 8734 >/tmp/httpserver.log 2>&1 &) \
     && sleep 1 && curl -s -o /dev/null -w "%{http_code}\n" http://localhost:8734/
   ```
   (This exact gotcha also appears in the `hero-images` skill for OG-image
   generation — same root cause, same fix, two different asset types.)
3. `browser_navigate` to `http://localhost:PORT/file.html`, then
   `browser_take_screenshot`. Use `fullPage: true` for a first look at the
   whole page, then a plain viewport screenshot (or a `zoom` region) once
   you need to inspect one area closely.
4. `Read` the screenshot file — never assume a change worked from the code
   alone. Every real bug caught in this project's logo work (color not
   applying, wrong symbol reused in the wrong panel, text cut off by a
   sticky header) was only visible in a screenshot, not in the markup.
5. Iterate: edit the scratch file, re-navigate (a fresh `browser_navigate`
   reloads it), re-screenshot.
6. Clean up scratch screenshots before ending the round (see below) and
   `pkill -f "http.server PORT"` once you're done previewing.

## Screenshots land in the repo root, not the scratchpad — clean up every round

Playwright's `browser_take_screenshot` `filename` param is resolved against
its own configured output directory, which in this environment is the shell
cwd — normally the project repo root, **not** wherever the source HTML file
lives. Passing a bare name like `sketch1.png` puts the file at
`/path/to/repo/sketch1.png`, sitting there as an untracked file in `git
status` until removed. It is not covered by a typical `.playwright-mcp/`
gitignore entry (that directory only holds the tool's own auto-generated
navigation snapshots, not explicit `filename` screenshots).

Treat "remove the scratch screenshots" as a mandatory last step of every
preview round, not an occasional tidy-up:

```bash
rm -f /path/to/repo/sketch*.png /path/to/repo/proposal-*.png
git status --porcelain   # confirm no stray .png files remain before moving on
```

## Cropping a close-up without re-navigating

To inspect one region of an already-captured full-page screenshot (e.g. a
tiny 14px mark inside a browser-tab mockup) without a fresh Playwright round,
crop the existing PNG directly:

```bash
sips --cropToHeightWidth <height> <width> --cropOffset <y> <x> input.png --out crop.png
```

Faster than adjusting the viewport and re-screenshotting when you already
have the full-page capture and just need to look closer at one part of it.

## Testing dark mode without an OS-level toggle

The artifact/site CSS pattern here keys dark mode off `prefers-color-scheme`
*and* an explicit `data-theme` attribute override. Force the dark branch
directly via `browser_evaluate` instead of fighting with OS/browser dark-mode
settings:

```js
() => { document.documentElement.setAttribute('data-theme', 'dark'); }
```

Screenshot again after setting it — same page, same server, no reload
needed.

## Testing responsive/small-size behavior

`browser_resize` before screenshotting to check mobile layout (e.g.
`390×844`) and to test how a mark or design element holds up at a specific
target pixel size (a favicon test grid rendered at literal 16/24/32/48px
`<svg>` widths, for instance) — resize the viewport, don't rely on CSS zoom
or browser devtools emulation, since those don't reliably match what
`browser_take_screenshot` actually captures.

## Common Mistakes

| Mistake | Fix |
|---|---|
| Navigating Playwright to a local file with `file://` | Serve the directory with `python3 -m http.server` and use `http://localhost:PORT/...` |
| Trusting the markup/CSS without looking | `Read` the actual screenshot — visual bugs (color, layout, wrong element reused) don't show up in source review |
| Leaving scratch `.png` files in the repo root after a preview round | `rm` them and confirm with `git status --porcelain` as the last step of every round |
| Re-navigating just to zoom into one detail of an existing screenshot | Crop the already-captured PNG with `sips --cropToHeightWidth ... --cropOffset ...` |
| Fighting OS/browser settings to preview dark mode | `browser_evaluate` to set `data-theme="dark"` directly on the page |
| Judging responsive/small-size behavior via CSS zoom or devtools emulation | `browser_resize` to the real target viewport/pixel size before screenshotting |
