# Project Creation Standards (Cookiecutters)

To ensure consistency across our data science and engineering projects, we strictly enforce the use of standardized templates.

## Data Science Projects

We use **Kedro** as our standard framework for data science projects and pipelines.

### Starting a New Project

**Do not create folders manually.** Use the official Kedro starters.

```bash
# Standard interactive creation
kedro new
# (Select 'spaceflights' or another suitable starter)
```

### Configuration Standards

When asked during setup:

- **Project Name**: Use Title Case (e.g., `Customer Churn Model`).
- **Repo Name**: Use kebab-case (e.g., `customer-churn-model`).
- **Tools**:
  - **Linting/Formatting**: Select `Ruff`.
  - **Testing**: Select `Pytest`.
  - **Config**: Select `YAML` (or `OmegaConf` if advanced features needed).

### Directory Structure

The resulting structure MUST be preserved:

- `src/`: Source code.
- `conf/`: Configuration catalogs and parameters.
- `data/`: Local data (ignored by git).
- `features/`: BDD Feature files (`.feature`) and steps.
- `notebooks/`: Experiments.
- `pyproject.toml`: Dependency management.
- `tests/`: Unit tests.

###
