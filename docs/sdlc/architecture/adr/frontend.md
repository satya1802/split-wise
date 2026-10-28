<!-- sdlc:auto:start adr -->
# ADR-0001: Use React 19 for Frontend

Status: Accepted  
Date: 2026-10-28

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v2.

## Considered Options

- React 19
- Vue
- Svelte

## Decision Outcome

Chosen option: React 19, because Drives the interactive split editor and live-recomputing balances across mobile and desktop browsers, delivering the responsive web app in NFR-001 without a native build.

## Consequences

A SPA needs client-side routing and state handling, but React's ecosystem and developer pool keep build and maintenance cheap for a free product.
<!-- sdlc:auto:end adr -->