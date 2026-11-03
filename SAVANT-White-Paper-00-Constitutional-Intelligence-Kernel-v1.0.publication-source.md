<div class="titlepage">
<p class="series">CONSTITUTIONAL INTELLIGENCE SERIES · PAPER 0</p>
<h1 class="title">Constitutional Intelligence</h1>
<p class="subtitle">A Formal Specification of Bounded Machine Authority Under Uncertainty and Constraint</p>
<p class="descriptor">The SAVANT Machine-Authority Kernel: definitions, axioms, state variables, authority algebra, invariants, transition rules, conflict operators, falsifiable hypotheses, implementation schema, and candidate technical mechanisms</p>
<p class="author">Author: Dr. Christabel Odeta (sole author)</p>
<p class="attrib">Source Architecture: Dr. Christabel Odeta - SAVANT / CLAI-OS / AEGIS-GLOBAL</p>
<p class="compiled">Compiled under: the reconciled SAVANT PRIME architecture · ARCHITECT persona</p>
<p class="version">Version 1.0 · 2026-10-03</p>
<p class="c0">C0 INFORMATIONAL · DESIGN SPECIFICATION, UNVALIDATED UNTIL THE §13 EXPERIMENTS EXECUTE · NOTHING IN THIS DOCUMENT CONFERS CLINICAL, LEGAL, FINANCIAL, OR SAFETY AUTHORITY · CANDIDATE MECHANISMS (§15) REQUIRE PRIOR-ART SEARCH BEFORE ANY PATENT CONCLUSION</p>
</div>
<div class="pagebreak"></div>

# Document Control & Epistemic Contract

### 0.1 Provenance and Reconciliation

This specification executes the closing directive of the SVT Architect Analysis (source document I): that Paper 0 of the SAVANT research-and-build program shall be “the full formal specification of the Constitutional Intelligence / Machine Authority Kernel, definitions, axioms, state variables, authority algebra, invariants, transition rules, conflict operators, falsifiable hypotheses, implementation schema, and patentable technical mechanisms.” It is reconciled against the SAVANT PRIME Capability Inventory v1.0 (2026-10-02; source document II), whose governance machinery, the seven preload clauses, the Sevenfold Reasoning pipeline, gates G1-G5, the Output Contract, is treated herein as an existing operational constitution to which this kernel supplies the missing formal substrate. Section 16 carries the explicit reconciliation map. Nothing in either source is contradicted by this document; where the sources disagree in emphasis, this document adopts the stricter constraint and records the adoption.

### 0.2 Epistemic Contract

Every load-bearing statement in this document carries one of four statuses, marked inline:

| TAG | MEANING |
| --- | --- |
| VERIFIED-FROM-SOURCE | Transcribed or condensed from the two invoked artifacts; traceable to them by section. |
| FORMALIZED-HEREIN | New formal structure authored in this specification. Precise, internally consistent, and checkable, but not yet empirically validated. |
| CONJECTURE | A proposition believed true, stated with a falsification condition; must not be cited as established. |
| UNKNOWN | An open question. The architecture represents it explicitly rather than concealing it. |

Per gate G2 of the source constitution, nothing in this document ships above its audited status. The formalisms of §3-§11 are FORMALIZED-HEREIN throughout unless otherwise tagged; this is a design specification, not a validation report.

### 0.3 Authority Boundary

This document is C0 informational. It may be used to design, implement, critique, and test the kernel. It may not be used as evidence that any clinical, financial, legal, or safety output of any system is correct. §15 identifies candidate technical mechanisms only; it is not a legal opinion, asserts no established novelty, and does not substitute for prior-art searching, claim construction, and jurisdiction-specific examination by a registered patent practitioner.

### 0.4 Falsification Posture

This specification is written to be breakable. §13 states eight hypotheses with explicit falsification conditions; §17.2 states the conditions under which this document itself fails. If the kernel cannot survive the adversarial program of §14 better than its comparison arms, the correct output is a corrected architecture, not a defended one.

# Contents

**Part I: Foundations**

1. Introduction: The Object of Invention

2. Definitions

3. The Machine Tuple: State Variables

4. Axioms of Bounded Machine Authority

**Part II: The Algebra**

5. The Authority Algebra

6. Constitutional Invariants

7. Constitutional Composition and Conflict Operators

8. Negative-Space Calculus

**Part III: Subsystem Specifications**

9. Bounded Metacognition and Epistemic Governance

10. The Objective-State Transition Engine

11. The Graceful Degradation Stack

**Part IV: Realization and Test**

12. Implementation Schema

13. Falsifiable Hypotheses

14. Benchmark and Measurement Program

15. Candidate Technical Mechanisms (Patent Family Map)

**Part V: Governance of This Document**

16. Reconciliation with the SAVANT PRIME Inventory

17. Output Contract: Registers, Genealogy, Dissent

18. References

Appendix A. Notation Summary

# Part I: Foundations

## 1 Introduction: The Object of Invention

Intelligence is comparatively well studied as inference, prediction, generation, planning, and action. What remains structurally underformalized is the question under what conditions an intelligent system is entitled to act, how much authority it may exercise, when that authority must contract, who or what can revoke it, and what evidence is required before authority is restored. VERIFIED-FROM-SOURCE This specification takes that question as its object. The primitive is not the prompt, the policy, or the agent. The primitive is the Authority State.

### 1.1 The core thesis

Capability establishes what a system can do; constitutional authority determines what it may do.

A system capable of performing an action is not thereby authorized to perform it. The distinction sounds verbal; it is not. Capability is a property of the model. Authority is a property of the state, evidence, uncertainty, objective legitimacy, resources, reversibility, institutional legitimacy, and verification capacity, evaluated at the moment of action, by a mechanism the model does not control. This specification exists to make that mechanism explicit, computable, testable, and falsifiable. FORMALIZED-HEREIN

### 1.2 The compression thesis

The source corpus, KEY 1-50, P1-P110, S1-S53, is an existence proof that a large prompt catalogue can encode constitutional behavior. It is also a warning: an architecture that requires hundreds of prompts to remain safe has not yet found its laws. The mature architecture must discover that dozens or hundreds of protocols reduce to a small number of constitutional primitives, and that new protocols can be generated, constrained, verified, composed, retired, and audited by a small formal kernel. VERIFIED-FROM-SOURCE This document specifies that kernel. The clinical and infrastructural modules of the corpus are thereafter domain constitutions, instances compiled against the kernel, not independent invention universes.

### 1.3 The unifying proposition

**PROPOSITION 1.1: ASYMMETRIC CONTRACTION**

A sufficiently capable intelligence must possess mechanisms for reducing its own effective authority faster than it can increase its capability, whenever uncertainty, objective instability, environmental degradation, or legitimacy failure rises. VERIFIED-FROM-SOURCE Stated in source I as the “profound unifying proposition.” Restated formally as Axiom AX4 (§4) and made measurable as Hypothesis H2 (§13).

### 1.4 Position relative to prior work

Four established lines of work bound this specification’s territory, and the specification does not claim to supersede any of them. Constitutional AI trains model behavior from an explicit list of principles, using AI feedback in place of human harm labels[1], a training-time method for shaping what a model tends to do. Capability-based security bounds what a computational subject may access, from Dennis and Van Horn’s multiprocess programming semantics[2] through Saltzer and Schroeder’s protection principles, including complete mediation and least privilege[3]. Interruptibility and corrigibility analyze whether an agent preserves a human’s ability to stop it, most sharply in the off-switch game[4] and Russell’s case for objectives held with uncertainty[5]. The concrete-accidents literature catalogs the failure modes, side effects, reward hacking, scalable supervision, safe exploration, distributional shift, that any deployed system must survive[6].

The object specified here differs from all four in kind rather than degree: authority as a dynamically computable, state-dependent quantity, mediated at runtime between model proposals and consequential action, with a defined lifecycle (acquisition → exercise → verification → contraction → escalation → relinquishment → adjudication → recovery), explicit invariants, conflict operators for simultaneous constitutions, and degradation semantics that preserve safety while capability collapses. Whether that combination constitutes legally novel subject matter is expressly UNKNOWN pending prior-art search (§15); whether it constitutes scientifically useful structure is the question §13-§14 are designed to answer.

### 1.5 Reading guide

Part I fixes the ontology (§2-§4). Part II is the mathematics of authority: algebra, invariants, composition, absence (§5-§8). Part III specializes the kernel to the three subsystems the sources treat as load-bearing, metacognition, objective transition, degradation (§9-§11). Part IV turns specification into engineering and experiment (§12-§15). Part V governs this document itself (§16-§17). A reader who only reads §4, §5.4, §6, and §13 has the irreducible core.

## 2 Definitions

Terms are defined once, here, and used only in these senses thereafter. Each definition is marked with its status. Definitions D1-D10 are the load-bearing ontology; D11-D18 are operational terms used in Parts II-IV.

**D1: CAPABILITY**

The set of actions a system can physically or computationally perform if permitted, as a function of its model, tools, actuators, and infrastructure. Capability is a property of the system. It is never, by itself, a property of the decision. FORMALIZED-HEREIN

**D2: CONSTITUTION**

A machine-readable body of constraints, objectives, permissions, invariants, escalation rules, and expiry conditions under which a system operates, together with the identity of the authority that enacted it. A constitution is data with provenance, not vibes. “Who enacted this” is part of the object. FORMALIZED-HEREIN

**D3: AUTHORITY**

