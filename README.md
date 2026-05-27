# CAN Bus Network Packet Communication Simulator & Priority Analyzer

A dual-framework (Python & MATLAB) in-vehicle Controller Area Network (CAN) simulator designed to model multi-ECU data transmission, simulate packet stream generation, and analyze bit-level physical priority arbitration logic.

## 📌 Project Overview
In modern automotive engineering, Electronic Control Units (ECUs) communicate over a shared CAN bus topology. Because the medium is shared, multiple ECUs frequently attempt to broadcast frames simultaneously. This project provides a comprehensive, storage-optimized cloud implementation analyzing how network prioritization prevents data destruction during microsecond-level frame collisions.

### Simulated Vehicle Nodes
* **Powertrain Control Module (PCM)** | **CAN ID: `0x100`** (High Priority) — Tracks rapid, dynamic fluctuations in Engine RPM.
* **Battery Management System (BMS)** | **CAN ID: `0x200`** (Medium Priority) — Tracks High-Voltage Battery State-of-Charge (SoC) drawdown.
* **Instrument Cluster Dashboard (IPC)** | **CAN ID: `0x300`** (Low Priority) — Tracks ambient cabin climate telemetry.

---

## 🛠️ System Architecture & Frameworks

This repository demonstrates protocol engineering using two distinct programming approaches:

### 1. Bit-Level Functional Simulation (Python / Google Colab)
* Implements a custom, native-logic simulator verifying the **wired-AND / wired-OR** open-drain transceiver dynamics.
* Models the clock-synchronized bit evaluation process where **Dominant bits (`0`)** systematically overwrite **Recessive bits (`1`)**.
* Proves protocol determinism by demonstrating zero-loss data preservation for the highest priority message during frame collisions.

### 2. Time-Domain Signal Telemetry (MATLAB / MATLAB Online)
* Models continuous automotive sensor waveforms over a synchronous simulation timescale.
* Packs real-time floating-point measurements into standardized hex payload data configurations across specified cycle frequencies ($10\text{ ms}$, $20\text{ ms}$, $50\text{ ms}$).
* Generates an object-oriented network bus packet analyzer trace log table and an advanced interactive diagnostic graphical dashboard.

---

## 📁 Repository Directory Structure

```text
CAN-Bus-Network-Simulator/
├── LICENSE
├── README.md
├── python_simulator/
│   ├── CAN_Bus_Arbitration_Simulator.ipynb
│   └── requirements.txt
└── matlab_simulator/
    ├── ECU_Network_Model.mlx
    └── can_bus_signals.mat
