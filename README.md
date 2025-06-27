# WSI Summer Internship 2025
During the summer I had the opportunity to fulfill an internship at Sigma Connectivity WSI. Together with [Mikaela](https://github.com/MikaelaDuran) we worked on an IoT-system where she built the backend and frontend, while I focused on the embedded system and connectivity.

## About the project
The project uses an IoT node that collects sensor data about temperature, humidity and pressure, and publishes this information to an MQTT broker.

There are two main subscribers to the MQTT topic(s):

* **A cloud-hosted server:** This server listens to the MQTT messages and stores the incoming sensor readings in a database hosted on Microsoft Azure. The stored data ensures historical tracking, analysis, and further processing of sensor values over time.
* **An ESP32 microcontroller:** This device subscribes to the same MQTT topic and displays the real-time sensor readings on an LCD screen, providing immediate visual feedback at the edge.

To facilitate integration with external systems and the frontend, the server also exposes an API. This API allows clients to fetch the stored sensor data in JSON format. The frontend application consumes this API to present relevant sensor information to users in an intuitive and user-friendly interface.

![IoT Architecture for the Summer Internship](resources/IoT%20Architecture.jpg)

## Modules
### BME280 Device Driver
Complete device driver for the BME280 sensor on Raspberry Pi Pico W using I2C.
* Measures temperature, humidity and air-pressure.
* Set up for indoor use as standard.
* Internal and External APIs for easy implementation.

https://github.com/lafftale1999/bme280_driver

---

### LCD1602 Device Driver
Complete device driver for an 16x2 Hitachi 44780 compatible LCD using the I2C module.
* Correct handling of \n and character overflow.
* External API only exposes user necessary functions.

https://github.com/lafftale1999/lcd_1602_i2c_driver

---

### Raspberry Pi Pico W BME280 WiFi MQTT
IoT node that publishes readings from the BME280 to a MQTT broker.
* WiFi and MQTT re-connect logic.
* Mutual TLS connection.

https://github.com/lafftale1999/raspberry_pi_pico_temp_sensor_reader

---

### ESP32 MQTT Weather Display
IoT node that subscribes to readings from the BME280 via the MQTT broker and then writes them out using the LCD device driver.
* WiFi and MQTT re-connect logic.
* Mutual TLS connection.

https://github.com/lafftale1999/esp32_mqtt_weather_display

---

### Mosquitto MQTT Docker Container
A lightweight Dockerized setup for running a Mosquitto MQTT Broker with support for plaintext, TLS and WebSocket communication.
* Automated setup with Docker Compose
* Generates CA, server and (optional) client certificates
* Supports multiple connection ports:
  * `1883`: plain MQTT (no encryption, no auth)
  * `8883`: MQTT with Mutual TLS
  * `9001`: WebSocket (username/password based)

https://github.com/lafftale1999/Mosquitto_MQTT_Docker

---

### Weather Backend
Server that subscribes to the MQTT broker mentioned in the Docker container and exposes APIs for frontend.
* Spring Boot Rest API
* Sending data to SQL database hosted with Azure
* Subscribes to broker using Eclipse Paho MQTT client

https://github.com/MikaelaDuran/weather-backend

---

### Weather Frontend
Single‑page web dashboard that visualises live & historical sensor data from the backend.
* React and TypeScript
* UI buildt with Tailwind CSS
* Interactive chart with temperature, humidity and pressure
* Date and time picker

https://github.com/MikaelaDuran/weather-frontend

## Thank you
Special thanks to [Nakerlund](https://github.com/nakerlund) and [J0nt3](https://github.com/j0nt392) for your guidance and support! And thank you to [Mikaela](https://github.com/MikaelaDuran) for being an awesome co-intern!
