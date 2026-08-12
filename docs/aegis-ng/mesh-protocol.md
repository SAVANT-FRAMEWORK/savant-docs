---
title: AEGIS-NG — 433 MHz LoRa Mesh Protocol
description: The four-tier sovereign mesh topology, RF link budget, CRDT offline sync, and bandwidth-zero design of AEGIS-NG.
---

# AEGIS-NG — 433 MHz LoRa Mesh Protocol

**Version:** 1.0.0
**Author:** Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
**Last Updated:** 2026-08-11
**SHA-256:** [PENDING-FIRST-RELEASE]

---

## 1. Design Doctrine: Bandwidth-Zero

The AEGIS-NG mesh is engineered to a doctrine called **bandwidth-zero**: the sensing, alerting, and coordination functions of a deployment must be fully operational with zero external bandwidth — no cellular, no satellite, no ISP — for an unbounded duration. External uplinks, when they exist, are a convenience for aggregation and remote oversight. They are never on the critical path. This doctrine is what makes the network *sovereign*: its operation does not depend on any infrastructure its operators do not own.

## 2. Physical Layer

| Parameter | Value | Rationale |
|---|---|---|
| Band | 433 MHz ISM (sub-GHz) | Superior foliage/terrain penetration and range per milliwatt vs. 868/915 MHz alternatives; appropriate to Nigerian field deployment |
| Transceiver | SX1278-class LoRa | Long-range chirp spread spectrum; low Rx current for solar budgets |
| Modulation | LoRa, SF7–SF12 adaptive | Rate adaptation trades throughput for link margin per hop |
| Bandwidth | 125 kHz | Standard LoRa configuration; adequate for signed event summaries |
| Coding rate | 4/5 (CR 4/8 for tier-4 long haul) | Forward error correction scaled to hop difficulty |
| Max Tx power | +20 dBm (regulated limit observed) | See link budget, §4 |
| Payload discipline | Signed event summaries only | Raw sensor streams never traverse the mesh (see [Node Types](node-types.md) §3) |

## 3. Four-Tier Sovereign Topology

```
TIER 1  SENSING (Group A beacons, N-A01..N-A05)
   o   o   o   o   o   o   o   o        <- transmit-only event summaries,
    \   |  /      \   |    /              no routing, no GPS
     \  | /        \  |  /
TIER 2  RELAY (Group B, N-B01..N-B04)    <- store-and-forward backbone,
      [R1]========[R2]                    signed hop attestations
        \        //   \
         \      //     \
TIER 3    HUB (Group C, N-C01..N-C03)    <- ward/LGA aggregation,
            [H-WARD]====[H-LGA]           local CRDT replicas,
              ||         ||               edge inference (M-03..M-06)
              ||  (optional uplinks —    ||
              ||   never critical path)  ||
TIER 4    COMMAND (Group D, N-D01, N-D02)
          [DISPLAY]====[CONSOLE]         <- signed role-bound control,
                                            dual-operator rule (N-D02)
```

Tier rules:

1. Traffic flows up (event path) and down (control path) along tier adjacency. No tier-1 to tier-3 direct links; a beacon that can reach a hub directly still routes through a relay, preserving the attestation chain.
2. Every forwarded message carries a hop attestation appended by each relay (signature over message hash + previous attestation). The hub can therefore verify the path, not just the payload.
3. Tier 4 control messages traverse down with role binding; relays drop unsigned or out-of-role control traffic and log the attempt.
4. Uplinks exist only at tiers 3–4 and are strictly optional. Removing every uplink degrades remote oversight, never local function.

## 4. RF Link Budget

Representative links for a typical LGA (Local Government Area) deployment: ward-scale hops (2 km), inter-relay backbone (8 km), and tier-4 long haul across difficult terrain (15 km, SF12/CR 4/8). Free-space path loss is derated by a terrain/foliage allowance per row — this is a field budget, not a laboratory budget.

