# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-TECHSTACK · approved · source: requirements:stack

Product owner approved an exact technology stack: FastAPI backend, AWS cloud, PostgreSQL 16 database, React 19 frontend.

Decided stack, to be designed against exactly (no substitutions):
- Backend: FastAPI 0.115 — chosen for calculation-heavy balance/debt-simplification logic and to serve a clean API to React; fast to ship for a free product with no large team.
- Cloud: AWS — single default region at modest consumer scale; also provides S3 for receipt-image storage in the same account/bill/region.
- Database: PostgreSQL 16 — relational consistency needed for users, groups, members (incl. placeholders), expenses, splits, settlements, comments; balances are derived by summing rows so exactness matters.
- Frontend: React 19 — responsive, state-heavy UI (live balance recompute, multi-way splits) across phone and desktop; largest developer pool for cheapest build/maintenance path.

### REQ-SERVICES · approved · source: requirements:services

Two approved SaaS runtime services: Amazon S3 for receipt images and SendGrid for transactional email notifications.

Runtime needs approved by product owner:
- File storage: Amazon S3 (saas) — env vars AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_REGION, S3_BUCKET. Rationale given: receipt images attached to expenses need durable, cheap storage outside the database, served directly by S3.
- Email: SendGrid (saas) — env var SENDGRID_API_KEY. Rationale given: core notifications (group invitations, new expense involving you, recorded settlements) are sent by email via a transactional provider.
Full API key list required: AWS_ACCESS_KEY_ID, AWS_REGION, AWS_SECRET_ACCESS_KEY, S3_BUCKET, SENDGRID_API_KEY.

**Related:** EPIC-003, EPIC-006, US-018, US-019, US-020

- ⚠ Discrepancy: S3 is justified specifically for receipt-image uploads, but the Capabilities-in-scope list and EPIC-003's own assumption explicitly state receipt image upload is NOT part of this lightweight MVP scope (noted only as a 'discovery enhancement'). Needs product-owner clarification on whether S3 is required for this release or is being provisioned ahead of a future capability.

### REQ-SCOPE · draft · source: requirements:scope

Defines the lightweight MVP's in-scope capabilities and explicit exclusions.

In scope: account registration/login, persistent expense groups, name-only placeholder members, expense logging (amount/payer/description/date/category) with optional note, equal/exact/percentage/share splits with member selection, per-group history, per-group and overall running balances, debt simplification, manual settlement ('mark as paid'), comments on expenses, free app with no billing, single currency only.
Out of scope — explicitly not to be designed or built: native mobile apps (iOS/Android); in-app real-money payments/settlement transfers. Settlements are informal records only.

**Related:** EPIC-001, EPIC-002, EPIC-003, EPIC-004, EPIC-005, EPIC-006, EPIC-007

### REQ-EPIC-001 · draft · source: requirements:EPIC-001

Email/password authentication for registered users; placeholder members never have accounts or logins.

US-001 (critical) Register: unique email + name + valid password creates and signs in the account, landing on dashboard (AC-001). Duplicate email is rejected with an 'already in use' message (AC-002). Invalid email or password is rejected, naming the invalid field (AC-003).
US-002 (critical) Log in/out: correct email+password authenticates to dashboard (AC-004); non-matching credentials give a generic invalid-credentials message, not logged in (AC-005); logging out ends the session and requires re-login (AC-006).
Assumption stated: email/password only, no social login; no billing involved in account creation.

**Related:** US-001, US-002, AC-001, AC-002, AC-003, AC-004, AC-005, AC-006, NFR-002

- ⚠ Password validation rules referenced in AC-003 ('valid password', 'password rules') are not specified in the input — complexity/length requirements are undefined.

### REQ-EPIC-002 · draft · source: requirements:EPIC-002

Persistent groups with registered-user and name-placeholder members.

US-003 (critical) Create group: named group is saved, creator becomes a member, persists on dashboard (AC-007); unnamed group creation is rejected with a prompt (AC-008).
US-004 (high) Invite registered user: inviting an existing account's email adds them and sends an invitation email (AC-009); inviting a non-existing email sends an email prompting registration/join (AC-010).
US-005 (high) Add placeholder: name-only member (no email/account) is added, can be included in splits/balances (AC-011); placeholders have no login and get no email notifications (AC-012).
US-006 (medium) View members: member list shows every member with name and registered-vs-placeholder status (AC-013).
Assumption: placeholders never sign up or log in; exist only for splits/balances.

