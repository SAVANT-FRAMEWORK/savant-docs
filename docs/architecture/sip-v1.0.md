---
title: SIP v1.0 — Sovereign Invocation Protocol
description: The trigger grammar and routing law that invokes work into the SPOS fractal.
---

# SIP v1.0 — Sovereign Invocation Protocol

**Version:** 1.0.0
**Author:** Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
**Last Updated:** 2026-08-11
**SHA-256:** [PENDING-FIRST-RELEASE]

---

## 1. Purpose and Standing

The Sovereign Invocation Protocol (SIP) is the grammar by which work enters the [SPOS v1.0](spos-v1.0.md) fractal. An invocation consists of a trigger prefix, a scope, and a context block. The trigger prefix is not decoration: it determines the SPOS layer of the work, the checkpoint class under which the output will be judged, and the prohibitions that attach to the acting persona. An invocation without a valid trigger is ungoverned work and is refused at the boundary.

SIP v1.0 is ratified under S50-ABSOLUTE checkpoint class A. The trigger set is closed: new triggers enter only by constitutional amendment, never by convention.

## 2. The Fifteen Trigger Prefixes

| # | Trigger | Function | Typical Output |
|---|---|---|---|
| 1 | `ARCHITECT` | Designs system structure, layer placement, and interface contracts. | Architecture specification |
| 2 | `AUDIT` | Examines an artifact against the predicate battery of its checkpoint class. | Signed verdict record |
| 3 | `STRATEGIZE` | Produces horizon-bound objectives and doctrine rationale. | L2 objective set |
| 4 | `HARDEN` | Identifies and closes failure modes in a design or artifact. | Hardening diff + rationale |
| 5 | `EXECUTE` | Performs deterministic production to an accepted specification. | Built artifact |
| 6 | `SYNTHESIZE` | Merges multiple verified inputs into one coherent artifact without new claims. | Synthesis document |
| 7 | `DECOMPOSE` | Breaks an objective into an ordered task graph with acceptance criteria. | Task graph |
| 8 | `REDTEAM` | Adversarially attacks a design, claim, or artifact to locate falsification. | Red-team findings record |
| 9 | `FORESIGHT` | Projects scenario branches and leading indicators over a declared horizon. | Scenario register |
| 10 | `OPTIMIZE` | Improves a measurable property of an artifact under fixed constraints. | Optimization diff + metric delta |
| 11 | `COMPLETE` | Brings a partially specified deliverable to full constitutional form. | Completed specification |
| 12 | `SAFETY` | Evaluates harm potential and safety invariants; may halt any pipeline. | Safety verdict (GO / NO-GO) |
| 13 | `RAG` | Retrieves and grounds claims against the approved corpus only. | Grounded citation record |
| 14 | `BUILD` | Constructs infrastructure, tooling, firmware, or deployment scaffolding. | Build artifact + manifest |
| 15 | `ORCHESTRATE` | Sequences and supervises multi-agent work across layers. | Orchestration plan + ledger |

## 3. The Ten One-Letter Shortcuts

For operator efficiency, ten triggers admit a one-letter shortcut. Shortcuts are exact aliases; they change nothing about routing, checkpoint class, or prohibition. The mapping is fixed:

| Shortcut | Trigger | Mnemonic |
|---|---|---|
| `A` | ARCHITECT | Architect |
| `B` | BUILD | Build |
| `R` | REDTEAM | Red-team |
| `S` | STRATEGIZE | Strategize |
| `H` | HARDEN | Harden |
| `E` | EXECUTE | Execute |
| `O` | ORCHESTRATE | Orchestrate |
| `C` | COMPLETE | Complete |
| `T` | AUDIT | au**T**it (audit; `A` is occupied by ARCHITECT) |
| `D` | DECOMPOSE | Decompose |

### 3.1 Why SAFETY Has No Shortcut — Deliberate Policy

`SAFETY` is the only trigger deliberately denied a one-letter form. The policy rationale is constitutional, not ergonomic: a safety invocation must always be the product of a deliberate, fully-spelled act. One-letter shortcuts exist to reduce friction, and friction is precisely what a safety halt must never lose. No abbreviation, alias, or autocomplete of `SAFETY` is permitted anywhere in the framework — including in tooling, shell aliases, and agent role cards. Violation is a class-A defect. Five triggers carry no shortcut for collision or policy reasons: SAFETY (policy), SYNTHESIZE (collides with `S`→STRATEGIZE), FORESIGHT (no unique non-colliding letter admitted), OPTIMIZE (collides with `O`→ORCHESTRATE), and RAG (collides with `R`→REDTEAM).

## 4. Routing Table: Trigger → SPOS Layer → Checkpoint Class

Checkpoint classes are defined in [S50-ABSOLUTE](s50-absolute.md) §3: **A** (constitutional), **B** (structural), **C** (artifact), **D** (operational).

