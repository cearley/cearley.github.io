---
name: hero-images
description: Use when sourcing, treating, or troubleshooting a stock photo or gradient background for a Hugo hero section, Open Graph share image, or favicon on this site — text-over-photo legibility, ImageMagick gradient direction bugs, generating text-overlay OG images or monogram favicons, this theme's front matter image params, or hugo server crashing after an asset change.
---

# Hero Images

## Overview

Recipe for turning a licensed stock photo (or a generated gradient) into a
hero/OG background with legible overlaid text, wired into this site's Hugo
front matter. Every gotcha below caused a real wrong-looking result in
production iteration — not hypothetical.

## Sourcing a licensed photo

WebFetch the Unsplash photo page (or a search-results page) with a prompt
asking for the direct `images.unsplash.com` CDN URL and the license terms —
one call gets both. Unsplash License = free for commercial use, no
attribution required. Always confirm the license explicitly before using an
image commercially, even from a normally-safe source.

## Crop to the target aspect ratio first

```bash
magick source.jpg -gravity center -crop <W>x<H>+0+0 +repage cropped.jpg
```

Match `<W>x<H>` to the real rendered aspect of the target container. The
theme's CSS uses `background-size: cover; background-position: top center`,
which crops centered — pre-cropping gives you control over composition
instead of leaving it to chance.

## ImageMagick `gradient:` defaults to top-to-bottom

`magick -size WxH gradient:'c1'-'c2'` is **vertical** regardless of which of
W/H is larger. Compositing that for a "left-to-right" fade produces a
diagonal/vertically-varying result that looks like a bug (it is one — yours).

True horizontal gradient: generate sideways, then rotate:

```bash
magick -size <H>x<W> gradient:'#0b0f3d'-'rgba(11,15,61,0)' \
  -rotate 90 -flop -resize <W>x<H>! horiz-gradient.png
```

`-flop` mirrors it — needed to put the opaque color on the left instead of
the right. Preview the mask alone (`Read` it) before compositing onto the
real photo; don't assume the direction, check it.

## Bake the text-legibility scrim into the image, not CSS

Don't lean on the theme's `background-blend-mode: overlay` to keep text
readable over a busy photo — real code/UI screenshots have too much fine
detail and fight with overlaid text at any blend setting. Instead:

1. Measure where the text actually renders (don't guess) — screenshot it first.
2. Solid color block sized to fully cover that zone, generous margin.
3. Long, gradual gradient tail past the text zone before reaching full photo clarity — "gradual" means the gradient itself is long, not that it starts early. A gradient that starts inside the text zone reintroduces the legibility bug even if the slope is gentle.
4. Composite: `magick photo.jpg mask.png -compose over -composite final.jpg`

## Tinting a grayscale/B&W photo to match the brand panel

A flat `-tint` wash looks muddy. Use a proper duotone instead: convert to
grayscale, then remap through a 2-color gradient as a lookup table so shadows
and highlights map to distinct brand colors while contrast is preserved:

```bash
magick photo.jpg -colorspace Gray \
  \( -size 1x256 gradient:'#0b0f3d'-'#e2e9fb' \) -clut duotone.jpg
```

Order matters: `gradient:'c1'-'c2'` puts `c1` at index 0 (maps to black/shadows)
and `c2` at index 255 (maps to white/highlights). Swapped order inverts the
photo's tonal range (shadows go light, highlights go dark) — looks like a
photo negative, not a tint. Use the exact same shadow color as the scrim
panel so the two blend seamlessly at the seam.

## Convert to webp

```bash
cwebp -q 82 source.jpg -o output.webp
```

Matches this site's asset convention; typically 5-10x smaller than PNG for photos.

## Check the layout before setting `image:` in front matter

This theme's `image:` front matter field is not purely SEO — on some layouts
(e.g. `_default/single.html`, used by `pages/about.md`) it also renders as a
**visible on-page banner**. Grep the theme layout for the page's section
before setting it:

```bash
grep -rn "Params.image" path/to/theme/layouts/
```

To change only the social-share image without touching a page's visible
photo, use the nested override — `seo/meta.html` checks this before falling
back to `.Params.image`:

```yaml
meta:
  og_image: "images/social/my-share-image.png"
```

## Generating an OG image with text overlay

Not every OG image is just a treated photo — for a text-forward share card
(company name, tagline, domain), render it as HTML and screenshot it rather
than compositing text with ImageMagick:

1. Crop/prepare the background photo first (same aspect-ratio rules as
   above — e.g. 1200x630 for OG), base64-encode it, and embed it as a
   `background-image: url('data:image/png;base64,...')` in a plain HTML
   file sized exactly to the target pixels (`width: 1200px; height: 630px`
   on `html, body`).
2. `@import` the site's actual Google Fonts URL (from `config.toml`
   `params.fonts.google_fonts`) so the rendered text uses the real
   typeface, not a system-font fallback.
