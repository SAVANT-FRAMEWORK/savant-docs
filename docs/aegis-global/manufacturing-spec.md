---
title: AEGIS-GLOBAL — Manufacturing & China Sourcing Specification
description: Complete manufacturing pathway for AEGIS-NG nodes — $46.30 per unit, with a single disclosed registry import.
---

# AEGIS-GLOBAL — Manufacturing & China Sourcing Specification

**Version:** 1.0.0
**Author:** Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
**Last Updated:** 2026-08-11
**SHA-256:** [PENDING-FIRST-RELEASE]

---

## 1. Purpose and Reader

This specification is written for two readers simultaneously: a contract manufacturer in Shenzhen executing a production run, and a sovereign partner or certified local engineer verifying that the run is buildable, honest, and complete. Everything needed to manufacture the AEGIS-NG node family ([Node Types](../aegis-ng/node-types.md)) is in this document, with exactly one exception, disclosed in §3: the canonical LCSC part-number registry, which is imported from Dr. Odeta's *AEGIS-GLOBAL China Sourcing Specification v1.0*. No other step requires information outside this document and the referenced sibling specifications.

## 2. Unit Economics

The China-sourced manufacturing pathway achieves a per-unit cost of **$46.30**, against two comparison baselines:

| Pathway | Per-Unit Cost | Delta vs. China Pathway |
|---|---|---|
| **China-sourced (this specification)** | **$46.30** | — |
| Local-only sourcing (Nigeria) | $60.70 | China pathway saves **23.7 %** |
| Western-only sourcing | $107.00 | China pathway saves **56.7 %** |

**Efficiency dividend:** at a program budget of $2,500,000, the China-sourced pathway's savings against the Western-only baseline yield an **efficiency dividend of $237,226** — capital that remains inside the program for additional units, certification cohorts, and field operations rather than leaving as procurement margin. The dividend is a program-level figure computed on the full procurement basket (units plus spares plus shipping share), not a naive per-unit multiplication; the computation sheet is part of the class-C checkpoint bundle for any budget narrative that cites it.

Per-unit cost composition ($46.30):

| Line | Amount |
|---|---|
| Electronic components (BOM, §3) | $24.80 |
| PCB fabrication (JLCPCB, §4) | $3.10 |
| SMT assembly (§5) | $5.60 |
| Enclosure, solar array, storage cell, cabling | $7.20 |
| Anti-tamper hardware (§7) | $1.10 |
| QC allocation (§6) | $1.40 |
| DAP Lagos logistics allocation (§8) | $3.10 |
| **Total** | **$46.30** |

## 3. Bill of Materials — Canonical Components, Registry-Marked Part Numbers

The BOM below is fully structured: component, function, package, quantity, target cost. Quantities are stated for the reference unit — one **N-C01 ward aggregation hub** (the most complex common build); Group A beacon builds drop the ESP32-S3 row and the display-adjacent rows, per the variant table in §3.2.

**Integrity rule (constitutional, STOP-grade):** the LCSC part-number column is *not* populated in this document. The canonical registry of LCSC part numbers exists in Dr. Christabel Odeta's **AEGIS-GLOBAL China Sourcing Specification v1.0**, which is the single source of truth for procurement identifiers. Every LCSC cell below is marked `IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry)`. **Inventing, guessing, or "provisionally filling" an LCSC part number is a STOP-grade defect**: a fabricated part number routes procurement to a wrong or counterfeit component and is indistinguishable from competence until field failure. An empty, marked cell is an honest instruction; a fabricated cell is a lie with a part number on it.

### 3.1 Reference BOM — N-C01 Ward Aggregation Hub

