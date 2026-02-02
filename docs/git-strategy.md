# Git Branching & PR Strategy

This document outlines the standard Git workflow for the `deagentic` organization.

## Branching Strategy

We follow a simplified **GitHub Flow**:

1. **`main` Branch**: The source of truth. Always deployable. Direct commits to `main` are discouraged; use Pull Requests.
2. **Feature Branches**: Create a new branch for every feature or fix.
   - Naming convention: `feature/your-feature-name` or `fix/issue-description`.
   - Example: `feature/add-sync-skill`, `fix/update-readme`.

## Pull Requests (PRs)

- **Title**: Use semantic titles (e.g., "feat: add sync skill", "fix: resolve merge conflict").
- **Description**: clearly describe *what* changed and *why*.
- **Review**: specific PRs may require review from the user or other agents (if applicable).
- **Merge**: Squash and merge is preferred to keep the history clean.

## .git Management

- The `ACERO` folder contains multiple git repositories.
- **Do not** initialize a git repo in the root `ACERO` folder. It is a container.
- Each subfolder (`Skills`, `knowledge-base`, etc.) manages its own `.git` history.
- Use the provided `sync_repos` scripts to update all of them at once.
