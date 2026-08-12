---
title: AEGIS-NG — Node Types (N-A01 – N-D02)
description: The fourteen-type field hardware family of the AEGIS-NG sovereign mesh — sensing, relay, hub, and command/display.
---

# AEGIS-NG — Node Types (N-A01 – N-D02)

**Version:** 1.0.0
**Author:** Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
**Last Updated:** 2026-08-11
**SHA-256:** [PENDING-FIRST-RELEASE]

---

## 1. Family Architecture

AEGIS-NG field hardware comprises fourteen node types in four role groupings. The grouping is functional and constitutional: a node's role determines its permitted radio behavior, its power budget, and its anti-tamper obligations. A node may never act outside its role grouping; a beacon that begins routing is a compromised beacon.

| Group | Role | Node Types | Firmware (F-series) | On-Device Models (M-series) |
|---|---|---|---|---|
| **A** | Sensing | N-A01 … N-A05 (5 types) | F-01 … F-05 | M-01, M-02 (where fitted) |
| **B** | Relay | N-B01 … N-B04 (4 types) | F-06 … F-08 | none |
| **C** | Hub | N-C01 … N-C03 (3 types) | F-09 … F-11 | M-03 … M-06 (where fitted) |
| **D** | Command / Display | N-D01, N-D02 (2 types) | F-12 | none (renders upstream inferences) |

Cross-references: F-01…F-12 are the signed firmware images enumerated in the firmware registry; M-01…M-06 are TensorFlow Lite Micro models compiled for the MCUs below. Both registries are governed artifacts (S50 class C) and are hash-pinned in each node's build manifest. No node ships with an unpinned firmware or model.

## 2. Constitutional Hardware Invariants

These apply to all fourteen types and are repeated here so each per-type table can be read against them:

1. **Power: solar-only.** Every field node is solar-powered with integrated storage. No grid dependency, no battery-swap logistics, no generator fuel chain. Storage is sized for ≥ 5 overcast days at full duty cycle (≥ 21 days for Group A at reduced duty).
2. **Radio: 433 MHz LoRa.** All mesh traffic is 433 MHz LoRa per the [Mesh Protocol](mesh-protocol.md). Sub-GHz ISM-band operation, long range, low power, license-appropriate for Nigerian deployment.
3. **No GPS on beacons.** Group A sensing beacons carry **no GPS receiver**. Location is bound at deployment (surveyor-recorded, signed into the node manifest) and never re-negotiated by radio. This removes the most common tracking-and-spoofing attack surface on field sensors and removes a power-hungry peripheral from a solar budget.
4. **Anti-tamper by construction.** Every enclosure carries tamper-mesh switches; detection of enclosure breach zeroizes key material and emits a signed tamper event to the mesh before shutdown (power reserve is reserved for exactly this transmission).
5. **Falsifiability per group.** Each group carries a group-level falsifiability test (§7) that a sovereign partner can run with field equipment.

## 3. Group A — Sensing Beacons (N-A01 … N-A05)

| Type | Sensing Function | MCU | Radio | Power | Anti-Tamper | Firmware | Model |
|---|---|---|---|---|---|---|---|
| N-A01 | Human presence / motion perimeter beacon | STM32L072 (ultra-low-power ARM Cortex-M0+) | SX1278 433 MHz LoRa, transmit-only into mesh | Solar-only, ≥ 21 days storage | Tamper-mesh switch; key zeroization; signed tamper event | F-01 | M-01 (presence classifier, TFLite Micro) |
| N-A02 | Environmental beacon (temperature, humidity, particulate) | STM32L072 | SX1278 433 MHz LoRa | Solar-only, ≥ 21 days storage | Tamper-mesh switch; key zeroization | F-02 | none (threshold logic in firmware) |
| N-A03 | Acoustic event beacon (gunshot / disturbance classification) | STM32L072 | SX1278 433 MHz LoRa | Solar-only, ≥ 14 days storage (audio duty) | Tamper-mesh switch; microphone self-test line | F-03 | M-02 (acoustic event classifier, TFLite Micro) |
| N-A04 | Water point / flow beacon | STM32L072 | SX1278 433 MHz LoRa | Solar-only, ≥ 21 days storage | Tamper-mesh switch; probe-disconnect detection | F-04 | none |
| N-A05 | Structural / fence-line vibration beacon | STM32L072 | SX1278 433 MHz LoRa | Solar-only, ≥ 21 days storage | Tamper-mesh switch; mount-detachment detection | F-05 | M-01 (shared presence/vibration classifier) |

Design notes: the STM32L072 is chosen for sub-µA sleep domains and native LoRaWAN-adjacent peripheral integration at very low cost; Group A duty cycles are ≤ 1 %, and all inference is on-device (M-series) so that raw sensor streams never traverse the mesh — only signed event summaries do. Beacons emit event summaries and heartbeats; they do not route (see §1 invariant: a beacon that routes is a compromised beacon).

## 4. Group B — Relay Nodes (N-B01 … N-B04)

| Type | Relay Function | MCU | Radio | Power | Anti-Tamper | Firmware | Model |
|---|---|---|---|---|---|---|---|
| N-B01 | Fixed mast relay (primary backbone) | ESP32-C3 (RISC-V, integrated RF front-end host) | SX1278 433 MHz LoRa, dual-buffer store-and-forward | Solar-only, ≥ 7 days storage | Tamper-mesh switch; key zeroization; signed tamper event | F-06 | none |
| N-B02 | Fixed mast relay, long-haul (high-gain antenna) | ESP32-C3 | SX1278 433 MHz LoRa, high-gain collinear | Solar-only, ≥ 7 days storage | Tamper-mesh switch; key zeroization | F-06 | none |
| N-B03 | Elevated terrain relay (ridgeline / tree platform) | ESP32-C3 | SX1278 433 MHz LoRa | Solar-only, ≥ 10 days storage (maintenance-light sites) | Tamper-mesh switch; tilt/detachment detection | F-07 | none |
| N-B04 | Mobile relay (vehicle / patrol-mounted) | ESP32-C3 | SX1278 433 MHz LoRa | Solar-only + vehicle auxiliary input (solar remains primary) | Tamper-mesh switch; motion-context attestation | F-08 | none |

