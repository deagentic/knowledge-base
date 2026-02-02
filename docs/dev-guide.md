# The Deagentic Way: A Developer's Guide

Welcome to the team! We are an **Agentic-First** organization. This means we write code not just for computers to execute, but for AI Agents to read, understand, and interact with.

## The Workflow: Think, Specify, Test, Code

We do not just "start coding". We follow a strict BDD (Behavior Driven Development) cycle at the development level.

### Step 1: Write the Feature (The "What")

Before writing a single line of Python, you must describe what you are building in plain English using Gherkin.

**File**: `features/login.feature`

```gherkin
Feature: User Login
  As a registered user
  I want to log in
  So that I can access my dashboard

  Scenario: Successful login
    Given I am on the login page
    When I enter valid credentials
    Then I should be redirected to the dashboard
```

*Why?* If an agent can't read this and understand what the system does, the code is already failed.

### Step 2: Write the Test (The "Proof")

Implement the test steps first. They should fail (Red).

**Philosophy: Test Results, Not Implementation**

- We care *what* happens, not *how* it happens.
- **Bad**: `assert logger.was_called_with("login_attempt")` (Testing implementation details)
- **Good**: `assert response.status == 200` (Testing the result/interface)
- **Why?** If we refactor the code but the result is the same, tests should pass.

**File**: `features/steps/login_steps.py`

```python
from behave import given, when, then

@given('I am on the login page')
def step_impl(context):
    # Logic to go to login page
    pass
```

### Step 3: Write the Code (The "How")

Now implement the logic to make the test pass (Green).

**Rules for Code:**

1. **Strict Typing**: We are Pydantic. Use Type Hints everywhere. `MyPy` checks must pass.
   - *Bad*: `def process(data):`
   - *Good*: `def process(data: UserSchema) -> AuthToken:`
2. **Documentation**: Every function needs a docstring. Agents read these to know how to use your tools.
   - *Format*: Google Style or simple summary.
   - *Content*: Explain `Args`, `Returns`, and `Raises`.

### Step 4: Git Hygiene

Once your tests pass:

1. **Atomic Commits**: `feat: implement login service` (See Conventional Commits).
2. **Pre-commit**: Run `pre-commit run --all-files` to auto-format (Ruff).
3. **Pull Request**: Open a draft PR if big, or a normal PR if done.

## Quality Checklist

- [ ] Does it have a `.feature` file?
- [ ] Do the tests pass?
- [ ] Is it fully typed?
- [ ] Is it documented for an Agent?
- [ ] Did pre-commit pass?
