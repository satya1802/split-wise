# split wise — SDLC Documentation

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start overview -->
split wise calculator

**Documentation version:** v3
<!-- sdlc:auto:end overview -->

## Contents

<!-- sdlc:auto:start contents -->
| Document | State |
|---|---|
| [Requirements](requirements/README.md) | v1 approved |
| [Architecture](architecture/README.md) | 9 entries |
| [Development](development/README.md) | 13 entries |
| [Testing](testing/README.md) | 0 entries |
| [Deployment](deployment/README.md) | 0 entries |
| [Maintenance](maintenance/README.md) | 0 entries |
| [Data model](architecture/data-model.md) | generated |
| [API (OpenAPI)](architecture/api/openapi.yaml) | generated |
| [Decisions (ADRs)](architecture/adr/README.md) | 4 decisions |
| [Sprint plan](development/sprint-plan.md) | 5 sprints |
| [Developer guide](development/developer-guide.md) | generated |
| [API reference](development/api-reference.md) | 1 route |
| [Test report](testing/test-report.md) | not run yet |
| [Tests](testing/test-cases.md) | 0 tests |
| [Deployment guide](deployment/deployment-guide.md) | not deployed yet |
| [Runbook](deployment/runbook.md) | not deployed yet |
| [Release notes](deployment/release-notes.md) | 0 releases |
| [Traceability matrix](traceability-matrix.md) | 22 requirements |
| [Changelog](CHANGELOG.md) | 3 versions |
<!-- sdlc:auto:end contents -->

## Open gaps

<!-- sdlc:auto:start open-gaps -->
### Requirements

- Discrepancy: S3 is justified specifically for receipt-image uploads, but the Capabilities-in-scope list and EPIC-003's own assumption explicitly state receipt image upload is NOT part of this lightweight MVP scope (noted only as a 'discovery enhancement'). Needs product-owner clarification on whether S3 is required for this release or is being provisioned ahead of a future capability.
- Password validation rules referenced in AC-003 ('valid password', 'password rules') are not specified in the input — complexity/length requirements are undefined.
- Conflict: this epic's own assumption excludes receipt-image upload from MVP scope, yet the approved services list (S3) is justified specifically by receipt-image uploads — see REQ-SERVICES open_gaps.
- Debt-simplification algorithm/approach is not specified beyond the outcome criteria (minimise transaction count, preserve net balances) — implementation approach left to architecture/design phase.
- Specific password rules to be enforced are not defined in the input (see REQ-EPIC-001 gap).

### Architecture

- No requirements-phase input was provided alongside this architecture; cannot independently confirm which US-xxx ids this design satisfies.
- Architecture input does not cite which US-xxx requirement(s) this path satisfies; cannot link related_ids without fabricating.
- Single-AZ RDS is explicitly dev-grade; no separate production HA deployment node is described in this input — unclear if this is final for production or a placeholder.
- This entry references NFR-001 and NFR-006 as the rationale for the React and AWS choices, but neither NFR-001 nor NFR-006 appears in the known requirement key list (US-001..US-022) — flagging this ID mismatch for reconciliation with the requirements phase.

### Development

- No execution/completion status (done, in-progress, blocked), code artifacts, commits, or PRs were provided for any item -- this entry documents planned scope only.
- No test results or QA sign-off recorded for this phase's input.
- Plan input does not state which specific backlog items (e.g. US-001, US-002, US-003, US-006) are assigned to this sprint; only the sprint's goal text is given. Mapping items to this sprint would require inference not present in the source and is therefore left unassigned.
- Plan input does not state which specific backlog items are assigned to this sprint; only the sprint goal text is given.
- No completion status, code, or test evidence provided for US-001, US-002, or their sub-tasks.
- No completion status, code, or test evidence provided for US-003 through US-006.
- No completion status, code, or test evidence provided for US-007 through US-012 or their sub-tasks.
- No completion status, code, or test evidence provided for US-013 through US-016 or their sub-tasks.
- No completion status, code, or test evidence provided for US-017.
- No completion status, code, or test evidence provided for US-018 through US-020.
- No completion status, code, or test evidence provided for US-021 or US-022.
- US-022 is assigned to qa-agent with no corresponding implementation task listed, which may indicate this item is verification-only rather than a build item -- plan input does not clarify.
<!-- sdlc:auto:end open-gaps -->
