# Repository Custom Instructions for GitHub Copilot

## Repository Overview

**Type:** Reference repository for GitHub Copilot custom instructions, skills, and best practices  
**Purpose:** Provide templates and examples for customizing Copilot agent behavior across different project types  
**Languages:** Markdown (documentation), Python (examples/scripts), JavaScript/TypeScript (examples)  
**Structure:** Modular skills library with reusable instruction templates

## Project Architecture

This repository is organized as a reference library:

```
.
├── .github/
│   ├── copilot-instructions.md       # This file (repository-wide instructions)
│   ├── instructions/                  # Path-specific instructions
│   │   ├── python.instructions.md
│   │   ├── typescript.instructions.md
│   │   └── markdown.instructions.md
│   └── skills/                        # Modular skills library
│       ├── python-expert/
│       └── skill-creator/
├── examples/                          # Project templates
│   ├── python-project/
│   ├── typescript-project/
│   └── fullstack-project/
├── AGENTS.md                          # Agent-level instructions
├── CONTRIBUTING.md                    # Contribution guidelines
└── README.md                          # Repository overview
```

## Key Files and Directories

- **/.github/skills/** - Reusable skill packages for specialized tasks
- **/examples/** - Complete project instruction templates for different tech stacks
- **AGENTS.md** - Instructions specifically for AI coding agents
- **README.md** - Documentation and usage guide

## Build and Validation

This repository contains documentation and templates, not executable code. However, when creating examples or scripts:

### Validation Steps

1. **Markdown linting**
   ```bash
   # Install markdownlint-cli if not present
   npm install -g markdownlint-cli
   
   # Lint all markdown files
   markdownlint '**/*.md' --ignore node_modules
   ```

2. **Python scripts validation** (for skill scripts)
   ```bash
   # Ensure Python 3.9+ is available
   python --version
   
   # Install dependencies if script has requirements
   pip install -r requirements.txt  # if exists
   
   # Run any validation scripts
   python .github/skills/*/scripts/*.py --help
   ```

3. **YAML frontmatter validation**
   ```bash
   # Check that all SKILL.md files have valid frontmatter
   grep -r "^---$" .github/skills/*/SKILL.md
   ```

### Testing Instructions

When adding or modifying instructions:

1. **Test with actual repository** - Copy instructions to a real project
2. **Verify Copilot behavior** - Ensure Copilot uses the instructions correctly
3. **Check for conflicts** - Ensure instructions don't contradict each other
4. **Validate commands** - All bash/shell commands must work as documented

## Coding Standards

### Markdown Files

- Use **ATX-style headers** (# ## ###)
- Maximum line length: **120 characters** for readability
- Use **fenced code blocks** with language identifiers
- Include **frontmatter** for skill files:
  ```yaml
  ---
  name: skill-name
  description: Brief description
  license: MIT
  ---
  ```

### Python Scripts (in skills)

- Follow **PEP 8** with Black formatting
- Use **type hints** for all functions
- Maximum line length: **100 characters**
- Include **docstrings** for all public functions
- Use **argparse** for CLI scripts

### File Naming Conventions

| Type | Convention | Example |
|------|-----------|---------|
| Skills | kebab-case | `python-expert`, `skill-creator` |
| Instructions | descriptive.instructions.md | `python.instructions.md` |
| Examples | kebab-case directories | `react-typescript-project` |

## Project Layout Best Practices

### Skills Directory Structure

Each skill should follow this pattern:
```
.github/skills/skill-name/
├── SKILL.md              # Required: Main skill definition
├── LICENSE.txt           # Optional: Specific license
├── references/           # Optional: Supporting docs
│   └── *.md
└── scripts/              # Optional: Helper scripts
    └── *.py
```

### Instructions Directory Structure

Path-specific instructions:
```
.github/instructions/
├── python.instructions.md       # For **/*.py
├── typescript.instructions.md   # For **/*.ts, **/*.tsx
├── markdown.instructions.md     # For **/*.md
└── config.instructions.md       # For config files
```

## Dependencies and Tools

This repository has **minimal dependencies** by design:

### Optional Tools (for validation)

- **markdownlint-cli** - Markdown linting
- **Python 3.9+** - For skill scripts
- **Node.js 18+** - For examples with npm scripts

### No Build Process Required

This is a **documentation repository**. Files are used as-is by:
- GitHub Copilot (reads `.md` files directly)
- Users copying templates to their projects
- AI agents reading instructions

## Working with This Repository

### Adding New Skills

1. Create directory: `.github/skills/new-skill-name/`
2. Add `SKILL.md` with proper frontmatter
3. Follow the [skill-creator](.github/skills/skill-creator/SKILL.md) guidelines
4. Keep skill focused and concise (context window is limited)
5. Test with Copilot before committing

### Adding New Instructions

1. Determine scope:
   - Repository-wide → Update `copilot-instructions.md`
   - Path-specific → Create/update file in `instructions/`
   - Agent-specific → Update `AGENTS.md`
2. Use clear, actionable language
3. Include working code examples
4. Test with actual Copilot usage
5. Document any workarounds or gotchas

### Adding Examples

1. Create directory: `examples/project-type-name/`
2. Include all three instruction types:
   - `copilot-instructions.md`
   - `instructions/` directory
   - `AGENTS.md`
3. Add `README.md` explaining the example
4. Ensure all commands are tested and work
5. Include common pitfalls section

## Important Notes

### Context Window Awareness

**The context window is a limited resource.** When writing instructions:

- ✅ Include non-obvious project-specific information
- ✅ Document validated commands and workflows
- ✅ Explain workarounds for known issues
- ❌ Avoid repeating what Copilot already knows
- ❌ Don't include unnecessary explanations
- ❌ Skip obvious best practices

### Instruction Priority

When multiple instruction types apply:

1. **Personal instructions** (user's Copilot settings) - Highest priority
2. **Repository instructions** (this file) - Medium priority  
3. **Organization instructions** - Lowest priority

All sets combine but avoid conflicts. Be specific and unambiguous.

### File Size Limits

Keep instruction files concise:
- `copilot-instructions.md`: **~2 pages** maximum
- Path-specific instructions: **~1 page** each
- Skills: **As needed** but optimize for clarity

## Validation Checklist

Before committing changes:

- [ ] All markdown files pass linting
- [ ] All code examples are tested and working
- [ ] Frontmatter is valid YAML
- [ ] File paths and globs are correct
- [ ] Commands include version requirements if needed
- [ ] No contradictory instructions
- [ ] Changes tested with actual Copilot usage

## Common Patterns

### Documenting Build Commands

Always include:
- Exact command to run
- Required pre-conditions
- Expected output or side effects
- Time estimates for long commands
- Known issues and workarounds

Example:
```bash
# Install dependencies (takes ~30 seconds)
npm install

# Build the project (takes ~2 minutes)
npm run build

# Known issue: First build may fail with ENOMEM
# Workaround: Increase Node memory with NODE_OPTIONS=--max-old-space-size=4096
```

### Documenting Architecture

Focus on:
- Where to find specific types of files
- How modules/components interact
- Configuration file locations
- Testing patterns
- Deployment workflows

## Search and Discovery

This repository is designed for:
- **Copying templates** to new projects
- **Reference documentation** for instruction patterns
- **Learning examples** of effective Copilot customization

The structure prioritizes browsability and clarity over code execution.

---

**When in doubt:** Trust these instructions. Only search for information if these instructions are incomplete or incorrect.
