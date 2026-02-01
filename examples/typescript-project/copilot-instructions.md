# TypeScript Project Custom Instructions

## Repository Overview

**Type:** Node.js TypeScript application  
**Node Version:** 18+  
**Package Manager:** npm  
**TypeScript Version:** 5.0+  
**Testing:** Vitest  
**Build Tool:** Vite

## Project Structure

```
src/
├── index.ts          # Application entry point
├── services/         # Business logic services
├── models/           # Type definitions and interfaces
├── utils/            # Utility functions
└── types/            # Shared types

tests/                # Test files (mirrors src/)
├── services/
└── utils/

dist/                 # Build output (gitignored)
node_modules/         # Dependencies (gitignored)
```

## Setup and Build

### Initial Setup

```bash
# Install dependencies (~1 minute)
npm install

# Verify installation
node --version  # Should be 18+
npm --version
```

### Development Workflow

```bash
# Start development server with hot reload
npm run dev

# Server starts on http://localhost:3000
# Auto-reloads on file changes
```

### Build Commands

```bash
# Build for production (~15 seconds)
npm run build
# Output: dist/

# Preview production build
npm run preview

# Type checking only (no build)
npm run typecheck
```

## Testing

### Running Tests

```bash
# Run all tests
npm test

# Run tests in watch mode
npm run test:watch

# Run tests with coverage
npm run test:coverage
# Opens coverage report in browser

# Run specific test file
npm test -- utils.test.ts

# Run tests matching pattern
npm test -- --grep="user"
```

**Expected:** Tests run in < 5 seconds. Coverage should be > 80%.

### Test Files

- Naming: `*.test.ts` or `*.spec.ts`
- Location: Mirror source structure in `tests/`
- Pattern: Describe-It style with Vitest

## Code Quality

### Type Checking

```bash
# Check types across entire project
npm run typecheck

# TypeScript will report any type errors
# Must pass before committing
```

### Linting

```bash
# Run ESLint
npm run lint

# Auto-fix issues
npm run lint:fix
```

### Formatting

```bash
# Format with Prettier
npm run format

# Check formatting without changes
npm run format:check
```

## TypeScript Configuration

Using **strict mode** with these key settings:

```json
{
  "compilerOptions": {
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "esModuleInterop": true,
    "skipLibCheck": true
  }
}
```

**All code must pass strict type checking.**

## Coding Standards

### Type Annotations

Always provide explicit types for function signatures:

```typescript
// ✅ Good
function processUser(id: number, name: string): UserResult {
  return { id, name, processed: true };
}

// ❌ Avoid
function processUser(id, name) {
  return { id, name, processed: true };
}
```

### Interfaces vs Types

- Use **interfaces** for object shapes
- Use **types** for unions, intersections, utilities

```typescript
// Interface for objects
interface User {
  id: number;
  name: string;
}

// Type for unions
type Status = "active" | "inactive" | "pending";

// Type for complex compositions
type UserWithStatus = User & { status: Status };
```

### Async/Await

Always use async/await over promises:

```typescript
async function fetchData(url: string): Promise<Data> {
  try {
    const response = await fetch(url);
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }
    return await response.json();
  } catch (error) {
    logger.error("Fetch failed:", error);
    throw error;
  }
}
```

### Error Handling

Create custom error classes:

```typescript
class ValidationError extends Error {
  constructor(message: string, public field: string) {
    super(message);
    this.name = "ValidationError";
  }
}

function validateInput(data: unknown): Data {
  if (!isValid(data)) {
    throw new ValidationError("Invalid data", "input");
  }
  return data as Data;
}
```

## Import Organization

Organize imports in groups:

```typescript
// 1. External dependencies
import { readFile } from "fs/promises";
import express from "express";

// 2. Internal modules
import { UserService } from "@/services/UserService";
import { formatDate } from "@/utils/date";

// 3. Type imports (separate)
import type { User, UserRole } from "@/types";
```

## Common Patterns

### Service Classes

```typescript
export class UserService {
  constructor(private readonly db: Database) {}

  async getUser(id: number): Promise<User | null> {
    const result = await this.db.query("SELECT * FROM users WHERE id = ?", [id]);
    return result.rows[0] ?? null;
  }

  async createUser(data: CreateUserDto): Promise<User> {
    // Validation
    this.validateUserData(data);
    
    // Creation
    const result = await this.db.query(
      "INSERT INTO users (name, email) VALUES (?, ?)",
      [data.name, data.email]
    );
    
    return { id: result.insertId, ...data };
  }

  private validateUserData(data: CreateUserDto): void {
    if (!data.email.includes("@")) {
      throw new ValidationError("Invalid email", "email");
    }
  }
}
```

### Type Guards

```typescript
interface Dog {
  type: "dog";
  bark(): void;
}

interface Cat {
  type: "cat";
  meow(): void;
}

type Animal = Dog | Cat;

function isDog(animal: Animal): animal is Dog {
  return animal.type === "dog";
}

function handleAnimal(animal: Animal): void {
  if (isDog(animal)) {
    animal.bark(); // TypeScript knows it's a Dog
  } else {
    animal.meow(); // TypeScript knows it's a Cat
  }
}
```

### Utility Types

Use TypeScript's utility types:

```typescript
// Pick specific properties
type UserPreview = Pick<User, "id" | "name">;

// Make all properties optional
type PartialUser = Partial<User>;

// Make all properties required
type RequiredUser = Required<User>;

// Omit properties
type UserWithoutPassword = Omit<User, "password">;
```

## Environment Variables

Type environment variables:

```typescript
// src/config.ts
import { z } from "zod";

const envSchema = z.object({
  NODE_ENV: z.enum(["development", "production", "test"]),
  PORT: z.string().transform(Number),
  DATABASE_URL: z.string().url(),
  API_KEY: z.string().min(1),
});

export const env = envSchema.parse(process.env);
```

Usage:
```typescript
import { env } from "@/config";

const server = app.listen(env.PORT);
```

## Known Issues and Workarounds

### Issue: Module resolution errors

**Problem:** Can't resolve `@/` imports

**Solution:** Ensure tsconfig.json has:
```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```

### Issue: Type-only imports warning

**Problem:** ESLint warns about type imports

**Solution:** Use `import type`:
```typescript
import type { User } from "@/types";
```

## Validation Checklist

Before committing:

1. **Type check:** `npm run typecheck` - Must pass
2. **Lint:** `npm run lint` - Must pass
3. **Format:** `npm run format` - Auto-fixes
4. **Tests:** `npm test` - All must pass
5. **Build:** `npm run build` - Must complete

All steps must succeed.

## Dependencies

Main dependencies:
- **express** - Web framework
- **zod** - Runtime validation
- **winston** - Logging

Development dependencies:
- **typescript** - Type system
- **vite** - Build tool
- **vitest** - Testing
- **eslint** - Linting
- **prettier** - Formatting

## Environment Variables

Required:
- `NODE_ENV` - Environment (development/production/test)
- `PORT` - Server port
- `DATABASE_URL` - Database connection
- `API_KEY` - API authentication

Example `.env`:
```bash
NODE_ENV=development
PORT=3000
DATABASE_URL=postgresql://localhost/mydb
API_KEY=your_key_here
```

---

**Trust these instructions.** Commands are tested and working. Only search if something fails.
