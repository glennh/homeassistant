# notifier

The **notifier** part of the [cat-detector](../README.md) system.

Alerts a human when the cat is at the door meowing.

## Hardware

- **Board:** Seeed Studio XIAO ESP32 C6
- **LED:** visual alert when a cat is detected — D4 = GPIO22 (via resistor)
- **Beeper:** audible alert when a cat is detected — D5 = GPIO23 (active buzzer)
- **Push button:** silences the current alert — D6 = GPIO16 (to GND)

## Connectivity

Connects to **WiFi** and talks to Home Assistant through **ESPHome** (native API).

## Status

Working ESPHome firmware — see `esp32c6-notifier.yaml`.

## Structure

```
notifier/
├── README.md
├── esp32c6-notifier.yaml   # ESPHome firmware
└── secrets.yaml            # wifi_password (not committed)
```

## Getting started

1. `cd notifier`
2. Create `secrets.yaml` with your WiFi password:
   ```yaml
   wifi_password: "your-wifi-password"
   ```
3. Flash with the ESPHome CLI or dashboard:
   ```sh
   esphome run esp32c6-notifier.yaml
   ```

## Behaviour

1. Turn on **Flasher Enabled** (from Home Assistant or the ESPHome dashboard).
2. While enabled, the LED flashes and the beeper sounds for 150 ms once per second.
3. Pressing the physical button (D6/GPIO16) turns the flasher off and silences it.
4. Turning the switch off also immediately stops the LED and beeper.

The **Beep Now** button in Home Assistant sounds a one-off 300 ms beep.

## Detection input

Exposed to Home Assistant through the ESPHome native API. Home Assistant can turn
the **Flasher Enabled** switch on/off (e.g. from a detector automation) or trigger
**Beep Now**. _Automation/topic scheme TBD._
