---
applyTo: "tests/**/*.py"
---

# Testing Guidelines

When working with test files in this project:

## Test Structure

Follow the **Arrange-Act-Assert** pattern:

```python
def test_user_creation():
    # Arrange
    user_data = {"id": 1, "name": "Alice", "email": "alice@example.com"}
    
    # Act
    user = User(**user_data)
    
    # Assert
    assert user.id == 1
    assert user.name == "Alice"
    assert user.email == "alice@example.com"
```

## Naming Conventions

- Test files: `test_<module_name>.py`
- Test functions: `test_<what_is_being_tested>`
- Test classes: `Test<ClassName>`

```python
# tests/test_utils.py

def test_validate_email_with_valid_input():
    assert validate_email("user@example.com") is True

def test_validate_email_with_invalid_input():
    assert validate_email("invalid") is False

class TestUserValidator:
    def test_valid_user(self):
        assert UserValidator.is_valid(user) is True
```

## Fixtures

Define shared fixtures in `conftest.py`:

```python
# tests/conftest.py

import pytest
from myproject.models import User

@pytest.fixture
def sample_user():
    """Provide a sample user for testing."""
    return User(id=1, name="Test User", email="test@example.com")

@pytest.fixture
def temp_config_file(tmp_path):
    """Create a temporary config file."""
    config = tmp_path / "config.json"
    config.write_text('{"key": "value"}')
    return config
```

Use fixtures in tests:

```python
def test_process_user(sample_user):
    result = process_user(sample_user)
    assert result.processed is True
```

## Parametrized Tests

Use `@pytest.mark.parametrize` for multiple test cases:

```python
import pytest

@pytest.mark.parametrize("email,expected", [
    ("user@example.com", True),
    ("invalid", False),
    ("", False),
    ("@example.com", False),
])
def test_validate_email(email, expected):
    assert validate_email(email) is expected
```

## Mocking

Use `unittest.mock` or `pytest-mock` for external dependencies:

```python
from unittest.mock import Mock, patch

def test_fetch_user_data():
    # Mock the requests.get call
    with patch("myproject.api.requests.get") as mock_get:
        mock_get.return_value.json.return_value = {"id": 1, "name": "Alice"}
        mock_get.return_value.status_code = 200
        
        result = fetch_user_data(1)
        
        assert result["name"] == "Alice"
        mock_get.assert_called_once_with("https://api.example.com/users/1")
```

## Exception Testing

Test that exceptions are raised correctly:

```python
import pytest

def test_invalid_user_id_raises_error():
    with pytest.raises(ValueError, match="User ID must be positive"):
        process_user(-1)

def test_missing_file_raises_error():
    with pytest.raises(FileNotFoundError):
        load_config("nonexistent.json")
```

## Async Testing

Use `pytest-asyncio` for async functions:

```python
import pytest

@pytest.mark.asyncio
async def test_async_fetch_user():
    user = await fetch_user_async(1)
    assert user.id == 1
```

## Test Markers

Mark tests by category:

```python
@pytest.mark.slow
def test_large_dataset_processing():
    # Test that takes > 5 seconds
    ...

@pytest.mark.integration
def test_database_connection():
    # Test requiring database
    ...

@pytest.mark.skip(reason="Feature not implemented yet")
def test_future_feature():
    ...
```

Run specific markers:
```bash
pytest -m "not slow"           # Skip slow tests
pytest -m integration          # Only integration tests
```

## Coverage Expectations

- **Overall coverage:** > 80%
- **New code coverage:** > 90%
- **Critical paths:** 100%

Check coverage:
```bash
pytest --cov=src/myproject --cov-report=term-missing
```

Focus on missing lines shown in report.

## Test Organization

Mirror the source structure:

```
src/myproject/
├── models.py
└── utils.py

tests/
├── test_models.py      # Tests for models.py
└── test_utils.py       # Tests for utils.py
```

## Common Patterns

### Testing File Operations

Use `tmp_path` fixture:

```python
def test_save_config(tmp_path):
    config_file = tmp_path / "config.json"
    save_config(config_file, {"key": "value"})
    
    assert config_file.exists()
    assert config_file.read_text() == '{"key": "value"}'
```

### Testing Logging

Use `caplog` fixture:

```python
def test_logging_output(caplog):
    with caplog.at_level(logging.INFO):
        process_data()
    
    assert "Processing started" in caplog.text
```

### Testing CLI

Use `monkeypatch` for sys.argv:

```python
def test_cli_with_args(monkeypatch):
    monkeypatch.setattr("sys.argv", ["prog", "--verbose"])
    result = main()
    assert result == 0
```

## Avoid Common Pitfalls

- ❌ Don't test implementation details - test behavior
- ❌ Don't share state between tests - use fixtures
- ❌ Don't write tests that depend on execution order
- ❌ Don't mock what you don't own (mock at boundaries)
- ✅ Do test edge cases and error conditions
- ✅ Do use descriptive test names
- ✅ Do keep tests focused (one concept per test)
- ✅ Do clean up resources (use fixtures with cleanup)
