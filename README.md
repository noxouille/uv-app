# README

## Setup

This project uses [uv](https://github.com/astral-sh/uv) for Python package and environment management.

### Prerequisites

Install uv:

```bash
# Windows (PowerShell)
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"

# macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Getting Started

1. Create virtual environment:

```bash
uv venv
```

2. Activate the environment:

```bash
# Windows
.venv\Scripts\activate

# macOS/Linux
source .venv/bin/activate
```

3. Install dependencies:

```bash
# Install from pyproject.toml
uv pip install -e .

# Or install specific packages
uv pip install package-name
```

### Common Commands

```bash
# Run Python scripts
uv run python app.py

# Install a package
uv pip install requests

# Install dev dependencies
uv pip install pytest black ruff

# List installed packages
uv pip list

# Upgrade a package
uv pip install --upgrade package-name
```

## Markdown Linting

This project uses **markdownlint-cli2** to ensure consistent Markdown formatting.

### VS Code (Recommended)

1. Open the project in VS Code
2. Install the **markdownlint** extension by David Anson (Ctrl+Shift+X → search "markdownlint")
3. Edit any `.md` file
4. See warnings appear as you type (wavy underlines)
5. View all errors in Problems panel (Ctrl+Shift+M)

**Note:** The markdownlint extension shows errors but does NOT auto-fix them. You must fix issues manually.

### Check Linting

```bash
# Check all files
uv run markdownlint-cli2 "docs/**/*.md" "*.md"

# Check specific file
uv run markdownlint-cli2 docs/DEVELOPMENT_PLAN.md
```

## Project Structure

- `pyproject.toml` - Project configuration and dependencies
- `.python-version` - Python version specification (3.11)
- `.venv/` - Virtual environment (auto-created by uv)
- `.vscode/` - VS Code settings
