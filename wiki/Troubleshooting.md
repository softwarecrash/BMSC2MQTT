# Troubleshooting

## BLE scan finds no devices

Check:

- The device is not in AP mode.
- WiFi is configured and connected.
- The correct BMS type is selected.
- The official BMS app is closed.
- The BMS is awake.
- The ESP32 is close enough to the BMS.

BLE BMS scan and connection are disabled while the ESP runs as setup access point.

## BLE connects but no data appears

Check:

- Correct BMS type.
- BMS is not connected to another app.
- Signal strength is stable.
- Reboot the BMS or ESP if the BMS BLE stack is stuck.

## Wired BMS shows no data

Check:

- RX/TX are crossed.
- GND is shared.
- Baud rate is correct.
- Correct BMS vendor is selected.
- For RS485, `RTS/DE` pin is configured correctly.
- RS485 A/B may need to be swapped depending on adapter labeling.

## MQTT does not connect

Check:

- MQTT host and port.
- Username/password.
- Broker is reachable from the ESP network.
- TLS setting matches the broker port.
- WebUI shows WiFi connected.

The firmware retries MQTT connection non-blocking.

## Home Assistant entities do not appear

Check:

- MQTT is connected.
- `HA Discovery` is enabled.
- BMS data exists on the Status page.
- Home Assistant MQTT integration is running.
- Restart Home Assistant if discovery data was changed recently.

Old retained discovery topics can keep old entities alive. Remove old retained topics if the MQTT base topic was changed.

## MOS or SOC control does not work

Check:

- Valid license is installed.
- BMS is connected.
- Selected BMS type supports the write operation.
- The BMS itself accepts the command.

JK and TDT are read-only in the current support matrix.

## DS18B20 shows -127

`-127` means the sensor was not detected.

Check:

- Wiring.
- Pull-up resistor.
- Sensor power.
- Correct data pin.

## WebUI asks for login

If `WebUI user` is configured, authentication is enabled. Clear the WebUI user in Network Settings if login should be disabled.

## Need a debug log

Open `Web Serial` in the WebUI if it is available on your device. Use the log when reporting BMS connection, MQTT or OTA issues.
