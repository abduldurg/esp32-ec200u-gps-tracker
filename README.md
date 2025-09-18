# esp32-ec200u-gps-tracker
ESP32-based GPS tracker using Quectel EC200U (A7076) GSM/4G module and u-blox GPS.  Sends location via HTTPS with Basic Authentication.


# ESP32 + EC200U (A7076) + u-blox GPS Tracker

This project uses an **ESP32** microcontroller with:
- **Quectel EC200U (A7076) GSM/4G module** for internet connectivity
- **u-blox GPS module** for location
- Sends GPS data to a remote server via **HTTPS GET** with Basic Authentication

## Features
- AT command control of EC200U via ESP32 UART1
- Automatic PDP context activation with retry
- HTTPS GET with custom headers
- Base64 encoded Basic Auth
- u-blox GPS location parsing
- Sends **Latitude, Longitude, Timestamp, Accuracy, DeviceID, Vehicle No**
- Skips repeated coordinates to save data

## Hardware Connections
| ESP32 Pin | EC200U Pin | Description        |
|-----------|------------|--------------------|
| GPIO 17   | TX         | ESP32 TX → Modem RX |
| GPIO 18   | RX         | ESP32 RX ← Modem TX |
| GPIO 10   | PWRKEY     | Power key pulse    |
| 3.3V/5V   | VCC        | Power              |
| GND       | GND        | Common ground      |

GPS (u-blox) is connected internally via EC200U AT commands.

## Configuration
Edit these values in the code before uploading:
```cpp
String vehicleNumber = "vehical no";     // your vehicle number
String authUser = "your username";       // server username
String authPass = "your password";       // server password
String host = "domain name";             // your server domain
String path = "full path";               // server API endpoint


Requirements

ESP32 board package in Arduino IDE

HardwareSerial + mbedtls library (built-in on ESP32)

SIM card with data plan (Airtel, Jio, etc.)

Usage

Power up ESP32 + EC200U with proper power supply (≥2A recommended).

Flash the sketch from tracker.ino.

Pair EC200U with your network APN (set in code, default: Airtel).

Open Serial Monitor @115200 baud to see logs.

Device will acquire GPS lock and send data every 30 seconds.
