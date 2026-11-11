# watermark

Tile a repeated diagonal text watermark over an image (JPG, PNG, WebP) or a PDF.

Requires Python 3 and [Pillow](https://python-pillow.org/). PDF input also needs
[PyMuPDF](https://pymupdf.readthedocs.io/) (Arch: `python-pymupdf`), or
[poppler](https://poppler.freedesktop.org/) (`pdftoppm`) if you only use `--flatten`.

```sh
watermark INPUT OUTPUT TEXT [--opacity 0-255] [--angle DEG] [--size PX]
                            [--spacing PX] [--color R,G,B] [--dpi N] [--overlay | --flatten] [--font FILE]
```

Defaults: opacity `75`, angle `35`, size `38`, spacing `100`, color `80,80,80`.

### PDFs

```sh
watermark contract.pdf contract-marked.pdf "CONFIDENTIAL"
```

By default each page is rendered to an image with the watermark baked into the
pixels, so it can't be removed as a separate layer. The original text is put
back as an invisible text layer (like a searchable scan), so you can still
select, search and copy it. Needs PyMuPDF.

Because pages are rebuilt, links, form fields, bookmarks, annotations and the
original metadata are dropped, and accented Latin text is kept but non-Latin
scripts (Cyrillic, CJK, ...) are not. File size grows.

| Flag | Result |
|---|---|
| *(default)* | Baked in + invisible text layer: unremovable, text selectable |
| `--overlay` | Watermark laid over the original pages: everything else is kept and the file stays small, but it can be removed in a PDF editor |
| `--flatten` | Image-only pages, no text at all; needs `pdftoppm`, not PyMuPDF |

`--dpi` (default 150) sets the render resolution. For PDFs, `--size` and
`--spacing` are in points and scaled to the DPI, so the look matches across
resolutions. An image can also be written to `.pdf`.

### Image example

```sh
watermark id.jpg id-marked.jpg "FOR VERIFICATION ONLY"
```
