# Contributing to Copilot Agent Reference

Thank you for your interest in contributing! This document provides guidelines for adding skills, instructions, and examples to this repository.

## How to Contribute

### Types of Contributions

1. **New Skills** - Add specialized skills to `.github/skills/`
2. **New Instruction Templates** - Add path-specific instructions
3. **Example Projects** - Add complete project templates to `examples/`
4. **Documentation Improvements** - Enhance existing documentation
5. **Bug Fixes** - Fix errors in existing instructions

## Adding a New Skill

### 1. Plan Your Skill

Before creating a skill, ask:

- **What specific knowledge does this provide?** - What does Copilot NOT already know?
- **Is it focused enough?** - Can it fit in 1-2 pages?
- **Will it be reusable?** - Can others benefit from this?
- **Does it already exist?** - Check existing skills first

### 2. Create Skill Structure

```bash
# Create skill directory
mkdir -p .github/skills/your-skill-name

# Create required file
touch .github/skills/your-skill-name/SKILL.md

# Optional: Add supporting materials
mkdir -p .github/skills/your-skill-name/references
mkdir -p .github/skills/your-skill-name/scripts
```

### 3. Write SKILL.md

Start with frontmatter:

```markdown
---
name: your-skill-name
description: Brief one-line description (80 chars max)
license: MIT
---

# Your Skill Name

Concise introduction (2-3 sentences).

## Core Principles

- Key principle 1
- Key principle 2
- Key principle 3

## Usage

Show concrete examples with code blocks.

## Examples

Demonstrate patterns with working code.
```

### 4. Follow Skill Guidelines

**Be Concise:**
- Context window is limited
- Every sentence must justify its token cost
- Prefer examples over explanations

**Set Appropriate Degrees of Freedom:**
- High freedom: Text-based instructions for flexible tasks
- Medium freedom: Pseudocode with parameters
- Low freedom: Specific scripts for fragile operations

**Include Only Non-Obvious Information:**
- ✅ Project-specific patterns
- ✅ Known workarounds for issues
- ✅ Validated command sequences
- ❌ Information Copilot already knows
- ❌ Obvious best practices
- ❌ Redundant explanations

### 5. Test Your Skill

Before submitting:

1. **Test with Copilot** - Verify Copilot uses the instructions
2. **Validate examples** - Ensure all code examples work
3. **Check frontmatter** - Verify YAML is valid
4. **Review length** - Keep skills concise

### 6. Submit Pull Request

```bash
# Create branch
git checkout -b add-skill-your-skill-name

# Add files
git add .github/skills/your-skill-name/

# Commit with descriptive message
git commit -m "Add your-skill-name skill for [purpose]"

# Push and create PR
git push origin add-skill-your-skill-name
```

## Adding Path-Specific Instructions

### 1. Determine Scope

Choose the right glob pattern for your instructions:

```yaml
---
applyTo: "**/*.py"              # All Python files
applyTo: "src/**/*.ts"          # TypeScript in src/
applyTo: "**/*.md"              # All Markdown files
applyTo: "tests/**/*"           # All test files
---
```

### 2. Create Instruction File

```bash
# Create instructions directory if needed
mkdir -p .github/instructions

# Create instruction file
touch .github/instructions/your-type.instructions.md
```

### 3. Write Instructions

Template:

```markdown
---
applyTo: "**/*.ext"
excludeAgent: "code-review"  # Optional
---

# File Type Guidelines

Introduction and scope.

## Style Rules

Specific coding standards.

## Common Patterns

```language
// Example code
```

## Avoid Common Pitfalls

- ❌ Don't do this
- ✅ Do this instead
```

### 4. Keep It Focused

Path-specific instructions should:
- **Target one file type** or directory
- **Be ~1 page** in length
- **Include concrete examples**
- **Document non-obvious patterns**

## Adding Example Projects

### 1. Choose Project Type

Common types:
- Python (Django, Flask, FastAPI)
- JavaScript/TypeScript (React, Node.js, Next.js)
- Full-stack (monorepo patterns)
- Specific frameworks or tools

### 2. Create Directory Structure

```bash
mkdir -p examples/your-project-type
cd examples/your-project-type

# Create all instruction types
touch README.md
touch copilot-instructions.md
mkdir -p instructions
touch instructions/language.instructions.md
touch AGENTS.md
```