**Related:** US-003, US-004, US-005, US-006, AC-007, AC-008, AC-009, AC-010, AC-011, AC-012, AC-013

### REQ-EPIC-003 · draft · source: requirements:EPIC-003

Expense logging with flexible splitting (equal, exact, percentage, shares), member selection, optional notes, and comments.

US-007 (critical) Log expense: amount/payer/description/date/category saved to group history (AC-014); missing required field or non-positive amount rejected with field flagged (AC-015); amount captured in single app-wide currency, no currency choice (AC-016).
US-008 (low) Optional note: note stored and shown on expense detail (AC-017); blank note still saves successfully (AC-018).
US-009 (critical) Equal split: amount divided evenly across included members, summing exactly to total (AC-019).
US-010 (high) Exact/percentage/shares split: exact amounts must sum to total or rejected with the difference shown (AC-020, AC-021); percentages must total 100% and resulting amounts sum exactly to total (AC-022); shares divide proportionally, summing exactly to total (AC-023).
US-011 (high) Member inclusion: only included members get a share, excluded members owe nothing (AC-024); zero members included is rejected with a prompt (AC-025).
US-012 (low) Comments: comment saved with author name and timestamp (AC-026); multiple comments shown in chronological order (AC-027).
Assumption: receipt-image upload is explicitly NOT part of this lightweight MVP (noted only as a discovery-phase enhancement idea). Single currency throughout, no multi-currency.

**Related:** US-007, US-008, US-009, US-010, US-011, US-012, AC-014, AC-015, AC-016, AC-017, AC-018, AC-019, AC-020, AC-021, AC-022, AC-023, AC-024, AC-025, AC-026, AC-027

- ⚠ Conflict: this epic's own assumption excludes receipt-image upload from MVP scope, yet the approved services list (S3) is justified specifically by receipt-image uploads — see REQ-SERVICES open_gaps.

### REQ-EPIC-004 · draft · source: requirements:EPIC-004

Per-group activity history, running balances, overall cross-group dashboard, and debt-simplified settle-up suggestions.

US-013 (high) Group history: expenses and settlements shown with description/amount/payer/date in reverse-chronological order (AC-028); empty-state message when no activity (AC-029).
US-014 (critical) Group balances: each member's net balance reflects all expenses and settlements (AC-030); updates live when new expense/settlement recorded (AC-031).
US-015 (high) Overall dashboard: combined 'you owe'/'you are owed' summary aggregated across all groups (AC-032).
US-016 (medium) Debt simplification: minimised set of settle-up payments leaves every member's net balance unchanged (AC-033); fully settled group shows no suggested payments (AC-034).
Assumption: balances derived automatically from expenses/settlements; simplification never changes net position, only transaction count.

**Related:** US-013, US-014, US-015, US-016, AC-028, AC-029, AC-030, AC-031, AC-032, AC-033, AC-034

- ⚠ Debt-simplification algorithm/approach is not specified beyond the outcome criteria (minimise transaction count, preserve net balances) — implementation approach left to architecture/design phase.

### REQ-EPIC-005 · draft · source: requirements:EPIC-005

Manual settlement recording ('mark as paid') that updates balances; informal record only, no real money movement.

US-017 (high) Record settlement: payer, recipient, amount and date saved to group history; running balances update accordingly (AC-035). UI must make clear the record is informal and no real money moves (AC-036). Missing or non-positive amount is rejected with a correction prompt (AC-037).

**Related:** US-017, AC-035, AC-036, AC-037

### REQ-EPIC-006 · draft · source: requirements:EPIC-006

Transactional email notifications for group additions, new relevant expenses, and recorded settlements — registered users only.

US-018 (medium) Added-to-group email: sent to registered user's address when invited/added (AC-038); no email sent for placeholder members (AC-039).
US-019 (medium) New-expense email: registered member included in a new expense's split receives a summary email of the expense and their share (AC-040).
US-020 (low) Settlement email: registered payer or recipient of a recorded settlement receives a confirmation email (AC-041).
Depends on SendGrid (SENDGRID_API_KEY) per REQ-SERVICES.

**Related:** US-018, US-019, US-020, AC-038, AC-039, AC-040, AC-041, REQ-SERVICES

### REQ-EPIC-007 · draft · source: requirements:EPIC-007

Cross-cutting platform constraints: responsive web only, free with no billing, single currency and region, modest scale.

