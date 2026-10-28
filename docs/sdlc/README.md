# split wise — SDLC Documentation

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start overview -->
split wise calculator

**Documentation version:** v1
<!-- sdlc:auto:end overview -->

## Contents

<!-- sdlc:auto:start contents -->
| Document | State |
|---|---|
| [Requirements](requirements/README.md) | v1 approved |
| [Architecture](architecture/README.md) | 0 entries |
| [Development](development/README.md) | 0 entries |
| [Testing](testing/README.md) | 0 entries |
| [Deployment](deployment/README.md) | 0 entries |
| [Maintenance](maintenance/README.md) | 0 entries |
| [Data model](architecture/data-model.md) | not generated yet |
| [API (OpenAPI)](architecture/api/openapi.yaml) | not generated yet |
| [Decisions (ADRs)](architecture/adr/README.md) | 0 decisions |
| [Sprint plan](development/sprint-plan.md) | not generated yet |
| [Developer guide](development/developer-guide.md) | not generated yet |
| [API reference](development/api-reference.md) | 0 routes |
| [Test report](testing/test-report.md) | not run yet |
| [Tests](testing/test-cases.md) | 0 tests |
| [Deployment guide](deployment/deployment-guide.md) | not deployed yet |
| [Runbook](deployment/runbook.md) | not deployed yet |
| [Release notes](deployment/release-notes.md) | 0 releases |
| [Traceability matrix](traceability-matrix.md) | 22 requirements |
| [Changelog](CHANGELOG.md) | 1 version |
<!-- sdlc:auto:end contents -->

## Open gaps

<!-- sdlc:auto:start open-gaps -->
### Requirements

- Discrepancy: S3 is justified specifically for receipt-image uploads, but the Capabilities-in-scope list and EPIC-003's own assumption explicitly state receipt image upload is NOT part of this lightweight MVP scope (noted only as a 'discovery enhancement'). Needs product-owner clarification on whether S3 is required for this release or is being provisioned ahead of a future capability.
- Password validation rules referenced in AC-003 ('valid password', 'password rules') are not specified in the input — complexity/length requirements are undefined.
- Conflict: this epic's own assumption excludes receipt-image upload from MVP scope, yet the approved services list (S3) is justified specifically by receipt-image uploads — see REQ-SERVICES open_gaps.
- Debt-simplification algorithm/approach is not specified beyond the outcome criteria (minimise transaction count, preserve net balances) — implementation approach left to architecture/design phase.
- Specific password rules to be enforced are not defined in the input (see REQ-EPIC-001 gap).
<!-- sdlc:auto:end open-gaps -->
