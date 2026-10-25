# UNOCTA site

The marketing page for UNOCTA, the Unattended Night Observatory Controller
and Train Automation, served by GitHub Pages from this repository.

- `index.html`, `styles.css`: the page, hand-written, no build step.
- `assets/shots/`: screenshots of the console, WebP, taken on the demo
  observatory profile (every device a simulator) on 25 October 2026, plus two
  GIF recordings (`steps.gif`, `phone.gif`) and the four device shots the hero
  composes (`device-*.webp`: 1920, 1440, 768 and 390 px).
- `assets/video/`: the target framing recording, MP4 and WebM, with a poster.
- `assets/fonts/`: Space Grotesk, Inter and IBM Plex Mono (SIL Open Font
  License, see the `OFL*.txt` files), the same files the console bundles.
- Icons are Lucide (ISC), inlined as an SVG sprite in `index.html`.

## Publishing

Settings → Pages → Build and deployment → Source: *Deploy from a branch*,
branch `main`, folder `/ (root)`. The `.nojekyll` file keeps GitHub from
running Jekyll over the files.

## Updating screenshots

Start the API on a spare port with a fresh data directory, sign in, load the
demo observatory with its sample targets and runs, switch to Auto and move
the demo clock into the night (`POST /api/v1/clock/demo`), then wait for the
first frames. Capture full pages at 1920 × 1080 with a device scale of 2 (the Camera page
at scale 1: under Playwright's scale emulation the viewer's canvas is drawn
at a fraction of its box) and convert to WebP at 1600 px wide; before the
night starts, set `simulatedSky.catalog.fieldArcmin` to 60 in the applied
profile (`GET /api/v1/profile/document`, `PUT /api/v1/profile`), so the
simulator renders 2048 px frames instead of the 20′ default; the device shots are the Now page at 1920,
Night at 1440, Safety at 768 × 1024 (touch) and Now at 390 × 844 (touch,
mobile). Replace each file in `assets/shots/` under the same name and set the
`width` and `height` attributes in `index.html` to the file's size, so the
layout stays stable while images load.

The GIFs are Playwright video recordings turned into frames (the bundled
ffmpeg writes PNG only) and assembled with Pillow: one palette for the whole
clip, and every pixel that did not move since the last frame stored as
transparent, which keeps a 15 s clip under a megabyte.
