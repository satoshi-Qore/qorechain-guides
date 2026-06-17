# First Contribution Guide

Welcome to QoreChain. This guide explains how to make your first contribution.

## Before You Start

- Read the [README](../README.md) to understand the project scope.
- Review [Code Standards](code-standards.md) and [Documentation Standards](documentation-standards.md).
- Search existing issues and pull requests to avoid duplicate work.

## Step 1 -- Fork and Clone

1. Fork the target repository on GitHub.
2. Clone your fork locally:

```bash
git clone https://github.com/YOUR_USERNAME/REPO_NAME.git
cd REPO_NAME
```

3. Add the upstream remote:

```bash
git remote add upstream https://github.com/satoshi-Qore/REPO_NAME.git
```

## Step 2 -- Create a Branch

Always create a branch from `main`:

```bash
git checkout main
git pull upstream main
git checkout -b your-branch-name
```

Branch naming convention:

| Type | Example |
|---|---|
| Bug fix | `fix/rpc-timeout-handling` |
| Feature | `feat/add-alert-rule` |
| Documentation | `docs/update-validator-setup` |
| Refactor | `refactor/config-loader` |

## Step 3 -- Make Changes

- Write code or documentation according to the relevant standards.
- Keep commits small and focused -- one logical change per commit.
- Use English in all commit messages.

Good commit message format:

```
type: short summary in present tense

Optional longer description if needed.
```

Examples:
- `fix: handle connection timeout in check_endpoint`
- `docs: add validator-setup tutorial`
- `feat: add disk usage alert rule`

## Step 4 -- Push and Open a Pull Request

```bash
git push origin your-branch-name
```

Open a pull request on GitHub using the [PR template](pull-request-template.md). Fill in all sections.

## Step 5 -- Review Process

- A maintainer will review your PR within a reasonable time.
- Respond to review comments by pushing additional commits -- do not force-push during review.
- Once approved, a maintainer will merge the PR.

## Questions

Open a GitHub Discussion or Issue if you need help before submitting a PR.
