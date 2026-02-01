# AI Agent Instructions

This file provides guidance for AI coding agents working in this repository or using it as a reference.

## Repository Context

This is a **reference repository** containing custom instructions, skills, and templates for GitHub Copilot. When working here, understand that:

- Files are **documentation**, not executable code (except example scripts)
- Users will **copy** these files to their own projects
- Quality and clarity are **paramount** - these instructions guide other AI agents
- Context window efficiency is **critical** - every token counts

## Working in This Repository

### Primary Tasks You'll Handle

1. **Creating new skills** - Follow the skill-creator guidelines strictly
2. **Writing instruction templates** - For different project types
3. **Improving existing documentation** - Based on user feedback
4. **Validating instruction quality** - Ensuring they work with Copilot
5. **Organizing examples** - Creating clear, tested templates

### Workflow Patterns

#### When Creating a New Skill

1. **Research thoroughly**
   - Understand the domain deeply
   - Identify what Copilot doesn't already know
   - Find the non-obvious patterns and gotchas

2. **Design concisely**
   - Every sentence must justify its token cost
   - Prefer examples over explanations
   - Match specificity to task fragility (see skill-creator guidelines)

3. **Structure properly**
   ```
   .github/skills/skill-name/
   ├── SKILL.md              # Frontmatter + concise instructions
   ├── LICENSE.txt           # If different from repo license
   ├── references/           # Supporting docs (only if needed)
   └── scripts/              # Helper scripts (only if needed)
   ```

4. **Validate effectiveness**
   - Test that Copilot actually uses the instructions
   - Verify examples work as shown
   - Ensure no conflicts with other skills

#### When Writing Instruction Templates

1. **Choose the right type**
   - Repository-wide: `copilot-instructions.md` - Project architecture, build commands
   - Path-specific: `.github/instructions/*.instructions.md` - File type rules
   - Agent-specific: `AGENTS.md` - How agents should work

2. **Include essential information**
   - ✅ Project structure and key file locations
   - ✅ Tested build/test/run commands
   - ✅ Known issues with workarounds
   - ✅ Non-obvious dependencies or conventions
   - ❌ Information Copilot already knows
   - ❌ Obvious best practices
   - ❌ Excessive explanations

3. **Use concrete examples**
   ```markdown
   ❌ "Follow best practices for error handling"
   ✅ "Always wrap network calls in try/except with specific exceptions:
       try:
           response = requests.get(url, timeout=10)
       except requests.Timeout:
           logger.error(f"Timeout fetching {url}")
           return None"
   ```

#### When Improving Documentation

1. **Understand the user's pain point**
   - What didn't work?
   - What was unclear?
   - What did Copilot misunderstand?

2. **Make targeted changes**
   - Fix the specific issue
   - Don't over-expand (context window!)
   - Test the improvement

3. **Maintain consistency**
   - Follow existing style and structure
   - Update related files if needed
   - Keep examples aligned

### Code Modification Patterns

#### Markdown Files

