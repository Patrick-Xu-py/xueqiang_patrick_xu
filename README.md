# Xueqiang Xu's academic website

Adapted from Jon Barron's public academic website: https://jonbarron.info/.

## Adding a publication

Copy an existing `<tr>` in the Selected Publications table of `index.html` and
fill in the four styled parts: the `<papertitle>` link, `<span class="authors">`,
`<span class="venue">` (short form, e.g. `KDD 2026`, with an optional
`<span class="venue-note">` after it), and `<p class="links">`.

Thumbnails live in `images/<paper>/` as a pair — `<paper>.png` is at rest and
`<paper>-1.png` shows on hover. **Both must be 3:2 on a white ground**, since
they fill the frame edge to edge; a figure of any other aspect will letterbox
against the white. To convert a figure crop, trim its white margin, then pad it
back out to 3:2 with a uniform margin (~4.5% of the width per side).
