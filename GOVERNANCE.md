# TW3 Governance

This document defines how decisions are made within TW3 and TW3-aligned DAOs. It builds on the roles and relationships defined in [STRUCTURE.md](STRUCTURE.md) and serves the principles established in [PHILOSOPHY.md](PHILOSOPHY.md).

Where a governance mechanic produces outcomes that contradict the philosophy, the mechanic must change.

## Voting model

Every participant's vote is counted individually. There are no bloc votes where a group decides internally and casts a single group-level decision. Each person's vote carries weight proportional to their standing within each group they belong to, and each group's total weight is equal to every other group's total weight.

### How it works

If a DAO has three groups — users, contributors, and investors — each group contributes one-third of the total vote weight. Within each group, individuals are weighted proportionally: a user who accounts for 10% of total user value holds 10% of that group's one-third share. A contributor with 25% of total soul-bound tokens holds 25% of the contributor group's one-third share.

All individual weighted votes are summed into a single final tally. The result is a true community-wide decision where every voice counts, but no single group can dominate because group weights are equal regardless of how many people or how much capital exists in each group.

### Multi-role voting

Participants who qualify in multiple groups vote in each one. A contributor-investor casts a weighted vote in the contributor group and a separate weighted vote in the investor group. This is permitted because group totals are structurally equal — holding positions in multiple groups does not break the balance.

## Proposal tiers

All governance actions fall into one of two tiers:

### Supermajority (default)

