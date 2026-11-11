# Security, privacy and trust
## Data classes
Public fiction; reviewed public historical data; restricted editorial sources; private self-reports; identity/authentication data; provider secrets.
The repository is public. Never commit private stories, source documents, credentials, consent forms or production exports. Example fixtures contain invented adults only.

## Access
Roles: viewer, author, reviewer, publisher, workspace admin. Membership checked on every request and background job.
PostgreSQL RLS is defense in depth. Application roles are not table owners or BYPASSRLS roles. Apply FORCE ROW LEVEL SECURITY where appropriate. Set verified tenant context with SET LOCAL inside each transaction; connection pooling must not leak prior context.
Use composite tenant foreign keys. Background jobs carry tenant identity but recheck membership, consent and deletion status before each external call and write.
A public-serving path reads a deliberately sanitized publication projection. It cannot use elevated private-table access to assemble arbitrary bundles.
Admin access is audited and scoped; production access is not granted simply because someone can use the author studio.

## Threat model
| Threat | Control and acceptance test |
|---|---|
| Cross-tenant object ID substitution | Row and nested-edge authorization; tenant A cannot read B's graph/source/job/media |
| Prompt injection in source | Treat source as untrusted data; no tool authority; source cannot change policy |
| Invented biographical details | Claim-kind checks, provenance, human review; no direct auto-publish |
| Private data in logs/analytics | Allowlisted metadata; redaction tests; session replay disabled on sensitive screens |
| SSRF from source URLs | Allowlist fetch service, block local/private ranges, revalidate redirects/DNS, no ambient credentials |
| Malicious upload | Quarantine, signature checks, scan, safe rendering |
| Stolen session | Secure cookies, CSRF protection, rotation, MFA for publishers/admins |
| Excessive generation/cost | Workspace quotas, budget reservation, concurrency and rate limits |
| Deleted data resurrected | Tombstones, job cancellation, restore-time deletion replay |
| Cache leakage | Private no-store and CDN bypass; short signed URLs; auth checks |
| Harassing private-person profile | Consent/purpose gates; public publication prohibited by default |
| Source/asset license breach | Rights manifests, release blocker, removal process |

## Personal reflection release gate
Private mode is adult-only initially. Explain processing purpose and external-provider use before submission. Do not require identifying others; default to aliases. Consent is revocable and scoped, not a blanket waiver.
Private cases cannot be public by a simple share toggle. Any publication requires a separate redacted derivative and appropriate consent; no private-to-public automatic reuse.
No data used for model training without a separate, explicit policy and opt-in. Provider contract/region/retention verification must precede sensitive processing.

## Retention proposal
Raw model request/response text: no general logging; accepted output retained as user content; temporary debugging copies disabled by default.
Failed temporary uploads: delete within 24 hours. Export packages: expire after 24 hours.
User deletion: immediately hide and reject access, cancel jobs; purge active rows, derivatives and storage within 7 days target. Backups expire within 30 days target. External-provider deletion limitations must be documented before S5.
Operational metadata proposed retention 30 days; security audit identifiers 90 days, minimized or pseudonymized subject to legal requirements.
These are proposed product policies, not verified legal compliance.

## Deletion workflow
Requested → access_revoked → jobs_cancelled → primary_purged → assets_and_derived_purged → provider_requests_recorded → completed.
Keep only minimal tombstone sufficient to prevent resurrection. On backup restore, replay deletion and consent-revocation ledger before exposing service.
Deletion status must not claim external-provider purge until confirmed or explicitly report the applicable retention deadline.

## Safety boundaries
No diagnosis, hidden-trauma discovery, spiritual punishment, moral guilt scores or factual certainty about motives. Content concerning abuse preserves power asymmetry and avoids recommending reconciliation as a universal outcome.
Private-mode distress handling is a product policy gate: no routine therapy impersonation; acute-risk inputs route to a reviewed support flow rather than automated life-story analysis. Country-specific resource content must be verified when used.
