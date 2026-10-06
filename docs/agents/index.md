---
title: Deployment Agent Stack — CLAI-OS & AEGIS-GLOBAL
description: The 20 specialist deployment agents, the extended SIP trigger matrix, and the track namespace rule.
---

# Deployment Agent Stack

**Version:** 2.0.0
**Author:** Dr. Christabel Odeta — SAVANT FRAMEWORK · CLAI-OS · AEGIS-GLOBAL
**License:** Savant-Commercial-1.0 (agent bodies) — catalog and trigger matrix public
**Governance:** PRIME → S1 → S50 → S52

The deployment agent corpus converts SAVANT IP into executed deployments: twenty
specialist agents across two tracks, each RASCEF-structured, each operating under
the meta-constitutional preloads (S1, S50, S52) and PRIME's governance gates.
Catalog entries and the trigger matrix below are public; full agent bodies are
commercial — abstracts and SHA-256 existence-commitments live in
[savant-prompts/commercial-tier](https://github.com/SAVANT-FRAMEWORK/savant-prompts/tree/main/commercial-tier).

## CLAI-OS Track — Clinical Division (10 agents)

| Agent | Function | SIP Trigger |
|-------|----------|-------------|
| CLAI-DEPLOY-01 | Academic/Clinical Publication Architect | `PUBLISH` |
| CLAI-DEPLOY-02 | Clinical Regulatory Diplomat | `REGULATE` |
| CLAI-DEPLOY-03 | Clinical Grant Strategist | `FUND` |
| CLAI-DEPLOY-04 | Hospital/Health System Partnership Negotiator | `PARTNER` |
| CLAI-DEPLOY-05 | Clinical Trial & Validation Architect | `EVALUATE` |
| CLAI-DEPLOY-06 | FHIR/Health IT Integration Engineer | `INTEGRATE` |
| CLAI-DEPLOY-07 | Open Source Clinical Community Architect | `COMMUNITY` |
| CLAI-DEPLOY-08 | Co-Authorship Invitation Deployer | `INVITE` |
| CLAI-DEPLOY-09 | Precision Medicine/Genomic Justice Coordinator | `PRECISION` |
| CLAI-DEPLOY-10 | Master Clinical Orchestrator | `DEPLOY` (S50 override) |

Clinical invariant: no CLAI-OS deployment agent may recommend autonomous clinical
diagnosis without human-in-the-loop at T2 minimum; deterministic safety paths
execute before stochastic reasoning; patient data never leaves sovereign node
jurisdiction.

## AEGIS-GLOBAL Track — Security Division (10 agents)

| Agent | Function | SIP Trigger |
|-------|----------|-------------|
| AEGIS-DEPLOY-01 | Sovereign Manufacturing Architect | `MANUFACTURE` |
| AEGIS-DEPLOY-02 | Field Deployment Coordinator | `FIELD` |
| AEGIS-DEPLOY-03 | Security & Threat Model Auditor | `AUDIT` |
| AEGIS-DEPLOY-04 | Hardware Supply Chain & BOM Engineer | `SUPPLY` |
| AEGIS-DEPLOY-05 | Law Enforcement Integration Diplomat | `LAW` |
| AEGIS-DEPLOY-06 | Security Grant Deployment Strategist | `FUND` |
| AEGIS-DEPLOY-07 | Regulatory Certification Engineer | `CERTIFY` |
| AEGIS-DEPLOY-08 | Training & Certification Curriculum Designer | `TRAIN` |
| AEGIS-DEPLOY-09 | Patent & Defensive Publication Prosecutor | `PATENT` |
| AEGIS-DEPLOY-10 | Master Sovereign Orchestrator | `DEPLOY` (S50 override) |

Sovereignty invariant: AEGIS-GLOBAL is open-architecture sovereignty transfer, not
product export. Safety invariant: no surveillance-as-a-service, no predictive
policing of civilians, no foreign data extraction; children's beacons are
passive-only with no biometric collection.

## The Trigger Namespace Rule

The SIP layer now carries **35 triggers**: 15 core prefixes plus 20 deployment
triggers. Ambiguity is resolved structurally, not by operator effort:

1. **Routing precedes invocation.** PRIME's mode detection (domain dimension)
   selects the active track — CLAI-OS, AEGIS-GLOBAL, or core — before any
   trigger resolves.
2. **One-letter shortcuts are track-local.** A letter resolves only within the
   active track; the same letter may bind different agents in different tracks
   without collision.
3. **Full-word triggers are globally unique**, except three deliberately
   harmonized homonyms — `FUND`, `DEPLOY`, `AUDIT` — which name one governance
   class with track-local specializations (e.g. `AUDIT` invokes core audit in
   the core track and AEGIS-DEPLOY-03 in the security track).

## Falsifiability Test

This page fails if any invocation is shown to resolve ambiguously under the
namespace rule, or if any agent body is found published in a public repository.
