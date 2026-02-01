# TypeScript Project Example

Example Copilot instructions for a TypeScript/Node.js project.

## Project Structure

```
typescript-project/
├── .github/
│   ├── copilot-instructions.md
│   └── instructions/
│       ├── typescript.instructions.md
│       └── tests.instructions.md
├── AGENTS.md
├── src/
│   ├── index.ts
│   ├── services/
│   ├── models/
│   └── utils/
├── tests/
│   └── utils.test.ts
├── package.json
├── tsconfig.json
└── README.md
```

## Files Included

### 1. copilot-instructions.md

Repository-wide instructions covering:
- Project setup with npm/yarn
- Build and development workflow
- Testing with Jest/Vitest
- TypeScript configuration
- Code organization

### 2. typescript.instructions.md

Path-specific instructions for TypeScript files:
- Type safety guidelines
- Interface vs type usage
- Async/await patterns
- Error handling
- Module organization

### 3. tests.instructions.md

Testing guidelines:
- Jest/Vitest patterns
- Mocking strategies
- Test organization
- Coverage requirements

### 4. AGENTS.md

Agent workflow instructions:
- TDD approach for TypeScript
- Type-first development
- Refactoring patterns

## Quick Start

```bash
# Copy to your project
cp -r typescript-project/.github /path/to/your/project/
cp typescript-project/AGENTS.md /path/to/your/project/

# Customize for your needs
# - Update package.json references
# - Adjust TypeScript strict settings
# - Modify test framework (Jest vs Vitest)
```

## Customization Tips

1. **Package manager** - Update commands for npm/yarn/pnpm
2. **Test framework** - Adjust for your testing library
3. **Build tool** - Document webpack/vite/esbuild specifics
4. **Type strictness** - Match your tsconfig.json settings
