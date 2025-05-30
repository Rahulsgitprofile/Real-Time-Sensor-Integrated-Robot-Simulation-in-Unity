# Real-Time-Sensor-Driven-Robot-Simulation
Real-Time Sensor-Driven Robot Simulation in Unity



#🦾 Real-Time Sensor-Driven Robot Simulation in Unity
> Project | Robotic Sensor Systems 
> Technologies: Unity 2022.3, ESP8266 (Arduino C++), MQTT (Mosquitto), C#

This project demonstrates **real-time integration of embedded sensor systems** with a 3D game environment using Unity. The goal was to simulate a responsive robotic system where physical sensor data from an **ESP8266 microcontroller** drives actions in a virtual world.



=====


> **University Project – Robotic Sensor Systems, Winter Semester 2024/25**  
> Master's Program in Robotics Systems Engineering, RWTH Aachen University



## 🔧 Features

### Embedded System (ESP8266 with Arduino IDE)
- Acquired real-time data from:
  - **MPU6050**: Gyroscope, Accelerometer, Temperature sensor
  - **Capacitive sensor**: Touch detection
  - **Rotary Encoder**: Directional input
  - **Infrared Sensor**: Proximity detection
- Implemented signal filtering (e.g., moving average, threshold filters)
- Established **Wi-Fi communication** using **MQTT protocol (Mosquitto broker)**
