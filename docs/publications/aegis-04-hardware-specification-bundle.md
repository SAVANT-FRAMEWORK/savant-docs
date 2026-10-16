---
title: AEGIS-NG Hardware Specification Bundle — SAVANT Publications
description: Production hardware specifications for five AEGIS-NG nodes: TALISMAN, STAFF, SENTINEL-Base, SENTINEL-THERMAL, GUARDIAN-NODE.
---

# AEGIS-NG Hardware Specification Bundle v1.0 — Nodes N-A01 TALISMAN, N-A05 STAFF, N-B01 SENTINEL-Base, N-B03 SENTINEL-THERMAL, N-C02 GUARDIAN-NODE (SAVANT AEGIS Series)

**Author:** Dr. Christabel Odeta — SAVANT / CLAI-OS / AEGIS-GLOBAL · **Version 1.0 · October 2026**
**Classification:** C0 INFORMATIONAL — confers no clinical, legal, financial, or safety authority.

DOI: [10.5281/zenodo.23409950](https://doi.org/10.5281/zenodo.23409950) · License: CC-BY-4.0 · [Full record (Zenodo)](https://doi.org/10.5281/zenodo.23409950)

## Abstract

This bundle publishes the production hardware specifications for five nodes of the AEGIS-NG civilian-protection mesh: N-A01 TALISMAN (personal duress beacon with kinetic-physiological hostility sensing and passive IR neutrality marking), N-A05 STAFF (solar-powered vigilante patrol staff with active IR marking), N-B01 SENTINEL-Base (mesh relay and store-and-forward backbone), N-B03 SENTINEL-THERMAL (thermal imaging and hostile-detection node with on-device TFLite Micro inference), and N-C02 GUARDIAN-NODE (mesh-to-external bridge: 433 MHz mesh receive, 4G LTE burst, 148 MHz VHF transmit, armed-forces liaison). Each specification covers system architecture, block diagrams, sensor suites, power budgets, cryptography, tamper behavior, and S50 axiom compliance. All performance figures — battery life, detection ranges, power draw, BOM costs — are unverified engineering targets. Zero-surveillance by design: no GPS on any civilian beacon. Hardware specifications are CC BY-SA 4.0; this deposit is CC-BY-4.0 per corpus convention.

## Merit

The bundle converts the master architecture into five buildable objects. Its merit is completeness at the production boundary: block diagrams, sensor suites, power budgets, cryptography, tamper behavior, and S50 axiom compliance per node — the level of disclosure a contract manufacturer or an independent verifier actually needs. The zero-surveillance property is implemented, not asserted: no civilian beacon carries GPS. The GUARDIAN-NODE specification defines the single controlled bridge between the civilian mesh and external response forces, which is where the architecture's safety guarantees are hardest and most consequential.

## Guidance for Use

**Who should read this work**

- Hardware engineers reproducing or auditing any of the five node designs.
- Manufacturers preparing quotations or DFM reviews.
- Security reviewers examining cryptography, tamper behavior, and the no-GPS guarantee.
- Certifiers checking S50 axiom compliance at the node level.

**What it enables**

- Five production-grade node specifications ready for manufacturing engagement.
- Node-level falsifiability: every figure labeled as an unverified target with a validation path.
- The complete sensing-to-response chain, from duress beacon to armed-forces liaison.

**How to cite**

```bibtex
@misc{odeta2026hardware,
  author    = {Odeta, Christabel},
  title     = {AEGIS-NG Hardware Specification Bundle v1.0 — Production Specifications for Nodes N-A01 TALISMAN, N-A05 STAFF, N-B01 SENTINEL-Base, N-B03 SENTINEL-THERMAL, and N-C02 GUARDIAN-NODE},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.23409950},
  url       = {https://doi.org/10.5281/zenodo.23409950}
}
```

**Related works in the series**

- [AEGIS-NG v2.0 INFINITE — Master System Document](aegis-02-aegis-ng-master-document.md)
- [Defensive Publication v5.0 (prior-art anchor)](aegis-01-defensive-publication-v5.md)
- [Manufacturing & China Sourcing Specification](aegis-05-manufacturing-sourcing-specification.md)

**Keywords:** AEGIS-NG · hardware specification · LoRa mesh node · safety beacon · thermal sensor · mesh relay · Guardian Node · anti-tamper · open hardware
