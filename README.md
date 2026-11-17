# VoltX
# VoltX 
> **Smart Area Metering and Anomaly Alert System**

[![Architecture](https://img.shields.io/badge/Architecture-Microservices-blue)]()
[![AI Engine](https://img.shields.io/badge/AI-PyTorch%20%7C%20Scikit--Learn-orange)]()
[![Signal Processing](https://img.shields.io/badge/Signal-SciPy%20FFT%2FTHD-green)]()
[![Platform](https://img.shields.io/badge/Docker-Compose-brightgreen)]()

---

## Project Overview
**VoltX** is a plant-wide smart factory platform that monitors, analyzes, and manages the entire industrial electrical hierarchy—from the main distribution board down to individual production lines and machines—at less than 5% of traditional sub-metering hardware costs. 

Instead of outfitting 30–100+ machines with costly industrial smart meters, VoltX uses **Single-Point Monitoring** at the main feeder (Microcontroller + PZEM-004T + CT Sensors) combined with a centralized multi-tier AI engine[cite: 2]. It performs high-frequency harmonic analysis via **SciPy**, disaggregates loads using **AI Virtual Sensors (Soft Sensors)**, tracks individual machine efficiency degradation, and localizes faults on a digital **Circuit Topology Graph**[cite: 2].

---

## Five-Layer System Architecture
1. **Layer 1 — Single-Point Edge Acquisition & Hybrid Simulator:** Captures aggregate telemetry (V, I, P, S, PF, Hz, high-rate current windows) over MQTT, alongside a Python synthetic fault and efficiency-drift injection engine[cite: 2].
2. **Layer 2 — SciPy Signal Processing Engine:** Cleans incoming windows and executes Fast Fourier Transform (FFT), Short-Time Fourier Transform (STFT), Total Harmonic Distortion (THD), and transient inrush envelope extraction[cite: 2].
3. **Layer 3 — Centralized AI-Driven Monitoring:** Combines unsupervised baselines (Isolation Forest), interpretable Random Forest (macro Event Behavior with SHAP), PyTorch 1D-CNN (sub-unit winding/bearing faults), and LSTM/GRU (temporal duty cycles and per-machine efficiency degradation tracking)[cite: 2].
4. **Layer 4 — Virtual Sensors & Circuit Topology Graph:** Disaggregates the single-point stream to estimate individual machine states/health and maps anomalies onto a NetworkX Directed Acyclic Graph (DAG) for automated Fault Localization[cite: 2].
5. **Layer 5 — Control, LOTO & Dashboard:** Role-based JWT access control (Maintenance Engineer, Plant Operator, Admin), Dual-Key Safety LOTO, 3-strike overload auto-lockout, automated shift handover reports, and live React dashboards[cite: 2].

---

## Repository Structure
```tree
├── architecture-diagrams/       # System architecture, data flow, and 5-layer diagrams
├── circuit-topology/            # NetworkX graph schemas and factory single-line diagrams
├── uml-diagrams/                # Use Case, Sequence, and Component diagrams
├── hardware-schematics/         # ESP32, PZEM-004T, and CT sensor wiring layouts
├── backend-services/            # Microservices source code (FastAPI, PyTorch, SciPy, MQTT)
├── frontend-dashboard/          # React, Tailwind CSS, and Recharts interfaces
└── docker-compose.yml           # One-command full-stack container orchestration
