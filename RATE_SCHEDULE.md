# TW3 Rate Schedule

This document defines the token reward rates for contributions to TW3 projects. All values follow the halving schedule described in [TOKENOMICS.md](TOKENOMICS.md) — the rates listed here are **base rates** for halving cycle 1. Each subsequent cycle applies the decay divisor to these values.

All rates are governance-adjustable. The community can propose changes through the standard governance process defined in [GOVERNANCE.md](GOVERNANCE.md). The long-term goal is to store these values in a DAO config smart contract so adjustments take effect on-chain without manual document updates.

## How rewards work

Every qualifying action earns a base point value. Points map 1:1 to both soul-bound contribution tokens and economic tokens (for contributor-class actions). The current halving cycle's decay rate is applied to the base value to determine the actual tokens minted.

Actions marked with **[U]** count toward usage votes (user group voice). Actions marked with **[C]** count toward contribution points (contributor group voice and economic tokens). Some actions count as both.

## Discussions

| Action | Base points | Type | Notes |
|---|---|---|---|
| Upvote a discussion | +1 | [U] | |
| Comment on a discussion | +2 | [U] | |
| Start a discussion | +3 | [U][C] | +1 per upvote received; +2 per comment received |
| Discussion accepted to repo | +100 | [U][C] | +2 per star; +5 per fork |

## Issues

| Action | Base points | Type | Notes |
|---|---|---|---|
| React to an issue comment | +1 | [U] | |
| Comment on an issue | +3 | [U] | +1 per reaction received |
| Start an issue | +6 | [U][C] | +1 per reaction received; +3 per comment received |
| Issue resolved (reporter credit) | +200 | [U][C] | Awarded to the issue author when the fix is merged |

## Code contributions

| Action | Base points | Type | Notes |
|---|---|---|---|
| Per line change (merged PR) | +50 | [C] | Must follow coding practices; earned by contributor |
| Per line change (admin review) | +50 | [C] | Earned by the approving admin |

When an admin requests changes to a PR:
- The contributor earns points for their original work.
- The admin earns points for the additional lines/changes they required.
- If a commit was 10 lines and the admin requests 5 additional lines, the contributor earns 500 (10 lines x 50) and the admin earns 250 (5 lines x 50) plus their standard review allocation.

## Media contributions

| Action | Base points | Type | Notes |
|---|---|---|---|
| Per MB of media (merged PR) | +100 | [C] | Must follow media guidelines |
| Per KB of optimized media (admin review) | +1 | [C] | Earned by admin when suggesting media optimization |

When an admin suggests media optimization:
- If the admin's suggestion reduces file size by 50 KB, the admin earns 50 points for the optimization work.
- The contributor retains their points for the original media submission.

## Reward calculation example

In halving cycle 1 (base rate):
- A contributor merges a PR with 20 line changes → 20 x 50 = **1,000 soul-bound tokens + 1,000 economic tokens**
- The reviewing admin approved with no changes requested → admin earns review points for the 20 lines = **1,000 soul-bound tokens + 1,000 economic tokens**

In halving cycle 2 (base rate ÷ 10):
- The same 20-line PR → 20 x 5 = **100 soul-bound tokens + 100 economic tokens**
- Same admin review → **100 soul-bound tokens + 100 economic tokens**

## What counts as a line change

- Added lines count.
- Deleted lines count.
- Modified lines count as one change (not an add + delete).
- Empty lines, comments-only changes, and whitespace-only changes do not count.
- Auto-generated code does not count.
- The specific rules for what constitutes a qualifying line change will be refined in [CODING.md](CODING.md).

## Challenge period

All rewards in this schedule are subject to the 7-day challenge period described in [CONTRIBUTING.md](CONTRIBUTING.md) and [TOKENOMICS.md](TOKENOMICS.md). Tokens are not minted until the hold period completes without a successful challenge.

## Governance adjustability

Every value in this document is a governance parameter. The community can propose changes to:
- Individual action point values
- The halving decay divisor (currently ÷10 per cycle)
- Which actions qualify for usage vs. contribution credit
- Admin review reward calculations
- What counts as a qualifying line change or media contribution

Changes to the rate schedule follow the standard governance proposal process. The intent is to eventually store all rate parameters in a DAO config smart contract, making adjustments automatic upon proposal approval.

---

For the full token model, see [TOKENOMICS.md](TOKENOMICS.md). For how to earn these rewards, see [CONTRIBUTING.md](CONTRIBUTING.md).
