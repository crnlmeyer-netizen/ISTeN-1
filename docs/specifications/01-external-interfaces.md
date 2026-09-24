# ISTeN-1 External Interface & Mechanical Specification

## 1. On-Board PCB Terminal & RF Connectors

### 1.1 Field Bus & Power Terminal Blocks
* **Connector Type:** 5.08mm (or 3.81mm) pitch screwless push-in PCB terminal blocks.

| Terminal Block | Pin Count | Pinout / Signals | Electrical Voltage Level | Description / Function |
| :--- | :---: | :--- | :--- | :--- |
| **SDI-12 Port** | 3 | `12V`, `DATA`, `GND` | $+12\text{V}$ Switched, $0\text{--}5\text{V}$ Logic | Bi-directional multi-drop telemetry for soil probes. |
| **RS-485 Port** | 4 | `12V`, `A`, `B`, `GND` | $+12\text{V}$ Switched, Differential $A/B$ | Modbus RTU communication for pumps, VFDs, and weather stations. |
| **Solar Input** | 2 | `V+`, `V-` | $+6.0\text{V}$ to $+24.0\text{V DC}$ | Solar panel input feeding the internal MPPT LiFePO4 buck charger. |

### 1.2 On-Board RF Interfaces
* **Connector Type:** Surface-mount Male U.FL connectors ($50\,\Omega$ characteristic impedance).

| Port | Signal / Protocol | Frequency Band | RF Routing Notes |
| :--- | :--- | :--- | :--- |
| **RF_CELL** | LTE-M / NB-IoT | $700\text{ MHz} \text{--} 2100\text{ MHz}$ | Driven by SIM7080G main antenna output. |
| **RF_GNSS** | Active GPS / GNSS | $1575.42\text{ MHz}$ (L1 Band) | Driven by SIM7080G GNSS port with active DC bias. |
| **RF_LORA** | Sub-GHz LoRa | $868\text{ MHz}$ / $915\text{ MHz}$ | Driven by SX1262 transceiver output via matching network. |

---

## 2. Enclosure Penetration & Cable Management

### 2.1 Waterproof Cable Glands
* **Hardware:** $3\times$ IP67 M12 / M16 Nylon Cable Glands (NBR rubber sealing grommets).
* **Application:** Accommodates direct-burial stripped wire runs for SDI-12, RS-485, and Solar Input directly into the internal PCB terminal blocks.

### 2.2 Panel-Mount RF Bulkheads
* **Hardware:** $3\times$ IP67 Panel-Mount SMA Female Bulkhead Connectors with integrated sealing O-rings and locknuts.
* **Internal Interconnect:** $50\,\Omega$ U.FL Female to SMA Female Bulkhead coaxial pigtail cables (1.13mm / RG178, $\approx 10\text{--}15\text{ cm}$).
* **External Interface:** $3\times$ External IP67 SMA Male omni-directional antennas (Cellular, GNSS Patch, LoRa Whip).
