# System Architecture

## Project
**ASL National Arena — Challenge #05: Industrial Temperature Monitoring and Emergency Fan Control**

## Overview
The system uses an ESP32, DHT22 temperature/humidity sensor, pushbutton, and LED representing the cooling fan. Temperature and humidity readings are published to a public MQTT broker over Wi-Fi.

## Main Components

- **ESP32:** Main controller.
- **DHT22:** Measures temperature and relative humidity.
- **Pushbutton:** Toggles the emergency fan output.
- **Fan LED:** Represents the cooling fan state in the simulation.
- **Wi-Fi:** Connects to the `Wokwi-GUEST` network.
- **MQTT broker:** `broker.hivemq.com`, port `1883`.

## Software Architecture

The firmware separates network management from the main control loop.

### Main control loop
- Checks the pushbutton.
- Applies a 25 ms debounce interval.
- Toggles the fan LED ON or OFF when a press is detected.
- Reads the DHT22 at 2-second intervals.
- Makes the latest successful sensor reading available to the network task.

### Network task
A FreeRTOS task pinned to ESP32 Core 0 manages:
- Wi-Fi connection and reconnection attempts.
- MQTT connection and reconnection attempts.
- MQTT client processing.
- Publishing the latest available sensor reading.

A critical section protects the shared sensor values and the new-reading flag.

## MQTT Data

- **Broker:** `broker.hivemq.com`
- **Port:** `1883`
- **Topic:** `asl/national-arena/challenge05/aryanaritro/temperature`
- **Payload format:** JSON

Example:

```json
{"temperature":24.00,"humidity":40.00}
```

## Timing

- Sensor sampling interval: 2,000 ms.
- Button debounce interval: 25 ms.
- Network retry interval: 5,000 ms.
- Main loop includes a 1 ms delay to yield processor time.

## Verification Notes

The Wokwi simulation demonstrated sensor readings, Wi-Fi connection, MQTT connection and publishing, and fan ON/OFF control. 
