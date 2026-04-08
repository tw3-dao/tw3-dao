# Contributing to TW3

This guide applies to all repositories under the TW3 organization. It covers how to join, how to contribute, and how contributions are rewarded. Individual projects may extend these guidelines but cannot contradict them.

Read the [Philosophy](PHILOSOPHY.md) first. If you don't share the values described there, this isn't the right community for you. If you do, welcome — there's work to be done.

## Prerequisites

### GitHub account

All TW3 activity happens on GitHub. You need an account to participate in discussions, file issues, submit code, and earn contribution tokens.

### Web3 wallet

You need an Ethereum-compatible wallet to sign data and link your GitHub identity to a crypto address. This is how contributions are tied to on-chain token rewards.

### Identity registration

TW3 uses a decentralized social consensus mechanism to verify contributor identities — no centralized login portal, no single point of control.

The process uses the [git-registry](https://github.com/TechnicallyWeb3/git-registry) project:

1. Create a request to associate your wallet with your GitHub ID.
2. A community validator issues a challenge.
3. You create a repository with signed data proving control of both your wallet and GitHub account.
4. The validator forks your proof repo and signs off, confirming the association.
5. Multiple validators can validate the same claim. The wallet with the most signoffs is considered the consensus owner.

Validators earn tokens for registering users. False registrations can be challenged with a stake-based mechanism.

While the registry is being built out, GitHub API-based verification serves as an interim solution. The goal is full on-chain identity verification.

## Your first contribution

If you're new to TW3, here's the recommended path:

1. **Read the docs** — Start with [PHILOSOPHY.md](PHILOSOPHY.md), then [STRUCTURE.md](STRUCTURE.md) and [GOVERNANCE.md](GOVERNANCE.md). Understand what TW3 is before you try to change it.
2. **Join a Discussion** — Browse open [Discussions](https://github.com/orgs/TechnicallyWeb3/discussions) and share your perspective. Thoughtful comments earn tokens.
3. **Improve documentation** — Low friction, high value. Typos, unclear explanations, missing context — all worth fixing. Every line change earns tokens.
4. **Pick up a `good-first-issue`** — These are scoped, well-defined tasks that don't require deep codebase knowledge.
5. **Tackle a `help-wanted` issue** — Broader scope, but the community has identified these as priorities.
6. **Propose an idea** — Once you understand the project, open a Discussion using the [project proposal template](.github/DISCUSSION_TEMPLATE/project-proposal.md).

## Branch model

All TW3 repositories use four long-lived branches:

| Branch | Purpose |
|---|---|
| `main` | Default branch, stable reference |
| `production` | Deployed/live code |
| `staging` | Pre-production testing |
| `development` | Active work, target for contributor PRs |

### Workflow

1. Fork the repository.
2. Create a feature branch from `development` (e.g., `feat/wallet-auth`, `fix/token-calc`, `docs/update-readme`).
3. Make your changes, commit, push to your fork.
4. Open a pull request targeting the `development` branch of the upstream repo.

Admins merge the chain upward via governance proposal: `development` into `staging` for testing, `staging` into `production` for deployment, and `production` into `main` as the stable reference. Contributors never PR directly to `staging`, `production`, or `main`.

## Commit conventions

TW3 uses [Conventional Commits](https://www.conventionalcommits.org/). Every commit message follows this format:

```
type(scope): description
```

**Types:**

| Type | When to use |
|---|---|
| `feat` | New feature or capability |
| `fix` | Bug fix |
| `docs` | Documentation changes |
| `refactor` | Code restructuring without behavior change |
| `test` | Adding or updating tests |
| `chore` | Maintenance, dependency updates |
| `style` | Formatting, whitespace, no logic change |
| `perf` | Performance improvement |
| `ci` | CI/CD pipeline changes |
| `build` | Build system or tooling changes |

**Scope** is optional but encouraged. It identifies which part of the project is affected:

```
feat(registry): add validator reputation tracking
fix(tokens): correct halving cycle boundary calculation
docs(contributing): add commit convention examples
```

**Breaking changes** append `!` after the type:

```
feat(governance)!: change voting model to weighted individual
```

## Pull request process

### Before you submit

- Your code passes all existing tests.
- You've added tests for new functionality where applicable.
- You've updated documentation for any changed behavior.
- You've added a changelog entry describing the change.
- Your code introduces no proprietary dependencies.
- Your commits follow the conventional commit format.

### PR requirements

Use the [pull request template](.github/PULL_REQUEST_TEMPLATE.md) when opening a PR. Every PR must include:

- A clear description of what changed and why.
- The type of change (maps to commit types).
- Links to related issues or discussions.
- A completed checklist confirming tests, docs, and changelog.

### What gets a PR rejected

- Code that doesn't follow the project's style conventions.
- Missing tests for testable functionality.
- Unnecessary complexity — solve the problem simply.
- Proprietary dependencies or closed-source requirements.
- Misalignment with TW3 principles.

Rejection is not personal. Admins will explain what needs to change. Fix the issues and resubmit.

## Review and merge

After you submit a PR:

1. An admin reviews for quality, style, test coverage, and alignment with TW3 principles.
2. The admin may request changes. Requested changes shift token rewards proportionally — admin review work earns tokens too.
3. Once approved, the admin merges the PR into `development`.
4. The 7-day challenge period begins (see below).

## Token rewards

Every qualifying contribution earns two types of tokens:

- **Soul-bound contribution tokens** — non-transferable, permanent record of your work. Determines your voting weight as a contributor.
- **Economic tokens** — liquid, transferable, represent ownership stake. Earn yield from platform revenue. Can be sold or staked.

Both token types follow the halving schedule described in [TOKENOMICS.md](TOKENOMICS.md). The specific reward rates per action are listed in the [Rate Schedule](RATE_SCHEDULE.md).

Actions that earn tokens include: merged code (per line change), media contributions (per MB), discussions started and commented on, issues filed and resolved, PR reviews, and admin work.

### Contribution tracking

Contribution tracking tooling is under development. The plan is to build an open-source GitHub metrics integration that surfaces contribution data in Discord, on the TW3 website, and eventually on-chain via oracle services.

Until tracking infrastructure is live, historical contributions will be recorded from GitHub activity and airdropped at token launch. Contributing now earns future tokens — the system honors work done before the infrastructure exists to track it in real time.

## Challenge period

All token rewards are subject to a **7-day hold** after the qualifying action (PR merge, discussion creation, issue resolution, etc.).

During this period, any community member can challenge the contribution — disputing its quality, validity, or alignment with TW3 principles. Challenges require a stake to discourage frivolous disputes.

### Revert process

If a challenge succeeds — meaning a **majority of admins** agrees the contribution should be reverted:

- The PR is reverted. Tokens are not awarded.
- There is no appeal. Majority admin consensus is final.
- The revert mechanism exists to catch contribution farming (e.g., adding and deleting the same lines) and to hold abusive or incompetent admins accountable.

If the challenge fails, the challenger's stake is forfeit and the contributor receives their tokens after the hold period.

Merged PRs remain merged unless explicitly reverted through this process. The default outcome is that contributions are accepted.

## Media contributions

Media contributions are anything non-code committed to a TW3 repository: documentation images, design assets, diagrams, marketing materials, UI mockups, or other visual/media files.

Media contributions earn tokens according to the [Rate Schedule](RATE_SCHEDULE.md), calculated per megabyte of qualifying content. The same challenge period and review process applies.

When submitting media:
- Use standard, open formats (PNG, SVG, WebP for images; MP4, WebM for video).
- Optimize file sizes — don't commit uncompressed assets when compressed versions serve the same purpose.
- Include alt text or descriptions for accessibility.
- Place files in the directory structure appropriate to the project.

## Discussions and proposals

### Starting a discussion

Any TW3 member can open a Discussion. Use the appropriate template:

- **[Project Proposal](.github/DISCUSSION_TEMPLATE/project-proposal.md)** — for new project ideas. These feed into the project lifecycle described in [STRUCTURE.md](STRUCTURE.md).
- **[Governance Proposal](.github/DISCUSSION_TEMPLATE/governance-proposal.md)** — for changes to governance rules, token parameters, or organizational structure.

Discussions earn tokens for both the author and participants. See the [Rate Schedule](RATE_SCHEDULE.md) for specific values.

### Filing issues

Use the appropriate template:

- **[Bug Report](.github/ISSUE_TEMPLATE/bug_report.md)** — for reporting defects.
- **[Feature Request](.github/ISSUE_TEMPLATE/feature_request.md)** — for proposing enhancements.

Well-documented issues that lead to fixes earn tokens for the reporter and the contributor who resolves them.

## Code of conduct

Treat people with respect. Disagree on ideas, not on personhood. If you can't engage constructively, this isn't the community for you.

Specific behavioral expectations will be formalized as the community grows. For now: the [Philosophy](PHILOSOPHY.md) is the guide. If your behavior contradicts its spirit, expect to be called on it.

---

For token reward rates, see [RATE_SCHEDULE.md](RATE_SCHEDULE.md). For the economic model, see [TOKENOMICS.md](TOKENOMICS.md). For governance mechanics, see [GOVERNANCE.md](GOVERNANCE.md).
