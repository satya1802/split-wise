# Sprint Plan

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start sprints -->
## Sprint 1: Sprint 1

Users can register, log in/out, create persistent groups, and view a group's member list.

Capacity: 20 points · Committed: 20

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-001 | Story | Register a new account | 8 | backend-agent | — |
| ↳ US-001-T1 | Task | Add users table migration | — | backend-agent | — |
| ↳ US-001-T2 | Task | Implement registration endpoint with validation and password hashing | — | backend-agent | — |
| ↳ US-001-T3 | Task | Build registration page and wire to API | — | frontend-agent | — |
| US-002 | Story | Log in and out | 5 | backend-agent | US-001 |
| US-003 | Story | Create a persistent group | 5 | backend-agent | US-002 |
| US-006 | Story | View group members | 2 | frontend-agent | US-003 |

## Sprint 2: Sprint 2

Groups can be populated with registered and placeholder members, and members can log expenses with equal splits.

Capacity: 20 points · Committed: 20

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-004 | Story | Add a registered user to a group by invitation | 5 | integration-agent | US-003 |
| US-005 | Story | Add a placeholder member by name | 3 | backend-agent | US-003 |
| US-007 | Story | Log an expense with core details | 8 | backend-agent | US-003 |
| ↳ US-007-T1 | Task | Add expenses table migration | — | backend-agent | — |
| ↳ US-007-T2 | Task | Implement expense create/list endpoints with validation | — | backend-agent | — |
| ↳ US-007-T3 | Task | Build expense creation form | — | frontend-agent | — |
| US-008 | Story | Add an optional note to an expense | 1 | backend-agent | US-007 |
| US-009 | Story | Split an expense equally | 3 | backend-agent | US-007 |

## Sprint 3: Sprint 3

Expenses support flexible split methods and comments, settlements can be recorded, and group-invite emails go out.

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-010 | Story | Split an expense by exact amounts, percentage or shares | 5 | backend-agent | US-007, US-009 |
| US-011 | Story | Choose which members are included in a split | 3 | frontend-agent | US-007 |
| US-012 | Story | Comment on an expense | 3 | backend-agent | US-007 |
| US-017 | Story | Record a settlement manually | 5 | backend-agent | US-003 |
| US-018 | Story | Notify a user when added to a group | 3 | integration-agent | US-004 |

## Sprint 4: Sprint 4

Groups show full activity history and computed balances, expense/settlement emails are sent, and the free/single-currency constraint is verified.

Capacity: 20 points · Committed: 18

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-013 | Story | View per-group expense and activity history | 3 | frontend-agent | US-007, US-017 |
| US-014 | Story | View running per-member balances within a group | 8 | backend-agent | US-009, US-010, US-017 |
| ↳ US-014-T1 | Task | Implement per-group balance calculation engine | — | backend-agent | — |
| ↳ US-014-T2 | Task | Implement GET /groups/{group_id}/balances endpoint | — | backend-agent | — |
| ↳ US-014-T3 | Task | Build group balances view | — | frontend-agent | — |
| US-019 | Story | Notify members of a new relevant expense | 3 | integration-agent | US-007, US-009 |
| US-020 | Story | Notify members of a recorded settlement | 2 | integration-agent | US-017 |
| US-022 | Story | Use the app free of charge in a single currency | 2 | qa-agent | US-003 |

## Sprint 5: Sprint 5

Users get an overall cross-group balances dashboard, debt-simplified settle-up suggestions, and a polished responsive layout.

Capacity: 20 points · Committed: 18

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-015 | Story | View overall balances across all my groups | 5 | backend-agent | US-014 |
| US-016 | Story | Simplify debts to minimise settle-up transactions | 8 | backend-agent | US-014 |
| ↳ US-016-T1 | Task | Implement debt-simplification algorithm | — | backend-agent | — |
| ↳ US-016-T2 | Task | Integrate simplified settle-up suggestions into balances endpoint | — | backend-agent | — |
| ↳ US-016-T3 | Task | Build settle-up suggestions UI | — | frontend-agent | — |
| US-021 | Story | Use the app on any device via a responsive web interface | 5 | frontend-agent | US-007, US-014, US-015 |

## Unscheduled

_Nothing unscheduled._
<!-- sdlc:auto:end sprints -->
