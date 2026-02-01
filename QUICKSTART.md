# Quick Reference - GitHub Copilot Custom Instructions

A cheat sheet for using and creating Copilot custom instructions.

## Three Types of Instructions

| Type | File Location | Scope | Use Case |
|------|---------------|-------|----------|
| **Repository-wide** | `.github/copilot-instructions.md` | Entire repository | Project architecture, build commands, general patterns |
| **Path-specific** | `.github/instructions/*.instructions.md` | Specific files matching glob | Language-specific rules, file type conventions |
| **Agent** | `AGENTS.md` (root) | AI coding agents | How agents should approach tasks and workflows |

## Quick Setup

### For a New Project

```bash
# 1. Create directories
mkdir -p .github/instructions

# 2. Create repository-wide instructions
touch .github/copilot-instructions.md

# 3. Create path-specific instructions
touch .github/instructions/python.instructions.md
touch .github/instructions/typescript.instructions.md

# 4. Create agent instructions
touch AGENTS.md
```

### Minimal copilot-instructions.md Template

```markdown
# Project Custom Instructions

## Repository Overview

**Type:** [Application type]
**Languages:** [Main languages]
**Frameworks:** [Key frameworks]

## Project Structure

```
src/              # Source code
tests/            # Test files
```

## Build and Test

```bash
# Install dependencies
[command]

# Run tests
[command]

# Build
[command]
```

## Coding Standards

- Standard 1
- Standard 2
```

### Minimal Path-Specific Instructions

```markdown
---
applyTo: "**/*.ext"
---

# File Type Guidelines

## Style Rules

- Rule 1
- Rule 2

## Common Patterns

```language
// Example
```
```

### Minimal AGENTS.md

```markdown
# AI Agent Instructions

## Working Approach

When working in this project:

1. Step 1
2. Step 2
3. Step 3

## Quality Standards

Before committing:
- Check 1
- Check 2
```

## Glob Patterns Reference

| Pattern | Matches |
|---------|---------|
| `**/*.py` | All Python files recursively |
| `**/*.ts,**/*.tsx` | All TypeScript files (both .ts and .tsx) |
| `src/**/*` | All files under src/ |
| `tests/**/*.test.ts` | Test files in tests/ |
| `**/*.md` | All Markdown files |
| `src/components/**/*.tsx` | React components in specific dir |

## Frontmatter Reference

### For Path-Specific Instructions

```yaml
---
applyTo: "**/*.py"              # Required: glob pattern
excludeAgent: "code-review"     # Optional: exclude from code review
---
```

### For Skills

```yaml
---
name: skill-name                # Required: kebab-case identifier
description: Brief description  # Required: one-line description
license: MIT                    # Required: license identifier
---
```

## What to Include

### In copilot-instructions.md

✅ **Include:**
- Project structure and key directories
- Exact build/test/run commands
- Non-obvious dependencies
- Known issues with workarounds
- Validation steps
- Required environment variables

❌ **Avoid:**
- Information Copilot already knows
- Obvious best practices
- Explanations of standard tools
- Task-specific instructions

### In Path-Specific Instructions

✅ **Include:**
- File-type specific standards
- Import organization patterns
- Testing conventions
- Error handling patterns
- Language-specific gotchas

❌ **Avoid:**
- General project info (use copilot-instructions.md)
- Unrelated file types
- Overly verbose explanations

### In AGENTS.md

✅ **Include:**
- How to approach tasks in this project
- Workflow patterns (TDD, etc.)
- Quality checks before committing
- Decision-making frameworks

❌ **Avoid:**
- Duplicating copilot-instructions.md
- General AI agent advice
- Unrelated to this project

## Common Commands to Document

### Build Commands

```markdown
## Build and Development

```bash
# Install dependencies (~30 seconds)
npm install

# Start dev server (auto-reload enabled)
npm run dev

# Build for production (~2 minutes)
npm run build

# Known issue: First build may fail with ENOMEM
# Workaround: NODE_OPTIONS=--max-old-space-size=4096 npm run build
```
```

### Test Commands

```markdown
## Testing

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=src --cov-report=html

# Run specific test
pytest tests/test_utils.py::test_function_name

# Run tests matching pattern
pytest -k "test_user"
```
```

### Quality Checks

```markdown
## Code Quality

```bash
# Format code
black src/ tests/

# Lint
ruff check --fix src/

# Type check
mypy src/

# Run all checks (do before commit)
black src/ tests/ && ruff check src/ && mypy src/ && pytest
```
```

## Testing Your Instructions

### Verify Copilot Uses Them

1. Open a file in your repository
2. Start typing or ask Copilot a question
3. Check the "References" section in Copilot's response
4. Confirm your instruction files are listed

### Validate Effectiveness

- **Do completions match your patterns?** - Check if Copilot follows your guidelines
- **Are suggestions accurate?** - Verify Copilot understands your project structure
- **Can it run commands?** - Test if documented commands work as shown

## Skill Creation Quick Guide

### 1. Create Structure

```bash
mkdir -p .github/skills/skill-name
touch .github/skills/skill-name/SKILL.md
```

### 2. Add Frontmatter and Content

```markdown
---
name: skill-name
description: One-line description
license: MIT
---

# Skill Name

Introduction (2-3 sentences).

## Core Principles

- Principle 1
- Principle 2

## Usage

Show examples.
```

### 3. Keep It Concise

- Context window is limited
- Only include non-obvious information
- Prefer examples over explanations
- Test with Copilot before committing

## Examples by Project Type

| Project Type | Key Instructions |
|--------------|------------------|
| **Python** | Virtual env setup, pytest patterns, type hints, Black/Ruff |
| **TypeScript** | tsconfig settings, import organization, type guards, testing |
| **React** | Component patterns, hooks usage, testing library, state management |
| **Node.js** | Module system, error handling, async patterns, middleware |
| **Full-stack** | Monorepo structure, API contracts, service dependencies |

## Troubleshooting

### Copilot Not Using Instructions

- ✓ Check file is saved
- ✓ Verify file location (.github/copilot-instructions.md)
- ✓ Check YAML frontmatter is valid
- ✓ Ensure glob patterns match your files
- ✓ Restart VS Code / IDE

### Instructions Too Long

- Remove obvious information
- Delete redundant sections
- Use examples instead of explanations
- Split into path-specific files

### Conflicting Instructions

- Be more specific in glob patterns
- Use `excludeAgent` in frontmatter
- Document priority explicitly
- Avoid contradictory rules

## Best Practices

1. **Start small** - Basic instructions, expand as needed
2. **Test commands** - Every command must work as shown
3. **Keep current** - Update when codebase changes
4. **Be specific** - Concrete > vague
5. **Show examples** - Code > prose
6. **Document gotchas** - Save others from same issues

## Resources

- [Official Docs](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions)
- [Custom Instructions Examples](https://docs.github.com/en/copilot/tutorials/customization-library/custom-instructions)
- [This Repository's Examples](examples/)

---

**Pro Tip:** Copy from [examples/](examples/) directory and customize for your project!
