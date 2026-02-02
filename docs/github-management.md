# GitHub Management & CI/CD

## Permissions

- **Organization Owners**: Have full access to all repositories.
- **Agents**: Should act with the permissions of the user operating them.
- **Skills Repo**: Publicly readable (sharing skills), writes restricted to maintain quality.

## GitHub Actions

We aim to use standard actions for:

1. **Linting**: Automating code quality checks.
2. **Sync Verification**: (Future) ensuring the `Skills` match the implementation.

## Project Management

### The Golden Rule: No Ticket, No Code

**Every commit must be traceable to a GitHub Issue.**

- **Bad Commit**: `fix bug`
- **Good Commit**: `fix: handle null user id (ref #42)`

### 1. Issues (The Unit of Work)

An **Issue** is a single, actionable task.

- "Implement Login Form"
- "Fix crash on startup"
- "Write documentation for API"

### 2. Milestones (The Unit of Time/Release)

A **Milestone** is a specific destination (Release/Sprint).

- **Example**: `v1.0 - MVP Launch`, `2024-Q1 - Performance Update`
- contains many Issues.
- has a **Deadline**.

### 3. Features (The Unit of Value)

A **Feature** is a high-level capability provided to the user.

- **Example**: "User Authentication", "Dark Mode".
- **Is it a Milestone?** **NO**. A Feature is a goal. It might be delivered in Milestone `v1.0`.
- If a Feature is huge, track it as a **GitHub Project** or an "Epic" Issue that links to smaller implementation Issues.

### Templates & Organization

- **Milestones**: Created by Leads/PMs.
- **Issues**: Created by anyone, but must be triaged.
- **Templates**: We provide templates for [Bug Report] and [Feature Request] in `.github/ISSUE_TEMPLATE`.
