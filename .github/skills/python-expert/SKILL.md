---
name: python-expert
description: Python coding assistant enforcing best practices including PEP 8, type hints, Pyright strict mode, Ruff linting, and clean code principles. Use when writing or reviewing Python code.
license: MIT
---

# Python Expert

Expert Python developer enforcing modern best practices for readable, maintainable, and type-safe code.

## Core Principles

- **Readability > cleverness** — Clear code beats clever code
- **Explicit > implicit** — No magic, no surprises
- **Fail fast and loudly** — Errors should be obvious
- **Small, composable functions** — Each does one thing well

## Code Standards

### Formatting (PEP 8 + Black)

- Max line length: **100 characters**
- Follow Black-compatible formatting
- Use 4 spaces for indentation

### Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| Variables/Functions | snake_case | `total_price`, `parse_document` |
| Classes | PascalCase | `DocumentParser` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRIES` |
| Private | _leading_underscore | `_parse_html` |

### Type Hints (Mandatory)

All public functions must have type hints.

```python
from typing import Optional

def find_user(user_id: int) -> Optional[str]:
    """Find user by ID."""
    if user_id > 0:
        return "user"
    return None
```

Prefer built-in types (Python 3.9+):
```python
def load_items() -> list[str]:
    ...
```

### Docstrings (Google Style)

```python
def fetch_document(url: str) -> str:
    """Fetch raw HTML from a URL.

    Args:
        url: Target document URL.

    Returns:
        HTML content.
    """
```

### Error Handling

Be explicit. Never use bare `except`.

```python
try:
    response = requests.get(url, timeout=5)
    response.raise_for_status()
except requests.RequestException as exc:
    raise RuntimeError("Fetch failed") from exc
```

## Tooling

### Pyright (Static Type Checking)

Use strict mode:
```json
{
  "typeCheckingMode": "strict",
  "reportMissingTypeStubs": false
}
```

### Ruff (Linting & Formatting)

Replaces flake8, isort, pycodestyle, pyupgrade.

```toml
[tool.ruff]
line-length = 100
select = ["E", "F", "I", "B", "UP", "SIM"]
fix = true
```

### Testing (pytest)

Test behavior, not implementation:
```python
def test_normalize_score():
    assert normalize_score(50, 100) == 0.5
```

## When Writing Code

1. **Add type hints** to all function signatures
2. **Keep functions small** — if it doesn't fit on one screen, split it
3. **Use descriptive names** — `user_count` not `uc`
4. **Handle errors explicitly** — catch specific exceptions
5. **Write docstrings** for public APIs
6. **Optimize for clarity first**, performance second

## When Reviewing Code

Check for:
- ❌ Missing type hints
- ❌ Bare `except:` clauses
- ❌ Lines > 100 characters
- ❌ Implicit returns or behavior
- ❌ Generic variable names (`data`, `temp`, `x`)
- ✅ Clear error messages
- ✅ Small, focused functions
- ✅ Proper naming conventions

## Remember

**Clean Python is boring Python** — and boring code scales.
