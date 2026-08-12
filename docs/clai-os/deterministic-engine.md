---
title: CLAI-OS — Deterministic Clinical Engine
description: Deterministic-first clinical reasoning with explicit-uncertainty failure semantics and ECDSA-256 signed output.
---

# CLAI-OS — Deterministic Clinical Engine

**Version:** 1.0.0
**Author:** Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
**Last Updated:** 2026-08-11
**SHA-256:** [PENDING-FIRST-RELEASE]

---

## 1. Design Doctrine: Deterministic First

CLAI-OS reasons about patients the way an avionics system reasons about an aircraft: from explicit state, through explicit transitions, to explicit conclusions. Probabilistic inference is admitted only as an annotative layer on top of a deterministic core; it may rank, it may never decide. The doctrine exists because clinical deployment in low-resource settings must survive audit by regulators, by clinicians, and by patients — and a system that cannot show its transitions cannot be audited.

Three consequences follow. First, every conclusion is reproducible: same patient state, same ruleset version, same conclusion. Second, every conclusion is explainable: the transition path *is* the explanation, not a post-hoc rationalization. Third, every failure is bounded: the engine has a designed failure mode (§4), not an emergent one.

## 2. State Machine Core

The clinical engine is implemented as a hierarchy of finite state machines. Each monitored clinical domain (e.g., maternal triage, malaria suspicion, dehydration assessment) is a machine; the patient session is the orchestrating machine.

```
PATIENT SESSION MACHINE (top level)

  +-----------+   intake valid    +-----------+   chain complete   +-------------+
  |  IDLE     | ----------------> | ASSESSING | -----------------> | CONCLUDED   |
  +-----------+                   +-----------+                    +-------------+
       ^                               |                                 |
       |                               | chain broken at                 | signed report
       |                               | any stage                       | emitted
       |                               v                                 v
  +-----------+  reset        +------------------+              [FHIR DiagnosticReport]
  | (restart) | <------------ | UNCERTAIN-HALT   |              [ECDSA-256 signed]
  +-----------+               +------------------+
                                       |
                                       | clinician resolves /
                                       | new evidence arrives
                                       v
                                  (re-enter ASSESSING
                                   at the broken stage)
```

Transition rules are data, not code: each machine is declared as a versioned ruleset artifact (transition table + predicate definitions), ratified under S50 checkpoint class B and hash-chained in the prompt/ruleset genealogy. A ruleset amendment follows the same regression-detection battery as any governed artifact — constraint coverage, authority scope, falsifiability preservation, output class stability — so a ruleset can never silently lose a guardrail.

## 3. The Six-Stage Reasoning Chain

Every clinical conclusion is produced by a fixed six-stage chain. Stages may not be skipped, reordered, or merged. If any stage cannot complete on the available evidence, the chain halts at that stage and the session enters UNCERTAIN-HALT (§4).

| Stage | Name | Input | Output | Halting Condition |
|---|---|---|---|---|
| 1 | **Evidence** | Raw observations (FHIR Observation set, vitals, history items) | Normalized evidence list, each item with source and timestamp | Evidence fails schema or provenance check |
| 2 | **Pattern** | Normalized evidence | Candidate clinical patterns matched by deterministic rule evaluation | No pattern matches above the rule-defined minimum |
| 3 | **Deviation** | Candidate patterns + reference ranges | Deviation vector: how far, in which direction, on which variables | Reference ranges undefined for a required variable |
| 4 | **History** | Deviation vector + longitudinal patient record | Trajectory assessment (new / chronic / resolving / worsening) | Longitudinal record required by rule but absent |
| 5 | **Validation** | Trajectory + contra-indication rules | Validated candidate set; contradictions removed | All candidates eliminated |
| 6 | **Conclusion** | Validated candidate set | Ranked conclusion set with full transition trace | — (always completes if reached) |

The transition trace recorded across stages 1–6 is part of the output. A CLAI-OS DiagnosticReport always answers not only *what* was concluded but *which transitions fired* — the audit trail is the explanation.

## 4. The Explicit-Uncertainty Failure Mode

The designed failure mode of CLAI-OS is the UNCERTAIN-HALT. The engine **fails transparently, not catastrophically**.

Concretely: when the chain halts, the engine emits an explicit uncertainty declaration naming the stage at which the chain broke, the predicate that failed, the evidence that was missing or contradictory, and the action required to resume (typically: a named observation, a clinician decision, or a referral). The system never interpolates across a gap, never averages away a contradiction, and never emits a conclusion of lower confidence dressed as a normal one. There is no "probable diagnosis" output class. A clinician reading CLAI-OS output will always be able to distinguish three states instantly: concluded (signed), halted (with named cause), and not yet assessed. This is the clinical analogue of the S50 rule: there is no "proceed with warning" state.

## 5. Signing and Anti-Tamper

Every concluded report is signed **ECDSA with curve P-256** over the SHA-256 digest of the canonical report serialization. The signing key is generated and held within the deployment's trust boundary; the corresponding verification key is published to the supervising institution.

Anti-tamper properties are structural, not policy-based:

1. **Digest binding.** Any post-hoc edit to the report — one changed value, one changed word — invalidates the signature. Verification is byte-exact and can be performed offline by any party holding the public key.
2. **Chain binding.** Each report embeds the hash of the ruleset version that produced it. A report therefore cannot be re-attributed to a different (e.g., looser) ruleset after the fact; the ruleset itself is genealogy-chained per [S50-ABSOLUTE](../architecture/s50-absolute.md).
3. **Ledger binding.** Session-level event logs (chain entries, halts, signings) are hash-chained and periodically anchored per the S50 anchoring procedure.
4. **Tamper-evident storage.** Reports are stored as FHIR resources (see [FHIR R4 Native](fhir-r4-native.md)) under patient-owned encryption; the signature lives *inside* the encrypted envelope, so decryption authority and verification authority are separable.

## 6. Relationship to Probabilistic Components

Where probabilistic models are attached (risk ranking, triage prioritization among concluded cases), they consume the deterministic chain's output and annotate it. They are forbidden from: introducing a conclusion absent from the validated candidate set; suppressing a validated candidate; or altering a halt decision. Violation of any of these is a class-A defect, because it converts an auditable system into an unauditable one.

---

## Falsifiability Test

**Claim:** CLAI-OS conclusions are reproducible, explainable from the transition trace, and incapable of silent catastrophic failure.

**Test 1 (reproducibility):** Replay any archived session — same evidence set, same pinned ruleset hash. If the conclusion set differs, determinism is falsified; file a REGRESSION record.

**Test 2 (traceability):** Select any signed DiagnosticReport. Reconstruct the stage-1→6 transition path from the embedded trace. If any transition lacks a firing rule reference in the pinned ruleset, explainability is falsified.

**Test 3 (failure semantics):** Withhold a rule-required observation from a test session. If the engine emits any conclusion-bearing output rather than an UNCERTAIN-HALT naming the missing observation, §4 is falsified and the deployment must be halted as a class-A defect.
