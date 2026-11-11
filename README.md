# myScripts

A collection of small command-line tools I make for myself. Each lives in its
own folder with its own README.

| Tool | What it does |
|---|---|
| [phonecam](phonecam) | Android phone as a Linux webcam via scrcpy + v4l2loopback |
| [watermark](watermark) | Tile a diagonal text watermark over an image |
| [gsearch](gsearch) | Search a git repo's working tree and entire history for a string |
| [gscrub](gscrub) | Remove a string from a git repo's entire history |

## Install

Copy or symlink whichever script you want onto your `PATH`:

```sh
install -Dm755 watermark/watermark ~/.local/bin/watermark
```

## License

Beerware — see [LICENSE](LICENSE).
