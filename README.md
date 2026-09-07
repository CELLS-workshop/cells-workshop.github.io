# CELLS — Workshop on Computing among Cells

Static website for the CELLS workshop series. Plain HTML and one stylesheet:
no build step, no framework, no JavaScript, no external requests. Open
`index.html` in a browser, or serve the folder with any static file server.

```
index.html            Series index: what CELLS is, the next edition, past editions
2026/index.html       CELLS'26
assets/css/site.css   The whole stylesheet. Colours are the tokens in :root.
assets/img/cells.svg  Workshop mark, recoloured and gently animated
assets/img/cells-original.svg   The mark as published on the original site
```

## When a new edition is announced

1. `cp -r 2026 2027` and edit `2027/index.html` — everything still to fill in is
   marked with a `TODO` comment.
2. In `index.html`, point "Next edition" at the new year and move the finished
   edition into the "Past editions" list, newest first.
3. Asset links in an edition page are all `../assets/...`; fix them if you nest deeper.

Editions before 2026 are hosted on the original site and linked from the list. To
bring one in-house, drop it in as `2019/` and change that one link.

## Editing an edition page

- **Speaker photo** — put the file in `assets/img/` and replace that speaker's
  `<div class="speaker__placeholder">` with the `<img class="speaker__photo">` line commented
  out just above it. It floats right of the bio, as on the earlier pages. Square images crop best.
- **Sponsor logo** — add an `<img>` before the sponsor name.
- **Programme** — a plain list; the speaker entries link to the `#speaker-N` anchors.

## Notes

- White ground and black text. The link blue is the mark's `#1e86fe`, muted and
  darkened to `#31608f` so it reads as text rather than as a highlight. The mark's
  green survives only as the short rule under the masthead tagline (`--green`).
- The mark in `cells.svg` has had its blue changed from `#1e86fe` to the same `#31608f`,
  so the logo and the links agree. Its greens, pinks and black wordmark are untouched.
  `cells-original.svg` is the unmodified file if you ever want it back.
- The mark also drifts: the seven bacteria, three green cells, four dots and four
  strands each shift a couple of pixels on a slow, out-of-phase loop. It is a
  `<style>` block inside `cells.svg` — delete it and the logo goes still. Nothing
  else in the file was touched: each animated shape is wrapped in a plain group, so
  its own Inkscape transform is left alone.
- Each shape in the mark also rocks a degree or two on an irregular loop, so the
  direction changes are unpredictable. Rotating about a shape's own centre needs no
  `transform-origin`: each shape is wrapped in `translate(centre)` / `.spin` /
  `translate(-centre)`, which puts the rotating group's origin on the shape's centre.
  The centres were computed from the geometry, not guessed.
- That block sticks to `translate` for the drift and declares the animation unconditionally. Two
  things to avoid inside an SVG that a page loads with `<img>`: gating the animation
  behind `prefers-reduced-motion: no-preference` (user-preference queries are not
  reliably evaluated in that context, so nothing animates), and `transform-box:
  fill-box` on a group, which is not honoured everywhere and makes rotation swing
  shapes around the logo's centre. Reduced motion is handled by an opt-out
  `prefers-reduced-motion: reduce` rule instead.
- The masthead sits on a pale tint with the mark's own cells and strands drifting
  behind it — an inline `<svg class="banner-motif">` at the top of each masthead,
  animated by the `.m` rules in `assets/css/site.css`. Delete the `<svg>` to remove it.
  Each shape is drawn around its own origin inside a positioning `<g>`, so the CSS
  transform rotates it in place; that is why no `transform-origin` or `transform-box`
  is needed anywhere. The motif is inline rather than a background image so the
  animation is driven by the page's own stylesheet. One rod divides on a loop: it is
  drawn twice, and the `<g class="daughter">` copy pulls out of the parent, drifts off
  the right-hand edge and fades, then slides back inside the parent while invisible so
  it can divide again — the pair shrinking as the cell divides and growing back once
  they have parted (`mother` plus the scale in the daughter's keyframes). Two rods do
  this, half a cycle apart so the divisions alternate:
  one daughter leaves through the right-hand edge (`divideRight`), the other through the
  bottom (`divideDown`). Each daughter is drawn before its parent so it emerges from
  behind it. The paths are not hand-drawn: a run-and-tumble simulation (velocity with
  inertia, occasional tumbles) was run offline and sampled into keyframes, each
  keyframe's rotation set to the heading of travel, so a cell always points where it is
  going. Rods drift along their long axis (`swim1`–`swim3`) rather than sideways. One
- The footer repeats the same motif, in blue only and with no animation at all — a
  separate inline `<svg class="footer-motif">` whose shapes carry no classes, so nothing
  can animate them. The green blobs reuse the actual
  outlines from the mark. Sections are separated by
  a hairline carrying a small cell glyph (`.section::before`).
- The pages print cleanly: navigation is dropped and link targets are expanded.
- Keep the heading order (`h1` → `h2` → `h3`) intact when editing.