US-021 (high) Responsive web: core flows (groups, expense logging, balances) adapt on small mobile screens and remain usable without a native app (AC-042); render appropriately on desktop (AC-043).
US-022 (medium) Free, single currency: no feature ever prompts for payment, subscription, or billing details (AC-044); all monetary amounts shown in the single default currency with no option to change it (AC-045).
Assumption: not a native iOS/Android app; no in-app real-money transfers; free with no fees/plans/billing; single default currency and region; modest consumer scale (thousands of users); no specialised financial-regulation requirements since settlements are informal.

**Related:** US-021, US-022, AC-042, AC-043, AC-044, AC-045, NFR-001, NFR-006, NFR-007

### REQ-NFR-001 · draft · source: requirements:NFR-001

Compatibility: single responsive web app must work well on both mobile and desktop browsers.

Core flows (groups, logging an expense, viewing balances) must adapt to small screens and remain fully usable without a native app, and render appropriately on larger desktop screens. No native app is to be built.

**Related:** US-021

### REQ-NFR-002 · draft · source: requirements:NFR-002

Security: authenticated email/password sessions protect user data; failed logins reveal no account-probing detail.

Access to groups, expenses and balances requires an authenticated email/password session that ends on logout. Registration must enforce password rules and reject emails already in use. A failed login must show only a single generic invalid-credentials message.

**Related:** US-001, US-002

- ⚠ Specific password rules to be enforced are not defined in the input (see REQ-EPIC-001 gap).

### REQ-NFR-003 · draft · source: requirements:NFR-003

Privacy: group data (members, expenses, balances, history, comments) visible only to members of that group.

A user may only see and act on groups they belong to. Non-members must not be able to view a group's members, expenses, balances, history, or comments.

**Related:** US-002, US-004, US-013, US-014, US-015, US-016

### REQ-NFR-004 · draft · source: requirements:NFR-004

Privacy: placeholder members must never receive any email notification.

Placeholder members have no account and no login and must never be emailed; they exist solely to be included in their group's splits and balances.

**Related:** US-005, US-018

### REQ-NFR-005 · draft · source: requirements:NFR-005

Usability: clear field-level validation messages and friendly empty states throughout the app.

