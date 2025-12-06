# DevPod Development Environment

This devcontainer provides a complete Python development environment with:

- **Python 3.12.12** (built from source)
- **uv** - Fast Python package installer and resolver
- **ruff** - Extremely fast Python linter and code formatter
- **JupyterLab** - For interactive notebooks

## Getting Started with DevPod Desktop

### 1. Open the Project in DevPod

1. Open DevPod Desktop
2. Click "Create Workspace"
3. Select this repository/folder
4. DevPod will automatically detect the `.devcontainer` configuration
5. Wait for the container to build (first time takes ~5-10 minutes)

### 2. Verify Installation

Once the container is running, open a terminal and verify:

```bash
python --version    # Should show Python 3.12.12
uv --version       # Should show uv version
ruff --version     # Should show ruff version
jupyter --version  # Should show JupyterLab version
```

### 3. Using the Environment

#### Install Python packages with uv

```bash
# Create a virtual environment
uv venv

# Activate it
source .venv/bin/activate

# Install packages
uv pip install numpy pandas torch torchvision matplotlib

# Or install from requirements.txt
uv pip install -r requirements.txt
```

#### Using Ruff

```bash
# Check code
ruff check .

# Format code
ruff format .

# Fix auto-fixable issues
ruff check --fix .
```

#### Using JupyterLab

```bash
# Start JupyterLab (will be accessible on port 8888)
jupyter lab --ip=0.0.0.0 --no-browser --allow-root
```

The Jupyter port (8888) is automatically forwarded, and you'll get a notification with the link.

## VS Code Extensions Included

- **Python** - Python language support
- **Pylance** - Fast Python language server
- **Ruff** - Linting and formatting
- **Jupyter** - Notebook support
- **Dependi** - Dependency management visualization
- **Even Better TOML** - TOML file support

## Resource Requirements

- **CPUs**: 2 cores minimum
- **Memory**: 8GB RAM
- **Storage**: 32GB

## Troubleshooting

### Container fails to build

- Check Docker/Podman is running
- Ensure you have enough disk space
- Check DevPod logs for specific errors

### Python packages not installing

- Make sure you're using `uv` instead of `pip` for faster installs
- If using `pip`, ensure you activate the virtual environment first

### VS Code extensions not working

- Wait for the extensions to fully install (check Extensions panel)
- Reload the window: Cmd+Shift+P → "Developer: Reload Window"

### Jupyter not accessible

- Check that port 8888 is forwarded (Ports panel in VS Code)
- Copy the token from the Jupyter terminal output