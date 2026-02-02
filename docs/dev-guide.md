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

**CRITICAL RULE**: Do NOT touch architecture or write implementation code until ALL behaviors (feature files) are written and approved. Design follows behavior.

### Step 2: Write the Test (The "Proof")

Implement the test steps first. They should fail (Red).

**Philosophy: Test Results, Not Implementation**

- We care *what* happens, not *how* it happens.
- **Bad**: `assert logger.was_called_with("login_attempt")` (Testing implementation details)
- **Good**: `assert response.status == 200` (Testing the result/interface)
- **Better**: Validate schema with Pydantic:

  ```python
  # Ensure the response adheres to the contract, not just "is 200"
  expected_schema = AuthResponse(token="ey...", user_id=123)
  assert AuthResponse(**response.json()) == expected_schema
  ```

- **Why?** If we refactor the code but the result is the same, tests should pass.

**Documentation Mandatory**:
Every test must explicitly state:

1. **HOW** it evaluates (e.g., "Checks HTTP 200 via `requests` and the response structure").
2. **WHAT** is the expected behavior (e.g., "Returns JSON with auth token").
3. **Why** this behavior matters.

**File**: `features/steps/login_steps.py`

```python
from behave import then
from backend.schemas import AuthResponse
from pydantic import ValidationError

@then('I should receive a valid auth token')
def step_impl(context):
    """Verifies the login response.

    This step checks if the response status is 200 and validates the
    JSON body against the `AuthResponse` Pydantic schema.

    How:
        Checks HTTP 200 via `context.response` and strict Pydantic validation.

    What:
        Expects a JSON payload containing a valid JWT `token` and `user_id`.

    Why:
        The frontend crashes if the token format is invalid or missing, blocking
        user access.

    Raises:
        AssertionError: If status is not 200.
        ValidationError: If the response body does not match the schema.
    """
    # 1. Check Interface (Status)
    assert context.response.status_code == 200, \
        f"Expected 200, got {context.response.status_code}"

    # 2. Check Contract (Schema)
    try:
        # Strict validation: extra fields might be allowed or forbidden depending on config
        data = AuthResponse(**context.response.json())
        context.auth_token = data.token # Store for subsequent steps
    except ValidationError as e:
        assert False, f"Contract broken, invalid schema: {e}"
```

### Step 3: Write the Code (The "How")

Now implement the logic to make the test pass (Green).

**Rules for Code:**

1. **Strict Typing**: We are Pydantic. Use Type Hints everywhere. `MyPy` checks must pass.
   - *Bad*: `def process(data):`
   - *Good*: `def process(data: UserSchema) -> AuthToken:`
2. **Documentation**: Every function needs a docstring. Agents read these to know how to use your tools.
   - *Format*: Google Style.
   - *Content*: Explain `Args`, `Returns`, and `Raises`.

### Step 4: Git Hygiene

Once your tests pass:

1. **Atomic Commits**: `feat: implement login service` (See Conventional Commits).
2. **Pre-commit**: Run `pre-commit run --all-files` to auto-format (Ruff).
3. **Pull Request**: Open a draft PR if big, or a normal PR if done.

## Quality Checklist

- [ ] Does it have a `.feature` file?
- [ ] Are the tests approved by other team member?
- [ ] Do the tests pass?
- [ ] Is it fully typed?
- [ ] Is it documented for an Agent?
- [ ] Did pre-commit pass?

## 7. Testing AI Agents (LLMs)

Testing deterministic code is easy. Testing probabilistic LLMs is hard. We split it into two:

### A. The "Plumbing" (Unit Tests) - **REQUIRED**

Test everything *around* the LLM. **Mock the LLM call.**

- **Input**: specific prompt structure.
- **Output**: JSON parsing, Pydantic validation.
- **Tools**: Test your tools as standard functions.

**Example**:

```python
# Don't call OpenAI. Mock the response.
@patch("openai.ChatCompletion.create")
def test_agent_parses_json(mock_llm):
    mock_llm.return_value = '{"action": "search", "query": "hello"}'
    result = agent.decide("hello")
    assert result.action == "search"
```

### B. The "Intelligence" (Evals) - **SEPARATE**

To test *if the agent is smart*, we use **Evals** (not Unit Tests).

- Create a dataset of inputs + expected outputs.
- Run a separate script (not `pytest` CI) to grade the agent.
- Use "LLM-as-a-Judge" to score the response.

**Example**:

```python
# evaluations/grade_agent.py
def grade_response(agent_output, expected_fact):
    judge_prompt = f"Did the agent mention '{expected_fact}' in: {agent_output}?"
    score = llm.ask(judge_prompt)
    assert "YES" in score
```