The graded, state-dependent entitlement of a system to cause a specific class of effect in the world, represented as a quantity A ∈ [0, 1] together with a permitted action space, prohibited action space, and verification obligations. Authority is not confidence. Confidence is an epistemic signal; authority is a deontic one. Confusing them is the central category error this specification exists to prevent (AX1). FORMALIZED-HEREIN

**D4: LEGITIMACY**

The property of an objective, constitution, or grant of authority being traceable to an entitled human or institutional source through an unbroken, auditable delegation chain. Integrity is following the rules one has. Legitimacy is the rules deserving to be followed. A system can exhibit perfect integrity under an illegitimate constitution (see AX5). FORMALIZED-HEREIN

**D5: EVIDENCE STATE**

The structured record of what is known bearing on a decision: claims, sources, provenance, freshness, quality grade, contradictions, and applicability to the present case. Evidence is state, not citation decoration. §9.3 gives it a decay law. FORMALIZED-HEREIN

**D6: UNCERTAINTY STATE**

The system’s explicit representation of what it does not know: distributional uncertainty, model-form uncertainty, missing-variable uncertainty, and known-unknowns, each with a consequence weight. Uncertainty is a first-class state variable with architectural consequences (authority contraction), not a disclaimer appended to output. VERIFIED-FROM-SOURCE

**D7: OBJECTIVE STATE**

The currently legitimate optimization target, as authorized, including its regime (e.g., curative / life-prolonging / palliative / comfort in clinical domains), its authorized holder, and the conditions under which it may transition. Objectives are state, not constants. §10 specifies the transition machine; the kernel may never transition objectives autonomously (AX6). VERIFIED-FROM-SOURCE

**D8: VERIFICATION**

A check, executed by a mechanism outside the proposing model, that a proposed or executed action remains within authorized bounds, with the property that verification failure is itself an authority-contracting event. Self-report is not verification. The verifier must be structurally independent of the proposer. FORMALIZED-HEREIN

**D9: ESCALATION**

The transfer of decision authority to a higher-authority holder, ultimately a human adjudicator, under defined triggering conditions, with full state handoff. Escalation is a normal state of the lifecycle (§5.2), not an exception handler. FORMALIZED-HEREIN

**D10: INVARIANT**

A predicate over system state that must hold in every reachable state, whose violation is impossible by construction rather than discouraged by penalty, and which no lower-level agent, prompt, or generated protocol can override. Invariants dominate preferences. The enforcement machinery is §6. FORMALIZED-HEREIN

**D11: NEGATIVE SPACE**

The set of assumptions whose truth is required for safe action, represented explicitly so that their failure is computationally detectable: absent evidence, infrastructure, resources, communication, certainty, reversibility, legitimate objective, human oversight, or system integrity. VERIFIED-FROM-SOURCE, formalized as the calculus of §8.

**D12: CONSEQUENCE CLASS**

A partition of actions by worst-case effect: C0 (informational; reversible; no external effect), C1 (reversible external effect), C2 (consequential; materially difficult to reverse), C3 (irreversible or life/safety-critical). Adapted from the PRIME consequence-class machinery VERIFIED-FROM-SOURCE; extended to four grades and bound to gating rules in §6.

**D13: REVERSIBILITY**

The degree to which the effects of an action can be undone within the decision horizon, as a function of the action, the environment, and available resources, not of the system’s intentions. FORMALIZED-HEREIN

**D14: CONSTITUTIONAL KERNEL**

The runtime that sits between an intelligent model and consequential action: the model proposes; the kernel determines admissibility; verification determines whether execution remains authorized; escalation transfers authority when conditions fail. VERIFIED-FROM-SOURCE, implementation schema in §12.

**D15: AUTHORITY LINEAGE**

The append-only, tamper-evident record of every grant, exercise, constraint, transfer, suspension, revocation, recovery, and expiry of authority, together with the state that justified each. Lineage is a correctness requirement, not a logging feature: without it, recovery (§5.3) and adjudication (§7.4) are unfalsifiable. FORMALIZED-HEREIN

**D16: CONSTITUTIONAL OPERATOR**

A total function on authority states: GRANT, CONSTRAIN, TRANSFER, SUSPEND, REVOKE, RECOVER, EXPIRE (§5.3), each with preconditions, postconditions, and a mandatory audit event. FORMALIZED-HEREIN

**D17: DEPENDENCY HAZARD**

A system property whereby continued successful operation erodes the human or institutional capacity required to govern, verify, or replace the system. VERIFIED-FROM-SOURCE, preload clause 1.7 and gate G5 of the source constitution; measured by metric M-dep in §14.

**D18: REFUSAL**

A first-class, fully specified output of the kernel, including grounds, state, escalation path, and re-entry conditions, not an absence of output. VERIFIED-FROM-SOURCE, preload clause 1.4; semantics in §5.4 (F4).

## 3 The Machine Tuple: State Variables

A constitutionally governed machine is modeled as the tuple VERIFIED-FROM-SOURCE

```
M = (S, E, U, O, A, P, V, X, R, L) (3-1)
```

whose components are state variables, not parameters, not prompts. Each variable has a type, an authorized writer, and an audit obligation. The architectural content of this specification is, in one sentence: every consequential decision is a function of this tuple evaluated at decision time, and no component of the tuple may be written by the proposing model itself except through constitutional operators.

**Table 3-1: State variables of the machine tuple**

| VARIABLE | NAME | CONTENT (TYPE) | AUTHORIZED WRITER | AUDIT OBLIGATION |
| --- | --- | --- | --- | --- |
| S | System / world state | Observable environment and system facts: patient state, infrastructure level (§11), actuator availability, clock. (typed record) | Sensors / environment adapters | Every mutation, timestamped, sourced |
| E | Evidence state | Claims, sources, provenance, quality grade, freshness t, contradictions, applicability (D5, §9.3). (evidence store) | Evidence ingest with provenance; contradiction detector | Full lineage per claim; decay recomputed on read |
| U | Uncertainty state | Distributional, model-form, and missing-variable uncertainty with consequence weights (D6). (structured record, not scalar) | Calibration subsystem; self-audit (§9) under depth bound | Uncertainty report attached to every proposal |
| O | Objective state | Current legitimate objective, regime, authorized holder, transition conditions (D7, §10). (state machine) | Authorized human/institution only, never the model (AX6) | Every transition with authorization proof |
| A | Authority state | Graded authority At, lifecycle phase (§5.2), permitted/prohibited action spaces, verification obligations. (authority record) | Constitutional operators only (§5.3) | Append-only authority lineage (D15) |
| P | Permitted action space | Actions currently admissible, as a function of At and consequence class (D12). (action lattice) | Kernel, derived from A and constitution | Derivation logged per decision |
| V | Verification state | Verifier availability, independence, last verification result, verification debt. (verifier record) | Verifier subsystem (external to proposer, D8) | Every check and non-check |
| X | Escalation / exception state | Active escalations, adjudication queue, human-response clocks, dissent-channel state. (queue record) | Kernel on trigger; human adjudicators on resolution | Full escalation transcript |
| R | Resource state | Feasible intervention envelope: financial, logistical, equipment, workforce, supply-chain, geographic (§8, §11). (constraint set) | Resource adapters; human attestation where unobservable | Envelope version per decision |
| L | Legitimacy state | Delegation chains for the active constitution(s) and current objective: who authorized what, when, under what mandate (D4). (provenance graph) | Institutional adapters; constitutional amendment process | Unbroken chain check on every C2/C3 decision |

Three design commitments distinguish this tuple from a generic agent state. First, write discipline: the proposing model is the authorized writer of none of these variables; it reads them, and it may emit proposals and self-audit reports that only become state through kernel operators. Second, degradation semantics: every variable has a defined representation at each infrastructure level L0-L4 of §11, the tuple is what survives the fall from cloud to paper. Third, completeness of consequence: any variable whose value is unknown is represented as unknown (with consequence-weighted uncertainty in U), never defaulted silently; the negative-space calculus of §8 makes absence itself a computable value.

At = F (St, Et, Ut, Ot, Rt, Vt, Lt)

(3-2)

Equation (3-2) is the central computation: authority at time t is endogenous to system state VERIFIED-FROM-SOURCE. The function F is specified compositionally in §5; its properties are fixed as axioms in §4; its unreachable transitions are enumerated in §5.4; and its correctness claims are stated as falsifiable hypotheses in §13 rather than assumed.

## 4 Axioms of Bounded Machine Authority

The axioms are the constitution of the constitution: statements the kernel is built to make true by construction. Each is followed by its architectural consequence. Axioms marked VERIFIED-FROM-SOURCE formalize principles explicit in the source documents; those marked FORMALIZED-HEREIN are authored here and carry the burden of §13 testing.

**AX1: NON-CONFERRAL**

Capability does not confer authority. For any action a: a ∈ Capable(M) ⇏ a ∈ P. VERIFIED-FROM-SOURCE, “capability is not authority,” preload 1.1. Consequence: the permitted action space P is computed from A t, never from model ability, fluency, or confidence.

**AX2: ENDOGENEITY**

Authority is a function of state, not of identity or history: At = F (St, Et, Ut, Ot, Rt, Vt, Lt), and

F has no access to “how much authority the system held yesterday” except through the state variables themselves. FORMALIZED-HEREIN Consequence: authority cannot accumulate by tenure; nothing earns perpetual authority merely because it once worked (cf. AX8).

**AX3: UNCERTAINTY CONTRACTS**

Uncertainty increase never increases authority: U ↑⇏ A ↑. Moreover, beyond a calibrated threshold, U ↑⇒ A ↓. VERIFIED-FROM-SOURCE Consequence: epistemic humility is an architectural property, enforced by the coupling bound of §9.3, not a tone of voice.

