# savant-docs

**SAVANT FRAMEWORK — Constitutional Documentation.** The public documentation repo for the SAVANT FRAMEWORK constitutional clinical intelligence infrastructure: SPOS, SIP, S50-ABSOLUTE, CLAI-OS, AEGIS-NG, and AEGIS-GLOBAL. Authored by Dr. Christabel Odeta.

- **Live site:** https://savant-framework.github.io/savant-docs/
- **Organization:** https://github.com/SAVANT-FRAMEWORK
- **Companion prompt corpus:** https://github.com/SAVANT-FRAMEWORK/savant-prompts
- **Demo:** https://github.com/SAVANT-FRAMEWORK/savant-demo

This is a MkDocs Material site. Content is plain Markdown under `docs/`; the built site is published from the `gh-pages` orphan branch.

## Documentation Map

| Section | Pages |
|---------|-------|
| Home | Constitutional record overview |
| Architecture | SPOS v1.0 (Sovereign Prompt Operating System) · SIP v1.0 (Sovereign Invocation Protocol) · S50-ABSOLUTE (Governance Engine) |
| CLAI-OS | Deterministic Clinical Engine · FHIR R4 Native Resource Layer · Integration Layer (Document A2) |
| CLAI-OS Operations | P1–P50 abstract & summary, split along the source document's own section boundaries: business model & publishing strategy · Global Equity extension (P51-G–P70-G) · Tiers 1–5 · Tiers 6–10 & deployment playbook · Africa extension (P51-AF–P70-AF) · module structures & Advanced Markets (Asia) · US & Arab region extensions |
| Prompt Corpus | 75 prompts / 15 tiers · 34 PRESENT / 41 PENDING ledger · license gate (KEY-001..020 AGPL-3.0 · KEY-021..075 Savant-Commercial-1.0) |
| AEGIS-NG | 14 node types (N-A01 – N-D02) · 433 MHz LoRa mesh protocol |
| AEGIS-GLOBAL | Manufacturing & China sourcing specification · local engineer certification curriculum |
| Grants | Universal grant narrative template |
| Compliance | P61–P70 regional compliance adapters (24 jurisdictions) |

## Local Build

```bash
pip install mkdocs-material
mkdocs serve           # local preview at http://127.0.0.1:8000
mkdocs build --strict  # canonical build; must pass clean
```

The site is designed for print/PDF export: all diagrams are ASCII, all data is tabular.

## Conventions

- **Honest absence:** PENDING canon entries are disclosed as ledger rows only — no placeholder pages.
- **Sanitization:** Pages derived from private working documents carry a source + sanitization-date header. SAVANT commercial licensing terms are redacted: `[Commercial licensing terms — inquiries via the GitHub organization]`.
- **Commits:** `[L5-EXECUTION] …` convention on `main`; site rebuilds are committed to `gh-pages`.
