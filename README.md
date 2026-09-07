# CELLS — Workshop on Computing among Cells

Website for the CELLS workshop series. 

```
index.html                    Series index: about, next edition, past editions
2026/index.html               CELLS'26
assets/css/site.css           Whole stylesheet; colours are the tokens in :root
assets/img/cells.svg          Workshop mark
assets/img/cells.png          Still version of the mark, 1216x447, transparent
assets/img/cells-original.svg The mark as published on the original CELLS site
```

## Adding an edition

1. `cp -r 2026 2027` and edit `2027/index.html`. Everything still to fill in is
   marked `TODO`.
2. In `index.html`, point "Next edition" at the new year and move the finished
   edition into "Past editions", newest first.

## Editing an edition page

- **Speaker photo** — put the file in `assets/img/` and replace that speaker's
  `<div class="speaker__placeholder">` with the `<img class="speaker__photo">` line
  commented out above it. Square images crop best.
- **Sponsor logo** — add an `<img>` before the sponsor name.
- **Programme** — a plain list; entries link to the `#speaker-name` anchors.

