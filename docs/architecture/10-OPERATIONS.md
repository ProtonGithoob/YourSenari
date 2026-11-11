# Deployment and operations
## Environments
Local: web, worker, PostgreSQL, object-store emulator; no production data.
Staging: isolated credentials, synthetic stories, same migration/policy configuration.
Production: stateless web, isolated workers, managed PostgreSQL with backups, private object store plus public CDN for reviewed assets.
Vendor/region remains undecided until provider, privacy and cost evaluation. Do not deploy personal reflection until its gates pass.

## Deployment flow
Validate contracts/content → meaningful automated tests → dependency/license scan → build immutable image → staging migration → smoke journey and isolation checks → production expand migration → deploy compatible web/worker → verify health → activate features.
Use additive expand/contract migrations. Old web and workers must coexist during rollout. Destructive migrations require backup/restore proof and explicit release planning. Roll back application image and publication pointer; do not blindly reverse destructive database migrations.

## Queue semantics
PostgreSQL jobs store workspace_id, payload_ref, idempotency_key, status, attempt, run_after, locked_by, lease_until, cancellation_version, input_hash.
Claim with SELECT FOR UPDATE SKIP LOCKED inside a short transaction; do not hold a transaction during external calls.
Heartbeat lease; expired leases may retry. Completion uses compare-and-set ownership/cancellation checks. At-least-once delivery means side effects need idempotent keys. Provider may bill twice after an ambiguous timeout; record attempt IDs and reconcile rather than promising exactly-once billing.
Outbox row created in the same transaction as state change. Dispatcher retries delivery; consumer stores processed event IDs. Dead-letter after bounded attempts and alert.
Separate lightweight analysis queue from expensive media jobs; one tenant cannot occupy every worker.

## Reliability targets (not measured)
Public catalog/bundle availability target 99.5% monthly for pilot. API p95 <=500 ms excluding generation and media transfer, measured at 50 concurrent readers and a representative bundle. Initial meaningful scene <=3 seconds on the documented mobile test profile; follow-up warmed transition <=200 ms. Public initial transfer <=2 MB excluding optional audio.
These are acceptance budgets to validate, not present performance claims.
Proposed recovery: RPO <=24 hours and RTO <=4 hours for pilot; tighten before sensitive-data scale. Use daily backups plus PITR where available and quarterly restore drills.

## Failure behavior
| Failure | User behavior |
|---|---|
| AI provider unavailable | Published stories continue; draft job shows retryable failure |
| Worker restart | Leased job resumes safely; no duplicate publication |
| Missing media | Accessible still/text fallback |
| DB unavailable | Error/retry; no fabricated progress-save success |
| Publication revoked | Stop online load; safe explanatory message |
| Source corrected | Flag affected claims and queue review |
| Model output invalid | Nonpublishable draft or rejected job |
| Cost limit reached | Explain quota; preserve existing drafts and playback |

## Observability
Metrics: scene-ready latency, transition failures, bundle validation failures, asset fallback rate, queue age, provider latency/usage, review rejection, citation violations, cross-tenant access failures, deletion lag.
Traces use request/job/revision IDs. Exclude names, case text, source excerpts and full prompts.
Alerts: repeated auth leakage test failure blocks release; queue age >10 minutes for pilot triggers investigation; any private cache exposure disables affected route and initiates incident handling.
Health checks distinguish web readiness, DB reachability and optional provider availability; provider failure must not mark all public playback unavailable.

## Cost and capacity
Compute per-analysis variable cost from input tokens × input rate + output tokens × output rate + retries + retrieval + media generation. Monthly cost adds storage, egress, database, workers, observability and editorial labor. Provider rates must be fetched at procurement; no unverified fixed quote here.
Reserve budget before job dispatch; release unused portion after completion; enforce daily workspace and system caps. Pre-render scene media, cache approved public bundles, deduplicate equivalent jobs within the same tenant, and avoid generating media on every click.
Pilot load profile: 50 concurrent public readers, 5 authors, 2 analysis workers, 1 media worker. This is a starting experiment, not supported capacity.

## Incident/recovery checklist
Contain access or publication; preserve minimal audit evidence; revoke credentials if relevant; identify affected revisions/users; correct and re-review; restore if necessary; replay deletion ledger; verify tenant isolation; communicate accurately. Review root cause before reenabling a disabled feature.