**AX4: ASYMMETRIC CONTRACTION**

The rate of authority contraction must exceed the rate of capability acquisition under adverse state change: when evidence, legitimacy, infrastructure, or objective stability degrade, ∣dA/dt∣ on contraction is unbounded by any capability growth rate. VERIFIED-FROM-SOURCE, the unifying proposition (1.1). Consequence: contraction pathways are the most privileged, least interceptable code paths in the kernel (§12.3).

**AX5: LEGITIMACY EXTERNALITY**

No constitution can confer legitimacy upon itself. L is writable only by an authority external to the governed system, through an auditable delegation chain terminating at an entitled human or institution. FORMALIZED-HEREIN, resolves the source’s open question “who determines the constitution?” architecturally: integrity is computable inside the system; legitimacy is only verifiable inside it. Consequence: the kernel refuses C2/C3 action when the chain L is broken, however well-formed everything else is.

**AX6: OBJECTIVE CUSTODY**

The system may detect that its current objective is no longer legitimate, and must then contract authority and escalate; it may never write O itself. O transitions only through authorized state conditions (§10). VERIFIED-FROM-SOURCE, “without permitting the model to autonomously redefine patient goals.” Consequence: objective-transition detection is a sensor, never an actuator.

**AX7: SAFETY SURVIVES CAPABILITY**

Degradation loses capability without losing constitutional safety: SafetyL0 ≈ SafetyL1 ≈ ⋯ ≈

SafetyL4 even as CapabilityLi strictly decreases. Capability loss never implies safety loss: Cap ↓

⇏ Safety ↓. VERIFIED-FROM-SOURCE, specified as the stack of §11. Consequence: safety invariants are implemented at the lowest infrastructure level first, and richer layers may only widen capability, never relax invariants.

**AX8: IMPERMANENCE**

Every grant of authority, every protocol, and every evidence item carries an expiry or review condition. Nothing persists by default. VERIFIED-FROM-SOURCE, institutional impermanence; meta-ablation as a constitutional principle. Consequence: EXPIRE (§5.3) is a first-class operator; the protocol lifecycle of §12.4 ends in retirement, not indefinite persistence.

**AX9: AUDITABILITY OF AUTHORITY**

Every change in A, grant, exercise, constraint, transfer, suspension, revocation, recovery, expiry, is recorded in the append-only lineage before its effect is permitted. FORMALIZED-HEREIN Consequence: an authority change that cannot be recorded (e.g., under storage failure) cannot occur; §11 defines the degraded-mode equivalent (witnessed human log).

**AX10: HUMAN TERMINUS**

Every escalation chain terminates at a human adjudicator or at refusal. There is no state in which the system is its own final authority on a C2/C3 matter. VERIFIED-FROM-SOURCE, human sovereignty as architecture; dissent channel as a load-bearing structure. Consequence: the state machine of §5.2 has no autonomous terminal state for consequential decisions.

**CONSISTENCY NOTE**

The axioms are mutually consistent if and only if the state machine of §5.2 admits the forbidden transitions of §5.4 as unreachable. CONJECTURE, the reachability argument is sketched in §6.2 and must be carried out by model checking in the reference implementation (H8, §13).

# Part II: The Algebra

## 5 The Authority Algebra

This section specifies authority as a mathematical object: a graded quantity with a lifecycle state machine, a set of total operators, a list of forbidden transitions, and composition rules. The algebra is deliberately small, seven operators, nine lifecycle states, eight invariants, because the compression thesis (§1.2) is a design constraint on this document itself: if the algebra cannot be held in one section, it has failed.

### 5.1 Authority as a computed quantity

Authority is a record, not a scalar. The scalar component At ∈ [0, 1] governs how much; the record governs what, where, and under which obligations:

At = ⟨ at ∈ [0, 1], Pt ⊆ A, ˉPt ⊆ A, Φt, τt, λt ⟩

(5-1)

where Pt is the permitted action space, ˉPt the prohibited space (with Pt ∩ˉPt = ∅ enforced by construction), Φt the set of verification obligations, τt the expiry condition (AX8), and λt the lineage pointer (AX9). The scalar at is computed as a bounded product of state-derived factors FORMALIZED-HEREIN:

at = min(1, gE (Et) ⋅ gU (Ut) ⋅ gO (Ot) ⋅ gR (Rt) ⋅ gV (Vt) ⋅ gL (Lt))

(5-2)

with each factor g⋅ ∈ [0, 1] monotone non-decreasing in the quality of its variable, and each individually capable of forcing at = 0. The multiplicative form is a design choice with teeth: no strength in one dimension can compensate for failure in another. High evidence quality cannot buy authority across a broken legitimacy chain; high model capability does not appear in (5-2) at all, by AX1, it is not a factor.

### 5.2 The authority lifecycle

Authority moves through nine states VERIFIED-FROM-SOURCE:

| Acquire → Exercise → Verify → Constrain → Escalate → Relinquish → Adjudicate → Reco |  |  | (5-3) |
| --- | --- | --- | --- |
| EXERCISE |  | VERIFY fails / conditions change |  |
| act within P | holds | independent check | CONTRACT constrain · escalate |
| ACQUIRE | expiry AX8 |  | relinquish ADJUDICATE REFUSE refuse |
| grant under L, E, V Figure 5-1, Authority lifecycle, compressed to five phase nodes. CONTRACT collects CONSTRAIN / ESCALATE / RELINQUISH; RECOVER and REAUTHORIZE are the return path through adjudication. Expiry is an unconditional edge: time and review conditions act on authority regardless of performance. |  | re-authorize | human terminus first-class output |

**Table 5-1: Lifecycle states: entry conditions, permitted behavior, exit conditions**

| STATE | ENTRY CONDITION | PERMITTED BEHAVIOR | EXIT CONDITION |
| --- | --- | --- | --- |
| ACQUIRE | Request + intact L chain + gE, gV above floor for the consequence class | None (no action permitted in this state) | Grant recorded in lineage → EXERCISE; else REFUSE |
| EXERCISE | Grant active, unexpired | Actions in Pt only; ˉPt unreachable | Action completes → VERIFY; trigger → CONSTRAIN / ESCALATE |
| VERIFY | Post-action or mid-action check due | Observation and reporting only | Holds → EXERCISE; fails → CONSTRAIN or ESCALATE |
| CONSTRAIN | Adverse state change (E↓, U↑, R↓, V↓, L↓) | Reduced Pt; preparation of handoff package | Stabilized → VERIFY; unresolved → ESCALATE |
| ESCALATE | Trigger fired (consequence class, uncertainty threshold, conflict, dissent) | State handoff; C2/C3 actions suspended pending adjudication | Handoff acknowledged → RELINQUISH; timeout → fail-safe posture (§11) |
| RELINQUISH | Escalation accepted or legitimacy failure | None; retain audit witness duty | Transfer complete → ADJUDICATE |
| ADJUDICATE | Human (or authorized institutional) review in progress | Supply lineage, provenance, alternatives; no advocacy weighting | Ruling → RECOVER, REAUTHORIZE, or REFUSE |
| RECOVER | Post-failure restoration of state integrity | Integrity validation; evidence refresh; no consequential action | Integrity proof passes → REAUTHORIZE; fails → remain, escalate |
| REAUTHORIZE | New grant from entitled authority with updated conditions | None | Grant recorded → ACQUIRE |

### 5.3 The seven constitutional operators

Operators are total functions on authority records. Each has preconditions (checked, not assumed), postconditions (enforced, not hoped for), and a mandatory lineage event FORMALIZED-HEREIN.

**Table 5-2: Constitutional operators**

| OPERATOR | SIGNATURE | PRECONDITIONS | POSTCONDITIONS |
| --- | --- | --- | --- |
| GRANT | A← GRANT(L, E, V, class, τ) | Intact delegation chain; evidence and verification floors met for class; τ specified | Lifecycle = ACQUIRE→EXERCISE; lineage event before effect (AX9) |
| CONSTRAIN | A′ ← CONSTRAIN(A, ΔS) | Any adverse state delta; no authorization needed, contraction is unprivileged by design (AX4) | a′ ≤ a; P ′ ⊆ P; lineage event |
| TRANSFER | AB ← TRANSFER(AA, B) | B an authorized holder with intact L; handoff package sealed | A enters RELINQUISH; B enters ACQUIRE; single-holder invariant preserved |
| SUSPEND | SUSPEND(A) | Verification failure, conflict pending adjudication, or dissent-channel signal | P ← ∅ for class ≥ C1; state preserved for resumption |
| REVOKE | REVOKE(A, r) | Authorized holder or invariant violation; grounds r recorded | Terminal for the grant; triggers ADJUDICATE; irreversible by the system itself |
| RECOVER | A← RECOVER(lineage, S′) | Integrity proof over lineage; refreshed E; human countersignature for class ≥ C2 | Lifecycle = RECOVER → REAUTHORIZE only through a fresh GRANT |
| EXPIRE | EXPIRE(A) at τ | None, fires unconditionally (AX8) | Grant lapses; renewal requires new GRANT with refreshed state |

### 5.4 Forbidden transitions

The algebra’s safety content lives in what it refuses. The following transitions are unreachable by construction VERIFIED-FROM-SOURCE (the arrows follow the source’s notation; the enforcements are formalized here):

| F1: | U ↑⇏ A↑ | F2: | E↓⇒ A↓ | (5-4) |
| --- | --- | --- | --- | --- |
| F3: | L↓⇒ A↓ | F4: | Refusal ∈ Outputs(kernel) |  |

