# watermark

Tile a repeated diagonal text watermark over an image (JPG, PNG or WebP).

Requires Python 3 and [Pillow](https://python-pillow.org/).

```sh
watermark INPUT OUTPUT TEXT [--opacity 0-255] [--angle DEG] [--size PX]
                            [--spacing PX] [--color R,G,B] [--font FILE]
```

Defaults: opacity `75`, angle `35`, size `38`, spacing `100`, color `80,80,80`.

```sh
watermark id.jpg id-marked.jpg "FOR VERIFICATION ONLY"
```
