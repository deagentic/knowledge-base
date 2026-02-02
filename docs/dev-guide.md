# The Deagentic Way: A Developer's Guide

Welcome to the team! This guide is your crash course on how we build software here. We focus on clean history, clear communication, and automated quality.

## 1. Git 101: Atomic Commits

**Rule**: One commit = One change.

- **Bad**: "Fix login bug and update readme and change color of button"
- **Good**:
  - Commit 1: "fix: resolve null pointer in login"
  - Commit 2: "docs: update install instructions"
  - Commit 3: "style: change primary button color"

This makes it easy to revert specific changes if something breaks.

## 2. How to Write a Commit

We follow **Conventional Commits**. Your commit message should look like this:

`type: short description`

**Types:**

- `feat`: A new feature (e.g., `feat: add dark mode`).
- `fix`: A bug fix (e.g., `fix: mobile layout overflow`).
- `docs`: Documentation only changes.
- `style`: Formatting, missing semi-colons, etc (no code change).
- `refactor`: A code change that neither fixes a bug nor adds a feature.
- `test`: Adding missing tests or correcting existing tests.
- `chore`: Changes to the build process or auxiliary tools.

## 3. Pull Request (PR) Etiquette

- **Start as Draft**: If you are still working, mark your PR as a "Draft".
- **Description is Mandatory**: use the template! Explain *what* you did and *why*.
- **Self-Review**: Read your own code diff before asking others to.
- **CI Checks**: Ensure all checks pass (green) before requesting review.

## 4. Code Review

- Don't take it personally. We review code, not people.
- If a reviewer asks for a change, reply with "Done" or explain why you disagree.
- Resolve conversations when the issue is fixed.

## 5. Testing & Quality (The Holy Grail)

We don't ship broken code.

- **BDD with Behave**: We use Behavior Driven Development. Write your features in Gherkin (`.feature` files) and implement steps in Python.
- **Pre-commit**: We use `pre-commit` to catch simple issues before they even reach GitHub.
  - Run `pre-commit install` once in every new repo.
  - It will auto-fix imports and formatting when you `git commit`.
