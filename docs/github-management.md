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

### 🛡️ Automated Enforcement

We provide a script to enforce this rule automatically.

**Installation**:
Copy the hook to your repository:

```bash
cp .github/hooks/commit-msg-issue-enforcer .git/hooks/commit-msg
chmod +x .git/hooks/commit-msg
```

Now, `git commit` will reject any message without an issue ID (e.g., `#123`).

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
- **Example**: "User Authentication", "Dark Mode".
- **Tracking Features**: Use the **Epic Pattern**.
  1. Create a "Tracking Issue" with the label `feature` or `epic`.
  2. In the body, list the sub-tasks:

     ```markdown
     # Feature: User Authentication
     - [x] Backend API (#102)
     - [ ] Frontend Login Form (#103)
     - [ ] Integration Tests (#104)
     ```

  3. Close the Tracking Issue only when all sub-tasks are done.

### 4. Automation (CI/CD for State)

We use GitHub's native **Keyword Automation** to link Code -> Issues.

- **In your Pull Request (PR) Description**, you MUST include:
  `Closes #123` or `Fixes #123`.

**The Lifecycle:**

1. **Open PR** with `Closes #123`.
2. **Merge PR** -> GitHub **automatically closes** Issue #123.
3. **Result**: Code is merged, Ticket is closed. Zero manual work.

### Templates & Organization

- **Milestones**: Created by Leads/PMs.
- **Issues**: Created by anyone, but must be triaged.
- **Templates**: We provide templates for [Bug Report] and [Feature Request] in `.github/ISSUE_TEMPLATE`.
