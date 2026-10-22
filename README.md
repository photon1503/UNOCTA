# UNOCTA site

The marketing page for UNOCTA, the Unattended Night Observatory Controller
and Train Automation, served by GitHub Pages from this repository.

- `index.html`, `styles.css`: the page, hand-written, no build step.
- `assets/shots/`: screenshots of the console, WebP, taken on a live
  observatory on 22 October 2026 (the two-train topology is the demo profile).
- `assets/video/`: the target framing recording, MP4 and WebM, with a poster.
- `assets/fonts/`: Space Grotesk, Inter and IBM Plex Mono (SIL Open Font
  License, see the `OFL*.txt` files), the same files the console bundles.
- Icons are Lucide (ISC), inlined as an SVG sprite in `index.html`.

## Publishing

Settings → Pages → Build and deployment → Source: *Deploy from a branch*,
branch `main`, folder `/ (root)`. The `.nojekyll` file keeps GitHub from
running Jekyll over the files.

## Updating screenshots

Capture the console at 1920 × 1080, convert to WebP at 1600 px wide, and
replace the file in `assets/shots/` under the same name; the `width` and
`height` attributes in `index.html` keep the layout stable while images load.
