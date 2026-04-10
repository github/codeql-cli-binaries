# Contributing to CodeQL CLI Binaries

Thank you for your interest in contributing to the CodeQL CLI distribution infrastructure for MILEHIGH-WORLD LLC. To maintain enterprise-grade resilience and ensure seamless automation via agentic workflows, we enforce strict contribution protocols.

## Commit Message Format

We strictly enforce **Conventional Commits**. This is non-negotiable as it powers our automated release versioning via `release-please`.

The format is:
`<type>(<scope>): <description>`

Common types:
- `feat`: A new feature (corresponds to a MINOR version bump)
- `fix`: A bug fix (corresponds to a PATCH version bump)
- `docs`: Documentation only changes
- `style`: Changes that do not affect the meaning of the code (white-space, formatting, etc)
- `refactor`: A code change that neither fixes a bug nor adds a feature
- `perf`: A code change that improves performance
- `test`: Adding missing tests or correcting existing tests
- `chore`: Changes to the build process or auxiliary tools and libraries

Example:
`feat(automation): add markdownlint workflow`

## Branching Strategy

To isolate work and track automated workflows, please use the following prefixes for your branches:

- `feature/<ticket-or-name>`: Standard development and new features.
- `hotfix/<issue>`: Production-critical patches.
- `agent/<tool-name>`: AI-driven workflows and agentic tool updates (e.g., `agent/jules`).

## Pull Request Process

1. Create a branch from `main` using the appropriate prefix.
2. Ensure your commit messages follow the Conventional Commits standard.
3. Documentation changes must pass the `markdownlint` and `lychee` checks in CI.
4. Once your changes are ready, open a Pull Request.
5. All PRs require review and approval before merging.
6. Upon merging to `main`, the `release-please` workflow will automatically manage versioning and changelog updates.
