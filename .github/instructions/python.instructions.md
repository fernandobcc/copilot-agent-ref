---
applyTo: "**/*.py"
---

# Python Code Guidelines

When working with Python files in this repository:

## Code Style

- **Follow PEP 8** with ruff formatting (replaces Black/isort/flake8)
- **Maximum line length**: 100 characters
- **Indentation**: 4 spaces (never tabs)
- **Imports**: Group in order: stdlib, third-party, local (separated by blank lines, auto-sorted by ruff)

## Type Hints

**Always include type hints** for function signatures:

```python
from typing import Optional

def process_data(items: list[dict], limit: int = 10) -> Optional[list[str]]:
    """Process data items up to limit."""
    if not items:
        return None
    return [item["name"] for item in items[:limit]]
```

Use modern type syntax (Python 3.10+):
- `list[str]` instead of `List[str]`
- `dict[str, int]` instead of `Dict[str, int]`
- `tuple[int, str]` instead of `Tuple[int, str]`
- `int | None` instead of `Optional[int]` (Python 3.10+)
- `str | int` instead of `Union[str, int]`

## Documentation

All public functions need docstrings:

```python
def calculate_score(points: int, bonus: float = 1.0) -> float:
    """Calculate final score with bonus multiplier.
    
    Args:
        points: Base points earned
        bonus: Multiplier for bonus calculation (default: 1.0)
    
    Returns:
        Final calculated score
    
    Raises:
        ValueError: If points is negative
    """
    if points < 0:
        raise ValueError("Points cannot be negative")
    return points * bonus
```

## Error Handling

- **Be specific** with exception types
- **Always provide context** in error messages
- **Use logging** for debugging information

```python
import logging

logger = logging.getLogger(__name__)

try:
    result = parse_config(config_file)
except FileNotFoundError:
    logger.error(f"Config file not found: {config_file}")
    raise
except json.JSONDecodeError as e:
    logger.error(f"Invalid JSON in {config_file}: {e}")
    raise ValueError(f"Cannot parse config: {e}") from e
```

## Script Structure

For executable scripts in this repo (like those in `.github/skills/*/scripts/`):

1. **Use argparse** for command-line arguments
2. **Include type hints** throughout
3. **Add docstrings** to all functions
4. **Use `if __name__ == "__main__":`** pattern
5. **Handle errors gracefully** with sys.exit(1)

```python
#!/usr/bin/env python3
"""Script to validate skill definitions."""

import argparse
import sys
from pathlib import Path

def validate_skill(skill_path: Path) -> bool:
    """Validate a skill directory structure.
    
    Args:
        skill_path: Path to the skill directory
        
    Returns:
        True if valid, False otherwise
    """
    skill_md = skill_path / "SKILL.md"
    return skill_md.exists()

def main() -> int:
    """Main entry point."""
    parser = argparse.ArgumentParser(description="Validate skill structure")
    parser.add_argument("skill_path", type=Path, help="Path to skill directory")
    args = parser.parse_args()
    
    if not validate_skill(args.skill_path):
        print(f"Invalid skill: {args.skill_path}", file=sys.stderr)
        return 1
    
    print(f"Valid skill: {args.skill_path}")
    return 0

if __name__ == "__main__":
    sys.exit(main())
```

## Common Patterns for This Repository

### File Operations

Use **pathlib** for file paths:

```python
from pathlib import Path

# Reading files
config_file = Path(".github/copilot-instructions.md")
content = config_file.read_text()

# Writing files
output_file = Path("output.md")
output_file.write_text(content)

# Checking existence
if config_file.exists():
    print(f"Found: {config_file}")
```

### YAML Frontmatter Parsing

When working with instruction files that have YAML frontmatter:

```python
import re
from typing import Tuple, Optional

def parse_frontmatter(content: str) -> Tuple[Optional[dict], str]:
    """Extract YAML frontmatter and content.
    
    Args:
        content: File content with potential frontmatter
        
    Returns:
        Tuple of (frontmatter_dict, content_without_frontmatter)
    """
    match = re.match(r'^---\n(.*?)\n---\n(.*)$', content, re.DOTALL)
    if not match:
        return None, content
    
    import yaml
    frontmatter = yaml.safe_load(match.group(1))
    body = match.group(2)
    return frontmatter, body
```

## Testing

Tests should be clear and focused:

```python
import pytest
from pathlib import Path

def test_validate_skill_valid_structure(tmp_path: Path) -> None:
    """Test validation with valid skill structure."""
    skill_dir = tmp_path / "test-skill"
    skill_dir.mkdir()
    (skill_dir / "SKILL.md").write_text("# Test Skill")
    
    assert validate_skill(skill_dir) is True

def test_validate_skill_missing_skill_md(tmp_path: Path) -> None:
    """Test validation fails without SKILL.md."""
    skill_dir = tmp_path / "test-skill"
    skill_dir.mkdir()
    
    assert validate_skill(skill_dir) is False
```

## Avoid Common Pitfalls

- ❌ Don't use bare `except:` - catch specific exceptions
- ❌ Don't use mutable default arguments (`def func(items=[]):`)
- ❌ Don't ignore type hints - they help catch bugs
- ❌ Don't skip docstrings on public APIs
- ✅ Do use f-strings for formatting (`f"Value: {x}"`)
- ✅ Do use context managers for files (`with open(...) as f:`)
- ✅ Do use pathlib instead of os.path
- ✅ Do validate user input early
