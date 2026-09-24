# ISTeN-1: Industrial Solar Telemetry Node
An ultra-low-power, off-grid agricultural field gateway featuring dual-RF connectivity (Cellular IoT + Sub-GHz LoRa), MPPT solar power management, industrial field-bus interfacing, and onboard environmental diagnostics.

---

## Technical Overview

The **ISTeN-1** is an industrial-grade field node designed for remote agricultural monitoring, soil telemetry, and asset tracking. Engineered to operate continuously under South African climate conditions, the system collects data from wired field sensors, bridges remote sub-nodes over LoRa, and streams encrypted telemetry to cloud infrastructure via Cellular IoT.

```text
                               +-----------------------------+
                               |    Field Probes (SDI-12)    |--+
                               +-----------------------------+  |
                                                                |
                               +-----------------------------+  |
                               |    Weather / VFD (RS-485)   |--+
                               +-----------------------------+  |
                                                                |
                               +-----------------------------+  |    +---------------------------+
                               |     Remote Nodes (LoRa)     |--+--->|   STM32 Microcontroller   |--+--->     [ Cellular / GNSS ]      ---> Cloud
                               +-----------------------------+       +---------------------------+  |
                                                                                   |                +---> [ SPI Flash / Local Buffer ]
                                                                                   |
+---------------+    +----------------+    +------------------+                    |
|  Solar Panel  |--->|  MPPT Charger  |--->|  LiFePO4 Battery |--------------------+
+---------------+    +----------------+    +------------------+
```
---

## Hardware Specifications

### 1. Processing & System Control
* **MCU:** Low-power ARM Cortex-M architecture running bare-metal C / FreeRTOS.
* **Local Storage:** Onboard SPI Flash memory for data buffering during cellular outages.
* **Timekeeping:** High-precision external Real-Time Clock (RTC) backed by a supercapacitor.
* **System Watchdog:** Dedicated hardware supervisor for automated fault recovery.

### 2. Wireless Connectivity & Location
* **Cellular IoT:** RF IC (e.g. SIMCom SIM7080G) supporting NB-IoT and LTE-M with 2G fallback.
* **Sub-GHz Radio:** LoRa transceiver (e.g. Semtech SX1262) for long-range, line-of-sight communication with off-grid field nodes.
* **GNSS / Positioning:** Integrated multi-constellation GPS/GLONASS positioning for geotagging and anti-theft asset tracking.

### 3. Industrial Wired Interfaces
* **SDI-12 Bus:** Bi-directional interface supporting commercial multi-depth soil moisture probes (e.g. AquaCheck, DFM).
* **RS-485 Modbus RTU:** Isolated differential serial interface with TVS surge protection for weather stations, flow meters, and VFDs.
* **Power-Gated Sensor Rail:** Switched $12\text{V}$ boost regulator supplying power to external probes only during sampling windows.

### 4. Power & Battery Management
* **Solar Input:** Onboard Maximum Power Point Tracking (MPPT) charger operating from solar panels.
* **Battery Chemistry:** High-thermal-stability $3.2\text{V}$ Lithium Iron Phosphate (LiFePO4) battery.
* **Power Profiling:** Ultra-low standby current ($<15\,\mu\text{A}$) in deep-sleep mode; onboard current monitoring via current sensor.

### 5. Onboard Diagnostics & Security
* **Motion & Anti-Theft:** Low-power 3-axis accelerometer with configurable interrupt flags for tilt/movement detection.
* **Internal Climate Monitoring:** Digital temperature and relative humidity sensor tracking enclosure conditions and thermal stress.
* **System Health:** Multi-channel current/voltage sensing for real-time power budget verification.

### 6. Physical & Mechanical Engineering
* **Enclosure:** Sealed IP67 junction box with weatherproof cable glands.
* **Thermal CAD:** Custom 3D-printed mounting chassis designed to act as a thermal dissipator under outdoor solar loading.

---

## Design for Manufacturing (DFM) & Compliance
* **Test Points:** Dedicated $1\text{ mm}$ bring-up test points for power rails ($3.3\text{V}$, $12\text{V}$, Solar, Battery) and communication lines (UART, RS-485, SDI-12).
* **Power Profiling Jumpers:** Cuttable solder jumpers and zero-ohm shunts for dynamic current measurements via oscilloscope or profiling hardware.
* **Circuit Protection:** Transient Voltage Suppression (TVS) diodes on exposed lines, P-MOSFET reverse-polarity protection, and ground isolation.
* **EMC Principles:** Four-layer PCB stackup with dedicated ground planes and filtered power entries to meet industrial noise immunity standards.

---

## Repository Structure

```text
├── docs/             # Engineering Logs, Trade-off Analyses, and Architecture Decision Records
├── firmware/         # C Drivers, Protocol Parsers, State Machines, and Unit Tests
├── hardware/         # Schematics, PCB Layouts, Gerber Files, and 3D CAD Models
└── misc/             # Miscellaneous stuff, e.g. datasheets
```
---
