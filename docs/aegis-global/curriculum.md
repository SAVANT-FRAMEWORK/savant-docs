---
title: AEGIS-GLOBAL — Local Engineer Certification Curriculum
description: Capacity transfer as the architect's only revenue — per-engineer certification ([Commercial licensing terms — inquiries via the GitHub organization]), delivered in multiple languages.
---

# AEGIS-GLOBAL — Local Engineer Certification Curriculum

> **Sanitized for public release:** 2026-08-18 — certification fee amount redacted and replaced with `[Commercial licensing terms — inquiries via the GitHub organization]` per SAVANT commercial-pricing policy; all other content preserved verbatim.

**Version:** 1.0.0
**Author:** Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
**Last Updated:** 2026-08-11
**SHA-256:** [PENDING-FIRST-RELEASE]

---

## 1. Constitutional: Training Is the Only Revenue

The AEGIS-GLOBAL commercial model contains exactly one revenue line for the architect: **certification training — [Commercial licensing terms — inquiries via the GitHub organization]**. There are no hardware margins, no per-unit royalties, no licensing rents on deployed nodes, and no recurring platform fees. This is a deliberate constitutional decision, and it is stated at the top of this document because it explains everything below it.

The reasoning is structural. A hardware margin makes the architect's interest diverge from the operator's: every node sold is revenue, so the architect benefits from dependency, from replacement cycles, proprietary spares, and knowledge asymmetry. A training-only model aligns the architect's interest with *capacity transfer*: revenue exists precisely when an engineer no longer needs the architect. The architect is paid once, at the moment dependency ends. This is the capacity-building frame, and it is not rhetoric, it is the only line on the invoice.

Consequences: the [Manufacturing Specification](manufacturing-spec.md) is complete and openly readable; the BOM is honestly marked rather than obscured; and the curriculum below teaches *everything* required to manufacture, deploy, and maintain the node family without recourse to the architect.

## 2. Certification at a Glance

| Attribute | Value |
|---|---|
| Fee | [Commercial licensing terms — inquiries via the GitHub organization] (one-time; no renewal fees, no seat licenses) |
| Duration | 10 instructional days + 2 assessment days |
| Cohort size | 12–20 (hands-on stations cap cohort size; this is a workshop, not a lecture series) |
| Prerequisite | Secondary-school technical literacy *or* demonstrated workshop aptitude (see §5, low-literacy adaptation); no prior electronics qualification required |
| Outcome | AEGIS-GLOBAL Certified Engineer — authorized to assemble, flash, deploy, maintain, and QC the full N-A01…N-D02 family |
| Assessment | Practical only. There is no written examination (see §5) |

## 3. Curriculum Modules

Five modules, each with a defined competence gate. A candidate who fails a gate repeats that module's practical, not the whole course.

### Module 1 — Assembly (Days 1–2)

Competence: build a complete node from kitted components to power-on.

- Reading the BOM and variant deltas ([Manufacturing Specification §3](manufacturing-spec.md)); recognizing registry-marked cells and the STOP-grade rule against fabricated part numbers
- Through-hole and connector-level assembly; enclosure fitting; solar array and storage cell integration
- Anti-tamper mesh switch installation, potting discipline, and the arming self-test at closure
- **Gate:** candidate assembles an N-A01 beacon that passes power-on and tamper-arm self-test.

### Module 2 — Flashing & Provisioning (Days 3–4)

Competence: take a built node from blank silicon to manifest-complete.

- F-series firmware images (F-01…F-12), hash verification against pinned build manifests, locked flashing over the debug interface
- Per-node key injection into the secure element; why no key is ever logged in plaintext
- Manifest construction: unit serial ↔ firmware hash ↔ key injection record hash-chain
- M-series model loading (M-01…M-06, TFLite Micro) on M-capable nodes; model hash pinning
- **Gate:** candidate provisions an N-C01 hub whose manifest audits clean end-to-end.

### Module 3 — Field Deployment (Days 5–7)

Competence: deploy a working mesh tier in real terrain.

- Survey discipline: binding beacon location at deployment (no GPS on beacons,location is surveyed, signed into the manifest, never radio-negotiated)
- Mast work and antenna installation; reading the link budget ([Mesh Protocol §4](../aegis-ng/mesh-protocol.md)) and applying the terrain allowance
- Tier discipline: placing relays and hubs, verifying attestation chains, commissioning store and forward paths
- Solar siting: irradiance, shading, seasonal allowance
- **Gate:** candidate team deploys a three-beacon, one-relay, one-hub cell that passes the Group A and Group B field falsifiability tests.

### Module 4 — Maintenance & Repair (Days 8–9)

