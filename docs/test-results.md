# Test Results

## Wokwi Simulation Verification

| Test | Expected behavior | Result |
|---|---|---|
| ESP32 startup | Firmware starts without rebooting | PASS |
| DHT22 reading | Temperature and humidity values are read | PASS |
| Wi-Fi connection | ESP32 connects to `Wokwi-GUEST` | PASS |
| MQTT connection | ESP32 connects to the HiveMQ public broker | PASS |
| MQTT publishing | Sensor values are published as JSON | PASS |
| Emergency fan ON | Button press turns the fan LED ON | PASS |
| Emergency fan OFF | Next button press turns the fan LED OFF | PASS |
| Wi-Fi disconnection and recovery | Fan remains controllable and network reconnects | PASS |
| Button response under 50 ms | Response time is below 50 ms | PASS |

## Observed Simulation Output

The Serial Monitor showed:

- `Temperature: 24.00 C`
- `Humidity: 40.00 %`
- `MQTT Connected!`
- `MQTT Published: {"temperature":24.00,"humidity":40.00}`
- `Emergency Fan: ON`
- `Emergency Fan: OFF`

## Verification Scope

These results are from the Wokwi simulation and the user's reported test output. Physical hardware testing was not reported.

The firmware uses a separate FreeRTOS network task so that Wi-Fi and MQTT operations are separated from the main button-control loop. 
