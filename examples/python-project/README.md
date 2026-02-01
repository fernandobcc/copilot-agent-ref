# Python Project Example

This example shows how to structure Copilot instructions for a Python project.

## Project Structure

```
python-project/
├── .github/
│   ├── copilot-instructions.md       # Repository-wide instructions
│   └── instructions/
│       ├── python.instructions.md    # Python-specific guidelines
│       └── tests.instructions.md     # Testing guidelines
├── AGENTS.md                          # Agent instructions
├── src/
│   └── myproject/
│       ├── __init__.py
│       ├── models.py
│       └── utils.py
├── tests/
│   ├── __init__.py
│   └── test_utils.py
├── pyproject.toml                     # Project metadata and dependencies
├── uv.lock                            # Lockfile for reproducible installs
└── README.md
```

## Files Included

### 1. copilot-instructions.md

Repository-wide instructions covering:
- Project overview and architecture
- Setup and build commands
- Testing workflow
- Code organization patterns

### 2. python.instructions.md

Path-specific instructions for Python files:
- Coding standards (PEP 8, type hints)
- Import organization
- Error handling patterns
- Testing conventions

### 3. tests.instructions.md

Path-specific instructions for test files:
- Pytest patterns
- Fixture usage
- Naming conventions
- Coverage expectations

### 4. AGENTS.md

Agent-level instructions:
- How to approach refactoring
- When to add type hints
- Test-driven development workflow

## Quick Start

Copy these files to your Python project:

```bash
# Create directories
mkdir -p .github/instructions

# Copy instructions
cp copilot-instructions.md /path/to/your/project/.github/
cp python.instructions.md /path/to/your/project/.github/instructions/
cp tests.instructions.md /path/to/your/project/.github/instructions/
cp AGENTS.md /path/to/your/project/
```

Then customize them for your specific project:
- Update project name and description
- Add your specific dependencies and versions
- Document your build/test commands
- Include any project-specific patterns

## Customization Tips

1. **Keep it concise** - Focus on what Copilot doesn't already know
2. **Include actual commands** - Show exact commands that work
3. **Document workarounds** - Known issues and solutions
4. **Update regularly** - Keep instructions current with codebase
