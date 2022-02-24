# Home Temperature Monitoring

Monitor the temperature across your home with ease.

## Overview

Multiple [agents](#Agents) spread across your home send temperature related data over [ESP-NOW](https://www.espressif.com/en/products/software/esp-now/overview) to one controller (which is also an agent, just specially configured), which then broadcasts that data to a configurable MQTT server. This is done to reduce the number of active connections on your network. Beyond that, what's done with the data is up to you. I plan on sending this to a self hosted IoT platform which will congest the data and allow me to easily view and generate alerts based on the data.

## Configuration

After plugging in for the first time, you will need to connect to the access point to configure your Wi-Fi credentials, MQTT server url, if this will be an agent or a controller, and if this is an agent then the MAC address of the controller (required for ESP-NOW communication). In the event that the Wi-Fi network cannot be reached after one hour, it will be set back into configuration mode. While in configuration mode, it will continuously attempt to connect back to the original network.

Having a configuration menu eases the flashing process, especially if you were to distribute these.

## Agents

Agents are made-up of the following main components:

1. [ESP32](https://www.espressif.com/en/products/socs/esp32) / [ESP8266](https://www.espressif.com/en/products/socs/esp8266) MCU - used for inner-device communicationn and sending all data over MQTT.
2. [BME280](https://www.bosch-sensortec.com/products/environmental-sensors/humidity-sensors-bme280/) - used for reporting relative humidity, barometric pressure, and ambient temperature.
3. 4 PIN LED Screen - used for displaying results of BME280 sensor (not required).

It is possible to swap components out but updates will need to be made to the code, depending on which component is swapped this could be extensive (in the case of moving away from an Espressif MCU for example as ESP-NOW would no longer be supported).

### V1 - Breadboard

For a proof of concept, the first version will be done on a breadboard. The actual electronics portion of this is rather straightforward, follow the wiring diagram below.

Wiring diagram coming soon

As part of V1, most of the code will need to be written. This includes everything from the configuration, ESP-NOW communication, reading sensor data, and sending data over MQTT. Unless the code is refactored to drop Arduino support and use [ESP-IDF](https://www.espressif.com/en/products/sdks/esp-idf), I don't see this changing much beyond V1.
