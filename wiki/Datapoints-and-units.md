# Datapoints and units

This page lists the common BMSC2MQTT values and their MQTT topics. Available values depend on the connected BMS and license state.

## System datapoints

| Value | MQTT topic | Unit | Description |
| --- | --- | --- | --- |
| `WiFiStatus` | `<topic>/WiFiStatus` | boolean | WiFi connected state |
| `RSSI` | `<topic>/RSSI` | dBm | WiFi signal strength |
| `IP` | `<topic>/IP` | text | Device IP address |
| `DS18B20/<index>` | `<topic>/DS18B20/<index>` | C | Optional DS18B20 sensor |

## BMS live datapoints

| Value | MQTT topic | Unit | Description |
| --- | --- | --- | --- |
| `bms/connected` | `<topic>/bms/connected` | boolean | BMS connection state |
| `bms/device` | `<topic>/bms/device` | text | Active BMS type |
| `bms/live/voltage` | `<topic>/bms/live/voltage` | V | Battery voltage |
| `bms/live/current` | `<topic>/bms/live/current` | A | Battery current |
| `bms/live/soc` | `<topic>/bms/live/soc` | % | State of charge |
| `bms/live/temperature` | `<topic>/bms/live/temperature` | C | Average or pack temperature |
| `bms/live/remaining_capacity` | `<topic>/bms/live/remaining_capacity` | Ah | Remaining capacity |
| `bms/live/total_ah_charge` | `<topic>/bms/live/total_ah_charge` | Ah | Cumulative charged capacity, currently available on Daly 100B / new Daly map |
| `bms/live/total_ah_discharge` | `<topic>/bms/live/total_ah_discharge` | Ah | Cumulative discharged capacity, currently available on Daly 100B / new Daly map |
| `bms/live/eta_minutes` | `<topic>/bms/live/eta_minutes` | min | Estimated remaining time |
| `bms/live/operation_mode` | `<topic>/bms/live/operation_mode` | text | BMS operation mode |
| `bms/live/cell_balance` | `<topic>/bms/live/cell_balance` | boolean | Cell balancing state |
| `bms/live/power_in` | `<topic>/bms/live/power_in` | boolean | Charge allowed / charge MOS |
| `bms/live/power_out` | `<topic>/bms/live/power_out` | boolean | Discharge allowed / discharge MOS |
| `bms/live/cycles` | `<topic>/bms/live/cycles` | count | Charge cycles |
| `bms/live/cell_max` | `<topic>/bms/live/cell_max` | V | Highest cell voltage |
| `bms/live/cell_min` | `<topic>/bms/live/cell_min` | V | Lowest cell voltage |
| `bms/live/cell_difference` | `<topic>/bms/live/cell_difference` | V | Difference between highest and lowest cell |
| `bms/live/cell_max_num` | `<topic>/bms/live/cell_max_num` | number | Highest cell number |
| `bms/live/cell_min_num` | `<topic>/bms/live/cell_min_num` | number | Lowest cell number |

## BMS meta datapoints

| Value | MQTT topic | Unit | Description |
| --- | --- | --- | --- |
| `bms/meta/serialNumber` | `<topic>/bms/meta/serialNumber` | text | Serial number or selected BLE identity |
| `bms/meta/cells` | `<topic>/bms/meta/cells` | count | Cell count |
| `bms/meta/tempSensors` | `<topic>/bms/meta/tempSensors` | count | Temperature sensor count |
| `bms/meta/statusCode` | `<topic>/bms/meta/statusCode` | code | Raw BMS status or warning code |
| `bms/errors/text` | `<topic>/bms/errors/text` | text | Decoded BMS error text |

## Dynamic arrays

| Value | MQTT topic | Unit | Description |
| --- | --- | --- | --- |
| `bms/cells/<index>` | `<topic>/bms/cells/<index>` | V | Cell voltage |
| `bms/temps/<index>` | `<topic>/bms/temps/<index>` | C | BMS temperature sensor |

## License visibility

Without a license, MQTT and Home Assistant only expose the basic values. Cell details, BMS temperatures, ETA, cycles, cumulative Ah counters and decoded errors require a valid license.
