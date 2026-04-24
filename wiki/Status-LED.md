# Status LED

BMSC2MQTT uses a 5 LED WS2812 strip.

## Boot

On boot the firmware shows a short white running light and then turns the LEDs off until normal status handling starts.

## Status mode

LED mapping:

| LED | Meaning |
| --- | --- |
| 0 | WiFi / RSSI |
| 1 | BMS status |
| 2 | MQTT status |
| 3 | Off in status mode |
| 4 | Off in status mode |

WiFi/RSSI colors:

| Color | Meaning |
| --- | --- |
| Green | Good signal, roughly better than `-60 dBm` |
| Orange | Medium signal, roughly `-80 dBm` to `-60 dBm` |
| Red | Weak signal, roughly below `-80 dBm` |

BMS status:

| Color | Meaning |
| --- | --- |
| Green | BMS connected / OK |
| Red | BMS offline or error |

MQTT status:

| Color | Meaning |
| --- | --- |
| Green | MQTT connected |
| Red | MQTT disconnected |

## AP mode

In access point mode:

- LED 0 is solid blue.
- MQTT is not evaluated.
- BLE BMS communication is disabled.

## SOC mode

When all required states are OK, the strip switches to SOC bar mode after a short delay.

All 5 LEDs are used as a charge bar. Intermediate SOC values can show a partial LED.

SOC colors:

| SOC | Color |
| --- | --- |
| `<= 10%` | Red |
| `11%` to `30%` | Orange |
| `> 30%` | Gradient toward green |
