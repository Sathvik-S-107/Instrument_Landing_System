# 🛬 Instrument Landing System (ILS) Using Fused Sensors

A hardware-based Instrument Landing System prototype that integrates a magnetometer + gyroscope with an STM32 microcontroller to estimate aircraft orientation and landing approach, aiming to reduce EMI-related inaccuracies seen in antenna-based ILS systems.

---

## 🚀 Overview

Conventional ILS systems rely on radio antennas placed near runways. Their close proximity may cause electromagnetic interference (EMI), distorting glide-slope data and increasing landing risk.

This project proposes an alternative/add-on system using:
✅ Inertial measurement (IMU + magnetometer)  
✅ STM32-based processing  
✅ Custom PCB  

This enables angle/heading estimation without dependence on RF systems.

---

## ✨ Features
- Sensor-fusion based ILS assistance
- STM32 processing
- Magnetometer + Gyroscope integration
- PCB design + fabrication (KiCad / Flux)
- IMU + Magnetometer offset calibration
- Real-time heading + angular output

---

## 📁 Project Structure

---

## 🧰 Hardware Components

| Component | Description |
|-----------|-------------|
| STM32 MCU | Core controller |
| MPU6050   | IMU – Gyro + Accelerometer |
| LIS3MDL   | Magnetometer |
| DS3231M   | Real-Time Clock |
| Custom PCB | Sensor & signal stage |

---

## 🔄 System Flow

Sensors → Sensor-Fusion → STM32 → Landing Guidance Output

---

## 🧾 Calibration Script (Node.js)

This script reads gyro + magnetometer raw data from STM32 over serial, collects samples, and computes offsets.

```js
const SerialPort = require('serialport');
const Readline = require('serialport/parser-readline');

const port = new SerialPort('/dev/ttyUSB0', { baudRate: 115200 });
const parser = port.pipe(new Readline({ delimiter: '\n' }));

let gyroOffsets = [0, 0, 0];
let magOffsets = [0, 0, 0];
let gyroData = [];
let magData = [];

// Number of calibration samples
const NUM_SAMPLES = 1000;

function parseData(data) {
  const [type, x, y, z] = data.split(',').map(Number);
  if (type === 0) {
    gyroData.push([x, y, z]);
  } else if (type === 1) {
    magData.push([x, y, z]);
  }
}

function calculateOffsets() {
  // Gyroscope calibration
  let gyroSum = [0, 0, 0];
  gyroData.forEach(([x, y, z]) => {
    gyroSum[0] += x;
    gyroSum[1] += y;
    gyroSum[2] += z;
  });
  gyroOffsets = gyroSum.map(sum => sum / gyroData.length);

  // Magnetometer calibration
  let magMin = [Infinity, Infinity, Infinity];
  let magMax = [-Infinity, -Infinity, -Infinity];
  magData.forEach(([x, y, z]) => {
    magMin[0] = Math.min(magMin[0], x);
    magMin[1] = Math.min(magMin[1], y);
    magMin[2] = Math.min(magMin[2], z);
    magMax[0] = Math.max(magMax[0], x);
    magMax[1] = Math.max(magMax[1], y);
    magMax[2] = Math.max(magMax[2], z);
  });

  magOffsets = magMax.map((max, i) => (max + magMin[i]) / 2);

  console.log('Gyro Offsets:', gyroOffsets);
  console.log('Mag Offsets:', magOffsets);
}

parser.on('data', line => {
  parseData(line.trim());
  if (gyroData.length >= NUM_SAMPLES && magData.length >= NUM_SAMPLES) {
    calculateOffsets();
    port.close(); // Stop after calibration
  }
});

port.on('open', () => {
  console.log('Serial Port Opened');
  port.write('START_CALIBRATION\n');
});

port.on('error', err => {
  console.error('Error:', err.message);
});
```
-------------------------------------
## ✅ Results
- Schematic validated
- PCB designed + fabricated
- Magnetometer + IMU functional
- Heading + angle extracted
- System ready for testing

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
