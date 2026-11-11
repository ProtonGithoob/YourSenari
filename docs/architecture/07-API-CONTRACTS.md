# API contracts (proposed v1)
This is a normative design table, not an implemented OpenAPI server. S2 generates and validates OpenAPI 3.1 from shared schemas.

## Conventions
Base /api/v1. JSON request/response. IDs are opaque UUIDs in production; sample fixtures use readable IDs. Every request gets a correlation ID. UTC timestamps use ISO-8601; historical dates use precision-aware event intervals.
Authenticated operations derive workspace membership server-side. Ignore client ownership claims. Browser mutations require CSRF protection with cookie auth. Use Secure, HttpOnly, SameSite cookies and rotate sessions.

## Endpoints
| Method and path | Access | Input | Output |
|---|---|---|---|
| GET /stories | Public | cursor, locale, mode | Published summaries and nextCursor |
| GET /stories/{id}/bundle | Public only for approved public publication; otherwise member | revision?, locale | Immutable StoryBundle + ETag |
| GET /publications/{id}/status | Public for public IDs; otherwise authorized | none | active/revoked, revision; Cache-Control: no-store |
| GET /stories/{id}/graph | Same as bundle | rootId, depth<=4, limit<=100, perspective | Authorized typed nodes/edges |
| GET /claims/{id}/evidence | Story-authorized | revision | Permitted evidence summaries, not private source blobs |
| POST /explorations | Viewer | publicationId, locale | Exploration ID and initial state |
| PATCH /explorations/{id} | Owner | state, expectedVersion | Updated state/version |
| POST /explorations/{id}/choices | Owner | choiceId, sequence, expectedVersion | Deterministic next state |
| POST /stories | Author | mode, subjectIds, locale | Draft story |
| POST /stories/{id}/revisions | Author | parentRevisionId, draft | New draft revision |
| POST /revisions/{id}/reviews | Reviewer | decision, reasons, contentHash | Immutable review record |
| POST /stories/{id}/publications | Publisher | reviewedRevisionId, expectedPublishedVersion | Publication |
| DELETE /publications/{id} | Publisher | reason | Revoked status and invalidation job |
| POST /analyses | Authorized author, S3 | inputRevisionId, requestedTask | 202 jobId/statusUrl |
| GET /jobs/{id} | Owner/workspace permission | none | Status, stage, sanitized error |
| POST /jobs/{id}/cancel | Owner | none | Cancel requested |
| POST /assets/uploads | Author, S2 | type, size, purpose | Restricted upload target and token |
| POST /assets/{id}/finalize | Author | upload token | Processing job |
| POST /account/exports | Owner, S5 | scope | 202 export job |
| POST /account/deletions | Owner, S5 | scope and reauthentication | 202 deletion request |

Source ingestion is initially controlled editorial ingestion. Arbitrary URL ingestion requires SSRF controls before activation.

## Envelopes and errors
Success collection: {items: [], nextCursor: null, requestId}.
Error: {error: {code, message, fieldErrors?, retryable}, requestId}.
400 malformed input; 401 unauthenticated; 403 forbidden action; 404 absent or unauthorized resource where enumeration matters; 409 version conflict; 413 oversized; 422 semantic validation; 429 quota with Retry-After; 503 unavailable.
Never echo source text, provider credentials or internal prompts in errors.

## Idempotency
POST analyses/publications/choices uses Idempotency-Key, scoped to authenticated principal and operation. Persist request hash and result for a proposed 24-hour window. Same key+same input returns same outcome; different input returns 409. Atomic uniqueness in PostgreSQL prevents two concurrent charges/publications.
Draft/progress edits use expectedVersion or If-Match; stale writes return 409/412 consistently per chosen HTTP contract, with a fresh authorized version descriptor. No silent last-write-wins.

## Job events
Poll first (2-second initial interval, exponential backoff capped at 15 seconds, pause on hidden tab); SSE can follow if needed. Proposed events: job.accepted, stage.started, stage.completed, candidate.review_required, job.failed, job.cancelled. Each carries jobId, sequence, stage, timestamp, progressCategory; no invented exact completion percentage.

## Pagination and limits
Cursor pagination with stable sort, default 20, max 100. Text input max 20,000 characters for initial analysis; uploaded source proposed max 10 MB with MIME verification. Limits configurable by policy and exposed before submission.
Published public bundles may use CDN caching with version-specific URLs. Private API and private media responses use no-store; CDN bypass, not merely obscure URLs.

## Authorization rule
Every job, asset, source span, graph node and nested relation is checked, not just the top-level story. An author cannot assign a reviewer role. Publication checks exact hash, permitted rights, review eligibility and absence of revoked dependencies in one transaction.
