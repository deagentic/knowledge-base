# knowledge-base

**The Single Source of Truth for the deagentic organization.**

---

## Table of Contents

| Document | Description |
|----------|-------------|
| [The Deagentic Mission](docs/mission.md) | Legacy Compression — the 4 pipelines that define what we build and why. |
| [Developer's Guide](docs/dev-guide.md) | BDD workflow, typing standards, and testing practices. |
| [GitHub Management & CI/CD](docs/github-management.md) | Issues, milestones, and feature delivery lifecycle. |
| [Project Creation Standards](docs/cookiecutter-standards.md) | Cookiecutter templates and Kedro project conventions. |
| [Git Branching & PR Strategy](docs/git-strategy.md) | Branch naming, PR workflow, and merge policies. |

---

## For AI Agents

Read the docs in this exact order to build full context before writing any code:

1. **[mission.md](docs/mission.md)** — Understand the 4 pipelines and the "why" behind every project.
2. **[dev-guide.md](docs/dev-guide.md)** — Learn the BDD-first workflow, typing rules, and testing expectations.
3. **[git-strategy.md](docs/git-strategy.md)** — Know how to branch, commit, and open PRs.
4. **[github-management.md](docs/github-management.md)** — Understand how issues and milestones drive delivery.
5. **[cookiecutter-standards.md](docs/cookiecutter-standards.md)** — Follow the standard project structure when scaffolding.

### The Learning Protocol & Shared Brain

We use a "Just-In-Time Instantiation" model for agent capabilities. 
*   **Source of Truth:** All reusable agent skills and tools live in the [deagentic/cornerstone-agents](https://github.com/deagentic/cornerstone-agents) repository.
*   **Local Usage:** Projects pull these skills dynamically using the `cornerstone sync` command, caching them in a local `.agents/_repo` directory.
*   **Contributing (Learning Protocol):** When an agent or developer creates a new skill (e.g., via the `skill-creator`), it must be pushed upstream to the `cornerstone-agents` repository so the entire organization can inherit the capability.

After reading all five, you have the full operating context for the organization.

---

## For Humans

Welcome to the team. Here is your onboarding path:

1. Start with **[The Deagentic Mission](docs/mission.md)** to understand what we are building and why it matters.
2. Read the **[Developer's Guide](docs/dev-guide.md)** to learn how we write code — BDD first, fully typed, well tested.
3. Review the **[Git Branching & PR Strategy](docs/git-strategy.md)** before your first commit.
4. Bookmark **[GitHub Management & CI/CD](docs/github-management.md)** for how we track work.
5. Check **[Project Creation Standards](docs/cookiecutter-standards.md)** when starting a new project.

---

> This repository is maintained by the deagentic team. Every agent and every developer reads from the same source.
