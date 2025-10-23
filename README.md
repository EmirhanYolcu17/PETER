# PETER — Soft-Pneumatic Modular Platform (Closed-Loop Control)

**Summer Research Project — Universidad Politécnica de Madrid (UPM), CAR Robotics & Cybernetics**  
**Period:** June 2025 – July 2025  
**Researcher:** Emirhan Yolcu (METU)  
**Mentor:** Jorge Garcia Samartin (PhD)  
**Supervisor:** Prof. Dr. Antonio Barrientos

---

## 🎯 Introduction

PETER is a modular soft-pneumatic platform capable of regulating its pose (pitch–roll–height) using inflatable legs with sensor-based closed-loop control. The system was first implemented in a **single-module configuration**, then extended to a **two-module architecture** with independent sensing and actuation.

![Single-module early prototype](media/photos/image1.png)

The primary objective of the internship was to develop the full kinematic control pipeline, implement real-time feedback stabilization, and perform validation using OptiTrack motion capture.

---

## ⚙️ System Overview

The platform consists of:
- Three soft-pneumatic legs per module  
- IMU and ToF sensing for orientation and height feedback  
- MATLAB-based inverse/forward kinematic mapping  
- Arduino for valve actuation and sensor interfacing  
- Optional multi-module architecture with shared Cartesian commands

![Two-module assembly](media/photos/image4.png)

All computation for (x,y,h) → (p,r,h) → leg lengths is done in MATLAB, while the timing of valve commands runs on Arduino.

---

## 🧭 Single-Module Closed-Loop Architecture

![Single loop architecture](media/diagrams/single_loop.png)

Workflow:
1) Desired (x,y,h) → `xyh_to_prh` → (p,r,h)  
2) (p,r,h) → `prh_to_leg_heights` → target legs  
3) IMU+ToF → measured (p,r,h)  
4) Error computed → P controller → valve commands

The loop continues until the platform stabilizes at the commanded spatial location.

---

## 🧩 Two-Module Architecture

![Dual loop architecture](media/diagrams/dual_loop.png)

In the dual-module setup:
- Top-level leg lengths are split across both modules  
- Each module has its **own IMU + ToF** and closes its own loop  
- I²C conflicts are resolved with hardware & software re-addressing  

This enables scalable multi-segment soft robotic structures.

---

## 🧮 Kinematic Functions

- `xyh_to_prh` — inverse mapping using nonlinear cost minimization (`fminsearch`)
- `prh_to_leg_heights` — Rodrigues-based forward kinematics for actuator lengths
- `prh_to_xyh` — Cartesian back-projection for feedback and validation

These three functions form the computational backbone of the controller.

---

## ✅ Validation & Experiments

Two validation stages were conducted:

**(1) Disturbance Rejection Test at (0,0)**  
External pushes applied — system recovers to neutral point.  
Video: https://youtube.com/shorts/rUIRMNMMSJA?feature=share

**(2) OptiTrack Laboratory Validation**  
Ground truth pose from OptiTrack was compared to reconstructed pose from measured (p,r,h).

![OptiTrack comparison](media/results/image5.png)

IMU data proved stable enough for control. ToF readings were noisier — alternative height sensing is recommended.

---

## 📈 Full Report (PDF)

[📄 **Open Full Report**](docs/PETER_Project_Summer_Internship_Report.pdf)

The report includes detailed derivations, diagrams, test procedures, OptiTrack validation, and improvement plan.

---

## 🚀 Future Work

- System identification of PETER using excitation signals  
- LQR / PD / filtered PI & anti-windup trials  
- I²C multiplexer for reliability and cleaner wiring  
- Better height sensing alternatives to ToF  
- Modular extension beyond two-segment structure

---

## 🏛️ Credits

This work was conducted at **UPM — CAR Robotics & Cybernetics Lab**  
Mentored by **Jorge Garcia Samartin** and supervised by **Prof. Antonio Barrientos**

---
