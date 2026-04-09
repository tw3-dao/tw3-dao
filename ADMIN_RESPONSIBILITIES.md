# Admin Responsibilities

This document defines the operational responsibilities of TW3 admins across the entire TechnicallyWeb3 organization. It is a practical implementation guide derived from [GOVERNANCE.md](GOVERNANCE.md) and [STRUCTURE.md](STRUCTURE.md).

This document cannot contradict any higher-authority document in the hierarchy defined in [GOVERNANCE.md](GOVERNANCE.md): [PHILOSOPHY.md](PHILOSOPHY.md) > [POSTULATES.md](POSTULATES.md) > [STRUCTURE.md](STRUCTURE.md) > [GOVERNANCE.md](GOVERNANCE.md). Where a conflict exists, the higher document wins and this document must be amended.

Individual project repositories may maintain their own admin responsibility documents that extend this one with project-specific duties. Those documents cannot contradict this one. When working on a specific project repo, admins should check for such a document before acting.

Org-wide changes to admin responsibilities must be proposed through this repo's governance process.

## Before you accept

If you are considering an admin nomination, understand what you are agreeing to. The admin role is a revocable responsibility delegated by the community, not an identity or title. You can voluntarily step down at any time.

Before accepting, confirm the following:

- [ ] You have read and understood the full document hierarchy — [PHILOSOPHY.md](PHILOSOPHY.md), [POSTULATES.md](POSTULATES.md), [STRUCTURE.md](STRUCTURE.md), [GOVERNANCE.md](GOVERNANCE.md), [TOKENOMICS.md](TOKENOMICS.md), [CONTRIBUTING.md](CONTRIBUTING.md), [RATE_SCHEDULE.md](RATE_SCHEDULE.md), and [CODING.md](CODING.md).
- [ ] You understand the branch model (`development` → `staging` → `production` → `main`) and the promotion thresholds defined in [governance.config.json](governance.config.json).
- [ ] You accept accountability to the community as described in the [admin elections](GOVERNANCE.md#admin-elections) section of GOVERNANCE.md. Any member can submit a removal proposal, and the community votes using the standard model.
- [ ] You understand that admin work earns contribution tokens like any other labor, at the rates defined in [RATE_SCHEDULE.md](RATE_SCHEDULE.md), subject to the same reward hold period as all contributions.
- [ ] You are prepared to share collective coverage of all responsibilities listed below. Admins delegate among themselves — there is no fixed assignment — but every responsibility must be covered.

## Core responsibilities

All responsibilities are shared across the admin group. Admins organize among themselves to ensure coverage. No single admin is required to handle everything, but collectively nothing can be left unattended.

### Discussion and community monitoring

- Monitor [GitHub Discussions](https://github.com/orgs/TechnicallyWeb3/discussions) for new ideas, proposals, and community feedback.
- Participate in discussions to understand community sentiment and surface concerns early.
- Track when a discussion reaches the support threshold defined in [governance.config.json](governance.config.json) (`support_threshold`). When it does, create the repository following the [REPO_SETUP.md](.github/REPO_SETUP.md) checklist.

### Issue management

- Track incoming issues across all org repos.
- Ensure proper labeling: `bug`, `enhancement`, `documentation`, `good first issue`, `help wanted`, `governance` at minimum.
- Respond to issues — clarify scope, confirm reproducibility for bugs, link to related discussions or duplicate issues.
- Close resolved or stale issues with a clear explanation of why.

### Pull request review

- Review PRs against: coding standards ([CODING.md](CODING.md)), commit conventions ([CONTRIBUTING.md](CONTRIBUTING.md#commit-conventions)), test coverage, documentation updates, changelog entries, absence of proprietary dependencies, and alignment with TW3 principles.
- Verify the PR relates to an active issue or approved discussion. PRs that appear out of nowhere with no community context deserve scrutiny.
- Accept or request changes with a clear explanation. Rejection is not personal — explain what needs to change so the contributor can resubmit. See the [review and merge](CONTRIBUTING.md#review-and-merge) process.
- Observe the self-approval rule (see [Self-approval](#self-approval) below).

### Peer review of admin actions

- Review recent merges by other admins. This is not optional — admins hold each other accountable.
- Challenge merges that do not meet quality standards or appear malicious. Challenges follow the [revert process](CONTRIBUTING.md#revert-process) in CONTRIBUTING.md, where a majority of admins can revert a merge.
- If an admin consistently merges substandard work, any community member (including other admins) can initiate a [removal proposal](GOVERNANCE.md#accountability).

### Steward actions

Admins execute actions that require human intervention where code cannot yet act autonomously. This includes:

- Blockchain transactions required by governance vote outcomes.
- GitHub administrative actions (repo creation, branch protection, access management).
- Discord channel management or other platform administration.
- Any off-chain execution of on-chain governance decisions.

Admins must act as if bound by the rules of code — faithfully executing community decisions without exercising discretion beyond what governance grants. An admin who refuses to execute a passed governance decision or who executes actions the community did not approve is subject to [accountability proceedings](GOVERNANCE.md#accountability).

### Repository and template maintenance

- Maintain the org-level repository template. When standards evolve, the template must be updated so new repos start compliant.
- Follow the [REPO_SETUP.md](.github/REPO_SETUP.md) checklist when creating new repositories.
- Ensure issue templates, PR templates, and discussion templates stay current across org repos.
- Archiving or sunsetting a repository is a community governance decision, not a unilateral admin action.

## Branch promotion

Branch promotion is driven by approval votes (👍 reactions) on pull requests, not by formal governance proposals. Admins merge when a PR has reached the required approval threshold for the target branch.

### Thresholds

Current values are stored in [governance.config.json](governance.config.json) and are adjustable through the standard governance proposal process.

| Target branch | Required approval | What it means |
|---|---|---|
| `development` | 10%+ of active members | Work is accepted for active development |
| `staging` | 50%+ of active members | Work is ready for pre-production testing |
| `production` | 66%+ of active members (supermajority) | Work is released — this constitutes a new version |
| `main` | Same as production | Stable reference updated from production |

### How thresholds scale

With 1 org member, that member satisfies all thresholds. With 2 members, both must approve for production and main (2/2 ≥ 66%). As the org grows, the required absolute number of approvals increases while the percentage remains governance-adjustable.

### Combining work

The `development` and `staging` branches may accumulate multiple merged issues or improvements before being promoted. There is no requirement to promote after every individual merge — admins use judgment about when a batch of work is ready to move up.

Merging `staging` into `production`, however, constitutes a version release and must be treated with the corresponding rigor.

## Self-approval

Admins should not approve their own pull requests. This is the founding admin's position, grounded in the [Philosophy's](PHILOSOPHY.md) accountability principles: those who hold power should be checked by others who hold power.

This is a governed rule — the community can change it through the standard governance proposal process. New members will have a say in whether this rule remains.

At sufficient scale (e.g., 10+ active members with a 10% development threshold), a contributor's PR can reach the development merge threshold through community votes alone, making self-approval unnecessary for that branch.

All admin rules are currently enforceable by social consensus. Automation through bots is a future improvement goal, built through the same contribution and governance process as everything else.

## Reward hold period

All token rewards — for both contributors and admins — are subject to a 7-day hold after the qualifying action. This applies to PR merges, discussion creation, issue resolution, and all other rewarded actions listed in [RATE_SCHEDULE.md](RATE_SCHEDULE.md).

The hold period is defined in [governance.config.json](governance.config.json) (`reward_hold_days`) and is governance-adjustable.

### What the hold period is

- A waiting period before tokens are minted and voting weight is applied.
- During the hold, the contributor's and reviewing admin's rewards are pending but not yet awarded.
- PRs, comments, and reactions made within the last 7 days do not count toward a participant's voting weight. This prevents freshly-earned influence from being used before the community has had a chance to scrutinize the work.

### What the hold period is not

- It is not a freeze on the merged code. Merged work stays merged unless explicitly reverted through the [challenge process](CONTRIBUTING.md#challenge-period).
- It is not an admin-specific duty. Admins have no special role during the hold — it applies passively and equally to everyone.

### Challenges during the hold

Any community member can challenge a contribution during the hold period. If a majority of admins agrees the contribution should be reverted, the PR is reverted and tokens are not awarded. If the challenge fails, the challenger's stake is forfeit and the contributor receives their tokens. See [CONTRIBUTING.md](CONTRIBUTING.md#challenge-period) for full details.

## Farming detection

Admins should watch for contribution farming — actions designed to inflate token rewards without providing genuine value. The [RATE_SCHEDULE.md](RATE_SCHEDULE.md) defines what earns tokens; farming exploits those rules.

This list will grow as the community encounters new patterns. Current known patterns to watch for:

- **Add-delete cycling** — adding and removing the same lines across successive PRs to generate line-change rewards.
- **Trivial formatting changes** — whitespace-only or style-only changes that do not meaningfully improve readability or comply with a linting requirement.
- **PR splitting** — breaking a single logical change into many small PRs to multiply per-PR reward opportunities.
- **Circular discussions** — creating issues or discussions that reference each other with no substantive content, to farm discussion and comment rewards.
- **Inflated media** — committing uncompressed or unnecessarily large media files when optimized versions would serve the same purpose, to inflate per-MB media rewards.
- **Orphan PRs** — pull requests that do not relate to any open issue, approved discussion, or documented need.
- **Reaction spam** — a suspiciously high volume of low-quality comments or reactions, particularly from accounts with no other meaningful activity.

When in doubt, use the rate schedule as a map of what is being gamed. Every line item in [RATE_SCHEDULE.md](RATE_SCHEDULE.md) is a potential farming target.

Suspected farming should be raised as a challenge during the hold period. If confirmed by admin majority, the contribution is reverted and no tokens are awarded.

## Version management

### Branch-to-version mapping

- `development` and `staging` accumulate work across multiple issues and improvements.
- Merging `staging` into `production` constitutes a **new version release**.
- After merging into `production` and then into `main`, the admin creates a version branch from `main` (e.g., `v1.0.0`) to maintain a permanent archive of that version's state.

### Version archiving

After each merge to `main`, create a version branch:

```bash
git checkout main
git pull origin main
git checkout -b v<MAJOR>.<MINOR>.<PATCH>
git push -u origin v<MAJOR>.<MINOR>.<PATCH>
git checkout development
```

Whether to archive the old version before merging to main (preserving the pre-merge state) or duplicate the new version after merging (preserving the post-merge state) is an open community decision. The current practice is to create version branches from `main` after the merge.

The versioning strategy for minor vs. patch releases is TBD and will be decided collaboratively as the org matures. For now, every merge to `main` gets a version branch.

## Opening new repositories

A new repository is created when a GitHub Discussion reaches the support threshold defined in [governance.config.json](governance.config.json) (`support_threshold`, currently 10% of active members).

When the threshold is met:

1. Confirm the discussion has genuine community support (not inflated by farming or duplicate accounts).
2. Follow every step in the [REPO_SETUP.md](.github/REPO_SETUP.md) checklist.
3. Announce the new repo in TW3 Discussions and link it back to the originating discussion.

No other triggers exist for repo creation. The project lifecycle is fully defined in [STRUCTURE.md](STRUCTURE.md#project-lifecycle).

---

For governance mechanics, see [GOVERNANCE.md](GOVERNANCE.md). For contribution workflows, see [CONTRIBUTING.md](CONTRIBUTING.md). For token reward rates, see [RATE_SCHEDULE.md](RATE_SCHEDULE.md). For the economic model, see [TOKENOMICS.md](TOKENOMICS.md).
