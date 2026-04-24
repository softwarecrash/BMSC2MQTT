# Firmware Update and Backup

Firmware updates and settings backup are available in `Firmware Update`.

BMSC2MQTT is intended to be used with ready-made firmware files. Users normally only need the released `.bin` or `.ota` files.

## Online update

The online updater checks GitHub Releases and downloads the OTA package from there.

Use this when:

- The ESP has internet access.
- A release package is available.
- You want the normal update path.

## Manual OTA update

Manual update uploads a firmware OTA file through the WebUI.

Recommended file type:

`.ota`

After a successful update the ESP reboots automatically.

## Backup

The WebUI can export settings as JSON.

The backup includes the device configuration, including:

- Network settings
- MQTT settings
- License key
- Device settings
- BMS settings
- BLE target information

## Restore

Restore imports a settings JSON file back into the device.

After restore, the firmware saves the new settings and reboots when required.

## Notes

- Keep a backup before changing BMS wiring, MQTT topic or network settings.
- Restoring old settings can bring back an old MQTT topic or old BLE target.
- If the device is no longer reachable after network restore, use AP mode or reset procedure.
