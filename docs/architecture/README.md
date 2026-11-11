# Architecture index
Date: 2026-11-11. Status: proposed baseline.

## Reading order
1. [AZ overview](00-PROJECT-AZ.md), [product](01-PRODUCT.md).
2. [System](02-SYSTEM.md), [visual](03-VISUAL-EXPERIENCE.md), [runtime](06-NARRATIVE-RUNTIME.md).
3. [Data](04-DOMAIN-DATA.md), [AI](05-AI-ANALYSIS.md), [API](07-API-CONTRACTS.md).
4. [Content](08-CONTENT-MEDIA.md), [security](09-SECURITY-PRIVACY.md), [operations](10-OPERATIONS.md).
5. [Quality](11-QUALITY.md), [roadmap](12-ROADMAP.md), [decisions](13-DECISIONS.md), [research](14-RESEARCH.md).
6. [Example bundle](examples/kamran.v1.json).

## Repository baseline
GitHub metadata and contents were inspected through the connected ProtonGithoob account. Repository was public, default branch main, size 0; contents API reported "This repository is empty." There was no existing code, AGENTS.md, build pipeline or dependency manifest. This is a greenfield design, not a code audit.

## Requirements and proposed decisions
User requirements: visual more than textual; choose a person; explore their life and behavior; emotional explanations; multiple perspectives; feedback loops; alternative paths; individual-to-society scale; optional spiritual meaning; architecture in this repository.

Architecture author recommendations: modular monolith, TypeScript browser/server, PostgreSQL relational graph, separate worker, curated fiction first, 2D scenes before 3D, server-side model adapters. These are proposed choices, not claims of user-approved technology.

| ID | Requirement | Documents | Delivery |
|---|---|---|---|
| R01 | Select person and life | 01, 03, 08 | S1 |
| R02 | Layered behavior explanations | 03, 04, 05 | S1/S3 |
| R03 | Perspective switch | 03, 06 | S1 |
| R04 | Interaction feedback loops | 04, 06 | S1 |
| R05 | Alternative responses | 06, 07 | S1/S3 |
| R06 | Individual to social scale | 03, 04 | S4 |
| R07 | Revise from new evidence | 04, 05, 08 | S3/S4 |
| R08 | Optional meaning lens | 01, 05, 08 | S4 |
| R09 | Visual accessibility | 03, 11 | All |
| R10 | Evidence identity | 04, 05, 11 | All |
| R11 | Private stories | 09, 10 | S5 |
| R12 | Commercial operation | 08, 09, 10, 14 | S5 |

MUST means architectural invariant. Performance and cost budgets are proposed targets, not measured outcomes. Future file paths are planned. Research describes source inspection, not integration benchmarks. A general psychological theory cannot establish an individual's motive.

[Documentation review record](15-DOCUMENTATION-REVIEW.md) records issues found and corrections.
