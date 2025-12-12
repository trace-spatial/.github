# Trace

**Offline-first spatial intelligence for finding lost objects through behavioral prediction.**

Trace reconstructs human movement patterns and detects cognitive disruptions to predict where you likely placed misplaced items—no cameras, no tags, no tracking. All intelligence runs on-device. Privacy is the foundation, not a feature.

---

## The Problem

You don't lose your keys because they moved. You lose them because your attention slipped the moment you set them down. Trace identifies these cognitive interruptions and maps them to physical locations in your space.

---

## How It Works

**1. Continuous Sensing**  
The sensing engine captures IMU data, reconstructs steps and turns, and generates movement episodes as you move through your environment.

**2. Zone Mapping**  
Environmental fingerprints (Wi-Fi, BLE) build a topological map of interaction zones—your desk, kitchen counter, sofa—without GPS or cameras.

**3. Behavioral Scoring**  
CEBE-X analyzes routine stability and attention breaks. It knows when you deviated from normal patterns.

**4. Prediction**  
When you ask "Where are my keys?", on-device inference surfaces the most likely zone based on movement history and behavioral disruptions.

**5. Visualization**  
The White Void UI highlights predicted zones with confidence indicators and optional guidance paths.

**6. Secure Collaboration (Optional)**  
If you misplaced something at a friend's house, Azure Confidential Computing matches your trace against their space map—zero-knowledge, encrypted end-to-end. Neither party sees the other's data.

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        Trace System                         │
└─────────────────────────────────────────────────────────────┘

┌──────────────┐      ┌──────────────┐      ┌──────────────┐
│  Mobile App  │◄────►│    Sensing   │◄────►│     Zone     │
│   (React     │      │    Engine    │      │    Mapper    │
│   Native)    │      │  (Rust Core) │      │ (Topo Graph) │
└──────┬───────┘      └──────────────┘      └──────┬───────┘
       │                                             │
       │              ┌──────────────┐               │
       └─────────────►│   CEBE-X     │◄──────────────┘
                      │  (Behavior   │
                      │   Model)     │
                      └──────┬───────┘
                             │
                      ┌──────▼───────┐
                      │  White Void  │
                      │      UI      │
                      └──────────────┘

Optional: Azure Confidential Computing Enclave
┌─────────────────────────────────────────────────────────┐
│  Zero-knowledge spatial matching between guest and host │
│  Private data never leaves the secure enclave           │
└─────────────────────────────────────────────────────────┘
```

---

## Repository Structure

| Repository | Visibility | Purpose |
|-----------|------------|---------|
| `trace-app` | Public | React Native app with White Void UI, inference pipeline, encrypted storage |
| `trace-sensing-engine` | Public | Rust/Swift/Kotlin engine for IMU processing, stance detection, PDR |
| `trace-zone-mapper` | Private | Privacy-preserving topological graph builder from Wi-Fi/BLE fingerprints |
| `trace-cebe-x-engine` | Private | Behavioral scoring engine for object placement inference |
| `trace-collab-secure-service` | Private | Azure Confidential Computing service for secure cross-user matching |

---

## Technology Stack

**Mobile:** React Native (TypeScript), Skia/GL for rendering  
**Native Engine:** Rust, Swift, Kotlin  
**Inference:** ONNX Runtime Mobile, TFLite (INT8 quantized)  
**Backend:** Azure Confidential Computing, Azure App Service  
**Storage:** Encrypted SQLite  
**ML Training:** Python, PyTorch, ONNX export

---

## Key Features

- Fully offline-first architecture
- No cameras, hardware tags, or continuous cloud sync
- Behavioral inference, not object tracking
- Privacy-preserving topological mapping
- Zero-knowledge secure collaboration
- Quantized on-device ML models
- Battery-efficient burst sampling with motion coprocessor integration

---

## Current Status

**MVP in Development:**

- Sensing engine API and native bindings complete
- Zone mapping prototypes functional (Python + TypeScript)
- CEBE-X scoring functions defined
- White Void UI components in progress
- Enclave handshake protocol designed

The MVP demonstrates the full sensing pipeline, cognitive scoring loop, and zone prediction interface.

---

## Design Principles

- Privacy-first and offline-first
- Explainable, human-centered predictions
- Modular, testable microservices
- Minimal cloud footprint
- Energy-efficient sensing architecture

---

## Team

Trace represents the engineering and research work developed for Imagine Cup and experimental deployments.

---

## Getting Started

Documentation for setup, architecture deep-dives, and API references coming soon.

For questions or collaboration inquiries, open an issue in the relevant repository.