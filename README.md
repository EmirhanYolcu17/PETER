# PETER — Soft-Pneumatic Modular Platform (Closed-Loop Control)

**Summer Research Project — Universidad Politécnica de Madrid (UPM), CAR Robotics & Cybernetics**  
**Project Period:** June 2025 – July 2025  
**Researcher:** Emirhan Yolcu (METU)  
**Mentor:** Jorge Garcia Samartin (PhD)  
**Supervisor:** Prof. Dr. Antonio Barrientos

---

## 🎥 Demonstrations

**Disturbance Rejection Test (Closed-loop):**  
https://youtube.com/shorts/rUIRMNMMSJA?feature=share

*(Insert additional test links here if added later)*

---

## 📡 Project Overview

**PETER** is a soft-pneumatic, modular parallel platform capable of actively regulating its pose (pitch–roll–height) through inflatable actuators. The system uses **IMU** and **Time-of-Flight sensors** for real-time feedback and maintains a commanded Cartesian center location via a closed-loop controller.

The platform was first implemented in a **single-module configuration**, then extended to a **two-module architecture** with separate feedback on each module.

---

## ⚙️ System Architecture

The system consists of:

1. **Pneumatic Actuation Module** — 3 inflatable legs per module, with directional valves  
2. **Sensor Suite** — IMUs for (p,r), ToF for height, I²C multi-device handling  
3. **Control Layer (MATLAB)** — Cartesian → (p,r,h) → leg lengths → valve commands  
4. **Embedded Layer (Arduino)** — Solenoid valve timing, ToF re-addressing, IMU sampling  
5. **Validation Setup** — OptiTrack motion capture with MATLAB-based reprojection & comparison

---

## 🧩 Single vs Two-Module Control

### **Single-Module**

- Global (x,y,h) target is converted to platform orientation and leg heights  
- One IMU + one ToF sensor provide feedback  
- P controller closes the loop

### **Two-Module**

- Required leg lengths are split across modules  
- Each module uses its own IMU + ToF for independent regulation  
- I²C conflicts resolved via electrical & software re-addressing

---

## 📐 Core Algorithms

- **`xyh_to_prh`** — inverse kinematics (MATLAB, cost minimization via `fminsearch`)
- **`prh_to_leg_heights`** — forward mapping from orientation to actuator space
- **`prh_to_xyh`** — back-projection for validation & IMU-based comparison

All mappings are used inside the real-time loop for error evaluation and actuator driving.

---

## ✅ Experimental Validation

Two-stage evaluation was conducted:

1) **Disturbance Rejection at (0,0)**  
Platform maintains equilibrium under external push  
→ Video linked above

2) **OptiTrack-Based Validation**  
Orientation and reconstructed center point compared against motion-capture ground truth  
→ Scripts available under `code_matlab/Validation`

---

## 🚀 Roadmap

- Experimental system-identification of PETER for model-based design  
- Alternative control (PD/LQR, filtered PI, anti-windup)  
- Use of I²C multiplexer for cleaner wiring & stable addressing  
- Replacement of ToF with higher-fidelity distance sensing

---

## 🏛️ Acknowledgements

Work conducted at **UPM — CAR Robotics & Cybernetics Laboratory**  
Mentored by **Jorge Garcia Samartin**, supervised by **Prof. Barrientos**  
Prepared as part of a funded summer research internship (2025)

---
