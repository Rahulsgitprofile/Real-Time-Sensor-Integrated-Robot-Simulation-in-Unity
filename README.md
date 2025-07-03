# 🤖 RSS Sensor-Driven Unity Game Environment

![Unity](https://img.shields.io/badge/Engine-Unity_2022.3+-black?logo=unity)
![Arduino](https://img.shields.io/badge/Microcontroller-ESP8266-blue?logo=arduino)
![MQTT](https://img.shields.io/badge/Protocol-MQTT-purple?logo=raspberrypi)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)

> A real-time Unity environment controlled using physical sensors via MQTT and ESP8266. Combines embedded systems, wireless protocols, and immersive 3D interaction.

---

## 🎥 Media

### 🖼️ Screenshots

<p align="center">
  <img src="https://github.com/user-attachments/assets/300e968e-693d-4dde-8c06-ce6649c9b72e" alt="Gameplay Screenshot 1" width="350" />
  <img src="https://github.com/user-attachments/assets/92feb680-0b6d-47e0-a294-6d9b5874ac60" alt="Robot Movement" width="650" />
</p>

*Figure 1.* ESP and sensors setup.  
*Figure 2.* Robot walking and jumping in the demo scene using ESP setup.

## 🧭 Overview

This project connects physical sensors to a Unity game scene to control:
- A robot character’s **movement**, **running**, and **jumping**
- In-game **camera direction**
- **Doors** opening and closing based on proximity detection
- A **temperature display** updated in real-time

The microcontroller collects and filters sensor data, then transmits it using MQTT, where Unity listens and acts accordingly. This allows seamless interaction between physical movements and game logic.

---
---

## 🔌 Hardware Setup

- **ESP8266 NodeMCU** – Microcontroller + Wi-Fi
- **MPU6050** – Gyroscope, Accelerometer, Temperature Sensor
- **Rotary Encoder** – Speed control & Jump trigger
- **Infrared Sensor** – Proximity detection for doors
- **Touch Sensor (Capacitive)** – Party mode activation
- Breadboards, jumper wires, USB cables

---

## 🧠 Arduino Logic (ESP_MQTT.ino)

**Responsibilities:**
- Initialize and calibrate sensors
- Establish Wi-Fi + MQTT connection
- Continuously collect data from:
  - MPU6050 (acceleration, gyro, temp)
  - Rotary encoder (speed, jump)
  - IR sensor (proximity)
  - Capacitive sensor (party mode)
- Apply signal **filtering**
- Encode all data to **JSON**
- Publish over **MQTT topics**

---

## 📡 Communication Protocol

### MQTT (Message Queuing Telemetry Transport)

- **Type:** Lightweight, publish-subscribe protocol ideal for low-power IoT
- **ESP8266:** Publishes sensor data to MQTT broker (`sensor/imu`, `sensor/temp`, etc.)
- **Unity:** Subscribes to relevant topics using MQTT client

**Advantages:**
- Reliable real-time messaging
- Low power consumption
- Easy to parse JSON format
- Scalable for multi-device or multi-room applications

---

## 🎮 Unity Integration

### 🦿 Robot Movement

- **MPU6050 Data → Player Movement**  
  - Tilt determines direction  
  - Custom dead zones to prevent idle noise-based movement  
  - Used `Mathf.Floor(Mathf.Sqrt(pitch² + roll²))` for movement threshold
- **Rotary Encoder → Speed Control**  
  - Rotation: player speed  
  - Push button: jump trigger
- **Flash Button → Toggle Modes**  
  - Switch between camera and player control  
  - Uses debounce logic for accuracy

### 📸 Camera Control

- Follows gyroscopic input when toggle is ON
- Jitter eliminated by removing `Time.deltaTime` dependency
- Camera logic modularized from movement logic

### 🚪 Door Control

- **IR Sensor** detects hand or object near door  
- MQTT sends proximity signal → Unity toggles door animation in `Door.cs`

### 🌡️ Temperature Display

- Real-time in-game UI panel
- Reads MPU6050 temp sensor
- Values updated via MQTT (`sensor/temp`)

---

## ✨ Highlighted Features

| Feature                        | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| 🔄 **MQTT Protocol**           | Real-time, efficient communication between ESP8266 and Unity                |
| 🔀 **Toggle System**          | Switch between camera and movement control using onboard button             |
| 🧼 **Debounce Logic**         | Ensures single accurate press per button click                             |
| 🧩 **Singleton Architecture** | Central `SensorValues` script accessed globally across all Unity scripts    |
| 🔧 **Modular Unity Code**     | Separate scripts for movement, camera, UI, door logic                       |
| 🕺 **Party Mode!**            | Capacitive touch sensor triggers an animated “party mode” sequence 🎉       |

---

## 📂 How to Run

### 1. Flash Arduino

- Open `ESP_MQTT.ino` in Arduino IDE  
- Set Wi-Fi SSID/password and MQTT broker IP  
- Install required libraries:
  - `PubSubClient`
  - `Adafruit_MPU6050`
  - `Encoder`
- Flash to ESP8266 using correct COM port

### 2. Set Up Unity

- Open the `Unity/` project in Unity Hub (2022.3+)
- Ensure MQTT client dependencies are resolved (e.g., M2Mqtt)
- In `SensorValues.cs`, set MQTT broker IP and topics
- Press Play and interact using real sensors!

---

## 📌 Notes

- All inputs are smoothed via custom low-pass filtering before action.
- Unity is decoupled from hardware logic—makes it testable with virtual data.
- Door states and UI are updated using event-based listeners for clean state transitions.

---

## 🛠️ Future Extensions


- Web dashboard for MQTT data monitoring
- Haptic feedback / audio events in party mode


---

> 🎮 A full real-time sensor fusion playground. Build. Sense. Play.

