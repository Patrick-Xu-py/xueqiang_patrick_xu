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

## Adding a photo

Drop the full-size file into `images/photos/`, then regenerate the thumbnails:

```
module load python/anaconda3/2.12.0   # only needed on a machine without PIL
python3 -c "
from PIL import Image; import os
s, d = 'images/photos', 'images/photos/thumbs'
for f in os.listdir(s):
    p = os.path.join(s, f)
    if os.path.isfile(p) and f.lower().endswith(('.jpeg','.jpg','.png')):
        im = Image.open(p).convert('RGB')
        im.resize((round(im.width*340/im.height), 340), Image.LANCZOS).save(
            os.path.join(d, f), 'JPEG', quality=82, optimize=True, progressive=True)
"
```

Keep the originals under a 2000px long edge (quality 85) — the lightbox never
shows more than a screenful, and a straight-off-the-camera 9 MB file will not
load on a slow connection. The strip shows the 340px-tall thumbnail (`src`) and
links to that original (`href`): nine originals are 3.4 MB, the thumbnails are
217 KB. Then add one
`<a><img></a>` line to the `.photo-track` in the Photos section —
**twice**, once in each half of the list. The strip loops by sliding exactly one copy of itself, so the two halves
have to stay identical or the seam will jump. The second copy carries
`aria-hidden="true" tabindex="-1"` so screen readers and the tab key see each
photo once.

Any aspect ratio works: the strip fixes the height and lets the width follow, so
portrait, square, and landscape shots sit together without cropping.
