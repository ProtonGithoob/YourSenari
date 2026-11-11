# Content, editorial and media pipeline
## Authoring lifecycle
draft → structured validation → editorial review → approved → published → superseded/revoked.
Rejected review returns a new editable draft. Approval applies to exact revision hash. Any text, relation, asset or source change invalidates approval of that revision.

Roles: author creates drafts; reviewer examines content/evidence/visual implication; publisher activates approved content. Same person may perform all roles for a fictional solo prototype, but role actions remain explicit. Public historical profiles require independent source/subject-matter review before release.

## Fictional pilot
Kamran, 38, manager. Two perspectives: Kamran and employee Leyla. Event: error in a report. Authored appraisal: fear that the error threatens professional standing. Alternative: workplace rewards harsh control. Employee interpretation: questions may be punished.
Timeline includes adverse and supportive experiences; no claim that all controlling behavior comes from childhood.
Three response options: accusation, clarifying question, pause and structured feedback. Include conditional outcomes: cooperative repair, unresolved disagreement, continuing systemic pressure.
No output is a user's assessment. Fiction badge persists across screenshots and exports.

## Story package
Metadata: mode, synopsis, age/content guidance, locale, authors, review.
Subjects: stable character definitions and relationships.
Events: chronological record with date precision.
Claims: kind, evidence, alternatives and limitations.
Scenes: visual cues, optional monologues, accessible summaries.
Choices: conditions, implications, outcomes, branch IDs.
Assets: content hashes, license/consent, alt text, audio transcripts.
Manifest: schema/compiler version, content revision, dependencies.
Meaning lenses: separate optional named tradition and reviewed references.

## Media strategy
Start with hand-curated 2D layered illustrations and reusable poses. Character identity sheet fixes silhouette, clothing palette and expression vocabulary across ages. Audio optional and pre-rendered. No real-person voice cloning or deceptive biographical reenactments.
Asset generation is an authoring action; generation output remains a draft. Review checks identity continuity, respectful depiction, rights, caption consistency and whether an expression implies unsupported certainty.
Do not generate image text for key labels: render localized UI text as HTML/SVG for accuracy and accessibility. This corrects the limitations of the earlier concept mockups.

## Processing
Upload to quarantine → verify signature/type/size → scan → remove unnecessary metadata → derivative encoding → review → immutable asset ID. Uploaded SVG is sanitized or rasterized; arbitrary embedded scripts and external fetches prohibited.
Media variants include responsive image sizes, reduced-motion static still and optional audio. Delivery manifest includes byte size and hashes. A missing asset displays a neutral fallback with the scene's accessible text.
Asset rights: creator, source, license, commercial use status, attribution, consent scope, expiration and transformation permission. Code license does not cover datasets or artwork automatically.

## Publication transaction
Check story mode, eligible review hash, all referenced claims, source status, asset approval and rights. Compile bundle. Save immutable publication row and update catalog pointer atomically. Emit outbox invalidation event after commit.
Public bundle contains only approved excerpts/locators, not complete proprietary sources or private author notes.
Revocation blocks origin publication reads immediately and triggers asynchronous CDN purge. A no-store status check before bundle opening and every 60 seconds while active targets connected-client detection within 90 seconds; offline or retained public downloads cannot be recalled. Private cases are never emitted to public bundles.

## Localization
Content keys with AZ primary and EN authoring support. Emotion terms, uncertainty labels and cultural interpretations receive human review, not only machine translation.
Review applies per locale where meaning changes. A translated quote identifies translation status. Do not collapse distinct religious traditions into universal karma terminology.
Historical references need source title, author/date, passage locator, access date and rights.
