# Flash and Installation

This project is distributed as ready-to-use firmware files. You do not need the source code to use BMSC2MQTT.

## What you need

- Supported ESP32 board or ready-made BMSC hardware.
- The matching firmware file for your hardware.
- USB cable or another flashing method supported by your board.
- Browser for the first setup.

## Firmware files

Use the firmware file that matches your hardware variant.

Typical file types:

| File type | Use |
| --- | --- |
| `.bin` | Initial flashing with an ESP flashing tool |
| `.ota` | Manual update from the WebUI |

Do not flash a firmware file for a different board unless it is explicitly listed as compatible.

## First flash

1. Connect the ESP32 to USB.
2. Start your flashing tool.
3. Select the correct COM port.
4. Select the matching `.bin` firmware.
5. Flash the device.
6. Reboot the ESP32.
7. Connect to the setup WiFi AP `BMSC2MQTT_AP`.
8. Open `http://192.168.4.1`.

After WiFi setup the device leaves AP mode and starts normal operation.

## Updating later

For normal updates use the WebUI:

1. Open `Firmware Update`.
2. Use online update if the ESP has internet access.
3. Or upload the matching `.ota` file manually.
4. Wait until the update finishes.
5. The ESP reboots automatically.

## Before flashing or updating

- Make a settings backup if the device is already configured.
- Check that the power supply is stable.
- Do not disconnect power during flashing or OTA update.
- Use the firmware file for the correct hardware.