| Trigger | Shortcut | SPOS Layer | Checkpoint Class | Governing Load-Bearing Prompts |
|---|---|---|---|---|
| ARCHITECT | A | L2 Strategic | A | SPOS-P5, SPOS-P6 |
| AUDIT | T | L1 Audit | A | SPOS-P3, SPOS-P4 |
| STRATEGIZE | S | L2 Strategic | B | SPOS-P5, SPOS-P6 |
| HARDEN | H | L3 Tactical | B | SPOS-P7, SPOS-P8 |
| EXECUTE | E | L5 Execution | C | SPOS-P11, SPOS-P12 |
| SYNTHESIZE | — | L3 Tactical | C | SPOS-P7 |
| DECOMPOSE | D | L3 Tactical | B | SPOS-P7, SPOS-P8 |
| REDTEAM | R | L1 Audit | B | SPOS-P4 |
| FORESIGHT | — | L2 Strategic | C | SPOS-P5 |
| OPTIMIZE | — | L3 Tactical | C | SPOS-P8, SPOS-P11 |
| COMPLETE | C | L3 Tactical | B | SPOS-P7, SPOS-P11 |
| SAFETY | — (by policy) | L1 Audit | A | SPOS-P3, SPOS-P4 |
| RAG | — | L5 Execution | C | SPOS-P11 |
| BUILD | B | L5 Execution | C | SPOS-P11, SPOS-P12 |
| ORCHESTRATE | O | L3 Tactical | B | SPOS-P8, SPOS-P9 |

Routing invariants:

1. Every trigger routes to **exactly one** layer. No ambiguity is tolerated at the boundary.
2. Checkpoint class is a function of the trigger, not of the operator's confidence. An operator may request a *stricter* class than the table specifies (escalation is always permitted), never a looser one.
3. `AUDIT` and `SAFETY` both route to L1 because both are veto-bearing functions; origination layers (L2–L5) may never self-certify.

## 5. Context Block Templates

Every SIP invocation carries a context block. Two canonical forms exist.

### 5.1 Minimal Context Block

The minimal form is sufficient for routine class-C/D work where the task graph position is unambiguous:

```
SIP CONTEXT BLOCK — MINIMAL
  trigger:        <one of the 15 prefixes, or valid shortcut>
  scope:          <single declarative sentence naming the work>
  inputs:         <list of artifact IDs or "none">
  acceptance:     <one falsifiable acceptance criterion>
```

### 5.2 Maximal Context Block

The maximal form is mandatory for all class-A and class-B work, all cross-layer orchestration, and any invocation touching L0-adjacent material:

```
SIP CONTEXT BLOCK — MAXIMAL
  trigger:            <full prefix (shortcuts NOT permitted at class A/B)>
  shortcut_used:      none
  scope:              <single declarative sentence naming the work>
  parent_objective:   <L2 objective ID this work serves; "L0-CONSTITUTIONAL" for
                       constitutional work>
  task_graph_ref:     <L3 task graph node ID>
  inputs:             <artifact IDs with version pins and expected SHA-256>
  corpus_constraints: <approved RAG corpus scope, or "corpus-free">
  prohibitions:       <explicit restatement of layer prohibitions for this task>
  acceptance:         <falsifiable acceptance criteria, enumerated>
  checkpoint_class:   <A | B | C | D — must match or exceed routing table>
  escalation_path:    <named persona one layer up>
  attribution:        Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
```

Two rules bind both forms. First, at class A/B the full trigger must be spelled; shortcuts are a class-C/D convenience only. Second, the `prohibitions` field of the maximal block must restate the layer prohibitions in the operator's own words — a copied-and-pasted prohibition is treated as an unread prohibition and fails checkpoint predicate C-3.

## 6. Refusal Semantics

The boundary refuses an invocation when: the trigger is absent or unknown; a shortcut is used at class A/B; the context block fails schema; or a `SAFETY` halt is active anywhere in the affected pipeline. Refusals are logged as operational events (class D) and are not themselves failure findings — refusal is the protocol working as designed.

---

## Falsifiability Test

**Claim:** The trigger set is closed, routing is total and unambiguous, and SAFETY is unreachable by abbreviation.

**Test 1 (totality):** For each of the fifteen triggers, resolve Section 4 to a unique (layer, checkpoint class) pair. Any row yielding zero or two pairs falsifies totality.

**Test 2 (closure):** Attempt to invoke with a sixteenth prefix. If the boundary produces work rather than a logged refusal, closure is falsified.

**Test 3 (policy):** Grep all framework tooling, role cards, and shell configuration for any single-character or abbreviated alias resolving to SAFETY. One hit anywhere falsifies §3.1 and is a class-A defect.
