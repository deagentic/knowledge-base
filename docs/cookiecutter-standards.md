# Project Creation Standards (Cornerstone CLI)

To ensure consistency and enable the Agentic CI infrastructure across all projects, we strictly enforce the use of **Cornerstone CLI** for scaffolding new projects.

## Starting a New Project

**Do not create folders manually and do not use generic tools like `cookiecutter` directly.** Use the official Cornerstone CLI.

### 1. Installation
Ensure you have the latest version of Cornerstone installed:
```bash
pip install git+https://github.com/deagentic/cornerstone
```

### 2. Scaffolding with Cornerstone
Use the `cornerstone new` command to scaffold a project using one of our standardized starters.

```bash
# Example: Create a new full-stack project
cornerstone new --starter full-stack
```

Available starters (which automatically map to agent capabilities like `server`, `archaeology`, `frontend`):
- `base`: Minimal project structure.
- `mcp`: Standard MCP server project.
- `api`: API project.
- `full-stack`: Full-stack web application.
- `pipeline`: Data science pipelines (Kedro).
- `legacy-modernization`: Projects focused on archaeology and modernization.

### 3. Agentic Initialization
After creating the project, you must initialize the agentic runtime and sync the shared brain:

```bash
cd <your-new-project>
cornerstone init --mode runtime
cornerstone sync
```

## Data Science Projects (Kedro)
For data science and data engineering projects, we continue to use **Kedro** under the hood, but the project must be generated via the Cornerstone `pipeline` starter to inherit the Agentic CI configurations.

### Directory Structure
Regardless of the starter used, the generated structure MUST be preserved as it contains critical Agentic CI configurations (like `.agents/`, `AGENTS.md`, and `.github/workflows/ci.yml`). Do not manually alter the agent routing files unless directed by the framework.
