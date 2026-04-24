# License Overview for WebUI, MQTT, and Home Assistant

Updated: 2026-04-13

Important:
- A license only unlocks data that your BMS actually provides.
- Depending on the BMS model or protocol, some values may still be unavailable.
- Write functions are only enabled if the active BMS type supports them safely.
- The same visibility rules are used by the WebUI, MQTT and Home Assistant Discovery.

## Available without a license

- BMS connection status
- State of charge (SOC)
- Battery voltage
- Battery current
- Calculated battery power in the WebUI
- Charge MOS and discharge MOS as status indicators

## Added with a license

- Battery temperature
- Cell voltage difference
- Highest and lowest cell including cell number
- Balancing status
- ETA / remaining time
- Charge cycles
- Remaining capacity
- Warnings and error messages
- Cell voltage chart
- Operation mode
- Set SOC by double-click, if supported by the BMS
- Switch charge MOS and discharge MOS, if supported by the BMS
- Relay functions

## MQTT and Home Assistant

Without a license, retained MQTT topics and Home Assistant discovery configs for locked values are cleared or not published.

With a valid license, additional topics and discovery entities become visible if the connected BMS provides the data.

Examples of license dependent values:

| Area | Examples |
| --- | --- |
| Live data | temperature, remaining capacity, ETA, cycles |
| Cell data | cell voltages, min/max cell, cell difference |
| Temperatures | BMS temperature sensors |
| Errors | decoded BMS error text |
| Controls | SOC write, MOS write, relay functions |

## Good to know

- A license only unlocks values that the connected BMS really provides.
- Write functions stay disabled unless the active BMS type supports them safely.
- When the license state changes, MQTT and Home Assistant discovery follow the same visibility rules automatically.
- JK and TDT are read-only in the current support matrix.
