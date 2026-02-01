---
applyTo: "**/*.ts,**/*.tsx,**/*.js,**/*.jsx"
---

# TypeScript/JavaScript Guidelines

When working with TypeScript or JavaScript files in this repository:

## Type Safety

**Prefer TypeScript** for all new code. Use strict mode:

```typescript
// tsconfig.json should include:
{
  "compilerOptions": {
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "noImplicitReturns": true
  }
}
```

## Code Style

- **Maximum line length**: 100 characters
- **Indentation**: 2 spaces
- **Semicolons**: Use them consistently
- **Quotes**: Prefer double quotes for strings
- **Trailing commas**: Use for multi-line arrays/objects

## Type Annotations

Always provide explicit types for function parameters and return values:

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

## Interfaces vs Types

Use **interfaces** for object shapes, **types** for unions/intersections:

```typescript
// Use interface for objects
interface User {
  id: number;
  name: string;
  email: string;
}

// Use type for unions
type Status = "pending" | "active" | "inactive";

// Use type for complex combinations
type UserWithStatus = User & { status: Status };
```

## Async/Await

Always use async/await over raw promises:

```typescript
// ✅ Good
async function fetchUserData(userId: number): Promise<User> {
  try {
    const response = await fetch(`/api/users/${userId}`);
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}: ${response.statusText}`);
    }
    return await response.json();
  } catch (error) {
    console.error("Failed to fetch user:", error);
    throw error;
  }
}

// ❌ Avoid
function fetchUserData(userId: number): Promise<User> {
  return fetch(`/api/users/${userId}`)
    .then(res => res.json())
    .catch(err => console.error(err));
}
```

## Error Handling

Be explicit about error types:

```typescript
class ValidationError extends Error {
  constructor(message: string, public field: string) {
    super(message);
    this.name = "ValidationError";
  }
}

function validateEmail(email: string): void {
  if (!email.includes("@")) {
    throw new ValidationError("Invalid email format", "email");
  }
}

try {
  validateEmail(userInput);
} catch (error) {
  if (error instanceof ValidationError) {
    console.error(`Validation failed for ${error.field}: ${error.message}`);
  } else {
    throw error;
  }
}
```

## React/JSX Patterns (if applicable)

### Component Definition

Use function components with TypeScript:

```typescript
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: "primary" | "secondary";
}

export function Button({ label, onClick, variant = "primary" }: ButtonProps): JSX.Element {
  return (
    <button className={`btn btn-${variant}`} onClick={onClick}>
      {label}
    </button>
  );
}
```

### Hooks

Type custom hooks properly:

```typescript
import { useState, useEffect } from "react";

interface UseUserResult {
  user: User | null;
  loading: boolean;
  error: Error | null;
}

function useUser(userId: number): UseUserResult {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);

  useEffect(() => {
    fetchUser(userId)
      .then(setUser)
      .catch(setError)
      .finally(() => setLoading(false));
  }, [userId]);

  return { user, loading, error };
}
```

## Module Organization

Structure imports clearly:

```typescript
// 1. External dependencies
import React, { useState, useEffect } from "react";
import { z } from "zod";

// 2. Internal modules
import { formatDate } from "@/utils/date";
import { Button } from "@/components/Button";

// 3. Type imports (separate)
import type { User, UserRole } from "@/types";

// 4. Styles
import "./styles.css";
```

## Null Safety

Use optional chaining and nullish coalescing:

```typescript
// ✅ Good
const userName = user?.profile?.name ?? "Unknown";
const count = config?.maxRetries ?? 3;

// ❌ Avoid
const userName = user && user.profile && user.profile.name || "Unknown";
```

## Array Operations

Prefer functional methods over imperative loops:

```typescript
// ✅ Good
const activeUsers = users.filter(u => u.status === "active");
const userNames = users.map(u => u.name);
const totalScore = scores.reduce((sum, score) => sum + score, 0);

// ❌ Avoid (unless performance critical)
const activeUsers = [];
for (let i = 0; i < users.length; i++) {
  if (users[i].status === "active") {
    activeUsers.push(users[i]);
  }
}
```

## Object Immutability

Use spread operators for immutable updates:

```typescript
// ✅ Good
const updatedUser = { ...user, name: "New Name" };
const updatedItems = [...items, newItem];

// ❌ Avoid
user.name = "New Name";
items.push(newItem);
```

## Type Guards

Create type guards for runtime type checking:

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

function makeSound(animal: Animal): void {
  if (isDog(animal)) {
    animal.bark(); // TypeScript knows it's a Dog
  } else {
    animal.meow(); // TypeScript knows it's a Cat
  }
}
```

## Common Patterns for This Repository

### Validation with Zod (if used)

```typescript
import { z } from "zod";

const SkillSchema = z.object({
  name: z.string().min(1),
  description: z.string(),
  license: z.string().optional(),
});

type Skill = z.infer<typeof SkillSchema>;

function parseSkill(data: unknown): Skill {
  return SkillSchema.parse(data);
}
```

### File Operations (Node.js)

```typescript
import { readFile, writeFile } from "fs/promises";
import { join } from "path";

async function readSkillFile(skillName: string): Promise<string> {
  const filePath = join(".github", "skills", skillName, "SKILL.md");
  try {
    return await readFile(filePath, "utf-8");
  } catch (error) {
    if ((error as NodeJS.ErrnoException).code === "ENOENT") {
      throw new Error(`Skill not found: ${skillName}`);
    }
    throw error;
  }
}
```

## Avoid Common Pitfalls

- ❌ Don't use `any` type - use `unknown` if type is truly unknown
- ❌ Don't ignore TypeScript errors with `@ts-ignore` without explanation
- ❌ Don't use `var` - always use `const` or `let`
- ❌ Don't mutate function parameters
- ✅ Do use const for values that don't change
- ✅ Do use === instead of == for comparisons
- ✅ Do provide default values for optional parameters
- ✅ Do use readonly for immutable arrays/objects
