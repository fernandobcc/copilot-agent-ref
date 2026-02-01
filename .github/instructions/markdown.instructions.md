---
applyTo: "**/*.md"
excludeAgent: "coding-agent"
---

# Markdown Documentation Guidelines

When working with Markdown files in this repository:

## File Structure

All Markdown files should follow this structure:

```markdown
# Title (H1 - only one per file)

Brief introduction or overview.

## Section (H2)

Content for the section.

### Subsection (H3)

Detailed content.
```

## Headers

- Use **ATX-style headers** (`#`, `##`, `###`) - never setext style
- Only **one H1** (`#`) per file (the title)
- Don't skip header levels (H1 → H3 without H2)
- Add blank line before and after headers

```markdown
✅ Good:

# Main Title

## Section One

Content here.

## Section Two

❌ Avoid:

# Main Title
## Section One (no blank line)
Content here.
#### Subsection (skipped H3)
```

## Code Blocks

Always use **fenced code blocks** with language identifiers:

````markdown
✅ Good:

```python
def hello():
    print("Hello, World!")
```

```bash
npm install
npm run build
```

❌ Avoid:

```
print("No language specified")
```

    Indented code block (hard to read)
````

## Lists

### Unordered Lists

Use `-` for consistency:

```markdown
✅ Good:

- First item
- Second item
  - Nested item (2 spaces)
  - Another nested item
- Third item

❌ Avoid:

* Mixed bullet
- styles in
+ same list
```

### Ordered Lists

Use `1.` for all items (auto-numbering):

```markdown
✅ Good:

1. First step
1. Second step
1. Third step

Easier to reorder and maintain.

❌ Avoid:

1. First step
2. Second step
3. Third step

(Harder to reorder)
```

## Links

### Internal Links

Use **relative paths** for files in the repo:

```markdown
✅ Good:

See [Python instructions](.github/instructions/python.instructions.md)
Check the [skill-creator](.github/skills/skill-creator/SKILL.md)

❌ Avoid:

See [Python instructions](/home/user/repo/.github/instructions/python.instructions.md)
Check the [skill-creator](https://github.com/user/repo/blob/main/.github/skills/skill-creator/SKILL.md)
```

### External Links

Include protocol and descriptive text:

```markdown
✅ Good:

See the [GitHub Copilot documentation](https://docs.github.com/en/copilot)

❌ Avoid:

See docs.github.com/en/copilot
Click [here](https://docs.github.com) for more info
```

## Emphasis

- Use `**bold**` for **important terms** or **strong emphasis**
- Use `*italic*` for *mild emphasis* or *introducing new terms*
- Use `` `backticks` `` for `code`, `filenames`, `commands`

```markdown
✅ Good:

Run the `build.sh` script to compile the project.
The **primary goal** is to create reusable templates.
Configure your *preferred* editor settings.

❌ Avoid:

Run the build.sh script (no backticks for script name)
The PRIMARY GOAL is... (all caps instead of bold)
```

## Tables

Use tables for structured data with clear alignment:

```markdown
| Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Value A  | Value B  | Value C  |
| Value D  | Value E  | Value F  |

With alignment:

| Left align | Center align | Right align |
|:-----------|:------------:|------------:|
| Left       | Center       | Right       |
```

## Horizontal Rules

Use `---` (three hyphens) for section breaks:

```markdown
✅ Good:

Content above.

---

Content below.

❌ Avoid:

***
___
```

## Line Length

- **Target**: 100-120 characters per line
- **Hard limit**: 120 characters
- Break long lines at natural points (after punctuation, before links)

## Frontmatter (for instruction files)

Use YAML frontmatter for path-specific instructions:

```markdown
---
applyTo: "**/*.py"
excludeAgent: "code-review"
---

# Python Instructions

Content starts here...
```

Required fields for instruction files:
- `applyTo`: Glob pattern(s) for files this applies to
- `excludeAgent` (optional): "code-review" or "coding-agent"

## Skill Files

Skill files (`.github/skills/*/SKILL.md`) must have:

```markdown
---
name: skill-name
description: Brief one-line description
license: MIT
---

# Skill Name

Introduction and purpose.

## Section

Content...
```

Required frontmatter:
- `name`: Kebab-case skill identifier
- `description`: One-line description
- `license`: License identifier (MIT, Apache-2.0, etc.)

## Examples in Documentation

When showing examples, use clear labels:

````markdown
✅ Good:

```python
# Good example
def greet(name: str) -> str:
    return f"Hello, {name}!"
```

❌ Avoid:

```python
# Bad example
def greet(name):
    return "Hello, " + name
```

Or use comparison blocks:

| ✅ Do | ❌ Don't |
|-------|----------|
| Use type hints | Omit type annotations |
| `f"Hello {name}"` | `"Hello " + name` |
````

## Callouts and Admonitions

Use blockquotes for notes and warnings:

```markdown
> **Note:** This feature requires Python 3.9+

> **Warning:** This command will delete all local changes

> **Tip:** Use `--help` flag for more options
```

## File References

When mentioning files:
- Use **backticks** for filenames: `README.md`
- Use **links** when referencing: [README.md](README.md)
- Use **bold** for emphasis on directories: **/.github/skills/**

## Common Patterns for This Repository

### Documenting Skills

```markdown
---
name: skill-name
description: What the skill does in one line
license: MIT
---

# Skill Name

Brief introduction (2-3 sentences).

## Core Principles

- Principle 1
- Principle 2

## Usage

How to use this skill with examples.

## Examples

Show concrete examples with code blocks.
```

### Documenting Instructions

````markdown
---
applyTo: "**/*.ext"
---

# File Type Guidelines

Introduction.

## Style Rules

Specific guidelines with examples.

## Common Patterns

```language
// Example code
```

## Avoid Common Pitfalls

- ❌ Don't do this
- ✅ Do this instead
````

### Example Projects

```markdown
# Project Name

Brief description.

## Prerequisites

- Tool 1 (version)
- Tool 2 (version)

## Setup

```bash
# Step 1
command1

# Step 2
command2
```

## Usage

How to use the project.
```

## Validation

Before committing Markdown files:

```bash
# Install markdownlint (if not installed)
npm install -g markdownlint-cli

# Lint all Markdown files
markdownlint '**/*.md' --ignore node_modules

# Fix auto-fixable issues
markdownlint '**/*.md' --fix --ignore node_modules
```

## Avoid Common Pitfalls

- ❌ Don't use HTML when Markdown works (`<br>` instead of double space)
- ❌ Don't skip blank lines around blocks (headers, code, lists)
- ❌ Don't mix indentation (spaces vs tabs)
- ❌ Don't use bare URLs (use `[text](url)` format)
- ✅ Do use consistent bullet styles
- ✅ Do specify language for code blocks
- ✅ Do use relative paths for internal links
- ✅ Do keep lines under 120 characters