- Use **ATX headers** (# ## ###) consistently
- Keep lines under **120 characters**
- Use **fenced code blocks** with language identifiers
- Include **frontmatter** for skills:
  ```yaml
  ---
  name: skill-name
  description: One-line description
  license: MIT
  ---
  ```

#### Python Scripts (in skills/)

- **PEP 8** + **Black** formatting
- **Type hints** on all functions
- **Docstrings** for public APIs
- Maximum **100 characters** per line
- Use **pathlib** for file operations
- Use **argparse** for CLI scripts

#### Examples

- Must be **fully tested** and working
- Include **README.md** in each example
- Show **complete setup** from scratch
- Document **common pitfalls**
- Keep updated with latest best practices

## Decision Making Frameworks

### When Unsure About Scope

Ask yourself:
1. **Does Copilot already know this?** → If yes, skip it
2. **Is this specific to this project type?** → If yes, include it
3. **Will this save exploration time?** → If yes, include it
4. **Can I show it in 2-3 lines?** → If yes, use example; if no, reconsider

### When Choosing Detail Level

| Situation | Approach | Example |
|-----------|----------|---------|
| **Standard pattern** | Brief mention | "Use pytest for testing" |
| **Project-specific pattern** | Show example | "Tests inherit from BaseTestCase with auto-mocked DB" |
| **Fragile/error-prone** | Detailed steps | "Build must run in this order: clean → install → generate → build" |
| **Context-dependent** | Guiding principles | "Prefer composition over inheritance for data processors" |

### When Handling Conflicts

If instructions might conflict:
1. **Be specific about scope** - Use path-specific instructions
2. **State priorities explicitly** - "For legacy code, ignore line length; for new code, enforce 100 chars"
3. **Use frontmatter** - Set `excludeAgent` to prevent conflicts
4. **Document the conflict** - Explain why different rules apply

## Quality Standards

### Every Instruction Should

- ✅ Be **tested** with actual Copilot usage
- ✅ Contain **working** code examples
- ✅ Include **version info** when relevant
- ✅ Document **workarounds** for known issues
- ✅ Use **precise** language (avoid vague terms)
- ✅ **Justify** its context window cost

### Every Skill Should

- ✅ Have **clear scope** and purpose
- ✅ Follow **skill-creator** guidelines
- ✅ Include **frontmatter** with metadata
- ✅ Be **maximally concise**
- ✅ Provide **executable** examples where appropriate
- ✅ Specify **degrees of freedom** appropriately

### Every Example Should

- ✅ **Work** when followed exactly
- ✅ Include **all necessary files**
- ✅ Document **prerequisites**
- ✅ Show **validation steps**
- ✅ Cover **common scenarios**
- ✅ Note **platform differences** if any

## Common Tasks and Approaches

### Creating Python Project Instructions

```markdown
Focus on:
- Project structure (where models, views, controllers live)
- Virtual environment setup (specific commands that work)
- Dependency management (requirements.txt, poetry, pipenv)
- Test runner commands (pytest, unittest, nose2)
- Linting/formatting (ruff, black, mypy configurations)
- Database migrations (alembic, Django, SQLAlchemy)
- Known issues (common errors and their fixes)
```

### Creating JavaScript/TypeScript Instructions

```markdown
Focus on:
- Package manager (npm, yarn, pnpm - which one and why)
- Build system (webpack, vite, esbuild, turbo)
- TypeScript config (strict mode, paths, decorators)
- Test framework (jest, vitest, mocha)
- Linting (eslint configurations)
- Module resolution (aliases, imports)
- Build targets (browsers, Node versions)
```

### Creating Full-Stack Instructions

```markdown
Focus on:
- Monorepo structure (if applicable)
- Service dependencies (what needs to run for local dev)
- Database setup (migrations, seeds, Docker)
- API contracts (OpenAPI, GraphQL schemas)
- Environment variables (required vars, examples)
- Development workflow (which order to start services)
- Testing strategy (unit, integration, e2e)
```

## Tool Usage Guidelines

### File Operations

- **Read** before modifying - understand existing structure
- **Batch operations** - use multi_replace when possible
- **Validate** - check files after changes
- **Respect structure** - maintain existing organization

### Search Strategies

1. **Start broad** - Use semantic search for concepts
2. **Get specific** - Use grep for exact patterns
3. **Verify context** - Read surrounding code
4. **Cross-reference** - Check related files

### Testing and Validation

- **Run commands** - Verify examples work
- **Test with Copilot** - Ensure instructions are actually used
- **Check references** - Validate links and paths
- **Lint markdown** - Use markdownlint if available

## Error Patterns to Avoid

### ❌ Over-Explaining

```markdown
Bad: "Python is a high-level programming language. When writing Python code, 
you should follow PEP 8, which is the style guide. PEP 8 recommends using 
4 spaces for indentation..."

Good: "Use 4-space indentation, max line length 100, Black-compatible formatting."
```

### ❌ Vague Instructions

```markdown
Bad: "Use appropriate error handling"

Good: "Catch specific exceptions: FileNotFoundError for missing files, 
ValueError for invalid input. Always log errors with context."
```

### ❌ Untested Commands

```markdown
Bad: "Run npm install && npm build"
       (might not work - needs npm run build)

Good: "npm install    # Takes ~30s
       npm run build  # Takes ~2min, outputs to dist/"
```

### ❌ Missing Context

```markdown
Bad: "The API uses JWT tokens"

Good: "API authentication: Include header 'Authorization: Bearer <token>'.
       Tokens expire after 1hr. Refresh endpoint: POST /auth/refresh"
```

## Meta-Instructions

### Updating This File

When improving AGENTS.md:
1. Keep it focused on **how to work in this repo**
2. Provide **decision frameworks**, not just rules
3. Use **examples** of good vs bad patterns
4. Update based on **actual agent behavior** you observe
5. Stay under **~3 pages** total length

### Self-Improvement Loop

As you work on tasks:
1. **Note patterns** - What works well? What's confusing?
2. **Identify gaps** - What guidance is missing?
3. **Propose updates** - Suggest improvements to instructions
4. **Validate changes** - Ensure improvements actually help

### Working with Users

When users ask for new content:
1. **Clarify intent** - Understand the actual need
2. **Research thoroughly** - Don't guess or hallucinate
3. **Show examples** - Demonstrate what you'll create
4. **Iterate** - Refine based on feedback
5. **Document decisions** - Explain your choices

## Reference Materials

### Within This Repo

- [skill-creator](.github/skills/skill-creator/SKILL.md) - How to create effective skills
- [python-expert](.github/skills/python-expert/SKILL.md) - Example of well-structured skill
- [copilot-instructions.md](.github/copilot-instructions.md) - Repository-wide patterns
- [examples/](examples/) - Complete project templates

### External Resources

- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [OpenAI Agents.md Spec](https://github.com/openai/agents.md)
- [Custom Instructions Guide](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions)

## Success Criteria

Your work is successful when:

- ✅ Users can **copy-paste** instructions and they work immediately
- ✅ Copilot **demonstrably uses** the instructions effectively
- ✅ Instructions are **concise** without sacrificing clarity
- ✅ Examples are **tested** and complete
- ✅ Documentation is **current** and accurate
- ✅ Context window is **respected** - no bloat

---

**Trust these instructions.** Only search for additional information if you find gaps or errors. Focus on creating high-quality, tested, concise content that serves as an excellent reference for Copilot customization.
