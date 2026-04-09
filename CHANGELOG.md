# Changelog

All notable changes to the TW3 DAO organizational repository will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Added

- admin.config.json — machine-readable admin roster with term length, permissions, and election dates
- ADMIN_ELECTIONS.md — interim GitHub-based admin election process: nomination via [ADMIN] issues, acceptance, reaction-based voting, PR ratification, term and re-election rules
- ADMIN_RESPONSIBILITIES.md — operational responsibilities for TW3 admins: branch promotion thresholds, version management, farming detection, onboarding checklist, self-approval rule, reward hold period, steward actions
- governance.config.json — machine-readable governance parameter values (branch thresholds, voting periods, reward hold, support threshold, supermajority)
- CODING.md — coding standards for all TW3 projects (Solidity, TypeScript, general principles)
- .github/REPO_SETUP.md — admin checklist for initializing new TW3 repositories

### Changed

- CONTRIBUTING.md — replaced git-registry prerequisite with tw3-profile fork-and-edit workflow as the current identity method; moved git-registry to future roadmap section; added note clarifying GitHub as the current operational medium; clarified that profiles are optional and anonymous contributions are allowed with deferred reward claims

## [0.2.0] - 2026-04-07

### Added

- CONTRIBUTING.md — universal contributing guide for all TW3 repos
- RATE_SCHEDULE.md — governance-adjustable token reward rates per contribution type
- .github/PULL_REQUEST_TEMPLATE.md — standard PR template
- .github/ISSUE_TEMPLATE/bug_report.md — bug report template
- .github/ISSUE_TEMPLATE/feature_request.md — feature request template
- .github/DISCUSSION_TEMPLATE/project-proposal.md — standard project proposal format
- .github/DISCUSSION_TEMPLATE/governance-proposal.md — governance proposal format

## [0.1.0] - 2026-04-07

### Added

- PHILOSOPHY.md — core beliefs, values, and principles (source of truth)
- POSTULATES.md — ten community-ratified axioms formalizing TW3 principles
- STRUCTURE.md — roles, token model, project types, lifecycle, and structural principles
- GOVERNANCE.md — voting model, proposal tiers, treasury, admin elections, amendments
- TOKENOMICS.md — dual-token model, halving schedule, bonding curve, liquidity phases, yield, fork transitions
- README.md — companion documents table linking all organizational docs
- LICENSE — AGPL-3.0

### Changed

- Cross-document consistency review: unified hierarchy of authority across POSTULATES, GOVERNANCE, and TOKENOMICS; added TOKENOMICS to all hierarchy listings; fixed STRUCTURE investor paths; corrected typos
