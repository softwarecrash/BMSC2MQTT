Welcome to the BMSC2MQTT wiki.

BMSC2MQTT is an ESP32 based BMS-to-MQTT bridge. It reads battery management systems over Bluetooth Low Energy or wired UART/RS485, shows live data in the WebUI and publishes the values to MQTT with optional Home Assistant Discovery.

## Quick links

- [Quick Start](Quick-Start)
- [Flash and Installation](Flash-and-Installation)
- [WebUI Overview](WebUI-Overview)
- [Supported BMS](Supported-BMS)
- [BMS Setup](BMS-Setup)
- [Wiring](Wiring)
- [Datapoints and units](Datapoints-and-units)
- [Settings reference](Settings-reference)
- [MQTT and Home Assistant](MQTT-and-Home-Assistant)
- [HomeAssistant integration](HomeAssistant-integration)
- [License WebUI MQTT HomeAssistant](License-WebUI-MQTT-HomeAssistant)
- [Status LED](Status-LED)
- [Firmware Update and Backup](Firmware-Update-and-Backup)
- [WebSerial](WebSerial)
- [Reset](Reset)
- [Troubleshooting](Troubleshooting)

## What it does

- Reads BMS data via BLE or wired UART/RS485.
- Shows live values, cell data and BMS status in the WebUI.
- Publishes data via MQTT.
- Creates Home Assistant MQTT Discovery entities when enabled.
- Supports online and manual OTA updates.
- Supports a 5 LED WS2812 status strip.
- Supports optional DS18B20 temperature sensors.
- Supports optional relay functions when unlocked.

## Notes

- Available values depend on the selected BMS and on the data the BMS actually provides.
- Write functions are only enabled when a valid license is present and the selected BMS supports the command safely.
- BLE BMS communication is disabled while the device is in WiFi Access Point setup mode.
