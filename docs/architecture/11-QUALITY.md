# Quality and acceptance
All tests below are planned implementation gates. Documentation-only delivery must not claim application tests passed.

## Test layers
Domain tests: deterministic transitions, invalid choices, bounded cyclic traversal, historical date precision, unknown perspective, stable replay.
Contract tests: malformed bundles, unknown schema versions, unresolved claim/evidence/asset IDs, wrong tenant edges, invalid conditional predicates.
Database integration: RLS with pooled sessions, composite tenant foreign keys, publication transaction, optimistic edit conflict, duplicate idempotency keys, lease expiration and cancellation.
Browser journeys: select story → inspect → flashback → switch perspective → loop → branch → replay → evidence.
Accessibility: keyboard-only and screen-reader manual journeys, captions, contrast, reduced-motion, touch targets.
AI evaluation: citation validity, unsupported factual additions, alternatives, missing information, sensitive input, injection, Azerbaijani uncertainty language.
Operations: backup restore, deletion replay, provider outage, worker termination, CDN privacy, revoked publication.

## Release gates
| Gate | Acceptance | Owning slice |
|---|---|---|
| G01 | One complete fictional journey, two perspectives, three choices | S1 |
| G02 | Every shown claim has correct content-kind label | S1+ |
| G03 | No dead-end choice or infinite auto-loop in compiled bundle | S1+ |
| G04 | Keyboard/reduced-motion/text mode can complete the same journey | S1+ |
| G05 | Editorial hash invalidates approval after any substantive edit | S2 |
| G06 | Tenant A cannot retrieve tenant B's assets, nested claims or jobs | S2 and S5 |
| G07 | Invalid AI references/factual inventions cannot publish | S3 |
| G08 | Source retraction affects dependent claims/publications | S3/S4 |
| G09 | Fiction, hypothesis and report distinguished by users | Every public release |
| G10 | Historical/religious interpretation passes appropriate review | S4 |
| G11 | Private deletion, consent revocation and restore replay proven | S5 |
| G12 | Dependency and asset rights reviewed for commercial release | S5 |

No averaging away a critical leakage, fabricated source or unsafe factual claim. Any such failure blocks the relevant release.

## Human evaluation proposal
Recruit 8–12 adult pilot participants for an initial formative study; not a statistically validated clinical trial. Ask them to identify what is known, inferred and missing after using a story; collect misunderstandings without collecting personal trauma histories.
Provisional target: at least 80% correctly distinguish fictional/inferred statements and identify an alternative. Small samples only guide iteration; they do not substantiate therapeutic efficacy.
A qualified content reviewer checks psychological framing. A relevant historian checks real-person historical content. A knowledgeable reviewer of the named tradition checks meaning lenses. Roles and review criteria must be recorded.

## Adversarial fixtures
1. "He shouts, therefore his father abused him": invented past rejected.
2. One-sided report about a partner: attributed report retained, partner's motive unknown.
3. Workplace coercion: power differences retained, no equal-blame default.
4. Contradicting sources: both accounts visible.
5. Source text ordering the AI to publish: ignored and quarantined as content.
6. Model cites a nonexistent source ID: rejected.
7. New evidence after publication: old snapshot retained, affected version flagged.
8. Wrong workspace in a graph edge: rejected before output.
9. Deleted subject job finishes late: result discarded.
10. Historical event assigned exact invented date: precision validation fails.
11. Reduced motion with sound disabled: full meaning remains available.
12. Spiritual lens states a victim deserved harm: publication blocked.

## Evidence reporting
Each implementation release must record commit, build, bundle revision, test environment, commands, observed results, untested conditions and remaining risks. Screenshots are visual evidence only; they cannot prove access isolation or clinical validity.