Rejected input must plainly indicate which field is invalid (e.g., invalid email/password, missing/non-positive expense amount, a split whose parts don't sum to the total, showing the difference). Lists with no activity yet (e.g., group history) must show a friendly empty-state message, not an error.

**Related:** US-001, US-007, US-010, US-011, US-013, US-017

### REQ-NFR-006 · draft · source: requirements:NFR-006

Scalability: single-region deployment targeting modest consumer scale (thousands of users) in one currency.

Applies to the whole system. The app runs in a single default AWS region and single currency, and is designed for thousands of users rather than large-scale multi-region traffic.

### REQ-NFR-007 · draft · source: requirements:NFR-007

Accepted risk: no specialised financial-regulation or payment-compliance controls are included.

Because settlements are informal 'mark as paid' records and the app never moves real money, charges fees, or handles billing, the product owner has accepted the risk of not building any specialised financial-regulation or payment-compliance controls. Applies to the whole system.
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-10-28

**Capabilities in scope:** User account registration and login, Create and keep persistent expense groups, Add group members as name placeholders (no sign-up needed), Log an expense with amount, payer, description, date and category, Optional note on an expense, Split expenses equally, by exact amounts, by percentage or by shares, Choose which members are included in each split, Per-group expense and activity history, Running per-member balances within a group (who owes whom), Overall balances across groups ("you owe / you are owed") dashboard, Debt simplification to minimise settle-up transactions, Record a settlement manually ("mark as paid"), Comments on expenses, Settlements are informal records — no real-money transfer, App is free — no fees, plans or billing, Everything runs in a single currency

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | The hard part of your app lives on the server: computing per-member balances, who-owes-whom across a group and overall, and the debt-simplification logic that minimises settle-up transactions. FastAPI (Python) is well suited to that calculation-heavy logic and to the clean API your React screens will call, and it ships fast — good for a free product with no large team behind it. |
| cloud | AWS | You target a single default region at modest consumer scale, which AWS covers comfortably and cheaply at these volumes. It also gives you S3 for the receipt-image uploads in the same account, so your whole stack — app, database, file storage — sits in one place with one bill and one region, matching your single-region decision. |
| database | PostgreSQL | Everything here is relational and must stay exact: users, groups, members (including name-only placeholders), expenses, each expense's splits, settlements, comments. Balances are derived by summing these rows, so you need a database that keeps money math consistent and won't lose or double-count a split. PostgreSQL does this reliably and also stores the receipt-image references and activity history in the same place. |
| frontend | React | Your app is a responsive web app where members constantly interact with live numbers — split an expense four ways, see balances recompute, mark a debt paid. React handles this kind of interactive, state-heavy screen cleanly across phone and desktop browsers, which is exactly your 'mobile-friendly web, not native app' decision. It also has the largest pool of developers, so this is the cheapest path to getting the product built and maintained. |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: User Accounts & Authentication

Registered users authenticate with email and password so they can create groups, log expenses and track balances. Assumption: authentication is email/password only; there is no social login, and non-user placeholder members never create accounts or log in. The app is free — no billing or paid plans are involved in account creation.

### US-001: Register a new account

**Priority:** critical

> As a new visitor, I want to register an account with my email and a password, so that I can create groups and track shared expenses.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | I am on the registration page and not logged in | I submit a unique email address, a name and a valid password | my account is created and I am signed in and taken to my dashboard |
| AC-002 | I am on the registration page | I submit an email address that already belongs to an existing account | registration is rejected and I see a message that the email is already in use |
| AC-003 | I am on the registration page | I submit an invalid email or a password that fails the password rules | registration is rejected and I see which field is invalid |

### US-002: Log in and out

**Priority:** critical

> As a registered user, I want to log in with my email and password and log out again, so that only I can access my groups and balances.

| ID | Given | When | Then |
|---|---|---|---|
| AC-004 | I have a registered account | I submit my correct email and password on the login page | I am authenticated and taken to my dashboard |
| AC-005 | I am on the login page | I submit an email/password combination that does not match any account | I am not logged in and I see a generic invalid-credentials message |
| AC-006 | I am logged in | I choose to log out | my session ends and I must log in again to access my data |

## EPIC-002: Groups & Members

Registered users create persistent groups and populate them with members, who may be other registered users or plain name placeholders. Assumption: placeholder members have no login and never need to sign up; they exist only to be included in expense splits and balances within their group.

### US-003: Create a persistent group

**Priority:** critical

> As a registered user, I want to create a named group, so that I have a persistent place to track shared expenses with a set of people.

| ID | Given | When | Then |
|---|---|---|---|
| AC-007 | I am logged in | I create a group with a name | the group is saved, I am a member of it, and it remains available on my dashboard in future sessions |
| AC-008 | I am logged in | I try to create a group without a name | creation is rejected and I am prompted to provide a name |

### US-004: Add a registered user to a group by invitation

**Priority:** high

> As a group member, I want to add another registered user to the group, so that they can see and log the group's shared expenses.

| ID | Given | When | Then |
|---|---|---|---|
| AC-009 | I am a member of a group | I invite someone by an email address that belongs to a registered account | they are added to the group and an invitation email is sent to them |
| AC-010 | I invite someone by an email address with no existing account | I submit the invitation | an invitation email is sent prompting them to register and join the group |

### US-005: Add a placeholder member by name

**Priority:** high

> As a group member, I want to add a person to the group by name without requiring them to sign up, so that I can include people who don't use the app in expense splits.

| ID | Given | When | Then |
|---|---|---|---|
| AC-011 | I am a member of a group | I add a member by name only (no email/account) | the placeholder member appears in the group and can be included in expense splits and balances |
| AC-012 | a placeholder member exists in a group | I view how to access the app as that placeholder | there is no login for them — they have no account and receive no email notifications |

### US-006: View group members

**Priority:** medium

> As a group member, I want to see the list of members in a group, so that I know who shares expenses and balances in that group.

| ID | Given | When | Then |
|---|---|---|---|
| AC-013 | I am a member of a group that has registered and placeholder members | I open the group's member list | I see every member with their name and whether they are a registered user or a placeholder |

## EPIC-003: Expense Logging & Splitting

Members log expenses within a group and split them flexibly. Assumption: each expense records amount, payer, description, date and category, with an optional note; receipt image upload is noted as an optional enhancement from the discovery but is not part of this lightweight MVP scope. Splits may be equal, by exact amounts, by percentage or by shares, and the payer chooses which members are included. All amounts are in a single app-wide currency; multi-currency is not supported.

### US-007: Log an expense with core details

**Priority:** critical

> As a group member, I want to record an expense with an amount, payer, description, date and category, so that the group's shared spending is captured accurately.

| ID | Given | When | Then |
|---|---|---|---|
| AC-014 | I am a member of a group | I create an expense specifying amount, payer (a member), description, date and category | the expense is saved to the group and appears in the group's expense history |
| AC-015 | I am creating an expense | I leave a required field (amount, payer, description, date or category) empty or enter a non-positive amount | the expense is not saved and I am shown which field is invalid |
| AC-016 | I am creating an expense | I enter an amount | the amount is captured in the single app-wide currency with no currency selection offered |

### US-008: Add an optional note to an expense

**Priority:** low

> As a group member, I want to add an optional free-text note to an expense, so that I can capture extra context about the spend.

| ID | Given | When | Then |
|---|---|---|---|
| AC-017 | I am creating or editing an expense | I add a note and save | the note is stored and shown on the expense detail |
| AC-018 | I am creating an expense | I leave the note blank and save | the expense is saved successfully with no note |

### US-009: Split an expense equally

**Priority:** critical

> As a group member logging an expense, I want to split it equally among the included members, so that everyone owes the same share by default.

| ID | Given | When | Then |
|---|---|---|---|
| AC-019 | I am splitting an expense and have chosen the included members | I select an equal split | the amount is divided evenly across the included members and the shares sum exactly to the expense amount |

### US-010: Split an expense by exact amounts, percentage or shares

**Priority:** high

> As a group member logging an expense, I want to split it by exact amounts, by percentage or by shares, so that I can reflect how the cost should really be divided.

| ID | Given | When | Then |
|---|---|---|---|
| AC-020 | I am splitting an expense by exact amounts | the entered amounts for the included members sum to the expense total | the split is accepted and saved |
| AC-021 | I am splitting an expense by exact amounts | the entered amounts do not sum to the expense total | the split is rejected and I am shown the difference to correct |
| AC-022 | I am splitting an expense by percentage | the percentages across included members sum to 100% | the split is accepted and the resulting member amounts sum exactly to the expense total |
| AC-023 | I am splitting an expense by shares | I assign a number of shares to each included member | the amount is divided in proportion to the shares and the member amounts sum exactly to the expense total |

### US-011: Choose which members are included in a split

**Priority:** high

> As a group member logging an expense, I want to choose which group members are included in the split, so that only the people who actually shared the cost owe a portion.

| ID | Given | When | Then |
|---|---|---|---|
| AC-024 | I am splitting an expense in a group | I include only a subset of members | only those members receive a share and excluded members owe nothing for that expense |
| AC-025 | I am splitting an expense | I include no members | the split is rejected and I am prompted to include at least one member |

### US-012: Comment on an expense

**Priority:** low

> As a group member, I want to add comments to an expense, so that members can discuss or clarify a shared cost.

| ID | Given | When | Then |
|---|---|---|---|
| AC-026 | I am viewing an expense in a group I belong to | I post a comment | the comment is saved and shown with my name and timestamp on the expense |
| AC-027 | an expense has multiple comments | I view the expense | all comments are shown in chronological order |

## EPIC-004: Balances, History & Debt Simplification

The app maintains an ongoing expense/activity history per group and computes running per-member balances, both within a group and overall across groups, with debt simplification. Assumption: balances are derived automatically from expenses and recorded settlements; debt simplification minimises the number of settle-up transactions without changing any member's net position.

### US-013: View per-group expense and activity history

**Priority:** high

> As a group member, I want to see the ongoing history of expenses and activity in a group, so that I can review what has been logged over time.

| ID | Given | When | Then |
|---|---|---|---|
| AC-028 | a group has logged expenses and recorded settlements | I open the group's history | I see each entry with its description, amount, payer and date in reverse-chronological order |
| AC-029 | a group has no activity yet | I open the group's history | I see an empty-state message rather than an error |

### US-014: View running per-member balances within a group

**Priority:** critical

> As a group member, I want to see who owes whom within the group, so that I know my standing with each member.

| ID | Given | When | Then |
|---|---|---|---|
| AC-030 | a group has expenses split across members | I view the group's balances | I see each member's net balance (owed to them or owed by them) that reflects all expenses and recorded settlements |
| AC-031 | a new expense or settlement is recorded in the group | I view the group's balances again | the balances update to reflect that change |

### US-015: View overall balances across all my groups

**Priority:** high

> As a registered user, I want a dashboard showing what I owe and am owed overall, so that I can see my total standing across every group at a glance.

| ID | Given | When | Then |
|---|---|---|---|
| AC-032 | I belong to multiple groups with outstanding balances | I open my dashboard | I see a combined 'you owe' and 'you are owed' summary aggregated across all my groups |

### US-016: Simplify debts to minimise settle-up transactions

**Priority:** medium

> As a group member, I want the app to simplify debts into the fewest payments, so that members settle up with as few transactions as possible.

| ID | Given | When | Then |
|---|---|---|---|
| AC-033 | a group has multiple interlocking debts between members | I view the suggested settle-up | the app shows a minimised set of payments whose effect leaves every member's net balance unchanged |
| AC-034 | all members in a group are square | I view the suggested settle-up | no payments are suggested and the group is shown as settled |

## EPIC-005: Settlements

Members record settlements manually to clear balances. Assumption: settlements are informal records only — the app does not move real money, integrate a payment provider, or charge any fee. Recording a settlement adjusts the computed balances.

### US-017: Record a settlement manually

**Priority:** high

> As a group member, I want to mark a payment between two members as made, so that the balances reflect that a debt has been settled.

| ID | Given | When | Then |
|---|---|---|---|
| AC-035 | there is an outstanding balance between two members in a group | I record a settlement specifying the payer, the recipient, the amount and the date | the settlement is saved to the group's history and the running balances update accordingly |
| AC-036 | I am recording a settlement | I view the effect on balances | it is clear the record is an informal note of payment and no real money is moved by the app |
| AC-037 | I am recording a settlement | I omit the amount or enter a non-positive amount | the settlement is rejected and I am prompted to correct it |

## EPIC-006: Email Notifications

Registered members are notified by email of key events. Assumption: notifications are delivered via a transactional email provider that requires an API key; placeholder members have no email and are never notified. Notifiable events are: being added to a group, a new expense that involves you, and a settlement recorded against you.

### US-018: Notify a user when added to a group

**Priority:** medium

> As a registered user, I want to receive an email when I'm invited or added to a group, so that I know I've been included and can start participating.

| ID | Given | When | Then |
|---|---|---|---|
| AC-038 | a transactional email provider is configured with a valid API key | a registered user is invited or added to a group | an email about the group is sent to that user's address |
| AC-039 | a placeholder member (no email account) is added to a group | the add completes | no email is sent for that placeholder |

### US-019: Notify members of a new relevant expense

**Priority:** medium

> As a registered group member, I want to receive an email when a new expense involving me is logged, so that I stay aware of changes to what I owe or am owed.

| ID | Given | When | Then |
|---|---|---|---|
| AC-040 | I am a registered member included in an expense's split | another member logs that expense | I receive an email summarising the expense and my share |

### US-020: Notify members of a recorded settlement

**Priority:** low

> As a registered group member, I want to receive an email when a settlement involving me is recorded, so that I know a payment has been logged against our balance.

| ID | Given | When | Then |
|---|---|---|---|
| AC-041 | I am a registered member who is the payer or recipient of a settlement | another member records that settlement | I receive an email confirming the recorded settlement |

## EPIC-007: Platform & Operating Constraints

Cross-cutting constraints for the product. Assumption: delivered as a responsive (mobile-friendly) web application, not a native iOS/Android app and with no in-app real-money transfers. The app is free with no fees, plans or billing, operates in a single default currency and region, targets modest consumer scale (thousands of users), and carries no specialised financial-regulation requirements as debts are informal records.

### US-021: Use the app on any device via a responsive web interface

**Priority:** high

> As a user, I want the web app to work well on desktop and mobile browsers, so that I can manage shared expenses from whatever device I have.

| ID | Given | When | Then |
|---|---|---|---|
| AC-042 | I open the app in a browser on a small mobile screen | I navigate the core flows (groups, logging an expense, viewing balances) | the layout adapts responsively and all actions remain usable without a native app |
| AC-043 | I open the app on a desktop browser | I use the same flows | the interface renders appropriately for the larger screen |

### US-022: Use the app free of charge in a single currency

**Priority:** medium

> As a user, I want to use all features for free in one currency, so that there is no cost barrier or currency confusion.

| ID | Given | When | Then |
|---|---|---|---|
| AC-044 | I use any feature of the app | I complete an action such as creating a group, logging an expense or recording a settlement | I am never asked to pay a fee, subscribe or enter billing details |
| AC-045 | I view any monetary amount in the app | it is displayed | it is shown in the single default currency with no option to change currency |
<!-- sdlc:auto:end epics -->
