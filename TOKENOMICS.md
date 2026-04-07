# TW3 Tokenomics

This document defines the economic model for TW3 — how tokens are created, distributed, valued, and how they flow between participants. It serves the principles in [PHILOSOPHY.md](PHILOSOPHY.md) and [POSTULATES.md](POSTULATES.md), implements the roles defined in [STRUCTURE.md](STRUCTURE.md), and operates under the mechanics defined in [GOVERNANCE.md](GOVERNANCE.md).

The specific rate schedule (points per action) is maintained separately as a governance-adjustable parameter set. This document defines the economic system; the rate schedule sets the dials.

## Two tokens, one supply

TW3 uses a dual-token model built on a shared supply cap:

- **Soul-bound contribution tokens** — non-transferable, permanent record of labor. Determine voting weight in the contributor group. Cannot be bought, sold, or transferred.
- **Economic tokens** — liquid, transferable, represent ownership stake in the project's economic output. Holders earn yield from platform revenue. These create the investor market.

Both tokens share a total supply of **20.48M** (a power of 2 for clean halving, a nod to Bitcoin's 21M). Both follow the same halving schedule. When a contributor earns soul-bound tokens for their work, they earn a corresponding amount of economic tokens at the same decaying rate.

## Halving model

Token emission follows a halving schedule that ensures practically unbounded longevity.

### How it works

The total supply is divided into halving cycles. Each cycle makes available half of the remaining unminted supply. When a cycle is exhausted, the reward rate decays to 10% of the previous rate — not 50% as in Bitcoin's model, but a sharper decay that dramatically extends the tail.

| Cycle | Tokens available | Reward rate | Cumulative effort multiplier |
|---|---|---|---|
| 1 | 10.24M | Base rate | 1x |
| 2 | 5.12M | Base rate ÷ 10 | 5x cumulative effort vs. cycle 1 |
| 3 | 2.56M | Base rate ÷ 100 | 25x |
| 4 | 1.28M | Base rate ÷ 1,000 | 125x |
| 5 | 0.64M | Base rate ÷ 10,000 | 625x |
| ... | ... | ... | ... |

Each halving cycle requires approximately 5x the cumulative effort of the previous cycle. By the final cycles, the activity required to mine the remaining tokens exceeds what any plausible community could generate — the supply is effectively inexhaustible while remaining technically finite.

### Why this matters

The halving model rewards early contributors more generously per unit of work. This is fair: early participation carries higher risk (unproven project, no users, no revenue) and deserves higher compensation. As the project matures and risk decreases, new contributors earn fewer tokens per contribution — but those tokens are worth more because the project is established.

The compounding scarcity works on two axes: contributors earn **fewer tokens** over time (halving decay) while the tokens they earn are **worth more** (bonding curve / market appreciation). Both axes reward early risk-taking.

### Governance adjustability

Both the current reward rate and the decay rate (the 10x divisor) are governance parameters. If the community finds that contributor incentives are insufficient — too hard to attract new contributors at the current rate — they can propose adjustments. A smaller decay rate (e.g., ÷4 instead of ÷10) would make later cycles more rewarding. A larger one would extend longevity further.

The halving schedule is a starting point designed for long-term sustainability, not a permanent fixture.

## Contributor mining

Contributors earn both token types through labor. Every qualifying action — merged code, reviewed pull requests, filed issues, started discussions, uploaded media, admin work — earns tokens according to the rate schedule and the current halving cycle.

### Dual earning

When a contributor earns soul-bound tokens for a contribution, they simultaneously earn economic tokens at the same rate. Both token types follow the same halving decay. This means contributors are always earning governance voice (soul-bound) and economic stake (economic tokens) in parallel.

### Admin and reviewer rewards

Admins who review, test, and approve contributions earn tokens for that work. If an admin requests changes to a contribution (e.g., adding lines, optimizing media), the additional work required shifts token value from the original contributor to the admin proportionally. This incentivizes thorough review — admins earn more when they improve contributions, not just rubber-stamp them.

### Challenge period

All token rewards are subject to a 7-day hold after the qualifying action (PR merge, discussion creation, issue resolution, etc.). During this period, any community member can issue a challenge — disputing the quality, validity, or alignment of the contribution.

Challenges require a stake to discourage frivolous disputes. If the challenge succeeds (determined by community review), the contribution's tokens are not awarded. If the challenge fails, the challenger's stake is forfeit. The specific stake amount and review process are governance parameters.

This hold applies to all token-earning actions: code contributions, media uploads, discussions, issues, reactions, and admin reviews.

## Economic token distribution

Economic tokens reach participants through three channels:

### 1. Contributor mining (primary)

Contributors earn economic tokens through labor, as described above. This is the primary source of new tokens and ensures that builders hold the largest initial economic stake.

Contributors may hold their economic tokens (retaining yield and investor-group voting weight), sell them to investors on the open market, or stake them for enhanced yield.

### 2. Investor minting (secondary)

Investors mint new economic tokens by depositing capital (e.g., USDC) to the treasury. This channel exists so projects can raise funds for operational expenses independently from contributor labor.

Investor minting uses a bonding curve — an automated pricing function where the mint price increases as more tokens are minted. However, **contributor sales are prioritized**: if contributors are selling economic tokens at or below the bonding curve price, investor demand is matched against contributor supply first. New tokens are minted only when demand exceeds available contributor supply. This ensures contributors can realize value from their tokens before dilutive minting occurs.

### 3. Secondary market

Once a liquidity pool is deployed (see Liquidity Phases below), economic tokens trade freely on decentralized exchanges. This is not a distribution channel — no new tokens are created — but it is how most participants will acquire tokens after the early stages.

## Bonding curve

The bonding curve is the pricing mechanism for investor minting during the pre-market phase.

### Properties

- **Monotonically increasing** — the price per token rises as more tokens are minted. Early investors pay less (higher risk), later investors pay more (lower risk).
- **Automated** — no governance vote is needed per mint. The curve executes trustlessly on-chain.
- **Treasury-direct** — all capital deposited through the curve goes to the project treasury. No individual receives minting proceeds.
- **Parameterized** — the curve's shape (linear, polynomial, logarithmic) and steepness are governance parameters set by supermajority vote.

### Safeguards

- **Rate caps** — maximum tokens minted per time period, preventing supply flooding.
- **Curve parameters set by supermajority** — existing holders must approve the terms of their own dilution.
- **Optional vesting** — the community may impose a lock-up period on minted tokens to prevent buy-and-dump.

## Liquidity phases

The economic token's market lifecycle follows three phases:

### Phase 1 — Bonding curve only

Before meaningful liquidity exists, the bonding curve is the sole mechanism for investor minting. Contributors mine tokens through labor and can sell peer-to-peer. The curve establishes a floor price and provides initial price discovery.

### Phase 2 — LP deployment

When the community determines there is sufficient liquidity and demand, it votes (via governance proposal) to deploy a liquidity pool on a decentralized exchange. The proposal specifies:
- How much treasury capital enters the pool
- Which trading pair (e.g., ECONOMIC/USDC)
- Which DEX and pool configuration
- Whether the bonding curve continues or is sunset

The recommended path is to **sunset the bonding curve** at LP deployment. Running both creates arbitrage opportunities that can drain the treasury. Once there is an active market, the market sets the price.

### Phase 3 — Protocol-owned liquidity

LP tokens are held by the treasury and governed by the DAO. They are never distributed to individuals. The community can vote to add or remove liquidity, but no individual can unilaterally withdraw it.

This ensures permanent, stable liquidity that doesn't depend on external liquidity providers who could pull out at any time.

Constraints on LP deployment (all governance-adjustable):
- Minimum treasury reserve before LP is votable (don't put the last dollar in the pool)
- Maximum percentage of treasury in the LP
- LP token governance rules

## Yield distribution

Revenue from TW3 projects flows to the treasury. The treasury distributes yield to economic token holders according to governance-set parameters.

### Initial allocation

- **25% of revenue** — distributed as yield to economic token holders, proportional to holdings.
- **Remaining 75%** — retained by the treasury for operational costs, investment, bounties, and reserves.

These percentages are governance-adjustable. Different TW3-aligned DAOs may set different allocations appropriate to their revenue model.

### Staking bonus

Economic token holders who stake their tokens earn a higher yield rate than passive holders. Staking is required for governance participation, but the enhanced yield provides an additional incentive — rewarding those who commit their capital to the project's governance rather than just extracting passive returns.

The staking yield multiplier is a governance parameter.

### TW3-specific considerations

TW3 itself, as a GitHub-based community with no direct revenue stream, does not currently generate revenue to distribute. For TW3 specifically:
- Yield comes from treasury appreciation (investment returns, project revenue from core projects)
- The community may propose airdrops, bonuses, or other value distributions to contributors
- Economic tokens still represent ownership stake and governance voice even without immediate yield
- As TW3 builds revenue-generating core projects (tools, services, infrastructure), those revenues feed the treasury and enable yield distribution

## Token scope

### TW3 token

A single TW3 economic token covers all repositories under the tw3-dao GitHub organization. Contributing to any TW3 core project earns TW3 tokens. There is no per-project token within the TW3 organization.

### Sovereign project tokens

Each TW3-aligned sovereign project deploys its own token with its own supply, halving schedule, and parameters. TW3 tokens and sovereign project tokens are separate assets.

### Cross-project economics

- **TW3 invests outward** — TW3 can purchase sovereign project tokens from its treasury, participating as an investor in aligned projects. This is governed by the standard proposal process.
- **Projects invest inward** — sovereign projects can purchase TW3 tokens from their own treasury, stake them, and participate in TW3 governance. They can also contribute to TW3 packages and earn contribution tokens.
- **Shared participants** — individual community members may hold tokens in both TW3 and sovereign projects. Since many TW3 members will be involved in sovereign projects, there is natural alignment of interests through overlapping stakeholders.

## Fork transitions

When a TW3 project forks into a sovereign DAO, the token transition follows these principles:

### Soul-bound tokens

Soul-bound contribution tokens are a permanent, immutable record. They are never burned, transferred, or destroyed. The fork takes a **snapshot** of the soul-bound token distribution at fork time and uses that as the basis for initial token distribution in the new project. Contributors do not need to take any action — the public record speaks for itself.

### Economic tokens

Economic tokens remain in the original project. They do not transfer to the fork. Contributors who hold economic tokens in the original project keep them. If they want economic stake in the fork, they contribute to the fork (earning new tokens through labor) or invest in it (purchasing the fork's native token).

### Why no burn-and-claim

A burn mechanism — where contributors destroy original-project tokens to receive fork tokens — creates an attack vector. Any project can fork the code, deploy a burn contract, and invite contributors to destroy real tokens for potentially worthless ones. There is no trustless way to distinguish a legitimate fork from a scam fork at the contract level.

The snapshot model eliminates this risk entirely. Forks honor contribution history by reading the public record. No one is asked to make a destructive choice.

### Disclosure

A fork that builds on TW3 work must credit the original contributors. A fork that fails to honor the contribution history of the pre-fork project — or misrepresents its relationship to the original — is acting against TW3 principles and should not receive TW3 support.

## Post-mining incentives

As halving cycles progress and per-contribution token rewards approach negligible amounts, the incentive model shifts from mining rewards to other value sources:

- **Yield from economic tokens** — if the project is successful, holding economic tokens produces ongoing yield from platform revenue.
- **Token appreciation** — fewer new tokens entering circulation means existing tokens may appreciate in value.
- **Governance voice** — soul-bound tokens still provide governance influence regardless of mining rewards.
- **Treasury-funded bounties** — the community can direct treasury funds toward specific work, compensating contributors directly rather than through mining.
- **Intrinsic value** — contributors who use the project they build have a direct interest in its quality and survival.

The transition from mining-heavy to yield-heavy incentives is gradual and tracks the project's maturity. Early-stage projects need generous mining rewards to bootstrap. Mature projects sustain themselves through the value they generate.

---

Token parameters (supply cap, halving divisor, reward rates, bonding curve shape, yield allocation, staking multiplier, challenge stake amounts, and LP constraints) are governance-adjustable through the processes defined in [GOVERNANCE.md](GOVERNANCE.md). The values described in this document are initial recommendations, not permanent constants.
