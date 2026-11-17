# Pinout and Connections

## ESP32 Connections

| Component | Component Pin | ESP32 Pin | Notes |
|---|---|---|---|
| DHT22 | VCC | 3V3 | Sensor power |
| DHT22 | SDA / DATA | GPIO 4 | Data signal |
| DHT22 | NC | Not connected | Leave unconnected |
| DHT22 | GND | GND | Common ground |
| Pushbutton | One terminal | GPIO 27 | Configured as `INPUT_PULLUP` |
| Pushbutton | Other terminal | GND | Pressing the button pulls GPIO 27 LOW |
| Fan LED | Anode (+) | GPIO 26 through 220 Ω resistor | Fan indicator output |
| Fan LED | Cathode (-) | GND | Common ground |
| DHT22 pull-up | One terminal | DHT22 DATA / GPIO 4 | 10 kΩ pull-up |
| DHT22 pull-up | Other terminal | 3V3 | Pull-up to sensor supply |

## Pin Definitions in Firmware

```cpp
#define DHT_PIN     4
#define BUTTON_PIN  27
#define FAN_PIN     26
```

## Button Logic

The button uses the ESP32 internal pull-up:

- Released: HIGH
- Pressed: LOW

The firmware toggles the fan LED state on each debounced button press.
