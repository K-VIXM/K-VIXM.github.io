<div align="center">

# VIXM (Vertiport Information Exchange Model)
**The Global Data Exchange Standard for Vertiports & Advanced Air Mobility (AAM)**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Standard Draft](https://img.shields.io/badge/Version-v1.0--Draft-cyan.svg)](#)
[![Web](https://img.shields.io/badge/Official_Site-k--vixm.github.io-0ea5e9.svg)](https://k-vixm.github.io/)

</div>

---

## 📌 Overview

**VIXM (Vertiport Information Exchange Model)** is an open, standardized information exchange model tailored specifically for Advanced Air Mobility (AAM) and Urban Air Mobility (UAM) ground infrastructures. 

Just as traditional aviation relies on **AIXM** (Aeronautical), **FIXM** (Flight), and **WXXM** (Weather), **VIXM** fills the missing infrastructure-side gap by standardizing the digital representation of vertiport physical layouts, dynamic operational availability, and tactical turnaround constraints.

---

## 🌐 The *IXM Ecosystem

VIXM is engineered to operate seamlessly within the global **SWIM (System Wide Information Management)** concept and UAM traffic management architectures (PSU/USS):

| Standard | Domain | Core Focus | Target Systems |
| :--- | :--- | :--- | :--- |
| **AIXM** | Aeronautical Information | Airspace, Routes, Traditional Aerodromes | AIS, NOTAM, ATM |
| **FIXM** | Flight Information | 4D Trajectories, Flight Intent, Flow Planning | ATC, Airline AOC, PSU |
| **IWXXM** | Weather Information | Meteorological Observations & Forecasts | MET Providers, Flight Dispatch |
| **VIXM** | **Vertiport Information** | **TLOF/FATO Geometry, Real-time Slot & Charger State** | **VPO, Fleet Operators, PSU/USS** |

---

## 🚀 Core Features

### 1. Static Infrastructure Model
* **Geometric & Physical Bounds:** Precise spatial definitions of TLOF, FATO, Safety Areas, and Obstacle Limitation Surfaces (OLS/OIS).
* **Vertiport Identification:** Standardized naming, spatial coordinates, geographic elevations, and access corridors.
* **Ground Facilities:** Gate layouts, passenger boarding bridges, charging pads, and emergency egress routing.

### 2. Dynamic Operational Model
* **Pad & Gate Availability:** Real-time occupancy status, scheduled occupancy windows, and turnaround durations.
* **Resource Readiness:** EV charging power limits, battery swap station health, fire suppression readiness, and MRO capabilities.
* **Tactical Restrictions:** Local surface wind threshold exceedances, micro-weather hazards, and temporary operating holds.

### 3. Interoperability & Schema Design
* **Standard Schemas:** Fully modeled in UML with derived **XML (GML-compliant)** and **JSON Schema** payloads.
* **API Compatibility:** Optimized for modern RESTful / gRPC microservices and asynchronous message brokers (MQTT/AMQP).

---

## 📂 Repository Structure

```text
├── docs/                # Architecture diagrams, specifications, and whitepapers
├── schemas/             # Formal schema definitions
│   ├── xsd/             # XML Schema Definitions (GML profile)
│   └── json/            # JSON Schema definitions
├── examples/            # Sample payloads (Static Vertiport & Dynamic State)
├── uml/                 # Enterprise Architect / Papyrus UML models
└── README.md
