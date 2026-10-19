# detector

The **detector** part of the [cat-detector](../README.md) system.

Runs on the ESP32 and detects cats.

## Hardware

- **Board:** Seeed Studio XIAO ESP32 C6
- **Microphone:** I2S input on the XIAO pads — LRCLK GPIO1, BCLK GPIO0, DIN GPIO2 (external ADC, left channel)
- **Presence sensor:** HLK-LD2410 24 GHz radar over UART — TX GPIO16, RX GPIO17, 256000 baud

Detection combines the microphone and the radar presence sensor to decide whether a cat is present.

## Connectivity

Connects to Home Assistant over **WiFi** via the ESPHome native API.

## Status

Working ESPHome firmware — see `esp32c6-detector.yaml`.

## Structure

```
detector/
├── README.md
├── esp32c6-detector.yaml   # ESPHome firmware
└── secrets.yaml            # wifi_password (not committed)
```

## Getting started

1. `cd detector`
2. Create `secrets.yaml` with your WiFi password:
   ```yaml
   wifi_password: "your-wifi-password"
   ```
3. Flash with the ESPHome CLI or dashboard:
   ```sh
   esphome run esp32c6-detector.yaml
   ```

## Exposed entities

| Entity | Type | Source |
| --- | --- | --- |
| Average Loudness | sensor | microphone RMS |
| Peak Loudness | sensor | microphone peak |
| Radar Target | binary sensor | LD2410 any target |
| Radar Moving Target | binary sensor | LD2410 moving target |
| Radar Still Target | binary sensor | LD2410 still target |

## Detection output

When a cat is detected, the detector reports it to Home Assistant, which drives
the [notifier](../notifier/README.md). Combining the loudness and radar entities
into a single detection is done in Home Assistant. _Automation TBD._
