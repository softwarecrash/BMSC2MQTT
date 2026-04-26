# Settings reference

## Network settings

| Setting | Description |
| --- | --- |
| Device name | Display name, hostname and default mDNS name |
| WiFi SSID 1 | Primary WiFi network |
| WiFi password 1 | Password for primary WiFi |
| BSSID 1 | Optional fixed access point MAC |
| BSSID lock | Connect only to the configured BSSID |
| WiFi SSID 2 | Secondary WiFi network |
| WiFi password 2 | Password for secondary WiFi |
| BSSID 2 | Optional fixed access point MAC for secondary WiFi |
| Static IP | Optional static IP address |
| Gateway | Optional static gateway |
| Subnet | Optional subnet mask |
| DNS | Optional DNS server |
| WebUI user | Optional WebUI login user |
| WebUI password | Optional WebUI login password |

If WebUI user is empty, no WebUI login is required.

## MQTT settings

| Setting | Description |
| --- | --- |
| MQTT server | Broker IP address or hostname |
| MQTT port | Broker port, default `1883` |
| MQTT user | Username, leave empty if not needed |
| MQTT password | Password, leave empty if not needed |
| MQTT topic | Base topic, default `BMSC2MQTT` |
| MQTT refresh | Publish interval in seconds. `0` disables periodic publishing |
| SSL/TLS | Use TLS connection. Current firmware accepts certificates without validation |
| HA Discovery | Publish Home Assistant MQTT Discovery config |

MQTT settings are applied after save and reboot.

## Device settings

| Setting | Description |
| --- | --- |
| LED brightness | Brightness for the WS2812 status LEDs |
| Relay mode | Function of relay output 0 or 1 |
| Relay trigger source | BMS value used for comparison |
| Relay trigger value | Value used by the relay comparison |
| Relay hysteresis | Difference before switching back |
| Relay failsafe | Switch relay state when BMS is offline or sleeping |

Relay functions are license dependent.

## BMS settings

| Setting | Description |
| --- | --- |
| BMS link | `0` BLE, `1` wired |
| BMS vendor | `0` Daly, `1` JK, `2` JBD, `3` 100B, `4` TDT |
| UART RX | RX pin, `-1` for board default |
| UART TX | TX pin, `-1` for board default |
| UART RTS/DE | RS485 direction pin, `-1` if unused |
| UART baud | Baud rate, default `9600` |
| Known BLE devices | Stored BLE device list |
| Last BLE address | Last selected BLE target |
| BLE auto reconnect | Automatically reconnect selected BLE BMS |

Use the wizard unless you need a special wired pinout or advanced BLE setup.
