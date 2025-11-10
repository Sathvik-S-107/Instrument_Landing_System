# 🛬 Instrument Landing System (ILS) using Fused Sensors

A hardware-based Instrument Landing System prototype using fused inertial sensors (magnetometer + gyroscope) and an STM32 microcontroller to estimate aircraft landing path and reduce EMI-related guidance errors.

-------------------------------------
## 🚀 Objective
Develop an ILS-like landing guidance system using:
- STM32
- MPU6050 (Gyro + Accelerometer)
- LIS3MDL (Magnetometer)
- Custom PCB
- Sensor fusion algorithms

-------------------------------------
## 📌 Motivation
Traditional ILS uses antennas placed closely, causing:
- Electromagnetic interference (EMI)
- Glide slope distortion
- Pilot misguidance
- Higher landing risk

Our fused sensor approach reduces EMI and provides reliable landing guidance.

-------------------------------------
## ✨ Features
- STM32-based control
- IMU + magnetometer fusion
- Custom PCB design + fabrication
- EMI-tolerant navigation data
- Heading + angular output
- Real-time sensing

-------------------------------------
## 📁 Project Structure
ILS-Fused-Sensors/
│
├── hardware/
│   ├── schematics/
│   ├── pcb/
│
├── firmware/
│   ├── src/
│   ├── include/
│
├── docs/
└── README.md

-------------------------------------
## 📡 Background
ILS supports landing using:
- Localizer → horizontal guidance
- Glide slope → vertical guidance

Antenna interference distorts glide-slope signals → risky landings.  
This project explores IMU-based replacement/backup to avoid EMI.

-------------------------------------
## 🧰 Hardware Used
STM32 MCU  
MPU6050  
LIS3MDL Magnetometer  
DS3231M RTC  
Voltage Divider  
Custom PCB  

-------------------------------------
## 🛠️ Methodology
1) Sensor acquisition  
2) Schematic design  
3) PCB layout  
4) Fabrication  
5) Assembly  
6) Sensor fusion  
7) Output analysis  

-------------------------------------
## 🔄 System Flow
Sensors → Fusion → STM32 → Landing guidance output  

-------------------------------------
## ✅ Results
- Schematic validated
- PCB designed + fabricated
- Magnetometer + IMU functional
- Heading + angle extracted
- System ready for testing

-------------------------------------
## 📊 Discussion
Pros:
- EMI-free  
- Compact hardware  
- Accurate heading  

Cons:
- Requires calibration
- Magnetic disturbances affect accuracy  

-------------------------------------
## 🔮 Future Work
- Kalman filtering
- Flight sim integration
- Hybrid RF + fused-sensor design
- ML-based correction
- Real aircraft testing

-------------------------------------
## 👨‍💻 Team
Shashank B  
S. Vaishnavi  
Sathvik S  

Under guidance of  
Mrs. Bhavana HT  
BMSCE, ECE Dept.

-------------------------------------
## 📄 References
Available in report.
