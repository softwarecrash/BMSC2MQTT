# BMS Setup

The BMS setup is done in `Device Settings`.

## Wizard

The wizard is the recommended setup path.

It guides through:

1. Link type selection.
2. BMS type selection.
3. BLE scan and device selection or wired parameter check.
4. Runtime test.
5. Save.

The wizard applies changes non-blocking while the firmware is running. Saving commits the configuration.

## Advanced mode

Advanced mode exposes the raw BMS settings.

| Setting | Description |
| --- | --- |
| BMS link | `Bluetooth` or `Wired` |
| BMS vendor | Daly, JK, JBD, 100B, TDT |
| UART RX | ESP32 RX pin for wired BMS |
| UART TX | ESP32 TX pin for wired BMS |
| UART RTS/DE | RS485 direction pin, `-1` if unused |
| UART baud | Serial baud rate |
| BLE auto reconnect | Reconnect to the selected BLE BMS automatically |
| BLE target | Last selected BLE BMS address |

## BLE setup

1. Configure WiFi first.
2. Leave AP mode.
3. Open `Device Settings`.
4. Select `Bluetooth`.
5. Select the BMS type.
6. Start scan.
7. Select the device.
8. Enable auto reconnect if desired.
9. Save.

Close the vendor app while BMSC2MQTT connects. Many BMS devices allow only one active BLE client.

## Wired setup

1. Select `Wired`.
2. Select the BMS type.
3. Set RX/TX pins or leave defaults if the board is wired for the defaults.
4. Set RTS/DE only for RS485 direction control.
5. Set the baud rate.
6. Test connection.
7. Save.

## AP mode and BLE

BLE BMS communication is disabled while the ESP is in AP setup mode. This keeps WiFi/Bluetooth coexistence stable during initial setup.

This means:

- BLE scan does not run in AP mode.
- BLE reconnect starts again after the device joins the configured WiFi.
- Wired BMS is not affected by this BLE limitation.
