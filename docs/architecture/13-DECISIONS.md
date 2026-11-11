# Architecture decision records
All decisions are proposed architecture-author recommendations as of 2026-11-11.

| ADR | Decision | Alternatives / consequence |
|---|---|---|
| 001 | Curated fiction first | Arbitrary real-person analysis would front-load evidence, consent and defamation risk; delayed to reviewed modes |
| 002 | Modular monolith + worker | Microservices increase consistency/operations overhead; boundaries permit later extraction |
| 003 | Three graphs: events, explanations, narrative | One graph conflates history, inference and presentation; shared IDs require explicit references |
| 004 | PostgreSQL relational graph | Neo4j deferred until measured query need; tenant integrity and versioning simpler in one source of truth |
| 005 | Scene-first DOM/SVG viewer | Pure graph dashboard too textual; full 3D deferred for accessibility and production cost |
| 006 | React Flow for authoring | Not required as primary viewer; larger graph optional Sigma.js |
| 007 | XState for explicit player transitions | Ad-hoc UI booleans permit impossible states; persist portable domain state |
| 008 | Versioned JSON story contract | Ink is useful inspiration; adopting separate narrative DSL now adds compiler/runtime mapping burden |
| 009 | AI outputs drafts only | Automatic publication rejected; review limits latency and scale but protects provenance |
| 010 | Qualitative evidence labels | Model confidence percentages rejected as uncalibrated |
| 011 | Meaning layer separate and opt-in | Blending metaphysical interpretation into historical causality obscures epistemic boundaries |
| 012 | Public immutable bundles; private no-store | Improves public performance while avoiding private CDN leaks |
| 013 | Database queue initially | Broker/Redis deferred; implement leases/idempotency, not naive fire-and-forget |
| 014 | Provider-neutral server adapters | No client keys; models chosen through evaluation, not fixed in architecture |
| 015 | Asset rights separate from code licensing | Permissive library license does not grant rights to biographies, translations or artwork |
| 016 | No hidden psychometric scoring | Emotion visuals are authored/illustrative; no diagnosis or measured biological claims |
| 017 | Private stories released last | Consent/deletion/provider policies must be proven before sensitive submissions |

## Open decisions and triggers
- Exact dependency versions: S1 compatibility spike, supported stable only.
- Hosting provider/region: S2 operations setup; S5 privacy constraints may narrow it.
- AI/media vendors: S3 benchmark and contracts; costs and retention verified then.
- Public repository license: owner business choice before reuse/distribution.
- Commercial prices, age verification and jurisdictions: S5 business/legal review.
- Historical catalog: content availability and source rights, not automatic scraping.
- Additional languages: human-reviewed terminology and accessibility capacity.
- Graph database, embeddings, broker, 3D: measured need, with ADR amendment.
- Medical claims: excluded; any future clinical product would require a separate validated scope.

Changes to invariants require an ADR amendment, contract version impact assessment, and an acceptance-test update. Record a decision as accepted only when implementation evidence or explicit approval supports that status.