| # | Component | Function | Package | Qty | Target Cost (USD) | LCSC Part # |
|---|---|---|---|---|---|---|
| 1 | STM32L072 (Cortex-M0+ ultra-low-power MCU) | Power management controller; sleep-domain governor | LQFP-48 | 1 | $2.40 | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |
| 2 | ESP32-S3 (dual-core Xtensa, vector extensions) | Primary application processor; TFLite Micro inference (M-03) | QFN-56 module or bare SoC per registry | 1 | $3.60 | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |
| 3 | ESP32-C3 (RISC-V MCU) | Radio coprocessor; store-and-forward buffer manager | QFN-32 | 1 | $1.50 | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |
| 4 | SX1278 433 MHz LoRa transceiver | Mesh radio physical layer | SMD-16 module footprint | 2 (primary + guard channel) | $4.20 (pair) | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |
| 5 | Solar charge controller IC + MPPT front-end passives | Solar-only power input regulation | SOT-23-6 + 0805 passives set | 1 set | $1.85 | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |
| 6 | LiFePO4 storage cell (sized to ≥ 5-day autonomy) | Energy storage | Prismatic/cylindrical per registry | 1 | $4.60 | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |
| 7 | Anti-tamper mesh switch set (enclosure intrusion) | Tamper detection; triggers key zeroization + signed event | Custom flex circuit + micro-switch pair | 2 pairs | $1.10 | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |
| 8 | Secure element (ATECC-class, ECDSA P-256) | Key custody; frame signing | UDFN-8 | 1 | $0.95 | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |
| 9 | Flash (NOR, 16 MB) — firmware + CRDT buffer | Non-volatile store-and-forward buffer | SOIC-8 | 1 | $0.70 | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |
| 10 | 433 MHz antenna (SMA, matched) + RF passives | Radiating element; matching network | SMA edge-mount + 0402 RF set | 1 set | $1.30 | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |
| 11 | Power-path & protection (ideal diode, TVS, fuse set) | Solar/battery/load arbitration; surge protection | SOD-123 / SMB set | 1 set | $0.90 | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |
| 12 | Debug/UART header + pogo test points | Factory flashing & QC interface | 2.54 mm header / pad array | 1 set | $0.25 | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |
| 13 | Passives & discretes remainder (R/C/L, LDOs, crystals) | Supporting circuitry | 0402/0603 set, 32.768 kHz + 40 MHz xtals | 1 lot | $1.45 | IMPORT-FROM: China Sourcing Specification v1.0 (canonical registry) |

Component subtotal: **$24.80** (matches §2 composition).

### 3.2 Variant Deltas

| Node Group | Delta vs. Reference BOM |
|---|---|
| Group A beacons (N-A01…N-A05) | Remove rows 2, 9 halved; STM32L072 (row 1) becomes primary processor; single SX1278; add sensor front-end per type (also registry-marked); smaller storage cell (≥ 21-day low-duty sizing). Target component cost: $14.10–$17.30 per type. |
| Group B relays (N-B01…N-B04) | Remove rows 1, 2; ESP32-C3 (row 3) becomes primary; add second flash; N-B02 adds high-gain antenna line. Target component cost: $15.60–$18.90. |
| Group C hubs (N-C02, N-C03) | Reference build; N-C02/N-C03 add uplink interface line (registry-marked). |
| Group D command/display (N-D01, N-D02) | Reference build plus display module line (registry-marked); N-D02 adds dual-operator authentication hardware (second secure element). |

## 4. PCB Fabrication (JLCPCB)

| Parameter | Specification |
|---|---|
| Fabricator | JLCPCB (Shenzhen) |
| Layer count | 4 (signal / GND / PWR / signal) |
| Board thickness | 1.2 mm |
| Copper weight | 1 oz all layers |
| Min trace/space | 4/4 mil (design uses ≥ 5/5 for yield margin) |
| Min via / annular ring | 0.3 mm drill / 0.15 mm ring |
| Surface finish | ENIG (lead-free; RF and secure-element pads require it) |
| Impedance control | 50 Ω ± 10 % on SX1278 RF feed to antenna pad; stackup per JLCPCB 4-layer standard, verified on coupon |
| Panelization | V-score, fiducials per panel corner, tooling strips per assembler requirement |
| Fabrication target cost | $3.10/unit at production volume |

## 5. SMT Assembly

Assembly is executed at JLCPCB SMT lines (or an equivalent line approved by class-C checkpoint) under these constraints:

1. **Full-turnkey from the canonical registry.** All placements source from the LCSC registry import (§3). No broker substitution, no "equivalent" parts without a signed equivalence record — RF and security components do not have silent equivalents.
2. **Secure element handling.** Row-8 secure elements are programmed with per-node keys at a segregated station; key injection records are hash-chained into the node manifest. No unprogrammed secure element leaves the assembly site; no programmed one is logged in plaintext.
3. **Firmware flashing.** F-series images ([Node Types §1](../aegis-ng/node-types.md)) are flashed over the row-12 interface, hash-verified against the pinned build manifest, and locked. The flashed hash is recorded per unit serial.
4. **First-article inspection.** First 10 units of any run: full X-ray of BGA/QFN solder joints, RF output measurement on both LoRa channels, tamper-switch actuation test. Run proceeds only after first-article class-C GO.

## 6. Quality Control Criteria

| Gate | Test | Acceptance |
|---|---|---|
| IQC | Component lot verification against registry | 100 % of lots traceable to registry part numbers; zero broker stock |
| Post-SMT | AOI + first-article X-ray | Zero critical defects; first-article GO per §5.4 |
| Power-on | Solar charge cycle test (simulated irradiance profile) | Full charge from 20 % within spec; no thermal excursion |
| RF | Tx power and Rx sensitivity per unit, both channels | Within 2 dB of design values ([Mesh Protocol §4](../aegis-ng/mesh-protocol.md)) |
| Tamper | Enclosure-breach simulation | Signed tamper event emitted; keys zeroized; verified at hub |
| Burn-in | 24 h at duty cycle | Zero failures; any failure halts lot pending root cause |
| Final | Manifest audit: firmware hash, key injection record, serial | Manifest hash-chain complete per unit |

## 7. Anti-Tamper at Manufacture

Anti-tamper is built, not bolted on: row-7 mesh switches are installed during enclosure assembly with potting over the secure-element and key-injection region; enclosure closure is the final assembly step and actuates the tamper circuit's arming self-test. Every unit leaves the factory already armed. The anti-tamper allocation in §2 ($1.10) covers the switch set and potting labor; the *behavior* is specified and tested in [Node Types §2.4 and §7](../aegis-ng/node-types.md).

## 8. Logistics — DAP Lagos

| Term | Specification |
|---|---|
| Incoterm | **DAP (Delivered at Place), Lagos, Nigeria** — seller bears carriage and risk to the named place; buyer handles import clearance |
| Packing | ESD shielding per unit; desiccant; tamper-evident carton seals; carton manifest hash-chained to unit serials |
| Documentation | Commercial invoice, packing list, HS classification sheet, and the manifest hash list — the receiving engineer verifies cartons against the hash list before acceptance |
| Insurance | Full replacement value, marine/air as routed |
| Lead time | Stated per PO; QC gates (§6) are not compressible to recover schedule |
| Logistics allocation | $3.10/unit (§2) at production volume |

## 9. Payment Terms

| Milestone | Payment | Gate |
|---|---|---|
| PO issuance | 30 % | Signed PO against registry-complete BOM |
| First-article GO | 20 % | Class-C first-article verdict (§5.4) |
| Lot completion + QC GO | 40 % | All §6 gates passed; manifest audit complete |
| DAP Lagos receipt verified | 10 % | Carton hash verification + receiving inspection |

No payment precedes its gate. No gate is waived to recover schedule. These terms are symmetric: they protect the manufacturer from speculative orders and the program from unverified goods, and they make the QC system — not goodwill — the arbiter of payment.

---

## Falsifiability Test

**Claim:** A sovereign partner with no prior SAVANT contact can manufacture the AEGIS-NG family from this document plus [Node Types](../aegis-ng/node-types.md), with the LCSC registry import as the *single* clearly-marked remaining action.

**Test:** Hand this document and node-types.md to a manufacturing engineer outside the framework. Ask them to enumerate every action required to reach DAP Lagos receipt. The answer must be: (1) import LCSC part numbers from the canonical registry (the only marked gap); (2) place the JLCPCB fabrication and SMT orders per §4–§5; (3) execute QC per §6; (4) receive and verify per §8. If the engineer identifies any *other* missing datum — an unspecified package, an undefined test threshold, an ambiguous variant delta — this specification has failed its gate, and the gap must be recorded as a signed REGRESSION record under S50 checkpoint class C before any grant narrative cites the $46.30 figure.