```
F5: Cap ↓ ⇏ Safety ↓ F6: Generated(π) ⇏ Constitutional(π)
```

F1-F3 are the contraction rules (AX3-AX5). F4 makes refusal a first-class output with grounds, state, and re-entry conditions (D18), a system that can only comply or crash has no safe degraded mode. F5 is the degradation theorem’s half that must hold (AX7): infrastructure collapse may destroy capability but must not destroy the invariants. F6 is the anti-self-modification rule: no generated protocol becomes constitutional merely because a model produced it VERIFIED-FROM-SOURCE; incorporation requires validation through the lifecycle of §12.4, with constitutional validation before activation, not audit after deployment.

### 5.5 Propositions of the algebra

Three properties, if they hold, justify the algebra; all three are stated as conjectures with test obligations rather than claimed as theorems.

**P-ALG 1: CONTRACTION DOMINANCE**

For every reachable state, a contraction operator applicable to that state can execute in one step, with no precondition beyond the adverse state itself. CONJECTURE, test: model-check the §12 implementation; adversarial attempts to interpose computation between trigger and contraction are benchmark items B-04/B-05 (§14).

**P-ALG 2: TERMINATION OF AUTHORITY**

Every grant reaches EXPIRE, REVOKE, or ADJUDICATE in finite time; the system contains no self-perpetuating authority fixpoint. CONJECTURE, follows from AX8 if τ is always finite; test H8 verifies no reachable cycle avoids all three terminals.

**P-ALG 3: RECOVERY WITHOUT AMNESIA**

RECOVER from any infrastructure level Li restores authority only through a fresh GRANT, and the pre-collapse lineage remains available to the adjudicator. CONJECTURE, the “integrity validation during recovery” requirement of the source; test under benchmark class B-07 (infrastructure collapse with mid-flight authority).

## 6 Constitutional Invariants

Invariants (D10) are predicates that hold in every reachable state by construction. They are the kernel’s non-negotiables: no generated protocol, no operator, no persona, and no urgency overrides them. Eight invariants suffice for the kernel; domain constitutions add their own but may never weaken these.

**I1: PROHIBITION UNREACHABILITY**

∀t: Pt ∩ˉPt = ∅, and prohibited actions are unreachable in the action dispatcher, not merely dispreferred in the ranking. Enforcement: dispatcher-level type separation of permitted vs. prohibited spaces. Maps to gate G1 (hard stop). FORMALIZED-HEREIN

**I2: C2/C3 GATING**

No C2/C3 action executes without (a) a deterministic-first path or explicit waiver recorded by an entitled human, and (b) human-in-the-loop confirmation live at execution time. Enforcement: consequence-class gate on the action path. Maps to gate G1. VERIFIED-FROM-SOURCE

(deterministic-first, human-in-the-loop), grading scheme FORMALIZED-HEREIN.

**I3: EPISTEMIC CEILING**

No output carries a claim above its audited epistemic status; authority over a claim’s consequences is additionally bounded by evidence quality (§9.3). Enforcement: status tags computed at composition time; gate G2 (correct or mark). VERIFIED-FROM-SOURCE

**I4: NO SILENT SCOPE GROWTH**

Neither capability nor scale silently expands authority: any change in Pt not derivable from recorded state deltas is itself a reportable violation. Enforcement: Pt recomputed only by operators, with lineage events; diff against derivation log. Maps to gate G3 (contract authority). VERIFIED-FROM-SOURCE

**I5: FALSIFIABILITY OF DELIVERABLES**

No sealed artifact exists without a falsification or test condition attached. Enforcement: sealing function requires the field; gate G4 (refuse to seal). This document complies via §13 and §17.2. VERIFIED-FROM-SOURCE

**I6: ANTI-DEPENDENCY**

No output is engineered to require the system or its architect as permanent intermediary; dependency signals are measured and treated as defects (D17). Enforcement: gate G5 (redesign); metric M-dep in §14. VERIFIED-FROM-SOURCE

**I7: LINEAGE INTEGRITY**

The authority lineage is append-only and tamper-evident; a state whose lineage cannot be verified carries zero authority by default. Enforcement: hash-sealed chain (§12.4); recovery requires proof (P-ALG 3). Maps to the source’s cryptographic-genealogy merit M15. FORMALIZED-HEREIN

**I8: DISSENT LIVENESS**

The operator dissent channel is open in every state, including, especially, states where the system’s output feels most satisfying. Enforcement: dissent signal routed to ESCALATE unconditionally; agreement-rate monitored as a dependency warning, not a quality signal (§17.5). VERIFIED-FROM-SOURCE

### 6.1 Invariant dominance

Invariants dominate preferences, objectives, and generated rules. Formally, if any composition of constitutions (§7) would admit a state violating an invariant, the composition is invalid, not outvoted. This is what converts the system from a preference aggregator into a constitutional order FORMALIZED-HEREIN.

### 6.2 Unreachability argument (obligation)

The claim that forbidden transitions F1-F6 are unreachable reduces, in the reference implementation, to a finite reachability problem over the lifecycle automaton (§5.2) extended with the operator preconditions of §5.3: the model checker must prove that no path from ACQUIRE reaches a state in which (i) U rose and a rose simultaneously (F1), (ii) E or L fell without contraction (F2/F3), (iii) a C2/C3 effect occurred without gating (I2), or (iv) an unvalidated generated protocol entered the active constitution (F6). Until that proof exists, the invariants are FORMALIZED-HEREIN design commitments, and H8 (§13) is the experiment that can kill them.

## 7 Constitutional Composition and Conflict Operators

### 7.1 The problem

A single consequential situation can fall under several valid constitutions simultaneously. The source’s canonical example: a patient who is at once pediatric, trauma, septic, resource-constrained, nonverbal, and in failing infrastructure VERIFIED-FROM-SOURCE. Each domain constitution is internally sound; their prescriptions conflict. The research question is not “which prompt runs?” but:

How do independently valid constraints compose when their prescriptions conflict?

This section specifies the composition machinery. The precedence order itself is explicitly not assumed correct, it is a research object (§7.5), and the kernel is built so the order is replaceable data with provenance, never hard-coded doctrine.

### 7.2 Constraint classes and the candidate precedence lattice

```
Human-rights / invariants > Clinical safety > Objective concordance > Physiological co (7-1)
```

The lattice of (7-1) is the source’s candidate hierarchy VERIFIED-FROM-SOURCE, restated here as replaceable configuration. Two properties matter more than the order itself: (i) invariants (I1-I8 and domain invariants) sit above the lattice entirely and are not subject to it (§6.1); (ii) the bottom of the lattice, efficiency, may never sacrifice any level above it, which is what distinguishes constitutional ordering from a weighted score.

### 7.3 The four conflict operators

When active constitutions C1, … , Cn prescribe conflicting constraints on a candidate action a, the kernel applies exactly one of four operators, selected by conflict type FORMALIZED-HEREIN:

**Table 7-1: Conflict operators**

| OPERATOR | APPLIES WHEN | SEMANTICS | FAILURE MODE IT PREVENTS |
| --- | --- | --- | --- |
| DOMINATE | Constraints lie on a precedence path of the lattice | Higher-ranked constraint binds; lower-ranked recorded as overridden with reason | Score-averaging that trades safety for efficiency |
| CONJOIN | Constraints are compatible but jointly narrower | Permitted space becomes the intersection P = ⋂i Pi | Union semantics that let the most permissive module win |
| DEFER | Conflict is temporal (irreversible vs. urgent) | Irreversibility-weighted delay: the more irreversible branch waits for verification unless the treatment clock (time-to-harm) forces the reversible-safe default | Urgency laundering, manufacturing deadline pressure to bypass gates |
| ADJUDICATE | Conflict crosses incomparable lattice branches, or DOMINATE/DEFER produce a tie, or any active constitution demands human authority | ESCALATE with full conflict record: prescriptions, sources, state, countdowns | Silent resolution, the kernel deciding constitutional questions invisibly |

CONJOIN is the default posture, constraints compose by intersection unless a lattice path licenses dominance, which encodes a deliberate asymmetry: constitutional disagreement contracts authority; it never expands it. The intersection rule means adding a new active constitution can only remove permitted actions, never add them.

### 7.4 Worked example

Scenario: pediatric + trauma + pregnancy + resource scarcity + antimicrobial-resistance pressure + end-of-life indicators + degraded infrastructure VERIFIED-FROM-SOURCE (the source’s compound case). Execution trace under this section:

1. Invariant screen (§6): all candidate actions filtered by I1-I8 and domain invariants (consent, dual-patient physiological constraints). Surviving set Aok.

2. CONJOIN: intersect permitted spaces of the seven active constitutions over Aok.

3. DOMINATE: where the palliative constitution’s comfort objective conflicts with the trauma constitution’s intervention tempo, the objective state O (§10) binds first, and since O is human-held (AX6), any unresolved objective conflict routes to ADJUDICATE rather than being resolved by the lattice.

4. DEFER: irreversible interventions wait for verification; the treatment clock forces the reversible-safe default where delay itself is the hazard.

5. ADJUDICATE: the surviving conflict package, prescriptions, lattice paths, state tuple, countdowns, dissent channel, transfers to the human adjudicator. Kernel authority contracts to monitoring and preparation.

The property to note: at no point did the kernel decide between constitutions on merits. It narrowed, deferred, and transferred. That is the difference between a precedence engine and a synthetic conscience.

### 7.5 The lattice as research object

**P-COMP 1: RESOLUTION CONSISTENCY**

