# WebSerial

WebSerial shows the live firmware log in the browser.

Open:

`/webserial`

or use the `Web Serial` menu entry when available on your device.

## Functions

| Button | Description |
| --- | --- |
| Clear | Clear the visible log window |
| Auto Scroll | Keep the newest log lines visible |
| Timestamp | Add browser-side timestamps to displayed lines |
| Reconnect | Reconnect the WebSerial websocket |
| Send | Send a command through the WebSerial input when supported |

## Use cases

Use WebSerial for:

- BLE scan and connection problems.
- Wired BMS parser or timeout problems.
- MQTT connection problems.
- OTA update status.
- License and control write checks.

## Notes

- WebSerial is only available on firmware variants that include it.
- If WebUI authentication is configured, WebSerial uses the same login.
- Keep logs short when reporting issues and include the BMS type, link type and firmware version if available.
