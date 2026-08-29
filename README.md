# Edge AI-Powered PLC Anomaly Detection for Motor Drive Systems

[![Project ID](https://img.shields.io/badge/Project_ID-PRJ__109-blue.svg)](https://github.com/Nidhish-XEA/Edge-Al-Powered-PLC-Anomaly-Detection-for-Motor-Drive-Systems)
[![Category](https://img.shields.io/badge/Category-Software-orange.svg)]()
[![Difficulty](https://img.shields.io/badge/Difficulty-Intermediate-yellow.svg)]()
[![Status](https://img.shields.io/badge/Status-Review--1_Complete-brightgreen.svg)]()
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> **Course**: CSE7102 Mini Project  
> **Institution**: School of Computer Science and Engineering, Presidency University  
> **Repository**: [https://github.com/Nidhish-XEA/Edge-Al-Powered-PLC-Anomaly-Detection-for-Motor-Drive-Systems](https://github.com/Nidhish-XEA/Edge-Al-Powered-PLC-Anomaly-Detection-for-Motor-Drive-Systems)

---

## 📌 Overview

Industrial motor drive systems (powering pumps, industrial fans, compressors, and conveyor belts) are critical assets in manufacturing environments. Unplanned motor failures lead to significant operational downtime, lost productivity, and inflated repair expenditures.

This project introduces an **Edge AI-Powered Anomaly Detection Framework** integrated with existing **Programmable Logic Controllers (PLCs)**. By capturing multi-sensor telemetry (vibration, current, temperature, and RPM) and processing it locally on Edge hardware (e.g., NVIDIA Jetson Nano), the system learns normal operational baselines and identifies early-stage mechanical and electrical degradation—enabling true **Predictive Maintenance (PdM)** without cloud latency or security concerns.

---

## 🛑 Problem Statement

Industrial facilities rely heavily on electric motor drive systems. However, traditional maintenance regimes face critical limitations:

1. **Catastrophic Failure & Downtime**: Bearings wear down, windings overheat, and shafts misalign over time. Unnoticed faults lead to sudden breakdown and expensive halt of production lines.
2. **Inadequacy of Manual Monitoring**: Periodic manual inspections often miss early micro-level signals of mechanical wear between inspection cycles.
3. **Wastefulness of Preventive Maintenance**: Time-based (fixed-schedule) maintenance frequently replaces fully operational, healthy motor components prematurely, incurring unnecessary costs.
4. **Cloud Latency & Connectivity Constraints**: Transmitting high-frequency raw vibration data to cloud servers introduces latency, bandwidth bottlenecks, and operational vulnerability during internet outages.

---

## 💡 Proposed Solution

We propose a non-intrusive, low-latency **Edge AI solution** that directly interfaces with unmodified industrial PLCs and auxiliary sensor arrays:

* **Non-Intrusive Integration**: Interfaces with existing PLCs to read operational state variables without interrupting motor control loops.
* **Multi-Modal Sensing**: Collects vibration (accelerometer), electrical current, surface temperature, and rotational speed (RPM) telemetry.
* **Local Edge Computing**: Runs lightweight machine learning models (e.g., One-Class SVM, Isolation Forest, Autoencoders) on Edge devices (NVIDIA Jetson Nano / Raspberry Pi) for real-time inference.
* **Early Anomaly Detection & Health Scoring**: Computes continuous Motor Health Index (MHI) and classifies states as **Normal**, **Warning**, or **Fault**.
* **Instant Operator Alerts**: Triggers local HMI dashboard indicators, physical beacons (Buzzer/LED), and remote notification dispatches to enable proactive maintenance before failure occurs.

---

## 📐 System Architecture

### Architectural Workflow Diagram

![System Architecture Diagram](./docs/architecture_diagram.png)

*Note: The detailed architectural workflow diagram is available in the [`/docs`](./docs/architecture_diagram.png) directory.*

### Data Flow Summary

```
+-------------------+      +-------------------+      +--------------------------------------------------+
|  Motor + Sensors  |      |   PLC (Existing)  |      |                 EDGE AI DEVICE                   |
| Vibration, Current| ---> | Controls Motor &  | ---> |  Data Acquisition -> Preprocessing & Noise Filter|
| Temp, RPM Signals |      | Generates Data    |      |  -> Feature Extraction (RMS, FFT, Kurtosis)     |
+-------------------+      +-------------------+      |  -> AI Anomaly Model (One-Class / Autoencoder)    |
                                                      |  -> Anomaly Scoring & Motor Health Index         |
                                                      +--------------------------------------------------+
                                                                               |
                                                                               v
+------------------------+      +------------------------------------------------------------------------+
|   Maintenance Action   |      |                             OUTPUT & ALERTS                            |
| Schedule Maint. / Parts| <--- | Real-time Alarm | Local HMI Dashboard | App Notification | Cloud Log  |
+------------------------+      +------------------------------------------------------------------------+
```

### End-to-End Pipeline Stages

1. **Motor Drive & Sensors**: Tri-axial accelerometers, current transformers, thermocouple sensors, and optical tachometers record real-time operational physical quantities.
2. **PLC Data Interface**: Existing industrial PLC manages machine sequencing while streaming operational status (Speed ref, Run time, Motor Load, Output Status) via industrial protocols (Modbus / MQTT).
3. **Edge AI Processing Unit**:
   * **Data Acquisition**: Synchronizes sensor streams and PLC state metrics.
   * **Preprocessing**: Applies bandpass filtering, noise attenuation, windowing, and normalization.
   * **Feature Extraction**: Extracts Time-Domain (RMS, Peak-to-Peak, Kurtosis, Crest Factor) and Frequency-Domain (Fast Fourier Transform - FFT) features.
   * **AI Detection Model**: Unsupervised/semi-supervised ML model evaluates incoming features against baseline patterns of normal operation.
   * **Health Indexing**: Generates anomaly probability score and Motor Health Index (MHI).
4. **Outputs & Operational Alerts**: Visual indicators on local HMI dashboard, instant local alarm triggers, and optional long-term telemetry logging to a central server.
5. **Predictive Maintenance Execution**: Maintenance teams schedule targeted component replacement before failure occurs.

---

## 🛠️ Tech Stack

| Category | Technologies & Tools |
| :--- | :--- |
| **Programming Language** | Python 3.10+ |
| **Data Processing & Analytics** | NumPy, Pandas, SciPy, Librosa |
| **Machine Learning / AI** | Scikit-learn, PyTorch / TensorFlow |
| **Industrial Protocols** | Modbus TCP/RTU, MQTT (Paho-MQTT, PyModbus) |
| **Edge Hardware Platform** | NVIDIA Jetson Nano / Raspberry Pi 4 |
| **Dashboard & HMI** | Streamlit / Flask, Matplotlib, Seaborn |
| **Version Control & Docs** | Git, GitHub, Markdown |

---

## 📊 Dataset & Phase 1 Validation Strategy

In Phase 1 and early Phase 2 (prior to live physical motor testbed integration), model training and performance validation will leverage the **Case Western Reserve University (CWRU) Bearing Dataset**—the globally recognized benchmark for bearing fault diagnostics.

* **Dataset Features**: High-frequency drive-end and fan-end accelerometer vibration signals.
* **Fault Classifications**: Normal baseline operation vs. Inner Race, Outer Race, and Ball element defect conditions.
* **Defect Severities**: Damage diameters of 0.007", 0.014", 0.021", and 0.028" under motor loads ranging from 0 HP to 3 HP.
* **Purpose**: Simulates real-world motor bearing degradation with industry-standard fidelity to validate feature extraction pipelines and anomaly detection models.

---

## 📅 Project Roadmap & Gantt Chart

### Project Schedule Timeline (September – November 2026)

![Project Gantt Chart](./docs/gantt_chart.png)

*Note: The complete execution timeline is tracked via the project Gantt chart located in [`/docs`](./docs/gantt_chart.png).*

### Execution Milestones

- [x] **Phase 1: Problem Definition & Requirements** *(07 Sep – 10 Sep 2026)*
- [x] **Phase 2: Literature Review & Dataset Study** *(10 Sep – 21 Sep 2026)*
- [x] **Phase 3: System Architecture Design** *(16 Sep – 24 Sep 2026)*
- [ ] **Phase 4: Data Collection / Dataset Preparation** *(21 Sep – 03 Oct 2026)*
- [ ] **Phase 5: Data Preprocessing & Feature Extraction** *(28 Sep – 14 Oct 2026)*
- [ ] **Phase 6: AI Model Development** *(04 Oct – 22 Oct 2026)*
- [ ] **Phase 7: Model Training & Evaluation** *(19 Oct – 30 Oct 2026)*
- [ ] **Phase 8: PLC Data Integration / Simulation** *(25 Oct – 09 Nov 2026)*
- [ ] **Phase 9: Edge AI Deployment** *(01 Nov – 16 Nov 2026)*
- [ ] **Phase 10: Anomaly Detection & Alert Module** *(08 Nov – 20 Nov 2026)*
- [ ] **Phase 11: Testing & Performance Evaluation** *(15 Nov – 29 Nov 2026)*
- [ ] **Phase 12: Documentation & Final Report** *(22 Nov – 30 Nov+ 2026)*

> 📍 **Current Project Status**: **Review-1 Completed** (Problem Definition, Literature Review, Architecture Design, and Execution Planning finalized. Implementation phase commencing next).

---

## 📁 Repository Directory Structure

```
Edge-AI-Powered-PLC-Anomaly-Detection-for-Motor-Drive-Systems/
├── docs/                      # Architectural diagrams, Gantt chart, literature review
│   ├── architecture_diagram.png
│   ├── gantt_chart.png
│   ├── literature_review.pdf
│   └── README.md
├── data/                      # Dataset documentation and local data placeholders
│   └── README.md
├── src/                       # Modular Python source code (Phase 2 implementation)
│   └── README.md
├── notebooks/                 # Jupyter notebooks for EDA and model prototyping
│   └── README.md
├── .gitignore                 # Python gitignore configuration
├── requirements.txt           # Dependency management (Phase 2 setup)
└── README.md                  # Main project repository documentation
```

---

## 👥 Project Team & Supervision

### Student Team Members (B.Tech Computer Science & Engineering)

| Name | Roll Number / USN | Role | GitHub Profile |
| :--- | :--- | :--- | :--- |
| **Nidhish K** | 20231COM0172 | System Architecture & Edge AI Lead | [@Nidhish-XEA](https://github.com/Nidhish-XEA) |
| **Nishan Suresh Mesta** | 20231COM0167 | Signal Processing & Feature Engineering | [@NishanMesta](https://github.com/NishanMesta) |
| **Roopa K A** | 20231COM0187 | PLC Integration & Dashboard Development | [@RoopaKA](https://github.com/RoopaKA) |

### Project Supervisor

* **Ms. Pathan Tasneem Farhana**  
  *Assistant Professor*  
  Department of Computer Science and Engineering  
  School of Computer Science and Engineering, Presidency University, Bengaluru

---

## 📜 License

This project is licensed under the [MIT License](LICENSE) - see the standard license terms for details.

---
*Created for **CSE7102 Mini Project (PRJ_109)**, Presidency University, School of Computer Science and Engineering.*
