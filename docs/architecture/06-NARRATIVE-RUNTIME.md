# Narrative runtime and scene compiler
## Two independent state machines
Playback: idle → loading → ready → playing/paused → inspecting/comparing/choosing → ready → completed. Error and revoked are explicit states.
Analysis computation: queued → running → validating → succeeded; failed/cancelled are terminal. Success means a validated draft was stored, not approved. Candidate review is a separate pending → approved/rejected lifecycle. Release job leases before human review; the five-minute job budget excludes editorial waiting. Analysis cannot mutate playback history.

## Serializable viewer state
{ bundleVersion, sceneId, perspectiveId, layer, timeCursor, branchId, choiceHistory, visitedSceneIds, playbackPositionMs, locale, reducedMotion, meaningLens, stateSchemaVersion }
Keep authentication and evidence text out of persisted progress. Anonymous MVP progress may be local and non-sensitive. S5 private progress requires authenticated server storage; do not place sensitive story bundles in localStorage.

## Pure domain interfaces (proposed)
loadBundle(raw): Result<StoryBundle, ValidationError[]>
transition(state, event, bundle): Result<ViewerState, TransitionError>
availableChoices(state, bundle): Choice[]
projectPerspective(bundle, eventId, perspectiveId): PerspectiveView
traceExplanation(bundle, behaviorId, maxDepth): ExplanationNeighborhood
forkScenario(bundleRevision, choiceId, assumptions): ScenarioDraft
compileStory(reviewedRevision, assetManifest): Result<StoryBundle, CompileError[]>

Renderer receives a projection, not direct database objects. Server validates saved progress and choices against the same versioned contracts.

## Narrative graph constraints
Every scene exists, is reachable from an entry or is explicitly an alternate entry. Every choice target exists; every scene has accessible text and a valid perspective. Runtime branching is finite per action. Authored cycles require an explicit user action or bounded repeat count; automatic transitions cannot create infinite animation loops.
Feedback loops are semantic patterns and can be animated once without replaying forever.
Perspective switch preserves event identity; if there is no view for that participant, display "not known" rather than synthesize.
Depth-limited graph traversal uses a visited set and node budget. UI defaults depth 2, API maximum depth 4; max 100 nodes/request.
Reject temporal contradictions unless edge is a narrative flashback or explicitly a recurrent pattern across distinct time steps.

## Conditions
Use declarative allowlisted predicates (selectedChoice, perspective, visitedScene, storyFlag), not arbitrary JavaScript or eval. Conditions cannot access private data or generate hidden psychological scores.
A branch may contain assumptions such as "the other person is willing to listen"; they remain visible. Do not make disclosure or compliance necessary for a successful ending.

## Compilation
Author sources → schema validation → graph checks → evidence/rights checks → accessibility checks → deterministic layout → asset manifest → canonical JSON hash → reviewed publication.
Compiler emits one bundle per revision and locale, with stable IDs. A model can propose author sources but cannot bypass compilation.
Dependency versions, compiler version and content hash are recorded. Sign or integrity-check manifests when crossing delivery boundaries.

## Replay and updates
Replay uses stored accepted content and viewer choices. It does not call AI again. Save choice sequence with a monotonic index; duplicate submission is idempotent.
A new published version does not silently replace an active session. Offer restart or compatible migration. Origin reads of a revoked publication are blocked immediately. Clients check a no-store publication-status endpoint before opening a bundle and every 60 seconds while active, also on visibility/network resume. Proposed connected-client detection target is <=90 seconds under normal connectivity. CDN purge is asynchronous. Cached public copies cannot be reliably clawed back; disconnected playback cannot guarantee revocation, so only intentionally public content is cacheable.
The example bundle in this directory is an illustrative contract fixture, not a complete validated runtime package.
