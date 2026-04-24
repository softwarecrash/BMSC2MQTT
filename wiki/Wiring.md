# Wiring

## Power

Use a stable power supply for the ESP32 board and connected modules. Do not power external BMS interfaces from weak GPIO pins.

Typical modules:

- ESP32 board or ready-made BMSC hardware supported by the firmware file.
- BLE BMS, no extra data wiring needed.
- UART TTL adapter path for wired BMS if the BMS exposes TTL.
- RS485 transceiver for RS485 based BMS.
- Optional WS2812 5 LED strip.
- Optional DS18B20 sensors.
- Optional relay module, depending on board/configuration.

## Firmware variants and default pins

Use the row that matches the firmware file / hardware variant you flashed.

`-1` means the pin is disabled by default or must be configured in `Device Settings`.

| Firmware / hardware | Status LED | BMS RX | BMS TX | RTS/DE | WS2812 | DS18B20 | Relay 0 | Relay 1 | BMS Wake |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `wemos_d1_mini32` | GPIO2 | GPIO23 | GPIO19 | -1 | GPIO17 | GPIO32 | GPIO4 | GPIO16 | GPIO15 |
| `wemos_d1_mini32_DBG` | GPIO2 | GPIO23 | GPIO19 | -1 | GPIO17 | GPIO32 | GPIO4 | GPIO16 | GPIO15 |
| `esp32c3` | GPIO10 | GPIO3 | GPIO2 | -1 | GPIO8 | GPIO4 | GPIO5 | GPIO6 | GPIO7 |
| `esp32s3` | GPIO10 | GPIO3 | GPIO2 | -1 | GPIO8 | GPIO4 | GPIO5 | GPIO6 | GPIO7 |
| `wt32-eth1` | GPIO2 | -1 | -1 | -1 | GPIO17 | GPIO32 | GPIO4 | GPIO16 | GPIO5 |
| `waveshare_esp32_s3_eth` | -1 | GPIO17 | GPIO18 | GPIO15 | GPIO17 | GPIO21 | GPIO4 | GPIO16 | GPIO7 |

Notes:

- `wemos_d1_mini32_DBG` is the debug variant and includes WebSerial.
- `wt32-eth1` has no default wired BMS UART pins. Set RX, TX and RTS/DE in `Device Settings` if you use wired BMS.
- `waveshare_esp32_s3_eth` uses GPIO17 as default BMS RX and WS2812 pin. If you use wired BMS and a WS2812 strip at the same time, move the wired RX pin in `Device Settings` or leave the WS2812 strip disconnected.
- On Ethernet boards, some pins are already used by LAN hardware. Use the matching firmware variant and avoid changing LAN pins.

## Pin functions

| Function | Connects to | Notes |
| --- | --- | --- |
| Status LED | Onboard single LED | Optional. `-1` means disabled |
| BMS RX | TX of BMS or adapter | Cross RX/TX |
| BMS TX | RX of BMS or adapter | Cross RX/TX |
| RTS/DE | RS485 DE/RE control | Use only for RS485 modules that need direction control |
| WS2812 | DIN of 5 LED strip | Use 5V/3.3V level rules for your strip/module |
| DS18B20 | 1-Wire data | Needs GND, VCC and usually a pull-up resistor |
| Relay 0 / 1 | Relay driver input | Do not drive large loads directly from GPIO |
| BMS Wake | Wake driver input | Wired BMS only, do not connect directly to high-current loads |

## Wired BMS UART

Basic UART wiring:

| ESP32 | BMS / adapter |
| --- | --- |
| RX | TX |
| TX | RX |
| GND | GND |

RX and TX are crossed. If there is no data, check RX/TX first.

Default wired UART pins can be changed in `Device Settings`:

| Setting | Meaning |
| --- | --- |
| UART RX | ESP32 pin that receives data from the BMS |
| UART TX | ESP32 pin that sends data to the BMS |
| UART RTS/DE | RS485 direction pin, use `-1` for normal TTL UART |
| UART baud | BMS serial speed |

## RS485

For RS485 you need a transceiver module.

| ESP32 | RS485 module |
| --- | --- |
| TX | DI |
| RX | RO |
| RTS/DE pin | DE and RE, depending on module |
| GND | GND |

Set the `RTS/DE` pin in Device Settings. Use `-1` only if the module handles direction automatically or no RS485 direction pin is needed.

Typical RS485 notes:

- Connect A/B according to your transceiver and BMS labeling.
- If there is no response, try swapping A and B.
- Keep GND connected between ESP/adapter and BMS side when required by your adapter.
- Use twisted pair wiring for longer RS485 cables.

## BLE BMS

BLE needs no data wiring. The ESP32 must be close enough to the BMS for a stable signal.

Notes:

- Configure WiFi before scanning BLE devices.
- BLE scan is disabled in AP mode.
- Close the official BMS app during connection tests.

## DS18B20 temperature sensors

DS18B20 sensors are optional. If a sensor shows `-127`, the sensor was not detected or the wiring is wrong.

Basic DS18B20 wiring:

| DS18B20 | ESP32 / board |
| --- | --- |
| VCC | 3.3V |
| GND | GND |
| DATA | DS18B20 pin from the pin table |

Common checks:

- Data pin matches the firmware/board wiring.
- GND is connected.
- VCC is connected.
- Pull-up resistor is present if required by the sensor wiring.

## WS2812 status strip

BMSC2MQTT expects a 5 LED WS2812 strip.

Basic wiring:

| WS2812 | ESP32 / board |
| --- | --- |
| 5V or VCC | Matching strip power supply |
| GND | GND |
| DIN | WS2812 pin from the pin table |

Important:

- Connect GND between ESP32 and LED strip power supply.
- Do not power a larger LED strip directly from an ESP32 GPIO.
- Use the LED brightness setting if the strip is too bright.

## Relays and wake output

Do not connect BMS wake or relay loads directly to GPIO pins. Use proper driver hardware, transistor stages, optocouplers or relay modules as required by the load.

Wake output is intended for wired BMS setups only. BLE devices do not use the wake GPIO.

Basic relay module wiring:

| Relay module | ESP32 / board |
| --- | --- |
| IN1 | Relay 0 pin |
| IN2 | Relay 1 pin |
| VCC | Module supply |
| GND | GND |

The relay functions are configured in `Device Settings`. Relay automation is license dependent.

## Ethernet pins

Ethernet pins are fixed by the hardware variant and should not be reused for BMS wiring.

### WT32-ETH01 / LAN8720

| Function | GPIO |
| --- | --- |
| ETH power | GPIO16 |
| ETH MDC | GPIO23 |
| ETH MDIO | GPIO18 |
| RMII REF CLK | GPIO0 |
| RMII TX EN | GPIO21 |
| RMII TXD0 | GPIO19 |
| RMII TXD1 | GPIO22 |
| RMII CRS DV | GPIO27 |
| RMII RXD0 | GPIO25 |
| RMII RXD1 | GPIO26 |

Because GPIO19 and GPIO23 are used by Ethernet on WT32-ETH01, the default BMS UART pins are disabled in the `wt32-eth1` firmware variant.

### Waveshare ESP32-S3 Ethernet / W5500

| Function | GPIO |
| --- | --- |
| W5500 MISO | GPIO12 |
| W5500 MOSI | GPIO11 |
| W5500 SCLK | GPIO13 |
| W5500 CS | GPIO14 |
| W5500 RST | GPIO9 |
| W5500 INT | GPIO10 |
