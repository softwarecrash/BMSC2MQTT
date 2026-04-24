# Quick Start

## First start

1. Flash the firmware to the ESP32.
2. Power the device.
3. If no WiFi is configured, the device starts an access point.
4. Connect to the WiFi AP:
   - SSID: `BMSC2MQTT_AP`
   - IP: `192.168.4.1`
5. Open `http://192.168.4.1` in a browser.
6. Configure WiFi in `Network Settings`.
7. Save the settings and wait for the reboot.

After WiFi is connected, the device is available by IP address and usually by mDNS:

`http://BMSC2MQTT.local`

The name depends on the configured device name.

## Configure MQTT

1. Open `MQTT Settings`.
2. Enter broker host and port.
3. Optional: enter MQTT username and password.
4. Set the base topic. Default is `BMSC2MQTT`.
5. Set the publish interval in seconds.
6. Enable Home Assistant Discovery if needed.
7. Save. The ESP reboots after saving MQTT settings.

## Configure the BMS

1. Open `Device Settings`.
2. Use the BMS setup wizard.
3. Select the link type:
   - Bluetooth
   - Wired
4. Select the BMS type.
5. For Bluetooth, scan and select the BMS.
6. For wired, check RX/TX/RTS and baud rate.
7. Test the connection.
8. Save the setup.

## Check data

Open the `Status` page. You should see:

- BMS connection state
- SOC
- Voltage
- Current
- Charge/discharge state
- Additional values depending on license and BMS support

If no BLE devices are found, leave AP mode first. BLE BMS scan and connection are intentionally disabled in AP mode.
