# Coding standards

This document defines the coding standards for all TW3 repositories. It applies universally to any project under the TW3 organization and to sovereign projects that seek TW3 alignment.

These standards exist because open-source code that anyone can fork must be code that anyone can read. If a contributor can't understand what they're forking, forkability is a fiction.

## Languages

TW3's primary languages are **Solidity** and **TypeScript**. Projects may use other languages when justified, but Solidity and TypeScript tooling, formatting, and testing requirements are non-negotiable for repos that use them.

Additional language standards can be added to this document through the standard governance proposal process as the community adopts new tooling.

## General principles

These apply regardless of language:

- **No dead code.** Don't commit commented-out blocks, unused imports, or unreachable branches. If it's not running, it's not shipping.
- **No commented-out code.** Comments explain intent, they don't preserve old implementations. Use version control for history.
- **Meaningful names.** Variables, functions, and files should describe what they represent. Abbreviations are acceptable only when universally understood (`tx`, `addr`, `msg`).
- **Single responsibility.** Functions do one thing. If a function needs an "and" in its description, split it.
- **DRY.** Don't repeat yourself. Extract shared logic into utilities or helpers. Duplication is a maintenance debt.
- **Fail explicitly.** Errors should be caught and handled with clear messages. Silent failures hide bugs that compound over time.
- **Keep functions short.** If a function exceeds ~40 lines, consider whether it's doing too much.

## Formatting and linting

### TypeScript / JavaScript

All TS/JS projects **must** include:

- **Prettier** for formatting (config committed to repo)
- **ESLint** for linting (config committed to repo)

Minimum Prettier config (`.prettierrc`):

```json
{
  "semi": true,
  "singleQuote": true,
  "trailingComma": "all",
  "tabWidth": 2,
  "printWidth": 80
}
```

Projects may extend this config but must not weaken it (e.g., disabling semicolons or trailing commas).

ESLint must extend a recognized base config (`eslint:recommended`, `@typescript-eslint/recommended`, or equivalent). Custom rules should be documented in the project README.

### Solidity

All Solidity projects **must** include:

- **solhint** for linting
- **prettier-plugin-solidity** for formatting

Minimum solhint config (`.solhint.json`):

```json
{
  "extends": "solhint:recommended",
  "rules": {
    "compiler-version": ["error", ">=0.8.0"],
    "func-visibility": ["warn", { "ignoreConstructors": true }],
    "reason-string": ["warn", { "maxLength": 64 }]
  }
}
```

### Indentation

**2 spaces** across all languages. No tabs. Configure your editor before contributing.

## Testing

Untested code is unfinished code. Every PR that introduces or modifies logic must include tests.

### Requirements

- **Solidity**: Hardhat with Chai/Mocha. Tests live in a `test/` directory at the project root.
- **TypeScript**: Vitest or Jest (project's choice, documented in README). Tests live alongside source or in a `test/` directory.
- **Coverage**: Projects should aim for meaningful coverage of business logic. 100% line coverage is not the goal — covering critical paths, edge cases, and failure modes is. Admins may reject PRs that add untested logic to critical paths.

### What to test

- Public functions and their expected return values
- Edge cases and boundary conditions
- Error handling and revert conditions (especially in Solidity)
- State transitions
- Access control (who can call what)

### What not to test

- Trivial getters/setters with no logic
- Third-party library internals
- Formatting or stylistic output

## Documentation

### TypeScript / JavaScript

Use **JSDoc** for all exported functions, classes, and interfaces:

```typescript
/**
 * Calculates the token reward for a contribution based on the
 * current halving cycle and the base point value.
 *
 * @param basePoints - Raw point value from RATE_SCHEDULE
 * @param currentSupply - Tokens already mined in this cycle
 * @returns Token amount to award
 */
export function calculateReward(basePoints: number, currentSupply: bigint): bigint {
  // ...
}
```

### Solidity

Use **NatSpec** for all public and external functions, state variables, events, and errors:

```solidity
/// @notice Registers a new contributor and links their GitHub identity to a wallet.
/// @param githubId The contributor's GitHub username hash
/// @param wallet The Ethereum address to associate
/// @dev Reverts if the GitHub ID is already registered.
function register(bytes32 githubId, address wallet) external {
    // ...
}
```

### README

Every project repository must have a README that covers:

- What the project does (one paragraph)
- How to install and run locally
- How to run tests
- Link to CONTRIBUTING.md in tw3-dao
- Any project-specific deviations from these coding standards

## File organization

### Naming conventions

Follow each language's community convention:

| Language | Files | Directories |
|---|---|---|
| TypeScript/JavaScript | `kebab-case.ts` for modules, `PascalCase.tsx` for React components | `kebab-case/` |
| Solidity | `PascalCase.sol` matching the primary contract name | `contracts/`, `interfaces/`, `libraries/` |
| Tests | Mirror source structure: `token-calc.ts` → `token-calc.test.ts` | `test/` or alongside source |

### Standard project structure

TypeScript projects:

```
src/
  index.ts
  utils/
  types/
test/
  index.test.ts
package.json
tsconfig.json
.prettierrc
.eslintrc
README.md
```

Solidity projects:

```
contracts/
  MyContract.sol
  interfaces/
  libraries/
test/
  MyContract.test.ts
scripts/
  deploy.ts
hardhat.config.ts
.solhint.json
.prettierrc
README.md
```

## Security practices

These apply primarily to Solidity but the principles extend to any code handling value or access control.

- **Check-effects-interactions pattern.** State changes before external calls. Always.
- **Reentrancy guards.** Use OpenZeppelin's `ReentrancyGuard` or equivalent on functions that transfer value.
- **Access control.** Every state-changing function must have explicit access control. No open `public` functions that modify sensitive state.
- **Integer safety.** Solidity 0.8+ handles overflow/underflow natively. For earlier versions, use SafeMath. Never assume arithmetic is safe.
- **Input validation.** Validate all external inputs. Check for zero addresses, empty arrays, overflow-prone values.
- **Avoid `tx.origin`.** Use `msg.sender` for authentication. `tx.origin` is a phishing vector.
- **Minimize `delegatecall`.** If you must use it, document exactly why and audit the target contract.
- **Events for all state changes.** Every meaningful state change emits an event. This is not optional — it's how off-chain systems and users track what happened.
- **Audit before deploy.** No TW3-aligned contract deploys to mainnet without at least one independent review. Community audit through the PR process counts for development-stage contracts.

## Dependency policy

- **Open source only.** Every dependency must be published under an open-source license. No proprietary packages, no "source available" licenses with usage restrictions.
- **Version pinning.** Lock exact versions in `package.json` (use `--save-exact`) or `package-lock.json`. Solidity imports should pin specific release tags, not branches.
- **Minimize dependencies.** Every dependency is a trust decision. Before adding one, ask: can this be written in fewer lines than the dependency's API surface?
- **Audit transitive dependencies.** Run `npm audit` (or equivalent) before merging. Known vulnerabilities in the dependency tree are blockers.
- **No proprietary build tools.** The entire build, test, and deploy pipeline must be reproducible using only open-source tooling.

## Enforcement

These standards are enforced through the PR review process. Admins must verify compliance before merging. Repeated violations without improvement may be grounds for rejecting future contributions from the same contributor until resolved.

This document is governance-adjustable. Standards can be added, modified, or relaxed through the standard proposal process described in [GOVERNANCE.md](GOVERNANCE.md).