3. Serve the file over HTTP, not `file://` — see the Playwright gotcha
   below — then navigate Playwright to it, resize the browser to the exact
   target dimensions, and screenshot.
4. Iterate on font-size/line-wrap the same way as hero-copy tuning: measure
   with `browser_evaluate` (does the headline wrap where you want it?)
   before treating a size as final.
5. Copy the resulting screenshot straight into the static asset path — it's
   already the exact target dimensions, no further resizing needed.

**Playwright MCP blocks `file://` URLs.** Trying to `browser_navigate` to a
local HTML file fails outright ("Access to file: protocol is blocked").
Serve the directory instead and navigate to `http://localhost:PORT/...`:

```bash
cd /path/to/scratch/dir && python3 -m http.server 8765 > /tmp/http-server.log 2>&1 & disown
```

## Generating a simple text-on-solid-color asset (e.g. favicon)

For a monogram/icon that's just bold text on a flat brand color, ImageMagick
alone is faster than the HTML+Playwright route — but named font aliases
like `-font "Helvetica-Bold"` fail with `unable to read font`. Pass the
actual font file path instead:

```bash
magick -size 256x256 xc:"#3b4a8f" \
  -gravity center -fill white -font "/System/Library/Fonts/Supplemental/Arial Bold.ttf" \
  -pointsize 105 -annotate +0+4 "CE" \
  favicon-master.png
```

Render once at high resolution (e.g. 256x256) and downsize from that master
for each target size (16x16, 32x32, 48x48 for `.ico`) rather than
re-rendering text at each size — keeps the weight/proportions consistent
and avoids hinting artifacts at the smallest sizes looking different from
the larger ones.

## Verify with a real screenshot, not a file preview

A standalone `Read` of the image file does not reflect `background-size:
cover` cropping/scaling in the actual container. Run `hugo server
--disableFastRender` in the background, navigate with Playwright at the real
target viewport width, screenshot, and `Read` that. Append `?v=N` to the URL
each iteration to defeat image caching.

## hugo server crashes after a content/static change

Symptom: `panic: Shift: unknown type *hugolib.pageMetaSource for
"/some/unrelated/path"` in the server log — unrelated to what you actually
edited — then the process dies and `curl` starts returning connection
errors. This is a live-reload/watch-mode Hugo bug, not a problem with your
edit. Just restart:

```bash
pkill -f "hugo server"
hugo server --disableFastRender > /tmp/hugo-server.log 2>&1 & disown
```

## Keep reference copies of accepted iterations

Before iterating further on a design you like, copy the current asset to a
descriptively-named sibling file (e.g. `hero-photo-solid-panel.webp`) in the
same directory. Cheap insurance for "go back to the previous one" without
git archaeology mid-session.

## Common Mistakes

| Mistake | Fix |
|---|---|
| Assuming `gradient:` is horizontal | Generate sideways + `-rotate 90` (+ `-flop` for direction) |
| Trusting a standalone file preview for legibility | Screenshot the real rendered page at target viewport |
| Setting `image:` in front matter without checking the layout | grep the theme layout for `.Params.image` first |
| Relying on CSS `overlay` blend for text legibility over a photo | Bake a solid+gradient scrim into the image itself |
| Making the fade "more gradual" by starting it earlier | Keep the solid zone fixed to the text bounds; lengthen the tail instead |
| Debugging a `hugo server` panic tied to an unrelated page | Just restart the server |
| Navigating Playwright to a local file with `file://` | Serve it with `python3 -m http.server` and use `http://localhost:PORT/...` |
| Using a named font alias (`-font "Helvetica-Bold"`) in ImageMagick | Pass the actual font file path instead |
