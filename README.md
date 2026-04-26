# BMSC2MQTT

## What The Device Does

- Reads BMS data via Bluetooth (BLE) or wired (UART/RS485), depending on BMS type.
- Shows live values in the web UI.
- Publishes data via MQTT (including Home Assistant Discovery when enabled).
- Supports OTA updates (online and manual).
- Uses a 5x WS2812 status LED strip.
- Optional: DS18B20 temperature sensors.
- Optional: relay outputs (depending on configuration).

## Supported BMS (Current State)

| BMS | Bluetooth (BLE) | Wired (UART/RS485) | Write (SOC/MOS) |
| --- | --- | --- | --- |
| Daly (Classic) | Yes | Yes | Yes |
| 100B (Daly new map) | Yes (currently Daly BLE profile) | Yes | Yes (wired), BLE depends on device |
| JK | Yes | Yes | No (read-only) |
| JBD | Yes | No | MOS yes, SOC no |
| TDT | Yes | Yes | No (read-only, BLE unlock available) |

![BMS Wizzard 1](readme/bms wizzard 1.jpg)

Important:
- Write functions are only active when:
  - a valid license is present,
  - the BMS is connected,
  - and the selected provider supports that write operation.

## Quick Start

1. Flash the firmware.
2. Power on the device.
3. If no WiFi is configured, the device starts an AP:
   - SSID: `BMSC2MQTT_AP` (or `${SOURCE_NAME}_AP`)
   - IP: `192.168.4.1`
4. Open `http://192.168.4.1` in a browser.
5. Configure WiFi in `Network Settings`.
6. Optional: configure your broker in `MQTT Settings`.
7. Open `Device Settings` and run the BMS setup wizard:
   - Select link type: Bluetooth or Wired
   - Select BMS type
   - Test connection
   - Save
8. Check live values on the status page.

Note:
- In normal WiFi mode, the device is also reachable via mDNS, for example `http://BMSC2MQTT.local` (name is configurable).

## Web UI Overview

- `Status`: live values, cell view, SOC bar, MOS switches (if unlocked).
- `Network Settings`: WiFi scan, SSID/password, optional BSSID lock, optional static IP.
- `MQTT Settings`: broker, port, topic, interval, TLS, HA discovery.
- `Device Settings`: BMS setup wizard and advanced BMS/UART settings.
- `Firmware Update`: online update (GitHub) and manual OTA update, plus backup/restore.
- `License Settings`: manage license key.
- `Web Serial`: live debug log in browser.

## BMS Setup: Wizard + Advanced

### Wizard (Recommended)

- Guides you step by step through:
  - link type
  - BMS type
  - scan/connect (BLE) or wiring test (wired)
  - save

### Advanced

- For special setups:
  - `bmsLink` (BLE/Wired)
  - `bmsVendor`
  - UART pins (`RX`, `TX`, optional `RTS/DE`)
  - baud rate
  - BLE auto-reconnect and device selection

Practical notes:
- Daly/100B wired is usually direct TTL.
- For RS485 with transceiver, set `RTS/DE` pin (otherwise `-1`).

## Important Runtime Mode: AP vs BLE

When Access Point mode is active (configuration mode), BLE-BMS is intentionally disabled.  
Reason: stable WiFi/Bluetooth coexistence.

This means:
- No BLE-BMS connection/scan while in AP mode.
- BLE-BMS automatically resumes when the device returns to normal WiFi mode.

## WS2812 Status LED Strip (Current Firmware Behavior)

The firmware uses 5 LEDs.

### Boot

- Short boot animation: white running light, then off.

### Status Mode

LED mapping:
- LED 0: WiFi/RSSI
- LED 1: Device/BMS status
- LED 2: MQTT status
- LED 3-4: off

Colors:
- WiFi/RSSI (LED 0):
  - Green for good signal (roughly better than -60 dBm)
  - Orange for mid-range signal (roughly -80 to -60 dBm)
  - Red for weak signal (roughly below -80 dBm)
  - If RSSI is not available yet: connected/disconnected only (green/red)
- Device (LED 1): green = OK, red = error/offline
- MQTT (LED 2): green = connected, red = disconnected

AP mode:
- LED 0 solid blue
- LED 2 off (MQTT is not evaluated in AP mode)

### SOC Mode

When all required states are OK, the display switches to an SOC bar after 5 seconds:
- All 5 LEDs show charge level (including partial LED for intermediate values).
- Colors:
  - <= 10%: red
  - 11-30%: orange
  - > 30%: gradient toward green

## MQTT Behavior

The base topic is configurable (default: `BMSC2MQTT`).

Examples (publish, retained):
- `<topic>/WiFiStatus`
- `<topic>/RSSI`
- `<topic>/IP`
- `<topic>/DS18B20/<index>`
- `<topic>/bms/device`
- `<topic>/bms/connected`
- `<topic>/bms/live/*`
- `<topic>/bms/meta/*`
- `<topic>/bms/cells/*`
- `<topic>/bms/temps/*`
- `<topic>/bms/errors/text` (only if not empty)

MQTT control topics (subscribe):
- `<topic>/bms/control/soc`
- `<topic>/bms/control/power_in`
- `<topic>/bms/control/power_out`

Payloads:
- `soc`: number (for example `50`)
- `power_in`, `power_out`: `true/false`, `1/0`, `on/off`
- `null`: resets the control value

## License (What It Means For Users)

Without a license:
- Visible BMS values are limited to connection state, SOC, voltage, current, calculated power and charge/discharge MOS status.
- Write functions (SOC/MOS) are locked.

With a valid license:
- Adds temperature, remaining capacity, ETA, cycles, operation mode, warnings, cell details and relay functions.
- Write functions available if supported by the provider.

## Firmware Update And Backup

- Online update: downloads OTA package from GitHub Releases.
- Manual update: upload OTA file in the UI (`.ota` recommended).
- Backup/Restore:
  - export settings as JSON
  - import later

## Common Issues

- BLE scan finds no devices:
  - check if AP mode is active (BLE is disabled in AP mode)
  - select the correct BMS type
  - close the vendor app while scanning/connecting

- Wired connection shows no data:
  - check RX/TX wiring (not swapped)
  - check baud rate
  - for RS485, set `RTS/DE` pin correctly

- MOS/SOC controls cannot be used:
  - check license status
  - BMS must be connected
  - BMS type/provider must support writes

- DS18B20 shows `-127`:
  - sensor not detected or not connected

## Summary

For normal commissioning, you only need to:
- configure WiFi
- configure MQTT (optional)
- run the BMS setup wizard

Everything else is available in the web UI.
