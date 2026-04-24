# WebUI Overview

The WebUI is the main control and setup interface.

## Pages

| Page | Use |
| --- | --- |
| Status | Live BMS data, SOC bar, cell overview and controls |
| Network Settings | WiFi setup, static IP and optional WebUI login |
| MQTT Settings | MQTT broker, topic, interval, TLS and Home Assistant Discovery |
| Device Settings | BMS wizard, advanced BMS settings, LED brightness and relay settings |
| Firmware Update | Online update, manual OTA update, settings backup and restore |
| License Settings | Enter and check license key |
| Web Serial | Live log for troubleshooting |

## Status page

The Status page shows the current BMS state.

Typical values:

- Connection state
- SOC
- Voltage
- Current
- Calculated power
- Charge/discharge MOS state
- Temperatures
- Cell voltages
- Error text

Some values are only visible with a valid license and only if the BMS provides them.

## Controls

Depending on BMS type and license, the Status page can offer:

- Set SOC
- Switch charge MOS
- Switch discharge MOS
- Wake wired BMS

If a control is hidden or disabled, the current BMS or license state does not allow that action.

## AP mode

When no WiFi is configured, the device starts in setup AP mode.

In AP mode:

- Open `http://192.168.4.1`.
- Configure WiFi first.
- BLE BMS scan is disabled until the device is in normal WiFi mode.
