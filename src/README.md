# Source Code Directory (`/src`)

This directory will house the modular Python source code for the **Edge AI-Powered PLC Anomaly Detection System**.

## Planned Architecture & Modules (Phase 2 & Phase 3)

- **`data_loader.py`**: Modules for loading, parsing, and streaming CWRU Bearing Dataset signals and simulated PLC signals.
- **`preprocessing.py`**: Signal noise filtering, normalization, sliding window framing, and Fast Fourier Transform (FFT) preprocessing.
- **`feature_extraction.py`**: Time-domain (RMS, Peak, Kurtosis, Crest Factor) and Frequency-domain statistical feature extraction.
- **`models/`**: Anomaly detection model implementations (One-Class SVM, Isolation Forest, Autoencoders, LSTM-Autoencoder).
- **`edge_deploy/`**: Lightweight inference runtime engine optimized for Edge AI hardware (NVIDIA Jetson Nano / Raspberry Pi).
- **`protocols/`**: Industrial communication handlers (Modbus TCP/RTU & MQTT protocol interface).
- **`dashboard/`**: Streamlit / Flask local HMI dashboard for real-time motor health index visualizer and alert management.

---
> **Status**: Review-1 Phase Complete. Module implementation will begin in Phase 2 (Data Preprocessing & Feature Extraction).