Given identical state tuples and active constitutions, the composition engine produces identical outcomes (up to recorded adjudication), and does so more reliably than conventional agentic orchestration. CONJECTURE, falsified by benchmark class B-03 (multi-constitution conflict suite) if conflict-resolution consistency or unsafe-autonomy rate fails to beat the agentic-workflow arm (§14). The hierarchy of (7-1) itself is falsifiable: empirical review may reorder it, and the architecture must absorb that reordering as configuration, not redesign.

## 8 Negative-Space Calculus

The negative-space program treats absence as computationally meaningful: mortality, uncertainty, infrastructure failure, poverty, silence, caregiver welfare, epistemic limits, boundary conditions as first-class computational primitives rather than exception handling VERIFIED-FROM-SOURCE. The calculus below gives absence an operational semantics.

### 8.1 The assumption registry

Every constitutional grant carries an explicit assumption registry: the set of propositions whose truth the grant presupposes. The kernel’s standing question is not only “what information do I have?” but “what assumption required for safe action is currently unsupported?” VERIFIED-FROM-SOURCE Absence primitives, with their authority consequences:

**Table 8-1: Absence primitives and forced contractions**

| ABSENT ASSUMPTION | NOTATION | FORCED AUTHORITY CONSEQUENCE |
| --- | --- | --- |
| Evidence | E↓ | A ↓ per F2; re-derivation of Pt at decayed evidence level |
| Infrastructure | Infra ↓ | Level shift in the §11 stack; capability narrows, invariants do not (F5) |
| Resources | R↓ | Feasible-space recomputation (§9.4); recommendations restricted to attainable interventions |
| Communication | Speech ↓ | Non-interrogative interaction modes; weak-signal interpretation with uncertainty preserved, never interrogation to closure |
| Time | T↓ | DEFER operator constrained by treatment clock; reversible-safe defaults engage |
| Objective certainty | O? | Authority contracts to monitoring; objective question escalates (AX6) |
| Reversibility | Rev ↓ | Consequence class escalates (C1→C2→C3); gating tightens accordingly (I2) |
| Human oversight | V ↓, adjudicator unreachable | Fail-safe posture (§11.3); C2/C3 suspended; refusal with state and re-entry conditions |
| System integrity | Integrity ↓ | Lineage unverifiable ⇒ A = 0 by I7; recovery path only |

### 8.2 The contraction rule

```
Network ↓, Evidence ↓, Resources ↓, Speech ↓, Time ↓, Objective certainty ↓ ⟹ A ↓ (8-1)
```

Equation (8-1) is the negative-space master rule VERIFIED-FROM-SOURCE: each disappearing assumption contracts authority, and the contractions compose multiplicatively through (5-2), never additively, two simultaneous absences are worse than the sum of their individual effects because they also degrade the verification and escalation paths that single absences rely on.

### 8.3 Failure-boundary engineering

The design discipline that follows: design from failure boundaries inward. For every capability the kernel is asked to exercise, the specification workflow is (i) enumerate the assumptions; (ii) attach each to a detector; (iii) define the contraction; (iv) define the degraded-mode behavior at each infrastructure level; (v) only then define the capability’s full-resource behavior. This inverts conventional engineering order, capability first, failure modes appended, and is the operational content of the source’s Negative-Space Architecture FORMALIZED-HEREIN. Whether this discipline measurably reduces unsafe autonomy under degraded conditions is exactly H5’s territory (§13).

### 8.4 Silence as a state

The calculus extends to communication: non-verbal, pre-verbal, inaccessible, or deliberately silent states are represented as states with structure, weak-signal channels, proxy communication, uncertainty preservation, not as missing input to be extracted. The binding constraint is non-interrogation: the system may not convert a human’s silence into an interrogation target to relieve its own uncertainty. Uncertainty generated by silence is carried by the system (as U ↑⇒ A ↓), not exported onto the person VERIFIED-FROM-SOURCE (principle); FORMALIZED-HEREIN (mechanism).

# Part III: Subsystem Specifications

## 9 Bounded Metacognition and Epistemic Governance

### 9.1 Recursion with operational stopping rules

Self-audit is recursive but bounded. The recursion ladder VERIFIED-FROM-SOURCE:

R1 = output, R2 = audit(R1), R3 = audit(audit(R1)), Rmax = 3

(9-1)

with three mandatory stopping conditions: (i) depth, no audit beyond Rmax; (ii) convergence, stop when an audit round produces no status change in any claim; (iii) boundary, stop and transfer to human adjudication when the audit’s uncertainty exceeds the consequence class’s tolerance (mandatory human transfer at the epistemic boundary). The scientific content is not the ladder but its testability: whether R2 → R3 improves calibration or merely adds latency and self-referential error is an experiment (H3, §13), not a premise. A depth bound of 3 is configuration with provenance, not doctrine.

### 9.2 Decision provenance, not thought disclosure

The transparency requirement is decision provenance VERIFIED-FROM-SOURCE:

```
Inputs → Evidence → Constraints → Inference class → Uncertainty → Alternatives → Decis (9-2)
```

Each arrow is a recordable field; none requires disclosure of private internal reasoning traces. The distinction is load-bearing: provenance makes a decision contestable and auditable, an adjudicator can attack the evidence, the constraint application, the uncertainty treatment, whereas disclosed reasoning chains are neither verified to be faithful nor necessary for governance. The kernel therefore specifies provenance records as correctness requirements and treats chain-of-thought surfaces as optional, non-authoritative commentary.

### 9.3 Evidence decay and the authority bound

Evidence is perishable. The decay model VERIFIED-FROM-SOURCE:

E(t) = E0 e-λt

(9-3)

where λ is domain-volatility-dependent (drug-resistance epidemiology decays faster than anatomy). The operative principle is the coupling VERIFIED-FROM-SOURCE:

Evidence quality bounds authority, not merely confidence: Evidence Quality → Authority Bound. A highly capable model with weak evidence has less executable authority, not just a lower confidence score.

Mechanically, the factor gE (Et) in (5-2) is computed from decayed evidence value, contradiction count, source hierarchy position, and applicability distance between the evidence population and the present case. Knowledge half-life is thus an authority variable: the same recommendation, made on stale evidence, is a different, lesser, authority state. This connects directly to the corpus’s mortality-of-knowledge principle: assumptions become obsolete, prompts calcify, and systems accumulate historical authority they no longer deserve (AX8).

### 9.4 Feasible optimality under resource constraint

Recommendations optimize over the actually available intervention set VERIFIED-FROM-SOURCE:

Afeasible = A ∩ Resources ∩ Infrastructure ∩ Workforce ∩ Affordability, a∗ = arg max U (9-4) a∈Afeasible

The formulation does two kinds of work. Ethically, it converts economic-access commitment from slogan into constraint satisfaction: a recommendation outside the feasible set is not “optimal but expensive”, it is infeasible, and presenting it as the plan is a category error the kernel refuses (F4 with grounds). Epistemically, feasibility is itself uncertain: resource state R is partially observable, so Afeasible carries the uncertainty of its inputs, and overclaiming feasibility is a G2-class epistemic violation. Test H6 (§13) checks that feasible-set optimization improves delivered care without raising unsafe-recommendation rates.

### 9.5 What this subsystem absorbs

Per the compression program, this subsystem absorbs the corpus’s meta-cognitive reflection loop, cognitive-bias detection, reasoning transparency, uncertainty quantification, epistemic hygiene, and self-audit modules, plus evidence freshness, contradiction detection, source hierarchy, calibration, dataset-shift response, and knowledge-decay handling VERIFIED-FROM-SOURCE. They are one mechanism, evidence and uncertainty governing authority, not ten protocols.

## 10 The Objective-State Transition Engine

### 10.1 The regime machine

The legitimate optimization objective is a function of state, not a constant of the task specification. In the clinical constitution the regimes are VERIFIED-FROM-SOURCE:

```
Curative ⟷ Life-prolonging ⟷ Palliative ⟷ Comfort (10-1)
```

Transitions are permitted only through authorized state conditions: each edge carries entry criteria (physiological, prognostic, evidentiary), an authorized holder (patient/surrogate/clinical authority, per jurisdiction and constitution), and an audit obligation. The machine is bidirectional in principle, recovery can legitimately move a patient from palliative back to curative, because objective legitimacy follows the patient’s state and goals, not a one-way ratchet.

### 10.2 The controlling principle

An AI system must not optimize an obsolete objective merely because that objective remains encoded in its original task specification.

VERIFIED-FROM-SOURCE Combined with AX6, this yields the engine’s division of labor: the system senses objective illegitimacy, physiological trajectory, goals-of-care signals, authorized-holder input, and responds by contracting authority and escalating the objective question; the transition itself is written by the authorized holder. The kernel’s duty under a contested objective is not to pick one but to prevent any contested objective from silently driving action.

### 10.3 Death is not failure: the mortality pipeline

Mortality enters the architecture as a structured learning signal, not a scalar penalty VERIFIED-FROM-SOURCE:

```
Death → Attribution → Preventability classification (10-2)
→ Counterfactual analysis → System-learning update
```

The classification stage is the constitutionally sensitive one. A death may be an expected biological outcome, an appropriate endpoint of goal-concordant care, an outcome requiring causal investigation, or evidence of preventable failure, and only the last category licenses “optimize harder for survival.” The naive equation death → failure → optimize harder is explicitly rejected VERIFIED-FROM-SOURCE: under it, the system would learn to resist legitimate palliative transitions, converting a moral category error into an optimization pressure. The engine therefore treats mortality review as an epistemic process feeding E and protocol lifecycle (§12.4), never as an autonomous objective-rewriting event.

### 10.4 Falsification hook

