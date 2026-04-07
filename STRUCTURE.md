# TW3 Structure

This document defines the roles, relationships, and project types that make up TW3 and the DAOs it supports. It describes *what the pieces are* — how decisions are made with those pieces is covered in [GOVERNANCE.md](GOVERNANCE.md).

Everything here implements the [Philosophy](PHILOSOPHY.md) and the [Postulates](POSTULATES.md). Where a structural detail conflicts with either, the higher-authority document wins.

## Three types of value

Every project receives value in three forms:

- **Labor** — people who build the project (code, content, operations, maintenance)
- **Capital** — people who fund the project (purchasing tokens, hiring contributors)
- **Usage** — people who sustain the project by being the market (paying for services, consuming content)

These three value types are the foundation of every role in a TW3-aligned DAO. A healthy project needs all three. No single type outranks another — they are structurally equal in collective voice.

## Roles

### Users

Users sustain the project by being the market. They are the people who pay for services or consume the product. Without users there is no revenue, no adoption, and no reason for the project to exist.

User voice is proportional to value provided. A user who has spent significant resources on a platform over time has earned a larger voice than a new arrival — but that voice dilutes as the user base grows. No early user retains permanent outsized influence simply for being early.

To prevent sybil attacks, user identity must be verified through mechanisms appropriate to the project — paid account history, identity verification, or other means that ensure one person equals one voice within the user group.

### Creators

Creators occupy a hybrid role. They provide labor (content that makes the platform valuable) and they sustain the market (their presence attracts users). A musician uploading a catalog to a streaming platform, an artist posting work to a social platform, a developer starting a discussion in TW3 — these are all creators.

Because creators provide both labor and usage, they hold voice in two groups: they count as users *and* as contributors. They earn soul-bound contribution tokens that reflect their labor but do not earn economic tokens the way code contributors do. Instead, creators are compensated directly by the platform's revenue model — the terms of which are set by the DAO.

Creators can choose to become investors by purchasing economic tokens with their own earnings, but this is a separate voluntary decision, not an automatic entitlement.

### Contributors

Contributors build the project. They write code, review pull requests, maintain infrastructure, manage operations, and do the work that makes the platform function.

Contributors earn two types of tokens:

- **Soul-bound contribution tokens** — non-transferable, represent the contributor's cumulative labor. These determine voting weight within the contributor group and cannot be bought or sold.
- **Economic tokens** — liquid, transferable, represent an ownership stake in the project's economic output. Holders of economic tokens earn yield from platform revenue. These tokens are what create the investor market: contributors can sell them to outside parties, converting their labor into capital.

Because contributors hold economic tokens, they naturally have standing in both the contributor and investor groups. This dual role is intentional — the people who build the project should own the largest share of it.

Contributor voice dilutes as more contributors join. An early contributor who wrote half the original codebase does not retain half the contributor vote forever. As the project grows, influence spreads. This is by design.

### Investors

Investors fund the project by acquiring economic tokens. There are three paths:

1. **Buy economic tokens** from contributors who choose to sell them.
2. **Hire contributors** — pay their salary, receive their economic tokens and contribution points. This is contributing through enterprise: the investor funds the labor and receives the tokens that labor earns.
3. **Mint new tokens** — deposit capital directly to the treasury in exchange for newly minted economic tokens, priced by a bonding curve. See [TOKENOMICS.md](TOKENOMICS.md) for the full minting model.

Investors must stake their tokens to participate in governance. Staked tokens cannot be transferred until the vote they are committed to is resolved, preventing manipulation through vote-and-sell tactics.

Investor voice is weighted by staked amount. But because the investor group's collective voice is equal to every other group's collective voice, no amount of capital can buy majority control over a project. An investor who holds 90% of all economic tokens still only controls a fraction of one group's vote.

### Role overlap summary

Not every participant fits neatly into one category. The overlap model:

| You are a... | You vote as... | You earn... |
|---|---|---|
| User | User | Usage-proportional voice |
| Creator | User + Contributor | Soul-bound tokens + direct platform revenue |
| Contributor | Contributor + Investor | Soul-bound tokens + economic tokens |
| Investor | Investor | Yield from economic tokens |

A single person can qualify as a user, creator, contributor, and investor simultaneously. They vote in every group they legitimately belong to. This is permitted because all groups carry equal collective weight — holding positions in multiple groups does not grant disproportionate power, and attempting to prevent it would only incentivize sybil workarounds that are worse than the overlap itself.

The one restriction: a person cannot serve as leader in more than one group.

## Leaders

Leaders are not elected. They are identified by performance — the top contributor by soul-bound tokens, the top investor by staked amount, the top user by cumulative value provided.

Leaders hold no voting power during normal operations. They are activated only during deadlocks, where their role is to resolve a decision that the broader groups could not. The specific mechanics of deadlock resolution are defined in [GOVERNANCE.md](GOVERNANCE.md).

Each role has one leader. A person who qualifies as leader in multiple roles must be assigned to only one — the specific rules for this are a governance concern.

## Admins

