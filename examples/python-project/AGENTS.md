# AI Agent Instructions for Python Project

When working as an AI coding agent in this Python project:

## Understanding the Project

This is a **Python application/library** with:
- Modern Python (3.9+) with type hints
- Pytest for testing
- Black/Ruff for code quality
- Clear separation: `src/` for code, `tests/` for tests

## Working Approach

### Before Making Changes

1. **Check existing patterns** in similar files
2. **Read relevant tests** to understand expected behavior
3. **Verify environment** is set up correctly

### When Adding Features

1. **Start with tests** - Write failing test first (TDD)
2. **Implement minimally** - Simplest solution that works
3. **Add type hints** - All public functions need them
4. **Update docstrings** - Explain what and why
5. **Run quality checks** - Black, Ruff, mypy
6. **Verify tests pass** - Including new tests

### When Fixing Bugs

1. **Write a failing test** that reproduces the bug
2. **Fix the minimal code** needed
3. **Verify the test passes**
4. **Check for similar issues** elsewhere
5. **Update documentation** if behavior changed

### When Refactoring

1. **Ensure tests exist** for code being refactored
2. **Make small changes** - One refactor at a time
3. **Run tests after each change**
4. **Keep behavior identical** - No feature changes during refactoring

## Code Style Enforcement

**Always run before committing:**

```bash
black src/ tests/           # Format code
ruff check --fix src/ tests/  # Lint and auto-fix
mypy src/                   # Type check
pytest                      # Run tests
```

If any fail, fix before proceeding.

## Type Hints Philosophy

- **All public functions** must have type hints
- **Private functions** should have type hints
- **Use specific types** - Avoid `Any`
- **Import from typing** as needed

Example:
```python
from typing import Optional

def find_user(user_id: int) -> Optional[User]:
    """Find user by ID, returns None if not found."""
    ...
```

## Testing Philosophy

- **Test behavior, not implementation**
- **One test, one concept**
- **Descriptive names** - `test_<what>_<when>_<expected>`
- **Arrange-Act-Assert** pattern
- **Use fixtures** for common setup
- **Mock external services** - Keep tests fast

## Error Handling

- **Catch specific exceptions** - Never bare `except:`
- **Provide context** - Include relevant details in error messages
- **Log appropriately** - Info for normal flow, error for failures
- **Fail fast** - Don't hide errors

Example:
```python
try:
    config = load_config(path)
except FileNotFoundError:
    logger.error(f"Config not found: {path}")
    raise
except json.JSONDecodeError as e:
    raise ConfigError(f"Invalid config in {path}: {e}") from e
```

## File Organization

- **Put models in `models.py`**
- **Put utilities in `utils.py`**
- **Keep modules focused** - One responsibility
- **Mirror tests** - `test_utils.py` for `utils.py`

## Common Workflows

### Adding a New Function

```bash
# 1. Write test first
# tests/test_utils.py
def test_new_function():
    result = new_function("input")
    assert result == "expected"

# 2. Run test (should fail)
pytest tests/test_utils.py::test_new_function

# 3. Implement function
# src/myproject/utils.py
def new_function(input: str) -> str:
    """Description of what it does."""
    return process(input)

# 4. Run test (should pass)
pytest tests/test_utils.py::test_new_function

# 5. Add type hints and docstring (already done)

# 6. Format and lint
black src/myproject/utils.py tests/test_utils.py
ruff check src/myproject/utils.py

# 7. Type check
mypy src/myproject/utils.py

# 8. Run all tests to ensure nothing broke
pytest
```

### Debugging Test Failures

```bash
# Run with verbose output
pytest -v

# Run with print statements visible
pytest -s

# Run specific failing test
pytest tests/test_utils.py::test_failing_case

# Use debugger
pytest --pdb

# Show full diff for assert failures
pytest -vv
```

## Decision Making

### When to Add a Dependency

Ask:
1. **Is it in stdlib?** - Prefer stdlib when possible
2. **Is it widely used?** - Check popularity/maintenance
3. **What's the alternative?** - Could we write it ourselves?
4. **What's the cost?** - Size, dependencies, security

Document decision in requirements.txt comment:
```txt
requests==2.31.0  # Best HTTP client, widely supported
```

### When to Extract a Function

Extract when:
- Function is > 20 lines
- Logic is reused in 2+ places
- Complexity makes testing hard
- Clear single responsibility

### When to Add Type: Ignore

**Rarely.** Only when:
- Third-party library has no type stubs
- Type checker has a known bug
- Refactoring to fix would be risky

Always add a comment explaining why:
```python
result = external_lib.func()  # type: ignore  # No stubs for external_lib
```

## Quality Standards

### Code Coverage

- Aim for > 80% overall
- New code should be > 90%
- Critical paths must be 100%

Check with:
```bash
pytest --cov=src/myproject --cov-report=term-missing
```

Focus on **missing lines** in output.

### Type Coverage

Check with:
```bash
mypy --strict src/
```

Fix all errors. If impossible, document why.

## Avoiding Pitfalls

### Don't

- ❌ Skip tests "because it's simple"
- ❌ Use `print()` for debugging (use logging)
- ❌ Commit without running quality checks
- ❌ Change multiple things at once
- ❌ Ignore type errors
- ❌ Write tests that depend on execution order

### Do

- ✅ Write tests for new code
- ✅ Run tests after each change
- ✅ Use type hints everywhere
- ✅ Keep functions small and focused
- ✅ Use descriptive names
- ✅ Document non-obvious decisions

## Getting Unstuck

If stuck:

1. **Run the tests** - What's actually failing?
2. **Check existing code** - How is it done elsewhere?
3. **Read the docs** - Check library documentation
4. **Simplify** - What's the minimal reproducer?
5. **Ask for help** - Provide specific context

## Success Criteria

Your work is complete when:

- ✅ All tests pass
- ✅ Black formatting applied
- ✅ Ruff linting passes
- ✅ Mypy type checking passes
- ✅ Coverage maintained or improved
- ✅ Documentation updated
- ✅ No regressions introduced

---

**Trust the copilot-instructions.md file.** It contains validated commands and patterns. Only deviate with good reason.
