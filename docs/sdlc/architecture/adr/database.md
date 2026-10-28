<!-- sdlc:auto:start adr -->
# ADR-0003: Use PostgreSQL 16 for Database

Status: Accepted  
Date: 2026-10-28

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v2.

## Considered Options

- PostgreSQL 16
- MySQL
- SQLite

## Decision Outcome

Chosen option: PostgreSQL 16, because Keeps all relational, money-exact data (users, groups, members, expenses, splits, settlements, comments) consistent so balances summed from rows never double-count; numeric(12,2) holds currency precisely.

## Consequences

Needs a managed instance (RDS) to run, but transactional integrity is essential to correct balances.
<!-- sdlc:auto:end adr -->