Design notes: relays route, buffer, and attest. They hold no sensor data beyond forwarding buffers, run no M-series inference, and implement the store-and-forward semantics of the [Mesh Protocol](mesh-protocol.md) §5. The ESP32-C3 is chosen for its RISC-V toolchain maturity, hardware secure boot, and cost position.

## 5. Group C — Hub Nodes (N-C01 … N-C03)

| Type | Hub Function | MCU | Radio | Power | Anti-Tamper | Firmware | Model |
|---|---|---|---|---|---|---|---|
| N-C01 | Ward aggregation hub (mesh-to-local-store) | ESP32-S3 (dual-core Xtensa, vector extensions) | SX1278 433 MHz LoRa + local Ethernet/Wi-Fi uplink option | Solar-only, ≥ 5 days storage, larger array | Tamper-mesh switch; dual zeroization domains; signed tamper event | F-09 | M-03 (event-fusion filter, TFLite Micro) |
| N-C02 | LGA hub with edge analytics | ESP32-S3 | SX1278 433 MHz LoRa + uplink option | Solar-only, ≥ 5 days storage | Tamper-mesh switch; dual zeroization domains | F-10 | M-04 (anomaly scoring), M-05 (triage ranking) |
| N-C03 | Clinical edge hub (CLAI-OS bridge) | ESP32-S3 | SX1278 433 MHz LoRa + facility LAN | Solar-only with facility auxiliary fallback (solar primary) | Tamper-mesh switch; dual zeroization domains; enclosure intrusion logging to CRDT | F-11 | M-06 (signal-quality gate for clinical sensor feeds) |

Design notes: hubs are the only nodes that bridge the mesh to other networks, and they do so under store-and-forward discipline — the mesh never depends on the uplink. The ESP32-S3 is chosen for its vector instruction support, which the M-03…M-06 TFLite Micro models require at acceptable latency. Hubs host the local CRDT replicas described in [FHIR R4 Native §4](../clai-os/fhir-r4-native.md) where clinical data is concerned.

## 6. Group D — Command / Display Nodes (N-D01, N-D02)

| Type | Command/Display Function | MCU | Radio | Power | Anti-Tamper | Firmware | Model |
|---|---|---|---|---|---|---|---|
| N-D01 | Field command display (map + event wall for LGA operators) | ESP32-S3 (display pipeline) | SX1278 433 MHz LoRa (receive-dominant) + LAN | Solar-only with facility auxiliary fallback (solar primary) | Tamper-mesh switch; operator-authentication binding; zeroization | F-12 | none (renders upstream inferences only) |
| N-D02 | Sovereign command console (state/national aggregation) | ESP32-S3 (display pipeline) | SX1278 433 MHz LoRa + uplink | Solar-only with facility auxiliary fallback (solar primary) | Tamper-mesh switch; dual-operator control for sensitive actions; zeroization | F-12 | none |

Design notes: Group D nodes issue commands into the mesh only through signed, role-bound control messages; an unsigned or out-of-role command is dropped at the first relay and logged as an operational event. Dual-operator control on N-D02 applies to any action affecting more than one LGA — the hardware enforces the two-person rule, not the policy document.

## 7. Falsifiability Tests by Group

**Group A (sensing).** Deploy one beacon of any A type at a surveyed position with its manifest location. Trigger its sensing modality with a controlled field event (walk the perimeter, fire a blank in a controlled range, run water). Verify: (1) a signed event summary arrives at the hub within the mesh latency bound; (2) the beacon ignores a replayed event packet from a third-party transmitter; (3) opening the enclosure produces a signed tamper event and key zeroization. Failure on any arm falsifies the group.

**Group B (relay).** Sever the direct link between a beacon and its hub, forcing store-and-forward through an N-B01/B02. Verify message delivery with sequence integrity and no duplication, and verify that delivery resumes ordering-correctly after a 6-hour relay power-down (covered panel) followed by restoration. Failure on ordering or loss falsifies §5 of the mesh protocol as implemented.

**Group C (hub).** Disconnect all uplinks from an N-C01 for 18 hours while feeding it synthetic mesh traffic at 2× rated load. Verify: no event loss, local CRDT replica divergence bounded and convergent at reconnect, and M-03/M-04 inference latency within specification on ESP32-S3. Failure falsifies the hub's offline claim.

**Group D (command/display).** Attempt to inject an unsigned control message and an out-of-role signed message at N-D01. Verify both are dropped at the first relay and logged. Then attempt a multi-LGA action on N-D02 with a single operator credential. If the action executes, the hardware two-person rule is falsified — a class-A defect.

---

## Falsifiability Test

**Claim:** Fourteen node types, four role groupings, solar-only, 433 MHz LoRa, no GPS on beacons, anti-tamper by construction — and every claim testable with field equipment.

**Test:** Manufacture or procure one node of each group per the [Manufacturing Specification](../aegis-global/manufacturing-spec.md), then execute the group test in §7 appropriate to each. Any group failing any arm of its test invalidates the corresponding section of this document; record as a signed REGRESSION record under S50 checkpoint class C. The tests require no proprietary tooling — only a surveyed position, a second transmitter, a covered solar panel, and time.
