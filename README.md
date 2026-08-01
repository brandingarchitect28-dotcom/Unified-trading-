# Younifiedd Trading — Cinematic Scroll Pass

Hero section (video, layout, JS) is byte-for-byte identical to the last
delivery — verified by diffing the HTML and checksumming the video file
before packaging.

## What changed everywhere else
The old system faded elements in once and left them static. This pass
replaces that with continuous, bidirectional, scroll-position-driven motion:

- **Scroll-scrub entrances**: every card, heading, image and stat now
  animates continuously with scroll position (opacity + translateY +
  rotateX + scale), not just once on first view — scroll up and they
  animate back out, scroll down and they animate back in, in real time,
  tied directly to scroll position rather than a fixed-duration reveal.
- **3D depth**: every card grid (systems, modules, dashboard, stories,
  community, timeline, framework) now sits in a real 3D perspective
  container, so the rotateX in the scrub system reads as actual depth,
  not just a fade.
- **Parallax layers**: large faint numerals (02–11) drift in the
  background of each section at their own scroll speed; the one-on-one
  and final-CTA background photos now have a slow continuous parallax
  drift inside their frame instead of sitting static.
- Fully responsive tuning: transform distances/angles are smaller on
  mobile (via CSS custom properties) so it reads as depth, not motion
  sickness, on a small screen.
- Respects `prefers-reduced-motion: reduce` — everything just shows at
  full opacity with no transform for anyone with that setting on.
- Safety net unchanged from before: every animated element defaults to
  fully visible in CSS. The motion system only *adds* movement — it can
  never leave something stuck hidden if JS is slow, blocked, or errors.
- Verified with a headless-browser pass: zero JS console errors and
  **zero horizontal overflow** at 5 viewport sizes (390×844, 844×390,
  768×1024, 1024×768, 1600×1000) scrolled through their full height in
  12 steps each — both portrait and landscape audited, not just desktop.

## Deploy to Netlify
Drag this folder (or the unzipped contents) onto https://app.netlify.com/drop,
or connect it via "Add new site" > "Deploy manually". `netlify.toml` is
auto-detected; no build command needed. Hero video + CTA still-frame are
embedded as base64 inside `index.html` — nothing external to break.

## Files
- `index.html` — the full site, self-contained
- `netlify.toml` — publish + header config
