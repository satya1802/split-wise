# Development

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
### DEV-PLAN · approved · source: plan:overview

Overall delivery plan (version 1) is approved. It organizes 7 epics / 22 user stories / 9 sub-tasks across 5 sprints of 20-point capacity each.

Plan status: approved, version 1. Structure: EPIC-001 User Accounts & Authentication; EPIC-002 Groups & Members; EPIC-003 Expense Logging & Splitting; EPIC-004 Balances, History & Debt Simplification; EPIC-005 Settlements; EPIC-006 Email Notifications; EPIC-007 Platform & Operating Constraints. Total estimated story points across the 22 stories = 95, against 5 sprints x 20 capacity = 100 planned capacity. Roles assigned across items: backend-agent, frontend-agent, integration-agent, qa-agent.

**Related:** US-001, US-002, US-003, US-004, US-005, US-006, US-007, US-008, US-009, US-010, US-011, US-012, US-013, US-014, US-015, US-016, US-017, US-018, US-019, US-020, US-021, US-022

- ⚠ No execution/completion status (done, in-progress, blocked), code artifacts, commits, or PRs were provided for any item -- this entry documents planned scope only.
- ⚠ No test results or QA sign-off recorded for this phase's input.

### DEV-SPRINT-1 · approved · source: plan:Sprint 1

Sprint 1 goal: enable account registration, login/logout, persistent group creation, and viewing a group's member list.

Capacity: 20 points. Goal as stated in the plan: 'Users can register, log in/out, create persistent groups, and view a group's member list.' The plan does not explicitly assign individual backlog items to this sprint.

- ⚠ Plan input does not state which specific backlog items (e.g. US-001, US-002, US-003, US-006) are assigned to this sprint; only the sprint's goal text is given. Mapping items to this sprint would require inference not present in the source and is therefore left unassigned.

### DEV-SPRINT-2 · approved · source: plan:Sprint 2

Sprint 2 goal: populate groups with registered and placeholder members and support logging expenses with equal splits.

Capacity: 20 points. Goal as stated in the plan: 'Groups can be populated with registered and placeholder members, and members can log expenses with equal splits.' No explicit item-to-sprint assignment given.

- ⚠ Plan input does not state which specific backlog items are assigned to this sprint; only the sprint goal text is given.

### DEV-SPRINT-3 · approved · source: plan:Sprint 3

Sprint 3 goal: support flexible expense split methods and comments, recordable settlements, and group-invite emails.

Capacity: 20 points. Goal as stated in the plan: 'Expenses support flexible split methods and comments, settlements can be recorded, and group-invite emails go out.' No explicit item-to-sprint assignment given.

- ⚠ Plan input does not state which specific backlog items are assigned to this sprint; only the sprint goal text is given.

### DEV-SPRINT-4 · approved · source: plan:Sprint 4

Sprint 4 goal: show full group activity history and computed balances, send expense/settlement emails, and verify the free/single-currency constraint.

Capacity: 20 points. Goal as stated in the plan: 'Groups show full activity history and computed balances, expense/settlement emails are sent, and the free/single-currency constraint is verified.' No explicit item-to-sprint assignment given.

- ⚠ Plan input does not state which specific backlog items are assigned to this sprint; only the sprint goal text is given.

### DEV-SPRINT-5 · approved · source: plan:Sprint 5

Sprint 5 goal: deliver a cross-group balances dashboard, debt-simplified settle-up suggestions, and a polished responsive layout.

Capacity: 20 points. Goal as stated in the plan: 'Users get an overall cross-group balances dashboard, debt-simplified settle-up suggestions, and a polished responsive layout.' No explicit item-to-sprint assignment given.

- ⚠ Plan input does not state which specific backlog items are assigned to this sprint; only the sprint goal text is given.

### DEV-EPIC-001 · approved · source: plan:EPIC-001

User Accounts & Authentication epic covers registration and login/logout.

US-001 Register a new account (8 pts, backend-agent) -- sub-tasks: US-001-T1 add users table migration (backend-agent); US-001-T2 implement registration endpoint with validation and password hashing (backend-agent); US-001-T3 build registration page and wire to API (frontend-agent). US-002 Log in and out (5 pts, backend-agent) -- no sub-tasks listed.