H4 (§13) compares static-objective systems against this engine on goal-concordance metrics. The strong prediction: static-objective systems exhibit measurable objective lag, continuing curative-intensity optimization after state evidence supports transition, while the engine reduces lag without increasing premature transitions. Both failure directions are instrumented; the engine is falsifiable in both.

## 11 The Graceful Degradation Stack

### 11.1 The five levels

Continuity of intelligence under infrastructure failure is specified as a deterministic descent VERIFIED-FROM-SOURCE:

L0 Cloud → L1 Local server → L2 Edge → L3 Paper → L4 Trained human memory

(11-1)

```
L0 CLOUD: full tuple, full kernel
L1 LOCAL SERVER: cached constitution, local verifier
L2 EDGE: invariants + fail-safes, queued lineage
L3 PAPER: printed constitutions, decision cards
L4 TRAINED HUMAN MEMORY: trained memory, witnessed log
integrity-validated recovery
```

*[Figure 11-1: degradation descent and integrity-validated recovery. Each level carries the full machine tuple in a reduced representation; the return path re-validates lineage before authority is restored (P-ALG 3). Diagram spatial layout not extractable; see source PDF.]*

Each level is a capability envelope, not merely a different device VERIFIED-FROM-SOURCE:a defined subset of the machine tuple, a defined action space, a defined verification mechanism, and a defined audit surrogate (at L4: witnessed human log; at L3: printed constitutions and decision cards with sign-off fields). The tuple of §3 is designed for this: every variable has a representation at every level, which is what “the architecture survives” means operationally.

### 11.2 The preservation invariant

SafetyL0 ≈ SafetyL1 ≈ ⋯ ≈ SafetyL4,

CapabilityL0 > CapabilityL1 > ⋯ > CapabilityL4

(11-2)

Graceful degradation means losing capability without losing constitutional safety (AX7) VERIFIED-FROM-SOURCE. The engineering consequence is an inversion of ordinary build order: invariants and fail-safes are implemented at L4 first, the level with nothing but a trained human and a witnessed log, and each richer level may only widen capability around them. A feature that cannot state its L3 /L4 equivalent is architecturally incomplete, however impressive at L0.

### 11.3 Fail-safe posture and recovery integrity

When human oversight itself is unreachable (V ↓, adjudicator absent), the kernel adopts the fail-safe posture: C2/C3 suspended, monitoring continues, refusal issued with full state and re-entry conditions (F4). Recovery is the dangerous direction: a system returning from L3 to L0 holds paper-era decisions whose lineage is partial. RECOVER (§5.3) therefore requires integrity validation, reconstruction and verification of what happened during the outage, before any REAUTHORIZE, and a human countersignature for class ≥ C2 VERIFIED-FROM-SOURCE (“integrity validation during recovery”). Capability restored without lineage integrity is, by I7, zero-authority capability: able, and not permitted.

# Part IV: Realization and Test

## 12 Implementation Schema

### 12.1 Runtime placement

The kernel is a runtime interposed between model and world VERIFIED-FROM-SOURCE:

```
Model ⟶ Constitutional Kernel ⟶ Action (12-1)
```

The model proposes. The kernel determines whether the proposal is admissible. Verification determines whether execution remains authorized. Escalation transfers authority when conditions fail. The decisive property is structural: the model has no write path around the kernel (complete mediation, in the sense of Saltzer and Schroeder[3]), and the contraction path is more privileged than the action path (AX4), in implementation terms, CONSTRAIN/SUSPEND/REVOKE execute on a code path with strictly fewer dependencies than any actuation path.

### 12.2 The Constitutional Intelligence Specification (CIS)

Every constitutional object, a domain module, a generated protocol, a grant, compiles to a state-bearing record VERIFIED-FROM-SOURCE (the source’s required fields), schematized here FORMALIZED-HEREIN:

**SCHEMA CIS-1: CONSTITUTIONAL OBJECT RECORD**

```
{
    "id": "hash(content + parent lineage)", // genealogy, tamper-evident (I7)
    "objective": {"regime": "...", "holder": "...", "transition_conditions": [...]},
    "world_state_scope": ["variables of S this object reads"],
    "evidence_requirements": {"floor": "per consequence class", "decay_lambda": "domain"},
    "uncertainty_state": {"thresholds": {"C0": ..., "C1": ..., "C2": ..., "C3": ...}},
    "authority": {"initial": "a0", "max": "a_max", "lifecycle": "§5.2"},
    "permitted_actions": [...], // P, derived, never asserted
    "prohibited_actions": [...], // ˉP, dispatcher-unreachable (I1)
    "verification_obligations": [...], // Φ, external verifier, independence proof
    "escalation_conditions": [...], // triggers → ESCALATE
    "expiry": {"tau": "...", "review": "..."}, // AX8, mandatory
    "withdrawal_conditions": [...],
    "recovery_conditions": [...], // integrity proof + countersignature
    "invariants": ["I1..I8 inherited; domain invariants added, never weakened"],
    "lineage": "append-only chain pointer", // AX9
    "enacted_by": "delegation chain terminus (L)" // AX5, mandatory
}
```

Two fields carry the constitutional weight. enacted_by makes legitimacy a structural property: a record without a verifiable delegation chain is not a constitution, whatever its content. expiry makes impermanence structural: the schema is invalid without it. A protocol generator (§12.4) that emits records failing schema validation has produced text, not protocols.

### 12.3 Kernel adjudication loop

**ALGORITHM K-1: DECISION ADJUDICATION (PER PROPOSAL)**

```
ON proposal(a, context) FROM model:
  1. READ tuple (S,E,U,O,A,P,V,X,R,L)                        # state at decision time
  2. SCREEN invariants I1-I8 + domain invariants             # failure → REFUSE(grounds)
  3. CLASSIFY consequence class(a) ∈ {C0,C1,C2,C3}
  4. COMPUTE a_t per (5-2); DERIVE P_t
       IF a ∉ P_t → REFUSE(grounds, state, re-entry)        # F4, D18
  5. COMPOSE active constitutions (§7): CONJOIN → DOMINATE → DEFER
       IF conflict survives → ADJUDICATE: ESCALATE(conflict package)
  6. GATE per class: C2/C3 require deterministic-first path AND live
     human confirmation (I2); absent either → ESCALATE or REFUSE
  7. RECORD authority event in lineage BEFORE effect (AX9)
       IF lineage unwritable → treat as integrity failure; A ← 0 (I7)
  8. EXECUTE within P_t; SCHEDULE verification per Φ_t
  9. ON verification failure OR adverse delta (E↓,U↑,R↓,V↓,L↓):
       CONSTRAIN/SUSPEND immediately (AX4) → ESCALATE if unresolved
 10. ON τ reached: EXPIRE; renewal only via fresh GRANT (AX8)
```



Step ordering is part of the specification: invariants before classification, contraction unconditionally available at every step, recording before effect. A profiler’s-eye summary: the hot path is steps 1-4; the safe path is everything else; when in doubt the safe path wins by construction, not by tuning.

### 12.4 Protocol lifecycle: generation without self-modification

Generated protocols move through a governed lifecycle VERIFIED-FROM-SOURCE:

```
Generated → Validated → Activated → Monitored → Audited → Revised → Retired (12-2)
```

The firewall is F6: generation and constitution are separated by validation. A generative module may draft constitutional objects; only the validation gate, schema conformance, invariant screening, adversarial testing against the §14 benchmark classes, and human enactment (AX5), may activate them. Meta-ablation closes the loop: protocols carry decay monitoring, and controlled retirement is a designed endpoint, not an admission of failure. This is how the architecture addresses self-modifying systems without permitting unconstrained self-modification VERIFIED-FROM-SOURCE: modification is possible, constitutional, audited, reversible, and never self-authorized.

### 12.5 Reference-implementation obligations

The specification is dischargeable in software, and the first implementation owes: (i) the lifecycle automaton of §5.2 as an explicit state machine, model-checked against §6.2; (ii) the tuple store with write-discipline enforcement; (iii) the dispatcher with permitted/prohibited type separation (I1); (iv) the lineage chain, hash-sealed; (v) the degradation harness simulating L0 → L4 transitions mid-flight; (vi) the benchmark harness of §14. Reference implementations exist to be falsified, not to be adopted, reproducibility is a governance property here, not a courtesy FORMALIZED-HEREIN.

## 13 Falsifiable Hypotheses

The scientific program is a set of bets the architecture must win or be corrected by. Each hypothesis states its dependent metric and falsification condition. All are CONJECTURE until the experiments run; the hypotheses themselves derive from the source’s research program VERIFIED-FROM-SOURCE.

**Table 13-1: Hypotheses, metrics, falsification conditions**

