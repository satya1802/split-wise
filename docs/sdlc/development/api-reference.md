# API Reference

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start endpoints -->
| Method | Path | Handler | Source | Summary |
|---|---|---|---|---|
| GET | /health | health | `backend/app/main.py:42` | Liveness probe, and the only route here that is not a stub. |
<!-- sdlc:auto:end endpoints -->

<!-- sdlc:auto:start drift -->
**Designed but missing:**

- GET /groups
- GET /groups/{group_id}/balances
- GET /groups/{group_id}/expenses
- GET /groups/{group_id}/expenses/{expense_id}/comments
- GET /groups/{group_id}/members
- GET /me/dashboard
- PATCH /groups/{group_id}/expenses/{expense_id}
- POST /auth/login
- POST /auth/logout
- POST /auth/register
- POST /groups
- POST /groups/{group_id}/expenses
- POST /groups/{group_id}/expenses/{expense_id}/comments
- POST /groups/{group_id}/members/invite
- POST /groups/{group_id}/members/placeholder
- POST /groups/{group_id}/settlements
<!-- sdlc:auto:end drift -->

<!-- sdlc:auto:start source -->
Generated from commit `e6446b9`
<!-- sdlc:auto:end source -->
