# Admin Elections

This document defines the interim process for nominating, electing, and removing TW3 admins using GitHub issues and pull requests. It is a procedural companion to the [admin elections](GOVERNANCE.md#admin-elections) section of [GOVERNANCE.md](GOVERNANCE.md), which remains the authoritative source for election rules, voting model, tiers, and accountability.

When on-chain voting infrastructure is operational, this process will be superseded by smart contract elections as described in GOVERNANCE.md. Until then, this document governs how admin changes are proposed, voted on, and ratified.

This document cannot contradict any higher-authority document in the hierarchy defined in [GOVERNANCE.md](GOVERNANCE.md): [PHILOSOPHY.md](PHILOSOPHY.md) > [POSTULATES.md](POSTULATES.md) > [STRUCTURE.md](STRUCTURE.md) > [GOVERNANCE.md](GOVERNANCE.md). Where a conflict exists, the higher document wins and this document must be amended.

## Admin config

The current admin roster is maintained in [admin.config.json](admin.config.json). This file is the machine-readable source of truth for who holds admin status, what permissions they hold, and when their term began.

Each admin entry contains:

| Field | Description |
|---|---|
| `username` | GitHub username |
| `permissions` | Array of permission strings. `"full"` grants all responsibilities defined in [ADMIN_RESPONSIBILITIES.md](ADMIN_RESPONSIBILITIES.md). Granular values may be introduced as the org grows. |
| `elected` | ISO 8601 date of election or appointment |

The `term_months` field defines the default term length in months (currently 36). Both the roster and the term length are governance-adjustable through the standard proposal process.

## Issue format

All admin elections use GitHub issues in this repository with the `[ADMIN]` tag in the title. The title must include one of the following action prefixes:

- **`[ADMIN] Add: @username`** — nominate a new admin
- **`[ADMIN] Remove: @username`** — propose removal of an existing admin
- **`[ADMIN] Change: @username`** — propose permission or term changes for an existing admin

The issue body must include:

1. A rationale for the proposed action
2. Which TW3 principles the proposal aligns with (reference [PHILOSOPHY.md](PHILOSOPHY.md) and [POSTULATES.md](POSTULATES.md))

## Nomination

Any community member may open an `[ADMIN]` issue to nominate a new admin, propose a removal, or propose changes. Self-nomination is permitted.

Before accepting a nomination, the nominee should confirm they have reviewed the responsibilities by reading [ADMIN_RESPONSIBILITIES.md](ADMIN_RESPONSIBILITIES.md) and completing the "Before you accept" checklist described there.

## Acceptance

For `Add:` and `Change:` proposals, the nominated user must post a comment on the issue explicitly accepting the nomination. This acceptance comment becomes the voting anchor — all votes are cast as reactions on this comment.

For `Remove:` proposals, no acceptance is required. The issue itself serves as the voting anchor.

If the nominee does not accept within the voting period, the nomination expires.

## Voting

The community votes using reactions on the voting anchor (the acceptance comment for `Add:`/`Change:`, the issue body for `Remove:`):

- **👍** — support the proposal
- **👎** — oppose the proposal

If a user casts both reactions, their vote is nullified.

### Voting period

The voting period follows [governance.config.json](governance.config.json):

| Proposal type | Duration | Source |
|---|---|---|
| Standard | `voting_periods.standard_days` (7 days) | Default for all admin elections |
| Urgent | `voting_periods.urgent_hours` (48 hours) | Leaders or admins may designate; subject to community challenge per [GOVERNANCE.md](GOVERNANCE.md) |
| Governance | `voting_periods.governance_days` (30 days) | If the community treats the action as a governance-tier change |

### Threshold

The default threshold is `supermajority` (0.66) from [governance.config.json](governance.config.json). The community may vote to move routine admin elections to simple majority per the [proposal tiers](GOVERNANCE.md#simple-majority) process in GOVERNANCE.md.

The threshold is calculated as: `👍 / (👍 + 👎)` after removing nullified votes (users who cast both reactions). Quorum requirements from GOVERNANCE.md apply.

## Ratification

When the voting threshold is met after the voting period closes:

1. A community member opens a pull request updating [admin.config.json](admin.config.json) to reflect the election result — adding, removing, or modifying the relevant admin entry.
2. The PR follows the standard branch promotion and approval process defined in [CONTRIBUTING.md](CONTRIBUTING.md) and [ADMIN_RESPONSIBILITIES.md](ADMIN_RESPONSIBILITIES.md).
3. The PR description must link to the originating `[ADMIN]` issue.

This creates a double confirmation: the community votes once in the election and once through the PR approval process. Both must pass for the change to take effect.

If the vote does not meet the threshold, the issue is closed with a summary of the result. No PR is opened.

## Term and re-election

Admin terms last `term_months` months from the `elected` date in [admin.config.json](admin.config.json) (currently 36 months).

When a term approaches expiration, any community member (including the incumbent) may open an `[ADMIN] Add: @username` issue to initiate re-election. The full nomination, acceptance, voting, and ratification process applies — there is no automatic renewal.

If an admin's term expires without a successful re-election, a PR is opened to remove them from [admin.config.json](admin.config.json) following the standard branch promotion process.

## Removal mid-term

Any community member may open an `[ADMIN] Remove: @username` issue at any time, following the same voting rules. Grounds for removal are defined in the [accountability](GOVERNANCE.md#accountability) section of GOVERNANCE.md.

An admin who is removed does not lose their contributor status or accumulated soul-bound tokens, consistent with GOVERNANCE.md.

## Voluntary resignation

An admin may resign at any time by opening an `[ADMIN] Remove: @username` issue (self-directed) or by notifying the other admins. A PR is opened to update [admin.config.json](admin.config.json) without requiring a community vote.

## Bootstrapping

TechnicallyWeb3 is the founding admin, self-appointed as the sole contributor of the organization on 2026-04-08. This is recorded in [admin.config.json](admin.config.json). As the community grows, this appointment is subject to the same re-election and removal processes as any other admin.

---

For election rules and the voting model, see [GOVERNANCE.md](GOVERNANCE.md). For admin operational responsibilities, see [ADMIN_RESPONSIBILITIES.md](ADMIN_RESPONSIBILITIES.md). For contribution workflows, see [CONTRIBUTING.md](CONTRIBUTING.md).
