# Implementation roadmap
Status: proposed delivery plan; not executed. [Product](01-PRODUCT.md) and [system](02-SYSTEM.md) are the design baseline.

## Ordered slices
No calendar promise is made before implementation spikes and content production estimates. Each slice ends in a reviewable user journey.

### S1 — Fictional visual journey
Future files: apps/web/src/features/player/*; packages/contracts/story-bundle.schema.json; packages/domain/narrative.ts; content/fiction/kamran/*; tests/domain/narrative.test.ts; tests/e2e/kamran.spec.ts.
Consumes: illustrative bundle contract and fictional story spec.
S1 bootstrap: locally validate/compile the story and record manual editorial review against its checked-in content hash. If publicly hosted, implement the minimal no-store publication-status endpoint and player checks; otherwise keep it a local demo. S2 replaces manual release operations with the full database workflow.
Produces: loadBundle, transition, projectPerspective, availableChoices and a responsive player.

- [ ] Lock supported stable dependencies and establish build/lint/type checks.
- [ ] Define executable JSON Schema from the example and complete story requirements.
- [ ] Add failing tests for invalid IDs, infinite auto-loops, illegal choices and unknown perspective.
- [ ] Implement pure transitions and bundle validation.
- [ ] Author complete scenes, two perspectives, three choices and accessible text.
- [ ] Implement scene-first player with timeline, layer opening, alternative explanation and replay.
- [ ] Verify keyboard, mobile, reduced-motion, static asset fallback and state persistence.
- [ ] Record G01–G04/G09 results. No AI credential is required.

### S2 — Authoring and controlled publication
Future files: apps/web/src/features/studio/*; packages/db/migrations/*; packages/domain/publication.ts; packages/content/compiler.ts; tests/integration/publication.test.ts.
Consumes: S1 contracts and player.
Produces: compileStory and immutable reviewed publications served by v1 API.

- [ ] Model normalized data, tenancy and RLS with wrong-tenant tests.
- [ ] Implement author/reviewer/publisher actions with exact-hash approval.
- [ ] Add optimistic edit conflict and duplicate publication tests.
- [ ] Implement rights manifests, asset quarantine and private source handling.
- [ ] Compile reviewed draft to immutable bundle; atomic pointer update plus outbox.
- [ ] Test revoke, missing asset and source status paths.
- [ ] Record G05/G06 and accessible studio journey.

### S3 — Assisted analysis
Future files: apps/worker/src/analysis/*; packages/domain/analysis-policy.ts; packages/contracts/analysis.schema.json; tests/evaluation/*.
Consumes: authorized input revision, source spans, job contracts.
Produces: AnalysisCandidate and unpublished scene suggestions.

- [ ] Define model adapter and budget/cancellation interface.
- [ ] Add failure fixtures for fabricated sources, invented memories and source injection.
- [ ] Implement extraction, authorized retrieval, generation and alternative critique.
- [ ] Validate output; keep model results nonpublishable until human review.
- [ ] Implement durable job leases, bounded retries and cost reservation.
- [ ] Test cancellation races, worker restart, provider outage and tenant isolation.
- [ ] Compare candidate quality with authored baseline and record G07/G08.
- [ ] Pin evaluated model/config versions; do not select solely by narrative fluency.

### S4 — Reviewed biographies and context
Future files: packages/domain/evidence-dependencies.ts; apps/web/src/features/context/*; content/historical/*; content/meaning/*.
Consumes: S2 publication workflow and S3 evidence pipeline.
Produces: sourced historical episode, bounded social graph, independent meaning overlay.

- [ ] Define source/rights editorial policy and reviewed real-person eligibility.
- [ ] Implement approximate chronology and competing source accounts.
- [ ] Add retraction dependency traversal and stale-publication handling.
- [ ] Add bounded context graph without changing canonical facts.
- [ ] Add named tradition overlays with opt-in and appropriate review.
- [ ] Validate G08/G10; public figures' motives remain hypotheses unless attributed.

### S5 — Private reflection and commerce
Future files: apps/web/src/features/privacy/*; packages/domain/consent.ts; apps/worker/src/deletion/*; packages/domain/entitlements.ts.
Consumes: all prior access, editorial and operations gates.
Produces: private-only case handling and optional paid entitlements.

- [ ] Finalize jurisdiction, privacy policy, provider retention/region and adult-only policy.
- [ ] Add private upload consent, aliases and purpose controls.
- [ ] Test no-store/cache bypass and nested private asset authorization.
- [ ] Implement export, deletion, provider handling and restore-time tombstone replay.
- [ ] Test late-job completion after deletion/consent revocation.
- [ ] Add billing only after provider selection; verify webhook signatures/idempotency and keep entitlements separate from access.
- [ ] Record G11/G12 and incident/restore rehearsal.

## Risks and dependency order
Content production may dominate development time. Prototype one complete story before building a large catalog. Scene renderer and evidence ontology must stabilize before model-driven generation. Private mode depends on proven isolation and deletion; do not ship it as an unfinished toggle.
Full historical and philosophical breadth requires specialist review and permissions; no deadline or content volume is promised.

## Definition of done
Feature works in a complete user journey, meaningful tests pass, accessible equivalent exists, content/provenance labels survive export, operational failure path is demonstrated, and limitations are recorded. A green unit suite alone is not product readiness.
