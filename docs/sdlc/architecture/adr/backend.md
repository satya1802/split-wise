<!-- sdlc:auto:start adr -->
# ADR-0002: Use FastAPI 0.115 for Backend

Status: Accepted  
Date: 2026-10-28

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v2.

## Considered Options

- FastAPI 0.115
- Django REST Framework
- Flask

## Decision Outcome

Chosen option: FastAPI 0.115, because Hosts the calculation-heavy logic — split validation, per-member and cross-group balances, debt simplification — behind a clean typed API the React screens call.

## Consequences

Being async-first and un-opinionated means auth and structure are assembled from libraries rather than batteries-included, which suits this focused service.
<!-- sdlc:auto:end adr -->