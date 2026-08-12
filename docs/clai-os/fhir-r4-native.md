---
title: CLAI-OS — FHIR R4 Native Resource Layer
description: The permanently open FHIR R4 clinical data layer — patient-owned encryption, offline CRDT sync, NDPR/GDPR alignment.
---

# CLAI-OS — FHIR R4 Native Resource Layer

**Version:** 1.0.0
**Author:** Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
**Last Updated:** 2026-08-11
**SHA-256:** [PENDING-FIRST-RELEASE]

---

## 1. Standing: The Permanently Open Layer

The FHIR R4 resource layer of CLAI-OS is **permanently open**, in the sense defined by the CAA (Constitutional Architecture Accord): the resource schemas, profiles, extension definitions, and sync semantics in this document are irrevocably placed in the open domain. They may not be closed, licensed against, or withdrawn in any future version of the framework. The reasoning core above this layer ([Deterministic Engine](deterministic-engine.md)) and the hardware below it (AEGIS-NG) carry their own IP posture; this layer does not, by constitutional decision. A health record standard that can be enclosed is a liability to every patient on it.

## 2. Resource Architecture

CLAI-OS is FHIR **R4 (4.0.1) native**: FHIR resources are the internal representation, not an export format. Three resource families carry the clinical load.

### 2.1 Patient

| Aspect | Specification |
|---|---|
| Profile | CLAI-Patient (FHIR R4 Patient + constrained extension set) |
| Identity | Pseudonymous system identifier at rest; legal identity resolvable only through a separately-held mapping under patient control |
| Required elements | `identifier` (system ID), `gender`, `birthDate` (or declared age band where birth records are unavailable — a documented extension, not a hack) |
| Prohibited at rest | Unencrypted legal name, national ID number, precise address (ward/LGA level only) |

### 2.2 Observation

| Aspect | Specification |
|---|---|
| Profile | CLAI-Observation (FHIR R4 Observation) |
| Vocabulary | LOINC codes where they exist; a published local code system (CLAI-CS) where they do not, with explicit LOINC mapping table for every local code |
| Provenance | Every Observation carries `performer` and device provenance; observations from AEGIS-NG nodes carry the node's signed attestation in `extension` |
| Integrity | Observation sets feeding the reasoning chain are digest-bound into the session trace (see Deterministic Engine §3, Stage 1) |

### 2.3 DiagnosticReport

| Aspect | Specification |
|---|---|
| Profile | CLAI-DiagnosticReport (FHIR R4 DiagnosticReport) |
| Content | Conclusion set, full six-stage transition trace, pinned ruleset hash, halt declarations (when the chain broke) |
| Signature | ECDSA P-256 detached signature over the canonical serialization, carried in a defined `extension`; verification is offline-capable |
| States | `final` (concluded and signed), `preliminary` is **never used** for conclusions — a halted session emits an uncertainty declaration resource, not a preliminary report. There is no "proceed with warning" state at the data layer either. |

## 3. Patient-Owned Encryption (AES-256)

The patient's record is encrypted at rest with **AES-256-GCM**, and the key hierarchy is patient-owned:

```
KEY HIERARCHY
  Patient Master Key (PMK)
    |-- derived: Record Encryption Key (REK) per record bundle
    |-- derived: Delegation Key (DK) per authorized clinician/facility, time-boxed
```

- The PMK is generated at enrollment and held under the patient's control (card, mnemonic, or designated custodian under documented consent law).
- Clinicians receive time-boxed Delegation Keys scoped to named record bundles. Revocation is immediate and local: re-encryption is not required because delegation is by key wrapping, not by re-keying the record.
- The platform operator cannot decrypt records. This is enforced by construction (the operator never possesses the PMK), not by policy. A system that *promises* not to read is weaker than one that *cannot* read; CLAI-OS is the latter.
- The ECDSA report signature (Deterministic Engine §5) lives inside the encrypted envelope: decryption authority and verification authority are separable, so a regulator can verify authenticity without gaining read access.

## 4. Offline-First CRDT Sync

CLAI-OS is designed for environments where connectivity is episodic. The design target is explicit: **18 hours of zero-bandwidth operation** with no functional degradation at the point of care.

Mechanism:

1. **Local-first storage.** Every facility node holds a complete local replica of its active record set. All clinical operations — assessment, reasoning, report signing — execute against the local replica. The network is never on the care pathway.
2. **CRDT replication.** Record bundles replicate as CRDTs (state-based, with per-field last-writer-wins registers for clinical scalars and grow-only sets for observations and reports). Observations and DiagnosticReports are append-only by nature, which is why the grow-only set carries them without conflict semantics at all.
3. **Bounded divergence.** At reconnect, replicas exchange state digests first, then deltas. Merge is deterministic and commutative: any two replicas receiving the same update set converge to the identical state, regardless of order. Convergence is a theorem of the CRDT algebra, not a hope.
4. **Conflict surface.** The only genuinely concurrent-writable fields are administrative (scheduling, bed assignment). These carry last-writer-wins with human-readable conflict notices to the facility queue. Clinical facts never last-writer-win; they accumulate.
5. **18-hour envelope.** Local replica capacity, sync payload budgets, and power budgets (aligned with AEGIS-NG node autonomy) are sized so that 18 hours of total connectivity loss — an unusually severe field event, not a routine one — leaves care delivery untouched. Sync backlog from 18 hours of operation converges in under 15 minutes on a restored 3G-class link.

## 5. NDPR / GDPR Alignment

The data-protection posture maps onto both the Nigeria Data Protection Regulation (NDPR) and the GDPR, under the configuration-as-compliance model specified in [P61–P70](../compliance/P61-P70.md):

| Principle | Mechanism in this layer |
|---|---|
| Data subject ownership | Patient-owned PMK; operator cannot decrypt (§3) |
| Consent | Delegation Keys are the machine-enforceable form of consent; issuance and revocation are consent events, logged and signed |
| Minimization | Pseudonymous identity at rest; prohibited-elements list in the Patient profile (§2.1) |
| Portability | The record is FHIR R4 end-to-end; export is a decryption away and requires no vendor cooperation |
| Erasure | Crypto-shredding: destroy the PMK-derived REKs; the ciphertext that remains is mathematically inert |
| Breach posture | An operator-side breach discloses ciphertext only; this is disclosed plainly in deployment agreements |

## 6. What Is Deliberately Not in This Layer

No analytics pipelines, no advertising surfaces, no secondary-use licensing, no third-party trackers. The FHIR layer exists to carry clinical facts between a patient, their clinicians, and the reasoning engine. Anything else would be a violation of the layer's open standing, and is listed here so that its absence is auditable rather than accidental.

---

## Falsifiability Test

**Claim:** This layer is open, patient-owned, offline-survivable to 18 hours, and convergent under partition.

**Test 1 (openness):** Implement a DiagnosticReport consumer from §2.3 alone, using a stock FHIR R4 library, with no framework code. If the profile requires an undocumented extension or a proprietary codec, the CAA openness guarantee is falsified.

**Test 2 (patient ownership):** Attempt operator-side decryption of a record bundle without any patient-derived key material. Success — by any path, including backups and logs — falsifies §3 and is a class-A defect.

**Test 3 (convergence):** Partition two facility replicas for 18 simulated hours, write to both (including concurrent administrative edits), reconnect, and verify byte-identical merged state plus human-readable conflict notices for the concurrent administrative writes. Any divergence falsifies §4.3.
