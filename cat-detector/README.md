# cat-detector

This is a cat detector system for homeassistant based on esp32. It has 2 parts, the detector and the notifier.

A sub-project of [homeassistant](../README.md).

## Parts

- **Detector** — detects the cat using a combination of presence sensor and microphone.
- **Notifier** — alerts a human when the cat is at the door meowing.

## Architecture

Both parts are **Seeed Studio XIAO ESP32 C6** boards that connect to Home
Assistant over **WiFi**. There is no direct board-to-board link — the detector
reports to Home Assistant, which drives the notifier.

```
Detector (XIAO ESP32 C6)              Home Assistant
  mic + presence sensor   ──────────▶  detection
                                            │
                                            ▼
Notifier (XIAO ESP32 C6)
  LED + beeper + silence button
```

## Status

Placeholder. Add the real implementation here.

## Structure

```
cat-detector/
├── README.md
├── .gitignore
├── detector/     # ESP32 firmware
└── notifier/     # alerts a human at the door
```

## Getting started

1. `cd cat-detector`
2. Add your code under `detector/` and `notifier/`.
3. Document how to build, flash, and run each part below.

## Usage

_TBD_

## License

MIT — see the [root LICENSE](../LICENSE).
