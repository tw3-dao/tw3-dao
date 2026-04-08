# Contributing to TW3

This guide applies to all repositories under the TW3 organization. It covers how to join, how to contribute, and how contributions are rewarded. Individual projects may extend these guidelines but cannot contradict them.

Read the [Philosophy](PHILOSOPHY.md) first. If you don't share the values described there, this isn't the right community for you. If you do, welcome — there's work to be done.

## A note on GitHub as the current medium

TW3 operates on GitHub today because it's where the community already lives — it provides discussions, version control, issue tracking, and an identity system that works right now. But GitHub is just the current vehicle. The DAO's principles don't depend on any single platform. As the community builds more decentralized infrastructure — on-chain registries, decentralized hosting, protocol-native governance — TW3 will migrate to those tools. We're building the plane while flying it, and GitHub is the runway we're using to take off.

Nothing in these docs requires GitHub permanently. Every process described here is designed to be replicated on any platform that supports the same workflows.

## Prerequisites

### GitHub account

All TW3 activity currently happens on GitHub. You need an account to participate in discussions, file issues, submit code, and earn contribution tokens.

### TW3 profile (optional)

A TW3 profile is **not required to contribute**. Anonymous contributions are welcome — if you have a GitHub account, you can participate in discussions, file issues, and submit code without linking a wallet.

However, to **receive token rewards**, you need to link your GitHub identity to an Ethereum-compatible wallet. Rewards are tracked by GitHub account regardless of profile status, so you can contribute now and claim later by creating a profile at any time. Nothing is lost.

To set up a profile, use the [tw3-profile](https://github.com/TechnicallyWeb3/tw3-profile) repository:

1. **Fork** the `tw3-profile` repo to your own GitHub account.
2. **Edit** your profile with your wallet address and a wallet signature (the signature proves you control the address and prevents unauthorized claims).
3. **Customize** optional details — display name (defaults to your GitHub username), profile image (defaults to your GitHub avatar), bio (defaults to your GitHub bio).
4. **Submit** your fork. The signed data in your profile serves as your identity claim.

The profile repo includes tooling to connect a hot or cold wallet for signing. Early versions may use local signing (`.env`-based private keys or mnemonics); future versions will support browser-based wallet connections to avoid private key exposure.

### Future: on-chain identity registry

The long-term goal is the [git-registry](https://github.com/TechnicallyWeb3/git-registry) project — a decentralized social consensus registry that lives on-chain:

1. A contributor requests to associate their wallet with their GitHub ID.
2. Community validators issue challenges and verify the claim through signed proof repos.
3. The wallet with the most validator signoffs is considered the consensus owner.
4. Validators earn tokens for registrations. False claims are challenged via a stake-based mechanism.

The `tw3-profile` fork-and-edit system serves as the bridge until the on-chain registry is operational. Profile data will migrate to the registry contract when it launches — no contributor loses their history.

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
