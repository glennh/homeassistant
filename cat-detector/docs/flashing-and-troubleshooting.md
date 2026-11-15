# Flashing and troubleshooting notes

## XIAO ESP32-C6 (current board)
- Native USB; flash from a Windows PC with Chrome/Edge at web.esphome.io using the ESPHome "Factory format" download. Hold BOOT while plugging in if no port appears.
- After the first flash, updates go over Wi-Fi from the ESPHome dashboard.
- `sound_level` needs `passive: false` (it is a required option).
- The board only joined Wi-Fi once the config pointed at the extender network; it is out of range of the main router.
- Adding a fallback `ap:` hotspot makes a Wi-Fi problem easy to spot and fix.

## Old ESP32 DevKit V1 (not used for this)
- Not detected by the Windows PC (no COM port or connect chime) even with the CP210x driver and several cables; detected fine on a Raspberry Pi 2.
- Flashed from the Pi 2 with `esptool --no-stub --port /dev/ttyUSB0 write_flash 0x0 firmware.factory.bin` because the Pi OS esptool package was missing its stub files.
- Afterwards the board boot-looped with `Fatal exception (28) LoadProhibited`. Possible causes were low power (the Pi reported undervoltage) or the firmware/framework; never fully resolved.
