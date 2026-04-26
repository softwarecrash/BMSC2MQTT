# Reset

BMSC2MQTT has a factory reset manager for clearing stored settings.

## Hardware reset sequence

The firmware counts hardware resets directly after boot.

Default behavior:

| Setting | Value |
| --- | --- |
| Reset window | 10 seconds |
| Required hardware resets | 6 |

If the ESP is reset 6 times inside the reset window, factory reset is triggered.

Only hardware style resets are counted. Software resets, watchdog resets and crashes are not counted for the factory reset sequence.

## What factory reset clears

Factory reset erases the NVS settings partition.

This clears stored configuration such as:

- WiFi settings
- MQTT settings
- Device settings
- BMS settings
- License key
- Stored BLE targets

After reset the device starts in AP setup mode again.

## Backup before reset

Use `Firmware Update` -> settings backup before resetting if you want to restore the configuration later.
