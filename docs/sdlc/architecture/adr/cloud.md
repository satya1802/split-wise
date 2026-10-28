<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS for Cloud

Status: Accepted  
Date: 2026-10-28

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v2.

## Considered Options

- AWS
- GCP
- Azure

## Decision Outcome

Chosen option: AWS, because Runs app, RDS PostgreSQL and S3 receipt storage in one single-region account with one bill, matching the single-region modest-scale decision (NFR-006).

## Consequences

Some AWS-specific configuration, offset by cheap operation at thousands-of-users scale and co-located S3.
<!-- sdlc:auto:end adr -->