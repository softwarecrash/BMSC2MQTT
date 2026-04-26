# MQTT and Home Assistant

## MQTT publish behavior

The base topic is configurable. Default:

`BMSC2MQTT`

Published topics are retained. Examples:

| Topic | Description |
| --- | --- |
| `<topic>/alive` | Device alive flag |
| `<topic>/WiFiStatus` | WiFi connected state |
| `<topic>/RSSI` | WiFi signal strength in dBm |
| `<topic>/IP` | Device IP address |
| `<topic>/DS18B20/<index>` | Optional external temperature sensor |
| `<topic>/bms/device` | Active BMS device/type |
| `<topic>/bms/connected` | BMS connection state |
| `<topic>/bms/live/voltage` | Battery voltage in V |
| `<topic>/bms/live/current` | Battery current in A |
| `<topic>/bms/live/soc` | State of charge in % |
| `<topic>/bms/live/power_in` | Charge MOS / charge allowed |
| `<topic>/bms/live/power_out` | Discharge MOS / discharge allowed |
| `<topic>/bms/live/total_ah_charge` | Cumulative charged capacity in Ah, if the active BMS provides it |
| `<topic>/bms/live/total_ah_discharge` | Cumulative discharged capacity in Ah, if the active BMS provides it |
| `<topic>/bms/meta/*` | BMS metadata |
| `<topic>/bms/cells/*` | Cell voltages |
| `<topic>/bms/temps/*` | BMS temperature sensors |
| `<topic>/bms/errors/text` | Decoded BMS error text |

The visible MQTT data follows the same license rules as the WebUI and Home Assistant Discovery.

## MQTT control topics

The firmware subscribes to:

`<topic>/bms/control/#`

Supported control topics:

| Topic | Payload | Description |
| --- | --- | --- |
| `<topic>/bms/control/soc` | number or `null` | Set SOC if the active BMS supports it |
| `<topic>/bms/control/power_in` | `true`, `false`, `1`, `0`, `on`, `off`, `null` | Charge MOS control if supported |
| `<topic>/bms/control/power_out` | `true`, `false`, `1`, `0`, `on`, `off`, `null` | Discharge MOS control if supported |
| `<topic>/bms/control/wake` | `true`, `1`, `on`, `wake`, `null` | Trigger wired BMS wake pin if available |

Legacy wake topic:

`<topic>/Device_Control/Wake_BMS`

Control writes require a valid license and a connected BMS. Unsupported writes are ignored.

## Home Assistant Discovery

Home Assistant integration does not need manual `configuration.yaml` sensors when discovery is enabled.

Requirements:

1. MQTT broker is installed and running in Home Assistant.
2. BMSC2MQTT MQTT settings are configured.
3. The BMS has live data in the WebUI.
4. `HA Discovery` is enabled in `MQTT Settings`.

After saving MQTT settings, the ESP reboots. When MQTT connects, discovery configs are published under:

`homeassistant/<component>/<topic>/<object>/config`

## If entities do not show up

1. Check that MQTT is connected in the WebUI.
2. Check that BMS data is visible on the Status page.
3. Check that `HA Discovery` is enabled.
4. Reboot the ESP after changing MQTT settings.
5. If old entities remain, remove them in Home Assistant or clear retained MQTT discovery topics.
6. If no new entities appear, restart Home Assistant.

## License visibility

Without a license, only the basic BMS values are published. With a valid license, additional temperatures, cell data, errors, ETA, cycles, cumulative Ah counters and relay related values become visible.
