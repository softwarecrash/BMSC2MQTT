# HomeAssistant integration

Home Assistant integration uses MQTT Discovery. No manual `configuration.yaml` sensors are required when discovery is enabled.

## Requirements

1. MQTT broker installed in Home Assistant.
2. BMSC2MQTT installed and connected to WiFi.
3. MQTT configured in `MQTT Settings`.
4. BMS data visible on the BMSC2MQTT `Status` page.
5. `HA Discovery` enabled in `MQTT Settings`.

## Setup

1. Open BMSC2MQTT in the browser.
2. Check the `Status` page and verify that BMS data is available.
3. Open `MQTT Settings`.
4. Enable `HA Discovery`.
5. Save the settings.
6. Wait for the ESP reboot.
7. Open Home Assistant.
8. Go to `Settings` -> `Devices & services` -> `MQTT`.
9. The BMSC2MQTT device should appear as an MQTT device.

If no entities appear, restart Home Assistant and check retained MQTT discovery topics.

More details: [MQTT and Home Assistant](MQTT-and-Home-Assistant)
