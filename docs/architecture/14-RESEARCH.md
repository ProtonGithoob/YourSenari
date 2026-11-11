# Research and technical selection
Research date: 2026-11-11. GitHub connector inspected repository metadata for the projects below. Official documentation was also searched for narrative structure, persistence and row-level security. This was a documentation and metadata review, not a code security audit or benchmark.

## Repository findings
| Project | Verified finding | Proposed role | Limit |
|---|---|---|---|
| [xyflow/xyflow](https://github.com/xyflow/xyflow) | MIT; node-based React/Svelte UI libraries | Authoring editor | Not a scene/narrative/psychological engine |
| [statelyai/xstate](https://github.com/statelyai/xstate) | MIT; state machines and actors | Explicit player lifecycle | Persisted state needs schema/version strategy |
| [inkle/ink](https://github.com/inkle/ink) | MIT; interactive narrative scripting | Study choice/branch/rejoin concepts | Separate DSL/runtime not adopted initially |
| [ncase/loopy](https://github.com/ncase/loopy) | CC0-1.0; systems-thinking tool | Feedback-loop visual inspiration | Symbolic signals are not validated psychology |
| [jacomyal/sigma.js](https://github.com/jacomyal/sigma.js) | MIT; graph visualization | Later dense-context view | Layout does not establish causality |
| [scottfr/simulation](https://github.com/scottfr/simulation) | GitHub metadata reports NOASSERTION; README inspected earlier states AGPL | Study system-dynamics ideas | Not adopted; verify full license before any incorporation |

Repositories were not archived in the inspected metadata. Star counts and development-branch names are deliberately not treated as quality or compatibility guarantees.
A mistaken lookup under inklestudios/ink returned 404; corrected canonical repository inkle/ink was then verified. No conclusions rely on the failed lookup.

## Official sources
- [React Flow documentation](https://reactflow.dev/learn): authoring primitives and interaction model; validate accessibility/performance for our custom nodes in S1/S2.
- [XState actors](https://stately.ai/docs/actors): explicit actor logic.
- [XState persistence](https://stately.ai/docs/persistence): persistence APIs; domain snapshots remain versioned independently.
- [Writing with Ink](https://github.com/inkle/ink/blob/master/Documentation/WritingWithInk.md): choices can branch, join and loop.
- [PostgreSQL row security](https://www.postgresql.org/docs/17/ddl-rowsecurity.html): per-row policies. Application and worker role design still matters; RLS is not automatic tenant isolation.
- [PostgreSQL documentation](https://www.postgresql.org/docs/): select a supported release and use matching documentation at implementation.
- [LOOPY](https://ncase.me/loopy/): visual systems explanation.
- [Kumu](https://kumu.io/) and [Kumu architecture](https://docs.kumu.io/overview/kumus-architecture): reference for layered relationship maps, not a source-code dependency.
- [Insight Maker open-source page](https://insightmaker.com/docs/open): differentiates free hosted modeling from reusable simulation package.

The earlier conversation also explored [Bodhidharma](https://github.com/srieg/bodhidharma), [vis-timeline](https://github.com/visjs/vis-timeline) and [Graphology](https://github.com/graphology/graphology). These remain optional reference candidates, not incorporated dependencies. Their full source, content provenance and current release licenses must be reviewed if selected.

## Interpretation of research
No inspected library supplies a validated engine that determines why a person behaves as they do. Our contribution is a domain model, editorial workflow and visual presentation that keep hypotheses visible. Narrative quality is evaluated separately from evidence quality.

## Commercial reuse gate
Before adding a dependency: pin release and integrity; read that release's license and bundled notices; inspect transitive dependencies; inventory copied code/assets; record attribution; evaluate maintenance/security; benchmark actual intended workload.
MIT/CC0 metadata are preliminary signals, not complete rights clearance. AGPL must not be relabeled "noncommercial": commercial use can be allowed with copyleft obligations, which need review for the intended integration.
Do not copy philosophical corpora, copyrighted biographies, translations, artwork or proprietary UI code merely because a reference application is public.

## Evidence limits
No application code existed in YourSenari at inspection. No repository was cloned or run for this research. No load test, clinical validation, security audit, paid procurement or vendor contract review was performed. All capacity, budget, and evaluation thresholds elsewhere are proposed.
