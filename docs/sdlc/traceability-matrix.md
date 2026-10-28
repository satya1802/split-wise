# Traceability Matrix

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start legend -->
Built from recorded links, not written by a model: requirement key → plan item (`source_stable_key`) → development ticket (`stable_key`) → the ticket's test steps → the last live deployment that started after the work finished. **AC tests** counts the story's acceptance criteria that have a test case, and those whose test cases all passed in the latest finished E2E run.
<!-- sdlc:auto:end legend -->

<!-- sdlc:auto:start matrix -->
| Requirement | Epic | Title | Plan items | Sprint | Design | Code | Commits | Ticket | Tests | AC tests | Deployed |
|---|---|---|---|---|---|---|---|---|---|---|---|
| US-001 | EPIC-001 | Register a new account | US-001, US-001-T1, US-001-T2, US-001-T3 | 1 | POST /auth/register, api, db, users, web | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-002 | EPIC-001 | Log in and out | US-002 | 1 | POST /auth/login, POST /auth/logout, api, users, web | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-003 | EPIC-002 | Create a persistent group | US-003 | 1 | GET /groups, POST /groups, api, db, group_members, groups, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-004 | EPIC-002 | Add a registered user to a group by invitation | US-004 | 2 | POST /groups/{group_id}/members/invite, api, db, email, group_invitations, group_members, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-005 | EPIC-002 | Add a placeholder member by name | US-005 | 2 | POST /groups/{group_id}/members/placeholder, api, group_members, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-006 | EPIC-002 | View group members | US-006 | 1 | GET /groups/{group_id}/members, api, group_members, web | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-007 | EPIC-003 | Log an expense with core details | US-007, US-007-T1, US-007-T2, US-007-T3 | 2 | GET /groups/{group_id}/expenses, POST /groups/{group_id}/expenses, api, db, expenses, web | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-008 | EPIC-003 | Add an optional note to an expense | US-008 | 2 | PATCH /groups/{group_id}/expenses/{expense_id}, api, expenses, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-009 | EPIC-003 | Split an expense equally | US-009 | 2 | POST /groups/{group_id}/expenses, api, db, expense_splits | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-010 | EPIC-003 | Split an expense by exact amounts, percentage or shares | US-010 | 3 | POST /groups/{group_id}/expenses, api, expense_splits, web | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-011 | EPIC-003 | Choose which members are included in a split | US-011 | 3 | POST /groups/{group_id}/expenses, api, expense_splits, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-012 | EPIC-003 | Comment on an expense | US-012 | 3 | GET /groups/{group_id}/expenses/{expense_id}/comments, POST /groups/{group_id}/expenses/{expense_id}/comments, api, comments, db, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-013 | EPIC-004 | View per-group expense and activity history | US-013 | 4 | GET /groups/{group_id}/expenses, api, expenses, settlements, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-014 | EPIC-004 | View running per-member balances within a group | US-014, US-014-T1, US-014-T2, US-014-T3 | 4 | GET /groups/{group_id}/balances, api, db, expense_splits, expenses, settlements, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-015 | EPIC-004 | View overall balances across all my groups | US-015 | 5 | GET /me/dashboard, api, expenses, groups, settlements, web | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-016 | EPIC-004 | Simplify debts to minimise settle-up transactions | US-016, US-016-T1, US-016-T2, US-016-T3 | 5 | GET /groups/{group_id}/balances, api, expense_splits, settlements, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-017 | EPIC-005 | Record a settlement manually | US-017 | 3 | POST /groups/{group_id}/settlements, api, db, settlements, web | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-018 | EPIC-006 | Notify a user when added to a group | US-018 | 3 | api, email, group_invitations, users | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-019 | EPIC-006 | Notify members of a new relevant expense | US-019 | 4 | api, email, expense_splits, expenses, users | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-020 | EPIC-006 | Notify members of a recorded settlement | US-020 | 4 | api, email, settlements, users | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-021 | EPIC-007 | Use the app on any device via a responsive web interface | US-021 | 5 | web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-022 | EPIC-007 | Use the app free of charge in a single currency | US-022 | 4 | api, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
<!-- sdlc:auto:end matrix -->