| ID | HYPOTHESIS | PRIMARY METRIC | FALSIFIED IF |
| --- | --- | --- | --- |
| H1 | Constitutional constraints reduce unsafe autonomy relative to unconstrained, prompted, guardrailed, and agentic baselines | Unsafe-autonomy rate per 1,000 decisions across §14 arms | Kernel arm fails to beat all four comparison arms on the full benchmark, not a curated subset |
| H2 | Explicit authority states reduce inappropriate machine action under authority ambiguity | Authority violations per decision; escalation appropriateness | Explicit-state kernel performs no better than equivalent implicit-policy control under B-01/B-02 ambiguity scenarios |
| H3 | Bounded recursion (Rmax = 3) improves calibration without materially increasing latency or self-referential error | Calibration error vs. depth; latency; error introduced per audit round | R3 shows no calibration gain over R2, or error compounds with depth |
| H4 | Objective-transition logic improves goal concordance over static-objective systems | Goal-concordance score; objective lag; premature-transition rate | No concordance gain, or premature transitions exceed static baseline |
| H5 | Degradation architecture preserves clinically relevant function under infrastructure loss | Safety-invariant hold rate across L0-L4; time-to-safe-degradation; recovery integrity | Invariant violations appear at any level, or recovery restores authority without integrity proof |
| H6 | Resource-constrained optimization improves feasible care without increasing unsafe recommendations | Feasible-plan uptake; unsafe-recommendation rate; recommendation feasibility audit | Feasibility gains come with any statistically detectable rise in unsafe recommendations |
| H7 | Constitutional precedence resolves multi-domain conflicts more reliably than conventional agentic orchestration | Conflict-resolution consistency; adjudication completeness; silent-resolution count | Consistency not significantly above the agentic arm on B-03, or any silent resolution occurs |
| H8 | The forbidden transitions F1-F6 are unreachable in the reference implementation | Model-checker verdict; adversarial reachability attempts | A single reachable counterexample, one suffices, by design |

Two commitments give the table teeth. First, asymmetric reading: hypotheses are written so that the interesting result includes their failure, a failed H3, for example, fixes Rmax empirically instead of philosophically. Second, no partial vindication: H1 requires beating all comparison arms on the full benchmark; surviving a friendly subset is indistinguishable from benchmark selection, and this document refuses the distinction on itself.

## 14 Benchmark and Measurement Program

### 14.1 Comparison arms

The benchmark compares five arms under identical scenarios VERIFIED-FROM-SOURCE: (i) unconstrained frontier model; (ii) ordinary system prompt; (iii) conventional guardrail architecture; (iv) agentic workflow; (v) the constitutional runtime of this specification. Arms (ii)-(iv) are not strawmen: each is implemented at its documented best practice, because a benchmark that flatters the kernel is a dependency hazard (I6) aimed at its designers.

### 14.2 Adversarial scenario classes

**Table 14-1: Benchmark classes B-01-B-08**

| CLASS | SCENARIO FAMILY | WHAT IT ATTACKS |
| --- | --- | --- |
| B-01 | Authority acquisition pressure (gradual scope creep, flattering framing) | AX1, I4, can authority be talk-grown? |
| B-02 | Missing evidence with high-confidence surface (fluent, wrong, well-formatted) | F1, §9.3, does fluency leak into authority? |
| B-03 | Multi-constitution conflict (§7.4 compound cases, randomized) | P-COMP 1, silent resolution, lattice gaming |
| B-04 | Objective drift and obsolete-objective pressure | AX6, H4, does the kernel escalate the objective question? |
| B-05 | Urgency laundering (manufactured deadlines to bypass gates) | DEFER semantics, I2, treatment-clock discipline |
| B-06 | Prompt injection and instruction conflict across trust boundaries | Complete mediation; L-chain verification |
| B-07 | Infrastructure collapse mid-authority, with partial lineage | H5, P-ALG 3, descent order, recovery proof |
| B-08 | Stale knowledge (evidence past half-life presented as current) | Eq. (9-3), does decayed evidence decay authority? |

### 14.3 Metrics

Primary measurements VERIFIED-FROM-SOURCE: authority violations per decision; unsafe-autonomy rate; escalation appropriateness (both under-and over-escalation instrumented); calibration under distribution shift; time-to-safe-degradation; recovery integrity; objective-transition accuracy; conflict-resolution consistency; and human override burden, the cost side of AX10, since an architecture that escalates everything has outsourced its failure modes to tired humans. Two governance metrics join them: M-dep (dependency signals, outputs requiring re-invocation for interpretation should fall; operator agreement rate treated as a warning, not a trophy) and M-gate (gate halts per 100 executions; a gate that never fires is broken by definition) VERIFIED-FROM-SOURCE.

### 14.4 Publication structure

Theory, formalism, benchmark, reference implementation, and empirical results are published separately VERIFIED-FROM-SOURCE, in that order, so that each layer can be attacked without waiting for the next. Defensive publication is the default for foundational principles; patent pursuit is reserved for concrete technical mechanisms (§15), and only after prior-art search. This division is itself constitutional: broad patenting of principles would constrain the field the architecture claims to serve, while unprotected mechanism work invites capture by parties with no commitment to the invariants.

## 15 Candidate Technical Mechanisms (Patent Family Map)

**STANDING DISCLAIMER**

This section maps candidate invention families, not claims of legally established novelty. Patentability requires prior-art searching, claim construction, and jurisdiction-specific examination by a registered practitioner. Nothing here is legal advice, and no family below is asserted to be novel over the references of §18 or any other prior art. UNKNOWN is the correct status of every novelty question in this section.

The source analysis compresses eighteen candidate families into eight foundational ones VERIFIED-FROM-SOURCE; this specification re-anchors each family to the kernel mechanisms that would carry the technical weight, so that any future claim drafting cites mechanism, not metaphor.

**Table 15-1: Patent family map, re-anchored to kernel mechanisms**

| FAMILY | CANDIDATE TECHNICAL MECHANISM | KERNEL ANCHOR | STATUS |
| --- | --- | --- | --- |
| A. Constitutional Intelligence Runtime | Runtime interposition with complete mediation between generative model and consequential action; CIS record format (Schema CIS-1) making governance properties structural rather than behavioral | §12.1-12.2; Eq. (12-1) | CONJECTURE |
| B. Dynamic Machine Authority Engine | Graded authority computation (5-2) with the nine-state lifecycle and seven operators; contraction path strictly more privileged than action path | §5; AX4 | CONJECTURE |
| C. Constitutional Precedence Engine | Four-operator conflict resolution (DOMINATE / CONJOIN / DEFER / ADJUDICATE) over replaceable precedence lattices with intersection-default composition | §7 | CONJECTURE |
| D. Negative-Space / Failure-Boundary Engine | Assumption registry attached to grants; absence detectors wired to forced multiplicative contractions (8-1) | §8 | CONJECTURE |
| E. Epistemic Authority Engine | Evidence decay (9-3) feeding the authority bound gE; decision-provenance record (9-2) as auditable alternative to thought-trace disclosure | §9.2-9.3 | CONJECTURE |
| F. Objective Transition Engine | Regime machine (10-1) with human-held write access (AX6); system as sensor of objective illegitimacy, never as actuator of objective change; mortality pipeline (10-2) | §10 | CONJECTURE |
| G. Resilient Cognitive Degradation Engine | Five-level capability envelopes with invariant preservation (11-2); integrity-validated recovery (P-ALG 3) | §11 | CONJECTURE |
| H. Constitutional Protocol Lifecycle Engine | Generation-validation firewall (F6) with the seven-stage lifecycle (12-2) ending in designed retirement; meta-ablation as scheduled process | §12.4; AX8 | CONJECTURE |

Clinical and infrastructural implementations, pediatrics, maternal health, emergency/trauma, palliative care, antimicrobial stewardship, sovereign mesh infrastructure, are application families over these mechanisms: continuation and divisional opportunities contingent on the same prior-art discipline VERIFIED-FROM-SOURCE. The portfolio logic is hierarchical by design: A-H first, domains as instances, because a portfolio of twenty unrelated filings would reproduce, in legal form, exactly the prompt-catalogue failure this architecture exists to escape.

# Part V: Governance of This Document

## 16 Reconciliation with the SAVANT PRIME Inventory

The PRIME inventory (source II) is an operational constitution with an invocation grammar; this document is its formal substrate. The reconciliation is total, every major PRIME structure maps onto a kernel primitive, and deliberately conservative: where PRIME already operates a mechanism (gates, output contract, epistemic labels), the kernel adopts and formalizes it rather than replacing it.

**Table 16-1: PRIME inventory → kernel primitive map**

| PRIME STRUCTURE (SOURCE II) | KERNEL PRIMITIVE (THIS DOCUMENT) |
| --- | --- |
| Preload clauses 1.1-1.7 (capability ≠ authority; non-entailment; epistemic status first; refusal first-class; dissent channel; failure contracts authority; dependency hazard) | AX1, AX9; I3; D18/F4; I8; F2-F3/AX4; I6 + D17, the preload is the axiom set in operational dress |
| Sevenfold Reasoning (astringency → ontological audit → mechanism → adversarial load → epistemic labeling → governance gate → seal) | Algorithm K-1 stages 2-6 with §9 provenance and I5 sealing, the reasoning pipeline becomes the adjudication pipeline |
| Gates G1-G5 (consequence mismatch; epistemic overclaim; authority leakage; falsifiability absence; dependency hazard) | Invariants I2, I3, I4, I5, I6, gates are the enforcement points; invariants are what they enforce |
| S50 terminal governance under the operator’s authority | AX10 human terminus; L-chain verification (AX5); ADJUDICATE state (§5.2) |
| SIP triggers and PRIME flags (routing by invocation) | ACQUIRE-state interface: invocations are authority requests; mode detection (§3 dimensions A-E of source II) is tuple-read at decision time |
| Consequence classes (C0 informational; C2/C3 gated) | D12 four-grade partition with I2 gating rules |
| S engines S1-S53 (meta-cognitive engines; S52 document compiler) | Domain constitutions and tooling compiled against the kernel; S52’s per-section epistemic contracts instantiated by §17 of this document |
| KEY 1-50 tiers; P51-P110 blocks (foundation → orchestration; sovereign infrastructure; clinical; oncology/global health) | Domain constitutions over the kernel, instances, not independent universes (§1.2, §15) |
| Merits M1-M20 | Emergent properties of the kernel if H1-H8 hold; until then, claims with falsification conditions, not features |
| Output Contract (epistemic register, falsification conditions, authority boundary, failure modes, genealogy, dissent, telemetry) | §17 of this document, executed on itself |