Competence: keep a deployed network alive for years without external support.

- Scheduled inspection: storage cell health, connector corrosion, mast hardware, panel cleaning
- Failure diagnosis from attestation chains and heartbeat telemetry; isolating a fault to node, link, or hub
- Field repair within the anti-tamper regime: what may be serviced (panels, antennas, masts) vs. what a tamper event correctly forbids (opening a sealed enclosure — replace, never open)
- CRDT sync hygiene: verifying convergence after isolation events, sneakernet sync via N-B04
- **Gate:** candidate diagnoses and resolves two seeded faults on a live training cell, one of which is a relay power fault resolved without any uplink.

### Module 5 — Quality Control & Verification (Day 10)

Competence: act as an independent QC authority over manufactured or repaired units.

- The seven QC gates of the [Manufacturing Specification §6](manufacturing-spec.md), executed with field equipment
- Executing the group falsifiability tests ([Node Types §7](../aegis-ng/node-types.md)) as a verifier, not just an operator
- Writing a QC record; when to refuse a unit; the discipline that QC gates are not compressible
- **Gate:** candidate runs a full QC pass on three units — one clean, one seeded with an RF fault, one seeded with a tamper-circuit fault — and correctly accepts the first and refuses the other two, with correct records.

### Assessment (Days 11–12)

All five gates re-verified under observation on unfamiliar units. Certification is issued per candidate with a signed record; the register of certified engineers is itself a governed artifact (S50 class C), because a credential that can be forged is worse than none.

## 4. Multi-Language Delivery 

The curriculum is delivered in **English, French,
Hausa, igbo, yoruba and other major international languages. This is a delivery requirement, not a courtesy: an engineer who must translate instruction mentally while holding a soldering iron is an engineer being trained worse.

- All instructional materials, station cards, and gate checklists exist in all six languages; translations are versioned artifacts and are regression checked like any other governed document — a translated checklist that drops a step is a class-C defect.
- Instructors are recruited from prior cohorts wherever possible, so that instruction in each language is delivered by an engineer, not an interpreter.
- Assessment is language-neutral by construction: it is practical. The gates in §3 are demonstrated, not described.

## 5. Low-Literacy Adaptation

Literacy is not a certification prerequisite, because the competences being certified are manual and procedural, and because excluding low-literacy candidates would exclude exactly the field technicians the program exists to create.

- **No written examination.** All gates are demonstrations judged against observable criteria.
- **Pictographic station cards.** Every procedure has a wordless sequential card form (numbered, illustrated steps) alongside its text form; the two forms are regression-checked against each other so the pictographic version can never silently drop a step.
- **Oral-first instruction with demonstration pairing.** Every concept is shown before it is named; candidates perform each operation alongside the instructor before performing it alone.
- **Memory scaffolding.** Hash verification, manifest chaining, and QC sequences are taught as fixed physical routines (point, read aloud, compare, mark) that do not require reading comprehension to execute correctly.
- **Honesty of the adaptation.** Where a task genuinely requires text (reading a registry part number, verifying a hash string), the candidate is taught the *minimum sufficient literacy* for that exact task which is recognizing the marked import cell, matching characters — rather than being waived past the safety-critical content. Adaptation lowers the entry barrier; it never lowers the gate.

## 6. Economics of the Model, Stated Plainly

A cohort of 16 engineers yields $15,600 in training revenue. It is the entirety of the architect's income from that cohort, forever. The cohort's output assembled nodes, deployed cells, maintained networks, QC authority belongs to the operators and their sovereign partners. 

---

## Falsifiability Test

**Claim:** A certified graduate can assemble, flash, deploy, maintain, and QC the full node family without further recourse to the architect, and the training-only revenue claim is real.

**Test 1 (capacity transfer):** Select any certified cohort. Without architect involvement, have it execute Modules 1→5 end to end on fresh kits, then run the four group falsifiability tests of [Node Types §7](../aegis-ng/node-types.md). Any failure attributable to curriculum content (rather than candidate performance) falsifies §3; record a REGRESSION record (S50 class C) against the module.

**Test 2 (revenue exclusivity):** Audit the program's invoices and procurement flows for any deployment. If any line item beyond the certification fee accrues to the architect — hardware margin, royalty, platform fee, "support subscription" — §1 is falsified and the misstatement is a class-A defect against every grant narrative that cited the capacity-building frame.

**Test 3 (low-literacy honesty):** Certify a low literacy candidate cohort by the pictographic/oral pathway, then independently re-run their QC judgments (Module 5 gate) on seeded units. If the pass rate diverges materially from literate cohorts, the adaptation is lowering the gate rather than the barrier — §5 is falsified.