**Related:** US-001, US-002

- ⚠ No completion status, code, or test evidence provided for US-001, US-002, or their sub-tasks.

### DEV-EPIC-002 · approved · source: plan:EPIC-002

Groups & Members epic covers creating groups and managing membership (registered users, placeholders, and viewing the member list).

US-003 Create a persistent group (5 pts, backend-agent). US-004 Add a registered user to a group by invitation (5 pts, integration-agent). US-005 Add a placeholder member by name (3 pts, backend-agent). US-006 View group members (2 pts, frontend-agent). No sub-tasks listed for any of these stories.

**Related:** US-003, US-004, US-005, US-006

- ⚠ No completion status, code, or test evidence provided for US-003 through US-006.

### DEV-EPIC-003 · approved · source: plan:EPIC-003

Expense Logging & Splitting epic covers creating expenses, notes, equal/flexible splits, member selection, and comments.

US-007 Log an expense with core details (8 pts, backend-agent) -- sub-tasks: US-007-T1 add expenses table migration (backend-agent); US-007-T2 implement expense create/list endpoints with validation (backend-agent); US-007-T3 build expense creation form (frontend-agent). US-008 Add an optional note to an expense (1 pt, backend-agent). US-009 Split an expense equally (3 pts, backend-agent). US-010 Split an expense by exact amounts, percentage or shares (5 pts, backend-agent). US-011 Choose which members are included in a split (3 pts, frontend-agent). US-012 Comment on an expense (3 pts, backend-agent).

**Related:** US-007, US-008, US-009, US-010, US-011, US-012

- ⚠ No completion status, code, or test evidence provided for US-007 through US-012 or their sub-tasks.

### DEV-EPIC-004 · approved · source: plan:EPIC-004

Balances, History & Debt Simplification epic covers activity history, per-group and overall balances, and debt-simplified settle-up suggestions.

US-013 View per-group expense and activity history (3 pts, frontend-agent). US-014 View running per-member balances within a group (8 pts, backend-agent) -- sub-tasks: US-014-T1 implement per-group balance calculation engine (backend-agent); US-014-T2 implement GET /groups/{group_id}/balances endpoint (backend-agent); US-014-T3 build group balances view (frontend-agent). US-015 View overall balances across all my groups (5 pts, backend-agent). US-016 Simplify debts to minimise settle-up transactions (8 pts, backend-agent) -- sub-tasks: US-016-T1 implement debt-simplification algorithm (backend-agent); US-016-T2 integrate simplified settle-up suggestions into balances endpoint (backend-agent); US-016-T3 build settle-up suggestions UI (frontend-agent).

**Related:** US-013, US-014, US-015, US-016

- ⚠ No completion status, code, or test evidence provided for US-013 through US-016 or their sub-tasks.

### DEV-EPIC-005 · approved · source: plan:EPIC-005

Settlements epic covers manually recording a settlement between members.

US-017 Record a settlement manually (5 pts, backend-agent). No sub-tasks listed.

**Related:** US-017

- ⚠ No completion status, code, or test evidence provided for US-017.

### DEV-EPIC-006 · approved · source: plan:EPIC-006

Email Notifications epic covers notifying users of group invitations, new relevant expenses, and recorded settlements.

US-018 Notify a user when added to a group (3 pts, integration-agent). US-019 Notify members of a new relevant expense (3 pts, integration-agent). US-020 Notify members of a recorded settlement (2 pts, integration-agent). No sub-tasks listed.

**Related:** US-018, US-019, US-020

- ⚠ No completion status, code, or test evidence provided for US-018 through US-020.

### DEV-EPIC-007 · approved · source: plan:EPIC-007

Platform & Operating Constraints epic covers responsive device support and the free/single-currency operating constraint.

US-021 Use the app on any device via a responsive web interface (5 pts, frontend-agent). US-022 Use the app free of charge in a single currency (2 pts, qa-agent). No sub-tasks listed.

**Related:** US-021, US-022

- ⚠ No completion status, code, or test evidence provided for US-021 or US-022.
- ⚠ US-022 is assigned to qa-agent with no corresponding implementation task listed, which may indicate this item is verification-only rather than a build item -- plan input does not clarify.
<!-- sdlc:auto:end narrative -->
