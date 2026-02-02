# Git Branching & PR Strategy

This document outlines the standard Git workflow for the `deagentic` organization.

## Branching Strategy

We follow a **Feature Branch Workflow** to ensure a linear and clean history.

1. **`main` Branch**: The source of truth. Always deployable. Protected.
2. **Feature Branches**:
   - Source: `main`
   - Naming: `feat/description`, `fix/description`, `chore/description`.
   - Lifecycle: Created for a task, merged via PR, **deleted immediately after merge**.

## Static Analysis & Quality Gate

Every repository MUST implement `pre-commit` hooks and CI checks using **Ruff**.

- **Linter**: Ruff (replaces Flake8, Isort).
- **Formatter**: Ruff (replaces Black).
- **Type Checker**: MyPy.

## Pull Requests (PRs)

- **Title**: MUST follow Conventional Commits (e.g., `feat: add user login`).
- **Template**: Use the standard organization template.
- **Merge Strategy**: **Squash and Merge** is preferred to maintain a clean history in `main`.

## .git Management

- The `ACERO` folder contains multiple git repositories.
- **Do not** initialize a git repo in the root `ACERO` folder. It is a container.
- Each subfolder (`Skills`, `knowledge-base`, etc.) manages its own `.git` history.
- Use the provided `sync_repos` scripts to update all of them at once.
