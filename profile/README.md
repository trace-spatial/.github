```markdown
# Trace

Trace builds offline-first, privacy-preserving spatial intelligence systems. Our work focuses on reconstructing human movement, detecting cognitive disruptions, and inferring object placement events without cameras or hardware tags. All core intelligence runs on-device, supported by a modular microservice ecosystem and secure collaboration flows built on Azure Confidential Computing.

Trace approaches the lost-object problem from a behavioral perspective. Objects rarely move spontaneously; they move when attention breaks. By combining inertial navigation, behavioral modeling, and topological mapping, Trace estimates where an item was most likely placed based on a user’s movement and routine stability.

---

## System Overview

Trace runs as a sequence of on-device engines connected through lightweight, encrypted data flows. Only the secure collaboration module touches the cloud, and even then, only in a zero-knowledge manner.

### High-Level Architecture Diagram

```

┌──────────────────────────────────────────────────────────────────┐
│                              Trace                               │
└──────────────────────────────────────────────────────────────────┘

┌──────────────┐       ┌──────────────────┐       ┌───────────────────────┐
│  Mobile App  │       │  Sensing Engine  │       │    Zone Mapper        │
│ (ReactNative)│◄──────┤ (Rust + Bindings)├──────►│  (Topo Graph Builder) │
└──────┬───────┘       └────────┬─────────┘       └───────────┬──────────┘
│                        Episodes                       Zones
│                            │                            │
│                            ▼                            │
│                   ┌────────────────┐                    │
│                   │  CEBE-X Engine │◄───────────────────┘
│                   │(Behavior Model)│
│                   └───────┬────────┘
│                        Predictions
▼                            │
┌──────────────────┐                │
│   White Void UI  │◄──────────────┘
│ (Visualization)  │
└──────────────────┘

Optional Secure Collaboration Flow
┌───────────────────────────────────────────────────────────────────┐
│ trace-collab-secure-service (Azure Confidential Computing Enclave)│
│ Performs zero-knowledge matching between guest traces and host    │
│ zone graphs. No private data ever leaves the enclave.             │
└───────────────────────────────────────────────────────────────────┘

```

---

## Core Problem

People do not lose objects because the object moves. They lose them because their attention slips for a moment at the exact time they place the object down. Trace identifies these cognitive interruptions and uses them to infer where a misplaced item is likely located.

---

## How Trace Works (Use-Case Walkthrough)

1. The user moves through their home.
2. The sensing engine captures short bursts of IMU data, reconstructs steps, stance phases, and turns, and emits movement episodes.
3. The zone mapper detects stable environmental fingerprints and builds a compact topological map of interaction zones (sofa, desk, kitchen island).
4. CEBE-X scores behavior for routine stability, boundary transitions, and attention disruptions.
5. When the user asks “Where are my keys?”, the app performs on-device inference to surface the most likely zone based on their earlier movement and the moment their routine broke.
6. The UI visualizes this as a pulsing red zone with an optional guidance path.
7. If the item was misplaced in someone else’s home, a zero-knowledge collaboration process through Azure Confidential Computing performs secure matching without revealing any maps or traces.

---

## Azure Integration Overview

Trace uses Azure in a minimal, privacy-preserving manner:

- **Azure Confidential Computing (TEE):** Enables secure guest–host matching when searching for objects in another user’s space without exposing private maps or traces.
- **Azure App Service (Gateway):** Provides a lightweight relay for encrypted data transfer and enclave attestation.
- **Optional:** Azure Managed Identity for secure enclave access and model distribution management.

The core sensing, mapping, and inference pipelines run fully offline on the device.

---

## Repository Structure

| Repository                   | Visibility | Purpose |
|-----------------------------|------------|---------|
| trace-app                   | Public     | React Native mobile application with the White Void UI, on-device inference pipeline, and encrypted storage. |
| trace-sensing-engine        | Public     | Rust/Swift/Kotlin native engine for IMU processing, orientation fusion, stance detection, and PDR. |
| trace-zone-mapper           | Private    | Builds privacy-preserving topological graphs from Wi-Fi/BLE fingerprints and kinematic transitions. |
| trace-cebe-x-engine         | Private    | Behavioral engine computing CSI, BLS, ADS, and ranking zones for object placement inference. |
| trace-collab-secure-service | Private    | Azure Confidential Computing enclave service for zero-knowledge cross-user spatial matching. |

---

## Key Features

- Offline-first architecture
- No cameras, no tags, no continuous cloud
- Behavioral inference rather than object tracking
- Privacy-preserving topological mapping
- Secure zero-knowledge collaboration
- Quantized on-device ML
- Battery-aware sensing architecture with motion-coprocessor integration

---

## Technology Stack

- **Mobile:** React Native (TypeScript), Skia/GL for spatial rendering  
- **Native Engine:** Rust, Swift, Kotlin  
- **Inference:** ONNX Runtime Mobile, TFLite (INT8 quantized)  
- **Backend:** Azure Confidential Computing, App Service  
- **Storage:** Encrypted SQLite  
- **ML Training:** Python, PyTorch, ONNX export, DP aggregation (optional)

---

## MVP Status

- Sensing engine API and bindings scaffolded  
- Zone mapping prototypes in Python and TypeScript  
- Early CEBE-X scoring functions defined  
- White Void UI components in development  
- Enclave handshake protocol designed  

The MVP focuses on the sensing pipeline, the cognitive scoring loop, and a functional UI demonstrating zone prediction.

---

## Development Principles

- Privacy-first and offline-first  
- Explainable predictions  
- Human-centered behavioral modeling  
- Modular and testable microservices  
- Minimal cloud footprint  
- Energy efficiency through burst sampling and hardware offload  

---

## Team

Trace represents the engineering and research work behind the Trace system, developed for Imagine Cup and related experimental deployments.
```