Admins are contributors with elevated operational responsibilities: managing repositories, reviewing and merging pull requests, creating project repos from approved discussions, and enforcing quality and alignment standards.

Admins are elected by the full community and can be removed by community vote. They are not a separate stakeholder group. They vote as contributors. Their admin role is a responsibility the community grants and revokes — not a power base, not a political class, not a board of directors.

Admin work (reviewing code, maintaining repos, managing operations) earns contribution tokens like any other labor. The role is compensated through the same system that rewards all contributors.

If an admin merges work that contradicts TW3 principles or a project's values, they are accountable to the community. Consequences are determined case by case and may include loss of admin privileges, re-election, or other measures the community deems appropriate.

## Project types

### TW3 core projects

Projects born from TW3 discussions, hosted under the TW3 GitHub organization, and governed by the TW3 community. TW3 itself — its tools, website, infrastructure, and DAO mechanisms — is the first core project.

Core projects follow TW3 structural requirements directly. Their governance, roles, and token model operate under TW3 community oversight.

### Sovereign projects

Independent DAOs that follow TW3 principles but govern themselves. A sovereign project may have originated in TW3 discussions, been forked from a TW3 core project, or been built entirely outside TW3.

TW3 does not own sovereign projects. It can invest in them through community vote, but investment does not necessicarily grant TW3 governance authority above any other investor. The project must meet TW3 structural requirements to qualify for support, but how it implements those requirements is its own decision.

Past support does not guarantee future support. Each request for TW3 investment is evaluated on its current alignment with TW3 principles.

### Forks

Forks are a legitimate and expected outcome of community disagreement. When a subset of a project's community believes the project has drifted from its values or that a better direction exists, they fork the codebase and build their own version.

A fork that better aligns with TW3 values should attract TW3 support accordingly. A fork that abandons DAO structure or violates TW3 principles will not receive TW3 support regardless of its origin.

## Project lifecycle

1. **Discussion** — Any TW3 member opens a GitHub Discussion describing the project idea using the standard proposal format.
2. **Support threshold** — The idea reaches a community-defined support threshold (initially ~10% of active members; adjustable by community governance). This signals genuine interest, not unanimous approval.
3. **Repo creation** — An admin creates the project repository under the TW3 organization.
4. **Development** — Contributors build. The project operates under TW3 structure with the roles and token model appropriate to its domain.
5. **Maturity and sovereignty** — If a project grows beyond TW3's scope or the community decides it should govern itself independently, it can fork into its own sovereign DAO. This is not abandonment — it is the intended path for successful projects.

Projects that do not reach the support threshold are not dead. A subcommunity that believes in the idea can fork the discussion into their own DAO, build the project independently, and later seek TW3 support as a sovereign project if it matures and aligns with TW3 principles.

## External projects joining TW3

A project not born in TW3 can seek alignment through two paths:

1. **Sovereign alignment** — Deploy as an independent DAO following TW3 principles and request community investment through the standard proposal process.
2. **Core integration** — Open a discussion to become a TW3 core project. The standard path is for TW3 admins to fork the repository into the TW3 organization. Transfer of ownership is available if the project owner volunteers it, but it is never required.

In both cases, the project must meet all TW3 structural requirements: fully open source, fully forkable with no proprietary dependencies, organized as a DAO with stakeholder governance.

## Maintaining alignment

For TW3 core projects: contributions that contradict TW3 principles should not be merged. Admins are the first line of enforcement and are accountable to the community for their judgment. If TW3 itself becomes compromised — if governance or code permits outcomes the [Philosophy](PHILOSOPHY.md) forbids — the philosophy is the source of truth. Systems are reformed, and if necessary, the community forks itself to preserve its principles.

For sovereign projects: alignment is verified at the point of each support request. The TW3 community evaluates whether the project's current structure, practices, and governance reflect TW3 principles. A project that was once aligned but has drifted should not receive further support until it corrects course.

## Structural principles for all TW3-aligned DAOs

Not every DAO needs to mirror TW3's exact structure. Different projects serve different domains and may require different role configurations. But every TW3-aligned DAO must satisfy these principles:

- Stakeholder groups must have **equal collective voice**. No single group dominates.
- Control **cannot be purchased**. Capital buys economic stake and yield, not governance majority.
- The project must be **fully open source** — forkable and operable without any proprietary dependency.
- The project must be governed as a **DAO** with transparent, auditable decision-making. No corporate hierarchies. No unilateral authority.
- **Power dilutes as projects grow.** Structures must ensure that the larger a project becomes, the harder it is for any single entity to control it.
- Groups must not be created to **artificially dilute or amplify** the voice of other groups.
- The number and definition of stakeholder groups is the DAO's decision, provided the above principles are met.

---

Voting mechanics, deadlock resolution, election procedures, treasury policy, and accountability processes are defined in [GOVERNANCE.md](GOVERNANCE.md). The full token model — halving schedule, bonding curve, liquidity phases, yield distribution, and fork transitions — is defined in [TOKENOMICS.md](TOKENOMICS.md).
