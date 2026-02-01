# GitHub Copilot Agent Reference Repository

A comprehensive reference repository providing custom instructions, skills, and best practices for GitHub Copilot agents. This repository helps AI coding assistants understand your project better and work more efficiently.

## 📋 What's Inside

### 🎯 Copilot Instructions

- **[.github/copilot-instructions.md](.github/copilot-instructions.md)** - Repository-wide custom instructions
- **[.github/instructions/](.github/instructions/)** - Path-specific instructions for different file types
- **[AGENTS.md](AGENTS.md)** - Agent-specific instructions for AI coding assistants

### 🛠️ Skills Library

Located in [.github/skills/](.github/skills/), each skill is a modular package that extends Copilot's capabilities:

#### Development Skills
- **[python-expert](/.github/skills/python-expert/SKILL.md)** - Python coding best practices with PEP 8, type hints, and modern patterns
- **[skill-creator](/.github/skills/skill-creator/SKILL.md)** - Meta-skill for creating new skills effectively
- **[mcp-builder](/.github/skills/mcp-builder/SKILL.md)** - Build MCP (Model Context Protocol) servers for LLM integration
- **[web-artifacts-builder](/.github/skills/web-artifacts-builder/SKILL.md)** - Create React/TypeScript web artifacts with modern tooling
- **[webapp-testing](/.github/skills/webapp-testing/SKILL.md)** - Test web applications using Playwright

#### Documentation Skills
- **[doc-coauthoring](/.github/skills/doc-coauthoring/SKILL.md)** - Collaborative document creation and testing workflow

### 📚 Examples & Templates

The [examples/](examples/) directory contains ready-to-use templates for various project types.

## 🚀 Quick Start

### For Your Own Repository

1. **Copy repository-wide instructions:**
   ```bash
   cp .github/copilot-instructions.md /path/to/your/repo/.github/
   ```

2. **Copy path-specific instructions:**
   ```bash
   cp -r .github/instructions /path/to/your/repo/.github/
   ```

3. **Copy agent instructions:**
   ```bash
   cp AGENTS.md /path/to/your/repo/
   ```

4. **Customize for your project** - Edit the files to match your specific needs

### Using Skills

Skills are located in `.github/skills/`. Each skill contains:
- `SKILL.md` - Main skill definition and instructions
- `references/` - Supporting documentation
- `scripts/` - Helper scripts
- `LICENSE.txt` - License information

To use a skill, reference it in your Copilot conversations or include it in your custom instructions.

## 📖 Types of Custom Instructions

### 1. Repository-Wide Instructions

File: `.github/copilot-instructions.md`

These apply to all Copilot requests in the repository. Include:
- Project overview and architecture
- Build and test commands
- Coding standards and conventions
- Dependencies and tech stack

### 2. Path-Specific Instructions

Files: `.github/instructions/*.instructions.md`

These apply to specific file types or directories:
- `python.instructions.md` - Python-specific guidelines
- `typescript.instructions.md` - TypeScript/JavaScript guidelines
- `markdown.instructions.md` - Documentation guidelines

### 3. Agent Instructions

File: `AGENTS.md` (root directory)

Instructions specifically for AI coding agents, including:
- How agents should approach tasks
- Preferred workflows and patterns
- Tool usage guidelines

## 🎓 How Copilot Uses These Instructions

When working in your repository, Copilot automatically:

1. Reads `copilot-instructions.md` for repository context
2. Applies path-specific instructions when editing matching files
3. Uses `AGENTS.md` for agent-level guidance
4. Combines all relevant instructions to provide better suggestions

## 🔧 Customization Guide

### For Different Project Types

Check the [examples/](examples/) directory for templates:
- **Python projects** - Django, Flask, FastAPI, data science
- **JavaScript/TypeScript** - React, Node.js, Next.js
- **Full-stack** - Monorepo patterns
- **Documentation** - Best practices for docs-as-code

### Best Practices

1. **Keep instructions concise** - Focus on non-obvious information
2. **Include actual commands** - Tested, working build/test commands
3. **Document workarounds** - Known issues and their solutions
4. **Update regularly** - Keep instructions in sync with code changes
5. **Be specific** - Concrete examples beat vague descriptions

## 📝 Creating New Skills

See the [skill-creator](.github/skills/skill-creator/SKILL.md) skill for comprehensive guidance on creating effective skills.

Key principles:
- **Concise is key** - Context window is limited
- **Set appropriate degrees of freedom** - Match specificity to task fragility
- **Include examples** - Show, don't just tell
- **Test thoroughly** - Validate that instructions work as intended

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Adding a New Skill

1. Create directory: `.github/skills/your-skill-name/`
2. Add `SKILL.md` with frontmatter and content
3. Include optional `references/`, `scripts/`, etc.
4. Test with Copilot
5. Submit PR with examples

### Improving Instructions

1. Test changes with actual Copilot usage
2. Verify commands work as documented
3. Keep style consistent with existing files
4. Update examples if needed

## 📚 Resources

### Official Documentation

- [GitHub Copilot Custom Instructions](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions)
- [About Response Customization](https://docs.github.com/en/copilot/concepts/prompting/response-customization)
- [Custom Instructions Examples](https://docs.github.com/en/copilot/tutorials/customization-library/custom-instructions)

### Community Resources

- [OpenAI Agents.md Specification](https://github.com/openai/agents.md)
- [Copilot Best Practices](https://github.blog/tag/github-copilot/)

## 📄 License

This repository is provided as a reference. Individual skills may have their own licenses (see each skill's LICENSE.txt file).

## 🙋 Support

For questions or issues:
- Check existing [examples/](examples/)
- Review [CONTRIBUTING.md](CONTRIBUTING.md)
- Open an issue for discussion

---

**Last Updated:** January 2026

**Maintained by:** GitHub Copilot Community