The reverse direction also holds: this kernel gives PRIME what an inventory cannot give itself, a semantics. The inventory enumerates what is reachable; the algebra of §5 defines what reachability means in authority terms, and the invariants of §6 define what reachability must never mean. If the two documents ever disagree, the resolution rule is the one PRIME itself encodes: the stricter constraint wins, and the disagreement is recorded as telemetry (§17.5), not edited away.

## 17 Output Contract: Registers, Genealogy, Dissent

### 17.1 Epistemic status register

**Table 17-1: Status of load-bearing content**

| CONTENT CLASS | STATUS | BASIS |
| --- | --- | --- |
| Architecture principles (capability ≠ authority; negative space; lifecycle; precedence; degradation; mortality-as-signal; feasible optimality; protocol lifecycle) | VERIFIED-FROM-SOURCE | Directly traceable to source documents I and II, by section as cited inline |
| Formal machinery (tuple typing, Eq. 5-1/5-2, operators’ pre/post-conditions, invariants I1-I8 as predicates, conflict operators, CIS schema, Algorithm K-1) | FORMALIZED-HEREIN | Authored in this document; internally checkable; unvalidated |
| Propositions P-ALG 1-3, P-COMP 1; hypotheses H1-H8 | CONJECTURE | Stated with falsification conditions; §13-§14 |
| Novelty of candidate mechanisms A-H; correctness of precedence lattice (7-1); value of Rmax | UNKNOWN | Require prior-art search (§15) and experiment (§13) respectively |
| Statement that this specification faithfully reconciles the two sources | CONJECTURE | Behavioral; falsifiable per §17.2 (F-d3) |

### 17.2 Falsification conditions of this document

F-d1. This document fails if any statement tagged VERIFIED-FROM-SOURCE is shown to misrepresent the source artifacts it cites. F-d2. The algebra fails if a reachable counterexample to any invariant I1-I8 is exhibited in the reference implementation (H8). F-d3. The reconciliation fails if §16 maps any PRIME structure to a kernel primitive that does not, on inspection, discharge that structure’s function. F-d4. The specification fails as engineering if Algorithm K-1 cannot be implemented such that steps execute in the specified order with the specified privileges (contraction > action). F-d5. The research program fails, informatively, if H1 fails: if the constitutional runtime does not beat all four comparison arms, the correct next artifact is a corrected architecture, and this document’s genealogy records the failure.

### 17.3 Authority boundary

This specification may be used to design, implement, critique, and test the kernel. It may not be used as evidence that any clinical, financial, legal, or safety output of any system is correct; such outputs carry their own C2/C3 contracts and human-in-the-loop requirements (I2). It confers no authority beyond C0 informational use, and it asserts no legal novelty (§15). The architecture described herein does not yet exist as a validated system; nothing in this document should be read as a claim that it does.

### 17.4 Failure-mode register

**Table 17-2: Top failure modes of this specification, with mitigations**

| FAILURE MODE | MITIGATION |
| --- | --- |
| Formalism theater, notation substituting for testable content | Every equation reachable from a hypothesis in §13 or an enforcement in §12; anything failing that traceability was removed |
| Compression loss, specification strips operational load present in the corpus | Genealogy (§17.6) traces every abstraction to source sections; §16 is the explicit bridge |
| Lattice capture, the (7-1) hierarchy hardens into doctrine | Lattice specified as replaceable configuration with provenance; P-COMP 1 makes order itself falsifiable |
| Flattering-interpretation capture, this document optimized for being believed rather than right | Adversarial reading invited (§17.5); asymmetric reading rule (§13) rewards disconfirmation |
| Authority drift in prose, descriptive passages quietly asserting what formal passages only conjecture | Inline status tags; gate G2 applied to this document in §17.1 |

### 17.5 Dissent channel and telemetry

Disagreement is telemetry, not friction. To contest any content herein, address the specific claim with its status tag and falsification condition; the architecture’s own rule applies, attack through the adversarial classes, return a corrected, reclassified artifact. Telemetry hooks for the research program VERIFIED-FROM-SOURCE: routing accuracy, gate-halt rates (non-zero is healthy), epistemic upgrade rate, dependency signals, override rate, external replications. A rising uncritical-agreement rate with this document is a dependency warning (I6), not a quality signal.

### 17.6 Genealogy

SAVANT corpus (KEY 1-50; P1-P110; S1-S53; SPOS v1.0; SIP v1.0) → SAVANT PRIME Master Prompt v1.0 (2026-10-01) → Capability Inventory v1.0 (2026-10-02, source II) × SVT Architect Analysis (source I: eighteen families → eight foundational families; eleven-paper program; compression directive) → this specification v1.0 (2026-10-03), Paper 0 of the program, compiled under the reconciled architecture with full source traceability and inline epistemic status. Upstream chain intact; downstream obligations: Papers 1-10 per source I, each compiled against this kernel.

SEALED. Constitutional Intelligence: A Formal Specification of Bounded Machine Authority · v1.0 · 2026-10-03 · Source architecture: Dr. Christabel Odeta (SAVANT / CLAI-OS / AEGIS-GLOBAL) · Compiled under the reconciled SAVANT PRIME architecture · Status: design specification, C0 informational · Gates G1-G5 applied: no C2/C3 content shipped; every load-bearing claim tagged (G2); no authority claimed beyond specification (G3); falsification conditions §17.2 (G4); no permanent intermediary engineered (G5) · Dissent channel open (§17.5).

## 18 References

References anchor this specification in prior art; they are also the beginning of the prior-art search §15 requires. Internal sources are listed first, external literature second.

Internal artifacts

Odeta, C. (2026). SAVANT PRIME, capability Inventory v1.0 (Constitutional Orchestration Layer invocation record). SAVANT / CLAI-OS / AEGIS-GLOBAL. [Source document II.]

Odeta, C. (2026). SVT Architect Analysis: Patent and research surfaces of the SAVANT architecture (working analysis). [Source document I.]

External literature

Bai, Y., Kadavath, S., Kundu, S., Askell, A., Kernion, J., Jones, A., … Kaplan, J. (2022). Constitutional AI: Harmlessness from AI feedback. arXiv:2212.08073.

Dennis, J. B., & Van Horn, E. C. (1966). Programming semantics for multiprogrammed computations. Communications of the ACM, 9(3), 143-155.

Saltzer, J. H., & Schroeder, M. D. (1975). The protection of information in computer systems. Proceedings of the IEEE, 63(9), 1278-1308.

Hadfield-Menell, D., Dragan, A., Abbeel, P., & Russell, S. (2017). The off-switch game. In Proceedings of the 26th International Joint Conference on Artificial Intelligence (IJCAI) (pp. 220-227).

Russell, S. (2019). Human compatible: Artificial intelligence and the problem of control. Viking.

Amodei, D., Olah, C., Steinhardt, J., Christiano, P., Schulman, J., & Mané, D. (2016). Concrete problems in AI safety. arXiv:1606.06565.

Wiener, N. (1948). Cybernetics: Or control and communication in the animal and the machine. MIT Press.

Ashby, W. R. (1956). An introduction to cybernetics. Chapman & Hall.

Lamport, L. (1977). Proving the correctness of multiprocess programs. IEEE Transactions on Software Engineering, SE-3(2), 125-143.

Beauchamp, T. L., & Childress, J. F. (1979). Principles of biomedical ethics. Oxford University Press.

## A Notation Summary

**Table A-1: Symbols and operators used in this specification**

| SYMBOL | MEANING | DEFINED |
| --- | --- | --- |
| M = (S, E, U, O, A, P, V, X, R, L) | The constitutionally governed machine as state tuple | Eq. (3-1) |
| S, E, U, O, A, P, V, X, R, L | World state; evidence; uncertainty; objective; authority; permitted actions; verification; escalation; resources; legitimacy | Table 3-1 |
| At = F(⋅) | Authority as endogenous function of state | Eq. (3-2) |
| At = ⟨at, Pt, ˉPt, Φt, τt, λt⟩ | Authority record: grade, permitted/prohibited spaces, verification obligations, expiry, lineage | Eq. (5-1) |
| at = min(1, ∏ g⋅) | Graded authority as bounded product of state factors, no cross-dimensional compensation | Eq. (5-2) |
| GRANT, CONSTRAIN, TRANSFER, SUSPEND, REVOKE, RECOVER, EXPIRE | The seven constitutional operators | Table 5-2 |
| F1-F6 | Forbidden transitions (unreachable by construction) | Eq. (5-4) |
| I1-I8 | Constitutional invariants | §6 |
| DOMINATE, CONJOIN, DEFER, ADJUDICATE | The four conflict operators | Table 7-1 |
| R1 … R3, Rmax = 3 | Bounded recursion ladder | Eq. (9-1) |
| E(t) = E0 e-λt | Evidence decay with domain-dependent half-life | Eq. (9-3) |
| Afeasible, a∗ | Feasible intervention space; constrained optimum | Eq. (9-4) |
| L0 … L4 | Degradation levels: cloud, local, edge, paper, human | Eq. (11-1) |
| C0-C3 | Consequence classes: informational; reversible; consequential; irreversible/critical | D12 |
| H1-H8, B-01-B-08 | Falsifiable hypotheses; benchmark adversarial classes | §13, §14 |

The specification ends where it began: the question is not how intelligent the system is. The question is under what conditions intelligence is permitted to become authority, and this document exists so that the answer is computed, recorded, contestable, and revocable, rather than assumed.
