# Python Project Custom Instructions

## Repository Overview

**Type:** Python application/library  
**Python Version:** 3.13+  
**Package Manager:** uv (Astral's ultra-fast package manager)  
**Testing Framework:** pytest  
**Code Quality:** ruff (formatting + linting), mypy

## Project Structure

```
src/myproject/        # Main application code
├── models.py         # Data models
├── utils.py          # Utility functions
└── __init__.py       # Package initialization

tests/                # Test files (mirrors src structure)
├── test_models.py
├── test_utils.py
└── conftest.py       # Pytest fixtures

docs/                 # Documentation
pyproject.toml        # Project metadata, dependencies, tool configs
uv.lock               # Lockfile for reproducible installs
.python-version       # Python version (managed by uv)
```

## Setup and Build

### Initial Setup

```bash
# Install uv if not already installed
curl -LsSf https://astral.sh/uv/install.sh | sh

# Sync dependencies (~2-5 seconds, uv is FAST)
uv sync

# uv automatically creates and manages the virtual environment
# No need for manual venv activation!
```

### Build Commands

This project doesn't require a build step for development. For distribution:

```bash
# Build package with uv
uv build

# Output: dist/myproject-0.1.0-py3-none-any.whl
```

## Testing

### Running Tests

```bash
# Run all tests (uv run automatically uses the project's venv)
uv run pytest

# Run with coverage
uv run pytest --cov=src/myproject --cov-report=html

# Run specific test file
uv run pytest tests/test_utils.py

# Run specific test
uv run pytest tests/test_utils.py::test_function_name

# Run with verbose output
uv run pytest -v
```

**Expected:** All tests pass in ~5 seconds. Coverage should be > 80%.

### Writing Tests

- Place tests in `tests/` directory
- Name test files: `test_*.py`
- Name test functions: `test_*`
- Use fixtures from `conftest.py`
- One test file per source file

## Code Quality

### Formatting

```bash
# Format code with ruff
uv run ruff format src/ tests/

# Check formatting without changes
uv run ruff format --check src/ tests/
```

**Always run before committing.**

### Linting

```bash
# Run ruff linter
uv run ruff check src/ tests/

# Auto-fix issues
uv run ruff check --fix src/ tests/
```

### Type Checking

```bash
# Run mypy
uv run mypy src/

# Strict mode (for new code)
uv run mypy --strict src/myproject/new_module.py
```

**All public functions must have type hints.**

## Coding Standards

### Imports

Organize in three groups, alphabetically within each:

```python
# Standard library
import sys
from pathlib import Path
from typing import Optional

# Third-party
import requests
from pydantic import BaseModel

# Local
from myproject.models import User
from myproject.utils import validate_email
```

### Type Hints

**Required for all public functions:**

```python
def process_user(user_id: int, active: bool = True) -> Optional[User]:
    """Retrieve and process user data."""
    ...
```

### Error Handling

Use specific exceptions with context:

```python
try:
    data = load_config(config_path)
except FileNotFoundError:
    logger.error(f"Config not found: {config_path}")
    raise
except json.JSONDecodeError as e:
    raise ConfigError(f"Invalid JSON in {config_path}: {e}") from e
```

### Logging

Use structured logging:

```python
import logging

logger = logging.getLogger(__name__)

logger.info("Processing user", extra={"user_id": user_id})
logger.error("Failed to connect", exc_info=True)
```

## Common Patterns

### Data Models

Use dataclasses or Pydantic:

```python
from dataclasses import dataclass

@dataclass
class User:
    id: int
    name: str
    email: str
    active: bool = True
```

### Configuration

Load from environment variables:

```python
from os import getenv

DATABASE_URL = getenv("DATABASE_URL", "sqlite:///default.db")
API_KEY = getenv("API_KEY")  # Required

if not API_KEY:
    raise ValueError("API_KEY environment variable required")
```

### File Operations

Use pathlib:

```python
from pathlib import Path

config_file = Path("config.json")
if config_file.exists():
    content = config_file.read_text()
```

## Known Issues and Workarounds

### Issue: Import errors in tests

**Problem:** Tests can't import from `src/myproject`

**Solution:** Install package in editable mode:
```bash
pip install -e .
```

### Issue: Slow tests

**Problem:** Some integration tests take > 10 seconds

**Solution:** Mark slow tests and skip during development:
```python
@pytest.mark.slow
def test_integration():
    ...

# Run without slow tests
pytest -m "not slow"
```

## Validation Steps

Before committing:

1. **Format code:** `black src/ tests/`
2. **Lint code:** `ruff check --fix src/ tests/`
3. **Type check:** `mypy src/`
4. **Run tests:** `pytest`
5. **Check coverage:** `pytest --cov=src/myproject`

All steps must pass before creating a pull request.

## Dependencies

Main dependencies (see requirements.txt for versions):
- **requests** - HTTP client
- **pydantic** - Data validation
- **python-dotenv** - Environment configuration

Development dependencies:
- **pytest** - Testing framework
- **pytest-cov** - Coverage reporting
- **black** - Code formatting
- **ruff** - Linting
- **mypy** - Type checking

## Environment Variables

Required:
- `API_KEY` - API authentication key

Optional:
- `DATABASE_URL` - Database connection (default: sqlite:///default.db)
- `LOG_LEVEL` - Logging level (default: INFO)

Example `.env` file:
```bash
API_KEY=your_api_key_here
DATABASE_URL=postgresql://user:pass@localhost/dbname
LOG_LEVEL=DEBUG
```

---

**Trust these instructions.** Only search for additional information if something doesn't work as documented.
