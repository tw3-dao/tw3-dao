# New repository setup checklist

This checklist is for TW3 admins creating new repositories under the TechnicallyWeb3 organization. Follow every step to ensure the repo is consistent with TW3 standards from the first commit.

## 1. Create the repository

- [ ] Create repo under the [TechnicallyWeb3](https://github.com/TechnicallyWeb3) GitHub org
- [ ] Set visibility to **Public**
- [ ] Initialize with a README (you'll replace the content immediately)
- [ ] Select **AGPL-3.0** license (or the license approved by governance for this project)
- [ ] Add an appropriate `.gitignore` for the project's primary language

## 2. Set up branches

Create the four long-lived branches in this order:

```bash
git checkout -b production
git push -u origin production

git checkout -b staging
git push -u origin staging

git checkout -b development
git push -u origin development
```

- [ ] `main` exists (created by default)
- [ ] `production` branch created from `main`
- [ ] `staging` branch created from `production`
- [ ] `development` branch created from `staging`
- [ ] Set `development` as the **default branch** in GitHub repo settings (Settings → General → Default branch)

## 3. Branch protection rules

Apply these rules in Settings → Branches → Add rule:

### `main`

- [ ] Require pull request reviews before merging (at least 1 approval)
- [ ] Restrict who can push (admins only, via merge from `production`)
- [ ] Do not allow force pushes
- [ ] Do not allow deletions

### `production`

- [ ] Require pull request reviews before merging (at least 1 approval)
- [ ] Restrict who can push (admins only, via merge from `staging`)
- [ ] Do not allow force pushes

### `staging`

- [ ] Require pull request reviews before merging (at least 1 approval)
- [ ] Restrict who can push (admins only, via merge from `development`)
- [ ] Do not allow force pushes

### `development`

- [ ] Require pull request reviews before merging (at least 1 approval)
- [ ] Require status checks to pass before merging (add CI checks when configured)
- [ ] Do not allow force pushes

## 4. Copy templates from tw3-dao

Copy the `.github/` templates directory from the [tw3-dao](https://github.com/TechnicallyWeb3/tw3-dao) repository:

```bash
# From the new repo root
cp -r ../tw3-dao/.github/PULL_REQUEST_TEMPLATE.md .github/
cp -r ../tw3-dao/.github/ISSUE_TEMPLATE/ .github/
cp -r ../tw3-dao/.github/DISCUSSION_TEMPLATE/ .github/
```

- [ ] `PULL_REQUEST_TEMPLATE.md` copied
- [ ] `ISSUE_TEMPLATE/bug_report.md` copied
- [ ] `ISSUE_TEMPLATE/feature_request.md` copied
- [ ] `DISCUSSION_TEMPLATE/project-proposal.md` copied
- [ ] `DISCUSSION_TEMPLATE/governance-proposal.md` copied

Modify templates if the project has specific needs, but keep the core structure intact.

## 5. Required files

Ensure these files exist at the repo root:

- [ ] **README.md** — project description, install instructions, how to run tests, link to tw3-dao CONTRIBUTING.md
- [ ] **LICENSE** — AGPL-3.0 (or governance-approved alternative)
- [ ] **CHANGELOG.md** — initialized with the [Keep a Changelog](https://keepachangelog.com/) format
- [ ] **.gitignore** — appropriate for the project's language/framework

## 6. Configure formatting and linting

Based on the project's language (see [CODING.md](https://github.com/TechnicallyWeb3/tw3-dao/blob/main/CODING.md)):

### TypeScript / JavaScript

- [ ] Add `.prettierrc` with TW3 minimum config
- [ ] Add ESLint config extending a recognized base
- [ ] Add `format` and `lint` scripts to `package.json`

### Solidity

- [ ] Add `.solhint.json` with TW3 minimum config
- [ ] Add `.prettierrc` with prettier-plugin-solidity
- [ ] Add `lint` script to `package.json`

## 7. Link to organizational docs

In the project README, include:

```markdown
## Contributing

This project follows TW3 organizational standards. See the
[CONTRIBUTING.md](https://github.com/TechnicallyWeb3/tw3-dao/blob/main/CONTRIBUTING.md)
in tw3-dao for the full contribution guide, and
[CODING.md](https://github.com/TechnicallyWeb3/tw3-dao/blob/main/CODING.md)
for coding standards.
```

- [ ] Link to CONTRIBUTING.md in tw3-dao
- [ ] Link to CODING.md in tw3-dao

## 8. Enable GitHub features

- [ ] Enable **Discussions** (Settings → General → Features) if the project will host proposals or community threads
- [ ] Enable **Issues** (should be on by default)
- [ ] Configure **Labels** — at minimum: `bug`, `enhancement`, `documentation`, `good first issue`, `help wanted`, `governance`

## 9. First commit

The initial setup should be committed to `development` and merged through the chain:

```bash
git add .
git commit -m "chore: initialize repo with TW3 project structure"
git push origin development

git checkout staging && git merge development && git push origin staging
git checkout production && git merge staging && git push origin production
git checkout main && git merge production && git push origin main
git checkout development
```

## 10. Announce

- [ ] Post in TW3 Discussions linking to the new repo
- [ ] Update any relevant project tracking or roadmap documents