Every action starts here. A supermajority requires a higher threshold of approval (the specific percentage is set by the community's initial governance parameters and can be amended by supermajority vote). This is the default for all decisions until the community explicitly moves a category of action to simple majority.

Actions that permanently require supermajority:
- Amendments to governance rules
- Changes to the voting model or group structure
- Modifications to the supermajority threshold itself

### Simple majority

The community can vote (by supermajority) to move specific categories of action to simple majority for routine decisions. Examples of actions that may be candidates for simple majority over time:
- Standard treasury expenditures below a community-set threshold
- Routine admin elections
- Approval of new project repos from discussions that have met the support threshold

The decision to move an action category from supermajority to simple majority is itself a supermajority vote, ensuring that lowering the bar for any decision type is a deliberate, broadly supported choice.

## Proposal process

### Standard proposals

1. A community member opens a GitHub Discussion using the standard proposal format, describing the action, its rationale, and its expected impact.
2. Discussion takes place off-chain (GitHub) to allow deliberation before commitment.
3. When the proposer believes the discussion has matured, they submit the proposal for on-chain vote.
4. The voting period opens. The proposal passes or fails based on the applicable tier threshold and quorum requirements.
5. If passed, execution follows — on-chain actions execute automatically via smart contract where possible; off-chain actions (like repo creation) are carried out by admins in accordance with the vote result.

### Urgent proposals

Leaders or admins may designate a proposal as urgent when operational necessity requires a shorter decision window. Urgent proposals carry a 48-hour voting period instead of the standard period.

To prevent abuse, the community can challenge urgent designation. If a challenge reaches a community-defined threshold of support, the proposal reverts to the standard voting period. Repeated misuse of urgent designation is grounds for admin accountability proceedings.

### Governance proposals

Any proposal that amends governance rules, the voting model, group structure, or the supermajority threshold requires:
- Supermajority approval
- A 30-day voting period
- Standard quorum (or higher, if the community sets a separate governance quorum)

The extended period ensures the community has adequate time to deliberate on changes that affect the system itself.

## Voting periods

| Proposal type | Duration | Who may initiate |
|---|---|---|
| Standard | Community-set default (initially 7 days) | Any member |
| Urgent | 48 hours | Leaders or admins |
| Governance change | 30 days | Any member |

All durations are adjustable by governance proposal at the appropriate tier.

## Quorum

A vote is valid only if participation meets or exceeds the minimum quorum threshold. If quorum is not met, the vote fails regardless of the outcome among those who did participate.

The quorum threshold is set by governance proposal and can be adjusted as the community grows. Different proposal types may have different quorum requirements if the community chooses to set them.

Low participation is a signal. If proposals consistently fail to meet quorum, it indicates either community disengagement or an unrealistic threshold — both are problems that governance should address rather than ignore by lowering standards silently.

## Deadlock resolution

True deadlocks — an exactly even split — are rare under weighted individual voting but possible. When a vote concludes within a margin too close to call (the exact threshold is a governance parameter), the following resolution process applies:

1. The vote is recalculated per group. Each group's internal majority determines that group's position.
2. If a group itself is internally deadlocked, the group's leader (top performer as defined in [STRUCTURE.md](STRUCTURE.md)) casts the deciding vote for that group.
3. The per-group positions are tallied. With an odd number of groups, resolution is guaranteed.

If the DAO uses an even number of groups and the per-group tally is itself tied, leaders from each group vote sequentially — the first three to establish a majority determine the outcome.

## Admin elections

Admins are elected on-chain by the full community using the standard voting model (individual weighted votes, equal group weight). Admin elections follow the proposal tier that the community has assigned to them — supermajority by default, potentially simple majority if the community votes to move them there.

### Election triggers

- Scheduled elections at community-defined intervals
- A removal proposal initiated by any community member (follows standard proposal process)
- Voluntary resignation by the admin

### Accountability

Admins hold operational power — what gets merged, what repos are created, what standards are enforced. This power is delegated by the community and revocable by the community.

If an admin acts against TW3 principles or the community's expressed will:
- Any member can submit a removal proposal
- The community votes using the standard model
- Consequences may range from loss of specific privileges to full removal, as the community decides

Admins who are removed do not lose their contributor status or accumulated soul-bound tokens. The admin role is a responsibility, not an identity.

## Treasury

### Revenue sources

- **Core project revenue** — all internal TW3 projects that generate revenue feed into the TW3 treasury.
- **Token minting** — investors deposit capital to the treasury in exchange for newly minted economic tokens (see Token Minting below).
- **Other sources** — donations, grants, or other income streams as they arise.

### Expenditures

Treasury funds are deployed through governance proposals. Categories of spending include:
- **Operational costs** — infrastructure, hosting, domains, tooling.
- **Investment in sovereign projects** — community-approved capital deployment to aligned external projects.
- **Bounties and grants** — incentive programs for specific work the community wants done.
- **Investor yield** — economic token holders earn yield from platform revenue, distributed according to the DAO's revenue model.

The specific thresholds for spending authority (e.g., small operational expenses vs. major investments) are governance parameters set by the community.

## Token minting

Economic tokens enter circulation through two paths:

### Contributor mining

Contributors earn economic tokens through labor. The rate at which tokens are earned relative to work performed is a governance parameter. This is the primary source of new tokens and ensures that the people who build the project hold the largest initial economic stake.

### Investor minting

Investors mint new economic tokens by depositing capital directly to the treasury. This allows the project to raise funds for expenses (domains, hosting, vendor costs) independently from contributor labor.

The recommended pricing mechanism is a bonding curve — an automated function where the mint price increases as more tokens are minted. This is self-regulating: early investors get lower prices (compensating for higher risk on an unproven project), later investors pay more (reflecting lower risk on a proven project). No oracle or external market is required.

As a project matures and its economic token trades on decentralized exchanges, the minting mechanism can migrate from a bonding curve to oracle-based market pricing through a governance proposal.

### Minting safeguards

- **Rate caps** — maximum tokens minted per time period, preventing supply flooding.
- **Curve parameters set by supermajority** — existing token holders must approve the terms under which their stake is diluted.
- **Treasury-direct** — minted funds go to the project treasury, never to individuals.
- **Optional vesting** — the community may impose a vesting period on minted tokens to prevent buy-and-dump behavior.

Minting parameters (curve shape, rate caps, vesting terms) are governance parameters adjustable by supermajority vote.

## On-chain governance

TW3 aims to maximize on-chain governance for transparency, auditability, and trustlessness.

### On-chain

- All votes (standard, urgent, governance)
- Admin elections and removal
- Treasury disbursement and token minting
- Proposal ratification

### Off-chain with on-chain integration goals

- Contribution tracking (GitHub activity, pull requests, code reviews) — currently off-chain, with a goal of building tools to bring contribution data on-chain via oracles or direct integration. This tooling is itself a TW3 project that can serve other DAOs.
- Content creation tracking (uploads, posts, engagement) — similarly off-chain with on-chain integration as a goal.

### Off-chain

- Discussions and deliberation (GitHub Discussions)
- Informal coordination and community communication

Admins are responsible for ensuring that off-chain actions faithfully reflect on-chain vote outcomes. An admin who fails to execute an on-chain decision off-chain (e.g., refuses to merge an approved PR or create an approved repo) is subject to accountability proceedings.

## Governance amendments

The rules in this document are not permanent. They are the community's best current attempt at fair governance and are expected to evolve.

Amendments to this document require:
- A governance proposal following the standard process
- Supermajority approval
- 30-day voting period
- Standard quorum or higher

No amendment may contradict [PHILOSOPHY.md](PHILOSOPHY.md). If a proposed governance change conflicts with the philosophy, the proposal must either be revised to align or the community must first amend the philosophy itself — which is the highest-bar decision TW3 can make and should be treated accordingly.

### Hierarchy of authority

1. **[PHILOSOPHY.md](PHILOSOPHY.md)** — source of truth, highest authority
2. **[STRUCTURE.md](STRUCTURE.md)** — defines the pieces, implements the philosophy
3. **This document (GOVERNANCE.md)** — defines the mechanics, implements the structure
4. **Smart contracts and code** — implements the governance

If any lower layer conflicts with a higher layer, the lower layer must change.

---

Initial governance parameters (quorum thresholds, voting periods, supermajority percentages, minting curve parameters, and spending tiers) will be set by the founding community and ratified through the first round of on-chain governance votes. These initial values are starting points, not permanent fixtures.
