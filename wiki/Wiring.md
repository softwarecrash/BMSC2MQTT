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

## Wired BMS UART

Basic UART wiring:

| ESP32 | BMS / adapter |
| --- | --- |
| RX | TX |
| TX | RX |
| GND | GND |

RX and TX are crossed. If there is no data, check RX/TX first.

## RS485

For RS485 you need a transceiver module.

| ESP32 | RS485 module |
| --- | --- |
| TX | DI |
| RX | RO |
| RTS/DE pin | DE and RE, depending on module |
| GND | GND |

Set the `RTS/DE` pin in Device Settings. Use `-1` only if the module handles direction automatically or no RS485 direction pin is needed.

## BLE BMS

BLE needs no data wiring. The ESP32 must be close enough to the BMS for a stable signal.

Notes:

- Configure WiFi before scanning BLE devices.
- BLE scan is disabled in AP mode.
- Close the official BMS app during connection tests.

## DS18B20 temperature sensors

DS18B20 sensors are optional. If a sensor shows `-127`, the sensor was not detected or the wiring is wrong.

Common checks:

- Data pin matches the firmware/board wiring.
- GND is connected.
- VCC is connected.
- Pull-up resistor is present if required by the sensor wiring.

## Relays and wake output

Do not connect BMS wake or relay loads directly to GPIO pins. Use proper driver hardware, transistor stages, optocouplers or relay modules as required by the load.

Wake output is intended for wired BMS setups only. BLE devices do not use the wake GPIO.