### 3. Include Complete Set

Each example needs:

1. **README.md** - Overview and usage
2. **copilot-instructions.md** - Repository-wide instructions
3. **instructions/*.instructions.md** - Path-specific instructions
4. **AGENTS.md** - Agent workflow

### 4. Make It Real

- **Test all commands** - Ensure they work as documented
- **Include prerequisites** - Required tools and versions
- **Document workarounds** - Known issues and solutions
- **Show validation** - How to verify it works
- **Add common pitfalls** - What goes wrong and how to fix

### 5. Write Clear README

```markdown
# Project Type Example

Brief description.

## Project Structure

```
Show actual file structure
```

## Files Included

Explain each instruction file.

## Quick Start

```bash
# Exact commands to use this template
```

## Customization Tips

How to adapt for specific needs.
```

## Documentation Improvements

### Fixing Errors

1. **Identify the issue** - What's wrong or unclear?
2. **Make minimal change** - Fix specific problem
3. **Test the fix** - Verify it works
4. **Update related docs** - Keep consistency

### Enhancing Clarity

1. **Add examples** - Show, don't just tell
2. **Improve organization** - Better headers, structure
3. **Fix formatting** - Consistent Markdown style
4. **Update references** - Ensure links work

## Code Quality Standards

### Markdown Files

- **ATX-style headers** (# ## ###)
- **120 character** line limit
- **Fenced code blocks** with language identifiers
- **Frontmatter** for skills and instructions

### Python Scripts

- **PEP 8** with Black formatting
- **Type hints** on all functions
- **Docstrings** for public APIs
- **argparse** for CLI tools

### Example Code

- **Must work** when copy-pasted
- **Include imports** - Show all needed imports
- **Add comments** - Explain non-obvious parts
- **Follow project standards** - Match the example's style

## Testing Your Contribution

### Before Submitting

- [ ] **Markdown lints** - Run `markdownlint '**/*.md'`
- [ ] **Frontmatter valid** - Check YAML syntax
- [ ] **Examples work** - Test all code samples
- [ ] **Links valid** - Verify all links resolve
- [ ] **Tested with Copilot** - Confirm instructions are used
- [ ] **No typos** - Proofread carefully
- [ ] **Consistent style** - Matches existing files

### Validation Commands

```bash
# Lint Markdown
markdownlint '**/*.md' --ignore node_modules

# Check Python scripts
black --check .github/skills/*/scripts/*.py
ruff check .github/skills/*/scripts/

# Validate YAML frontmatter
grep -r "^---$" .github/skills/*/SKILL.md
```

## Pull Request Guidelines

### PR Title Format

```
Add [skill-name] skill for [purpose]
Fix [issue] in [file]
Improve [section] documentation
Add [project-type] example
```

### PR Description Template

```markdown
## What

Brief description of the change.

## Why

Why this change is needed.

## Testing

How you tested this:
- [ ] Tested with Copilot
- [ ] Validated examples work
- [ ] Checked markdown linting
- [ ] Verified links

## Related Issues

Closes #123 (if applicable)
```

### Review Criteria

Your PR will be reviewed for:

1. **Usefulness** - Does this add value?
2. **Conciseness** - Is it as brief as possible?
3. **Accuracy** - Do examples work?
4. **Consistency** - Does it match existing style?
5. **Completeness** - Is everything needed included?

## Getting Help

If you need help:

1. **Check existing examples** - Look at similar contributions
2. **Read skill-creator** - See [skill-creator](.github/skills/skill-creator/SKILL.md)
3. **Review AGENTS.md** - Understand agent workflows
4. **Open an issue** - Ask questions before starting large work

## Code of Conduct

- **Be respectful** - Treat others with kindness
- **Be constructive** - Provide helpful feedback
- **Be collaborative** - Work together toward better docs
- **Be patient** - Reviews take time

## Recognition

Contributors will be:
- Acknowledged in release notes
- Listed in contributors section (when added)
- Credited in any derived works

## License

By contributing, you agree that your contributions will be licensed under the same license as this project (MIT).

---

**Thank you for contributing!** Your efforts help make Copilot more effective for everyone.
