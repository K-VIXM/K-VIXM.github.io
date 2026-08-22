<div align="center">

# VIXM & UIXM Standard Initiative
**The Open Data Exchange Standards for Vertiports & Urban Air Mobility (AAM/UAM)**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Standard Draft](https://img.shields.io/badge/Version-v1.0--Draft-cyan.svg)](#)
[![Web](https://img.shields.io/badge/Official_Site-k--vixm.github.io-0ea5e9.svg)](https://k-vixm.github.io/)

</div>

---

## 📌 Overview

**VIXM (Vertiport Information Exchange Model)** and **UIXM (UAM Flight Information Exchange Model)** are open, global data exchange specifications engineered specifically for Urban Air Mobility (UAM) and Advanced Air Mobility (AAM).

Traditional aviation relies on **AIXM** (Aeronautical), **FIXM/FF-ICE** (Flight), and **IWXXM** (Weather). However, the ultra-dense, low-altitude, and high-cadence nature of eVTOL operations requires a specialized digital paradigm:

* **VIXM (Ground Infrastructure)**: Standardizes vertiport physical geometry, dynamic pad/gate availability, and tactical turnaround constraints.
* **UIXM (Airborne & Flow / UAM FF-ICE)**: Serves as the **"FF-ICE for UAM"**, standardizing 4D corridor trajectories, collaborative flight intent, battery/SOC constraints, and tactical PSU-to-PSU flight plan negotiation.

Together, **VIXM + UIXM** bridge the ground-air divide, delivering end-to-end digital twin synchronization across the entire UAM ecosystem.

---

## 🌐 The *IXM Ecosystem Matrix

VIXM and UIXM are designed to operate natively within the global **SWIM (System Wide Information Management)** architecture and UAM Traffic Management (PSU/USS):

| Standard | Domain | Core Focus | Target Systems |
| :--- | :--- | :--- | :--- |
| **AIXM** | Aeronautical Information | Airspace Structures, Routes, Traditional Aerodromes | AIS, NOTAM, ATM Providers |
| **FIXM** | Flight Information (Traditional) | En-route Flight Plans, Traditional 4D Trajectory | ATM, Airline AOC, ICAO FF-ICE |
| **IWXXM** | Weather Information | Meteorological Forecasts & Observations | MET Services, Dispatchers |
| **VIXM** | **Vertiport Information (Ground)** | **TLOF/FATO Geometry, Real-time Slot & Charger State** | **VPO, Fleet Operators, PSU/USS** |
| **UIXM** | **UAM Flight Information (Air & Flow)** | **UAM-native FF-ICE, Low-Altitude 4D Corridor Intent, SOC-aware Trajectory** | **PSU/USS, eVTOL Fleet Operators, Vertiport Coordinators** |

---

## ✈️ UIXM: The "FF-ICE for UAM" Vision

Traditional ICAO **FF-ICE** (Flight and Flow Information for a Collaborative Environment) transformed traditional airline flight planning into dynamic, collaborative 4D trajectory negotiation. 

**UIXM extends this legacy into low-altitude urban airspace:**

1. **Corridor-Aware 4D Flight Intent:** Standardized sharing of precision 4D trajectories adapted to urban airspace corridors and dynamic geo-fencing.
2. **Battery & Energy-Aware Trajectories:** Integration of State-of-Charge (SOC), reserve power thresholds, and weather-impacted climb profiles directly into flight data.
3. **Tactical Vertiport Slot Interlocking:** Direct synchronization with **VIXM** to ensure that airborne flight plan adjustments automatically reconcile with real-time vertiport TLOF/FATO availability and charging reservations.
4. **Collaborative PSU/USS Negotiation:** Streamlined machine-to-machine protocols for conflict resolution, tactical rerouting, and dynamic priority handling in multi-operator airspace.

---

## 🚀 VIXM Core Features

### 1. Static Infrastructure Model
* **Geometric & Physical Bounds:** Precise spatial definitions of TLOF, FATO, Safety Areas, and Obstacle Limitation Surfaces (OLS/OIS).
* **Vertiport Identification:** Standardized naming, spatial coordinates, geographic elevations, and access corridors.
* **Ground Facilities:** Gate layouts, passenger boarding bridges, charging pads, and emergency egress routing.

### 2. Dynamic Operational Model
* **Pad & Gate Availability:** Real-time occupancy status, scheduled occupancy windows, and turnaround durations.
* **Resource Readiness:** EV charging power limits, battery swap station health, fire suppression readiness, and MRO capabilities.
* **Tactical Restrictions:** Local surface wind threshold exceedances, micro-weather hazards, and temporary operating holds.

### 3. Interoperability & Architecture
* **Standard Schemas:** Fully modeled in UML with derived **XML (GML-compliant)** and **JSON Schema** payloads.
* **API & Event Streaming:** Optimized for modern RESTful, gRPC, and asynchronous event brokers (MQTT/AMQP/Kafka).

---

## 📂 Repository Structure

```text
├── docs/                # Architecture specifications, whitepapers, and SWIM integration guides
├── schemas/             # Formal schema definitions
│   ├── vixm/            # Vertiport Information Schemas (XSD & JSON)
│   └── uixm/            # UAM Flight & Flow (FF-ICE) Schemas (XSD & JSON)
├── examples/            # Sample payloads (Static Vertiport, Dynamic State, 4D Flight Intent)
├── uml/                 # Enterprise Architect / Papyrus UML class models
└── README.md
```

---

## 🛠️ Sample Payloads Preview

### 1. VIXM Dynamic Vertiport State (`vertiport-state.json`)
```json
{
  "$schema": "[https://vixm.aero/schemas/v1.0/vertiport-state.json](https://vixm.aero/schemas/v1.0/vertiport-state.json)",
  "vertiportId": "ICN-VP-01",
  "timestamp": "2026-08-22T11:00:00Z",
  "operatingStatus": "OPERATIONAL",
  "tlofStatus": [
    {
      "padId": "TLOF-ALPHA",
      "state": "RESERVED",
      "assignedFlightId": "UAM-KR-102",
      "expectedClearanceTime": "2026-08-22T11:15:00Z"
    }
  ],
  "chargingServices": [
    {
      "chargerId": "CHG-01",
      "powerAvailableKw": 350,
      "healthStatus": "NORMAL"
    }
  ]
}
```

### 2. VIXM Static Vertiport Geometry (`vertiport-layout.xml` - GML Compliant)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<vixm:Vertiport xmlns:vixm="[http://www.vixm.aero/schema/1.0](http://www.vixm.aero/schema/1.0)"
                 xmlns:gml="[http://www.opengis.net/gml/3.2](http://www.opengis.net/gml/3.2)"
                 gml:id="VP-ICN-01">
  <vixm:identifier>ICN-VP-01</vixm:identifier>
  <vixm:name>Incheon Central Vertiport</vixm:name>
  <vixm:designatorDValue uom="M">14.5</vixm:designatorDValue>
  <vixm:tlofArea>
    <vixm:TLOF gml:id="TLOF-ALPHA">
      <vixm:elevation uom="M">24.5</vixm:elevation>
      <vixm:geometry>
        <gml:Polygon srsName="urn:ogc:def:crs:EPSG::4326">
          <gml:posList>37.4692 126.4505 37.4692 126.4510 37.4688 126.4510 37.4688 126.4505 37.4692 126.4505</gml:posList>
        </gml:Polygon>
      </vixm:geometry>
    </vixm:TLOF>
  </vixm:tlofArea>
</vixm:Vertiport>
```

### 3. UIXM Collaborative Flight Intent (`uam-flight-intent.json` - UAM FF-ICE)
```json
{
  "$schema": "[https://vixm.aero/schemas/v1.0/uixm-flight-intent.json](https://vixm.aero/schemas/v1.0/uixm-flight-intent.json)",
  "flightId": "UAM-KR-102",
  "operatorId": "K-AAM-AIR",
  "aircraftType": "S-A2-EVTOL",
  "departureVertiport": "ICN-VP-01",
  "arrivalVertiport": "YBD-VP-03",
  "energyProfile": {
    "departureSOC": 92.5,
    "estimatedArrivalSOC": 48.0,
    "minimumReserveSOC": 20.0
  },
  "corridorTrajectory4D": [
    {
      "waypoint": "CORRIDOR-A-ENTRY",
      "lat": 37.4712,
      "lon": 126.4520,
      "altMeters": 450,
      "estimatedTime": "2026-08-22T11:16:30Z"
    }
  ],
  "interlockedGroundSlot": {
    "arrivalPadId": "TLOF-01",
    "slotTime": "2026-08-22T11:32:00Z"
  }
}
```

### 4. UIXM Flight Intent XML (`uam-flight-intent.xml` - FF-ICE GML/XML Profile)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<uixm:FlightIntent xmlns:uixm="[http://www.vixm.aero/schema/uixm/1.0](http://www.vixm.aero/schema/uixm/1.0)"
                   xmlns:gml="[http://www.opengis.net/gml/3.2](http://www.opengis.net/gml/3.2)"
                   gml:id="FLT-UAM-KR-102">
  <uixm:flightIdentification>UAM-KR-102</uixm:flightIdentification>
  <uixm:operatorIdentification>K-AAM-AIR</uixm:operatorIdentification>
  <uixm:aircraftType>S-A2-EVTOL</uixm:aircraftType>
  <uixm:departureVertiportRef>ICN-VP-01</uixm:departureVertiportRef>
  <uixm:arrivalVertiportRef>YBD-VP-03</uixm:arrivalVertiportRef>
  <uixm:energyProfile>
    <uixm:departureSOC uom="PERCENT">92.5</uixm:departureSOC>
    <uixm:estimatedArrivalSOC uom="PERCENT">48.0</uixm:estimatedArrivalSOC>
    <uixm:minimumReserveSOC uom="PERCENT">20.0</uixm:minimumReserveSOC>
  </uixm:energyProfile>
  <uixm:interlockedGroundSlot>
    <uixm:assignedPadId>TLOF-01</uixm:assignedPadId>
    <uixm:slotTime>2026-08-22T11:32:00Z</uixm:slotTime>
  </uixm:interlockedGroundSlot>
</uixm:FlightIntent>
```

---

## 🤝 Contributing

Contributions from vertiport operators, PSU/USS developers, eVTOL manufacturers, and aviation regulatory authorities are warmly welcomed:

1. Fork the Repository.
2. Create your Feature Branch (`git checkout -b feature/UIXM-4D-Corridor`).
3. Commit your Changes (`git commit -m 'feat: Add battery reserve profile to UIXM'`).
4. Push to the Branch (`git push origin feature/UIXM-4D-Corridor`).
5. Open a Pull Request.

---

## 📄 License

This project is distributed under the **MIT License**. See `LICENSE` for more information.
