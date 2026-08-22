<div align="center">

# The *IXM Framework
**Unified Data Exchange Standards for UAM Infrastructure (VIXM) & Operations (UIXM)**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Standard Draft](https://img.shields.io/badge/Version-v1.0--Draft-cyan.svg)](#)
[![Web](https://img.shields.io/badge/Official_Site-k--vixm.github.io-0ea5e9.svg)](https://k-vixm.github.io/)

</div>

---

## 📌 Overview

**The \*IXM Framework** is an open, harmonized data exchange initiative designed specifically for Advanced Air Mobility (AAM) and Urban Air Mobility (UAM).

Traditional aviation interoperability relies on **AIXM** (Aeronautical), **FIXM/FF-ICE** (Flight), and **IWXXM** (Weather). The \*IXM Framework extends this global heritage to meet the high-cadence, low-altitude demands of eVTOL operations across two core pillars:

* **VIXM (Vertiport Information Exchange Model)**: Digitalizes ground infrastructure, TLOF/FATO physical bounds, dynamic pad allocation, turnaround timelines, and charger health.
* **UIXM (UAM Flight Information Exchange Model)**: Functions as the **"FF-ICE for UAM"**, standardizing 4D corridor trajectories, battery/SOC constraints, tactical intent negotiation, and interlocked vertiport slot planning.

---

## 🌐 The *IXM Ecosystem Matrix

The \*IXM standards operate natively within the global **SWIM (System Wide Information Management)** environment and UAM Traffic Management (PSU/USS) architectures:

| Standard | Domain | Core Focus | Target Systems |
| :--- | :--- | :--- | :--- |
| **AIXM** | Aeronautical Information | Airspace Structures, Corridors, Traditional Aerodromes | AIS, NOTAM, ATM Providers |
| **FIXM** | Flight Information (Traditional) | En-route Flight Plans, Trajectory Synchronization | ATM, Airline AOC, ICAO FF-ICE |
| **IWXXM** | Weather Information | Meteorological Forecasts & Micro-weather Observations | MET Services, Dispatchers |
| **VIXM** | **Vertiport Information (Ground)** | **TLOF/FATO Geometry, Real-time Slot & Charger State** | **VPO, Fleet Operators, PSU/USS** |
| **UIXM** | **UAM Flight Information (Air & Flow)** | **UAM FF-ICE, Low-Altitude 4D Intent, SOC Trajectory** | **PSU/USS, eVTOL Operators, Fleet Hubs** |

---

## ✈️ UIXM: The "FF-ICE for UAM" Vision

Traditional ICAO **FF-ICE** (Flight and Flow Information for a Collaborative Environment) transformed airline flight dispatching into collaborative 4D trajectory negotiation. 

**UIXM brings this capability to dense urban airspace:**

1. **Corridor-Aware 4D Flight Intent:** Dynamic multi-waypoint trajectories synchronized with urban corridor definitions and airspace geofencing.
2. **Energy & Battery Profiles:** Integration of State-of-Charge (SOC), reserve margins, and weather-dependent power burn profiles directly into flight data.
3. **Tactical Slot Interlocking:** Seamless data binding between airborne UIXM trajectories and ground-level VIXM pad/charger reservations.
4. **Collaborative PSU-to-PSU Coordination:** Machine-to-machine protocols for dynamic rerouting, conflict avoidance, and priority management.

---

## 🚀 VIXM Core Features

### 1. Static Infrastructure Model
* **Geometry & Safety Bounds:** Exact spatial layouts of TLOF, FATO, Safety Areas, and Obstacle Limitation Surfaces (OLS/OIS).
* **Vertiport Master Data:** Universal vertiport identifiers, reference points, elevations, approach corridors, and local operating limits.
* **Ground Facilities:** Boarding gates, passenger flow paths, charging pads, and emergency support zones.

### 2. Dynamic Operational Model
* **Pad & Slot States:** Real-time pad occupancy, allocated flight identification, scheduled turnaround windows, and availability feeds.
* **Charging & Utility Telemetry:** Charging station status, available kW throughput, battery swap metrics, and MRO service capacity.
* **Tactical Restrictions:** Local micro-wind alerts, surface hazards, and immediate operational restrictions.

### 3. Interoperability & Schema Design
* **Schema Profiles:** Unified UML models providing both **XML (GML-compliant)** for SWIM architectures and **JSON Schema** for modern REST/WebSocket/gRPC streams.
* **Event Broker Ready:** Structured for high-frequency pub/sub networks (MQTT, AMQP, Kafka).

---

## 📂 Repository Structure

```text
├── docs/                # Architecture specifications, SWIM guidelines, and whitepapers
├── schemas/             # Formal schema definitions
│   ├── vixm/            # Vertiport Information Schemas (XSD & JSON)
│   └── uixm/            # UAM Flight & Flow (UAM FF-ICE) Schemas (XSD & JSON)
├── examples/            # Sample payloads (Static layouts, dynamic states, flight intents)
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

### 2. VIXM Static Vertiport Geometry (`vertiport-layout.xml`)
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

### 4. UIXM Flight Intent XML (`uam-flight-intent.xml` - GML Profile)
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

Contributions from vertiport developers, PSU/USS operators, eVTOL manufacturers, and aviation regulatory authorities are warmly welcomed:

1. Fork the Repository.
2. Create your Feature Branch (`git checkout -b feature/NewSchemaFeature`).
3. Commit your Changes (`git commit -m 'feat: Add battery reserve profile to UIXM'`).
4. Push to the Branch (`git push origin feature/NewSchemaFeature`).
5. Open a Pull Request.

---

## 📄 License

This project is distributed under the **MIT License**. See `LICENSE` for more information.
