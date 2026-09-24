# ISTeN-1 Hardware Architecture & Peripheral Design Rationale

## External Interfaces [see ./specifications/01-external-interfaces.md]

### 1. External Sensors/Connectors Decisions

#### 1.1 Multi-Drop Buses for Sensors
* **Decision:** Solitary single-channel ports selected for SDI-12 (1x 3-pin) and RS-485 Modbus RTU (1x 4-pin) [versus multiple ports each].
* **Rationale:** Both SDI-12 and RS-485 are inherently multi-drop topologies capable of addressing multiple slave devices on a single physical cable harness. Duplicate physical connectors would add redundant level-shifting circuitry, PCB footprint area, and component cost without increasing protocol capability.
* **Power Distribution:** A single high-side power-gated $12\text{V}$ boost converter rail feeds both ports. Power gating ensures external sensors draw zero quiescent current during deep-sleep sleep cycles.

#### 1.2 RS-485 Pinout & Ground Reference
* **Decision:** 4-pin terminal interface (`12V`, `A`, `B`, `GND`).
* **Rationale:** Retaining a dedicated signal ground line (`GND`) alongside differential pairs ($A/B$) prevents common-mode voltage offsets from exceeding transceiver absolute maximum ratings during long field cable runs across agricultural land.

### 2. Wireless Radio & Antenna Strategy

* **Decision:** Discrete Cellular (LTE-M/NB-IoT) + GNSS module combined with a separate Sub-GHz LoRa transceiver.
* **Rationale:** No single commercial SoC combines cellular stack processing, active GNSS reception, and high-power Sub-GHz LoRa physical layer hardware on one die.
* **RF Isolation:** 3 dedicated male U.FL surface-mount connectors feeding panel-mounted SMA female bulkheads via $50\,\Omega$ coaxial pigtails. Distinct physical paths isolate cellular transmission bursts from LoRa receiver front-ends.

### 3. Power Architecture & Solar MPPT Tracking

* **Decision:** LiFePO4 chemistry ($3.2\text{V}$ nominal, $3.6\text{V}$ float) paired with a dedicated MPPT charger IC and $6\text{V}\text{--}24\text{V}$ solar input stage.
* **Rationale:** LiFePO4 offers superior thermal stability and cycle life ($>2000$ cycles) compared to Li-ion in harsh outdoor agricultural environments. Dynamic MPPT tracking ensures maximum power extraction during overcast conditions or low solar angles.
* **Protection Pipeline:** TVS surge clamping, P-MOSFET reverse-polarity protection, and input LC filtering prevent field wiring damage and RF interference.
---

## Internal Sensors [see ./specifications/02-internal-sensors.md]
