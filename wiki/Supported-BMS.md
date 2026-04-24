# Supported BMS

Current support state:

| BMS | Bluetooth BLE | Wired UART/RS485 | Write functions |
| --- | --- | --- | --- |
| Daly Classic | Yes | Yes | SOC and MOS |
| 100B / Daly new map | Yes, currently Daly BLE profile | Yes | Wired SOC and MOS, BLE depends on device |
| JK | Yes | Yes | No, read-only |
| JBD | Yes | No | MOS yes, SOC no |
| TDT | Yes | Yes | No, read-only. BLE unlock is available |

## Important

- The table describes firmware support, not a guarantee that every hardware variant behaves the same.
- Write functions need a valid license.
- Write functions are only active when the selected BMS type supports the operation.
- Commands without verified protocol bytes, checksum and response handling stay disabled.

## Link type notes

### Bluetooth

BLE uses the shared BMS manager/connector/protocol stack. The firmware scans, connects, subscribes to notifications and polls the selected BMS profile.

In AP mode BLE is disabled. Configure WiFi first, then run the BLE wizard in normal WiFi mode.

### Wired

Wired BMS connections use UART or RS485 depending on the BMS and interface hardware.

Typical settings:

| Setting | Meaning |
| --- | --- |
| RX | ESP32 receive pin |
| TX | ESP32 transmit pin |
| RTS/DE | RS485 direction pin, use `-1` if not needed |
| Baud | BMS serial baud rate |

Daly/100B wired is usually direct TTL or Modbus style communication depending on hardware. JK wired uses its own frame protocol. TDT wired uses its own RS485 framing.
