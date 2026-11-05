# phonecam

Turn an Android phone into a Linux webcam using [scrcpy](https://github.com/Genymobile/scrcpy)'s
camera-streaming mode and [v4l2loopback](https://github.com/umlaeute/v4l2loopback).

The phone's camera is streamed into a virtual `/dev/video*` device that any app
(browser, video call client, OBS, etc.) can pick up like a regular webcam.

## Features

- Connects over USB if the phone is plugged in.
- Otherwise reconnects to a remembered wireless-debugging device, or pairs a
  new one — auto-discovering it over mDNS where possible.
- Remembers up to 10 wireless devices and the last camera id used on each,
  pinned to the device's `ro.serialno` so a reused/spoofed address on the
  same network isn't silently trusted as a different, previously-paired
  phone.
- Remembers a rotation per camera id, so front/back cameras come out right
  side up without having to pass `--rotate` every time.
- Headless by default (no scrcpy preview window); `--window` shows one.

## Requirements

- `scrcpy` (recent enough to support `--video-source=camera` and `--v4l2-sink`)
- `adb`
- `v4l2loopback-dkms` (or your distro's equivalent kernel module package)
- `sudo` access, to `modprobe v4l2loopback` on first run
- A phone with *Settings > Developer options > Wireless debugging* available,
  if you want to use it without a cable

## Install

```sh
install -Dm755 phonecam ~/.local/bin/phonecam   # or anywhere on your PATH
```

## Usage

```
phonecam [--camera-id=N] [--rotate=N] [--window] [--new]
         [--list-devices] [--reset] [--list-cameras] [-h]
```

| Flag | Effect |
|---|---|
| `--camera-id=N` | Use this camera id instead of the saved/prompted one. |
| `--rotate=N` | Clockwise capture rotation: `0`, `90`, `180` or `270` (default: `270`). Also saves it as the default for that camera id. |
| `--window` | Show the scrcpy preview window (default: headless). |
| `--new` | Skip remembered devices and pair/connect fresh. The result is remembered afterwards. |
| `--list-devices` | Show remembered wireless devices and exit. |
| `--reset` | Forget all remembered devices and per-camera rotations. |
| `--list-cameras` | Just list the phone's cameras (device must be connected) and exit. |
| `-h`, `--help` | Show usage. |

First run (no device known yet):

```sh
phonecam
```

It will look for a USB connection, then try mDNS auto-discovery of wireless
debugging, and finally walk you through pairing — enter the pairing code
shown under *Wireless debugging* on the phone when prompted.

Environment variables `PHONECAM_VIDEO_NR` (default `10`), `PHONECAM_SIZE`
(default `1280x720`) and `PHONECAM_FPS` (default `30`) can override the
virtual device number, capture resolution and frame rate.

## State

Remembered devices and camera rotations are stored under
`~/.config/phonecam/` (`devices`, `camera_rotations`). Use `--reset` to clear
them.

## License

MIT — see [LICENSE](LICENSE).