| Parameter | Ward hop (2 km) | Backbone hop (8 km) | Long haul (15 km) |
|---|---|---|---|
| Frequency | 433 MHz | 433 MHz | 433 MHz |
| Tx power | +14 dBm | +20 dBm | +20 dBm |
| Tx antenna gain | +2 dBi | +3 dBi | +5 dBi |
| Rx antenna gain | +2 dBi | +3 dBi | +5 dBi |
| Free-space path loss | 65.2 dB | 77.2 dB | 82.7 dB |
| Terrain/foliage allowance | 10 dB | 15 dB | 20 dB |
| Total path loss (budgeted) | 75.2 dB | 92.2 dB | 102.7 dB |
| Spreading factor | SF7 | SF10 | SF12 |
| Rx sensitivity | −123 dBm | −132 dBm | −137 dBm |
| Received power | −57.2 dBm | −66.2 dBm | −72.7 dBm |
| **Link margin** | **+65.8 dB** | **+65.8 dB** | **+64.3 dB** |

Reading: even the long-haul tier carries > 60 dB of margin. This is deliberate over-engineering — field conditions (rain season foliage, ad-hoc mast heights, antenna aging) consume margin unpredictably, and a sovereign network must survive its operators' worst day, not its best. Margin this large also permits substantial derating of mast height and antenna quality where logistics demand it, which is cost-relevant per the [Manufacturing Specification](../aegis-global/manufacturing-spec.md).

## 5. Store-and-Forward Semantics

1. **Durable buffering.** Each relay buffers messages in non-volatile storage with sequence numbers and expiry. A relay that loses power loses nothing; on restoration it resumes forwarding in sequence order. Six-hour relay outage is a tested design case ([Node Types §7](node-types.md), Group B test).
2. **At-least-once with dedup.** Delivery is at-least-once; hubs deduplicate by message ID. The system prefers a duplicate it can drop to a loss it cannot detect.
3. **Backpressure.** When a hub's local storage crosses its watermark, it signals upstream relays to hold; beacons continue sensing and their event queues absorb the pause. No tier ever drops silently.
4. **Priority lanes.** Tamper events and safety alerts preempt routine telemetry. A node's dying transmission (post-tamper event) is the highest-priority frame in the protocol.

## 6. Offline Sync (CRDT)

Hub-local state — event logs, node health, operator annotations, and (for N-C03) clinical record bundles — is replicated as CRDTs per the semantics defined in [FHIR R4 Native §4](../clai-os/fhir-r4-native.md). Properties restated at mesh level:

- **Convergence is algebraic.** Any two hubs exchanging the same update set converge to identical state regardless of order or timing. Episodic inter-hub links (a weekly patrol relay visit, for instance) are sufficient.
- **18-hour zero-bandwidth envelope.** Every node tier is storage- and power-sized so that 18 hours of total isolation produces zero functional loss locally and a bounded, fully-convergent sync backlog at reconnect.
- **Sneakernet is a first-class transport.** An N-B04 mobile relay physically carried between isolated hubs performs the same CRDT state exchange as a radio link. Bandwidth-zero includes the case where even the mesh's inter-hub RF path is absent.

## 7. Security Posture

All frames are signed at origin; all hop attestations are chained (§3.2); key material is per-node, provisioned at manufacture and zeroized on tamper ([Node Types](node-types.md) §2.4). There is no mesh-wide master key: compromising one node yields one node's keys and one node's role, and the role system (beacons can't route, relays can't command, commands need tier-4 roles) bounds what that yields. Replay protection is by sequence number plus attestation chain; the Group A falsifiability test includes a live replay attempt for exactly this reason.

---

## Falsifiability Test

**Claim:** The mesh delivers signed, ordered, loss-free event traffic across a four-tier topology with > 60 dB link margin on its hardest hop, and survives 18 hours of total isolation with zero local degradation.

**Test 1 (margin):** Survey a representative 15 km tier-4 path in the target LGA. Compute FSPL, apply the 20 dB terrain allowance, and measure actual received power with a field strength meter. If measured margin falls below +30 dB (half the budgeted margin), §4 is falsified for that terrain class and the deployment plan must add a relay.

**Test 2 (store-and-forward):** Execute the Group B test from [Node Types §7](node-types.md) — link severance plus 6-hour relay power-down. Any message loss or ordering violation falsifies §5.

**Test 3 (bandwidth-zero):** Disconnect all uplinks in a pilot ward for 18 hours. If any sensing, alerting, or display function degrades, §1's doctrine is falsified; record a signed REGRESSION record (S50 class C) and halt scale-up.
