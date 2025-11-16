---
name: best-practices
description: Production-ready code patterns and security best practices
---

# Best Practices - Production Ready Code

Enforces security-first, type-safe, tested code patterns.

## TypeScript Rules

### Always Use Strict Mode
```typescript
// tsconfig.json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true
  }
}
```

### Never Use `any`
```typescript
// ❌ Bad
const data: any = fetchData();

// ✅ Good
const data: unknown = fetchData();
if (isUserData(data)) {
  // Type guard
}
```

## API Security

### Always Validate Input
```typescript
import { z } from 'zod';

const UserSchema = z.object({
  email: z.string().email(),
  name: z.string().min(2).max(100)
});

// In your API
const validated = UserSchema.parse(req.body);
```

### Never Expose Sensitive Data
```typescript
// ❌ Bad
return user; // Includes password hash

// ✅ Good
const { password, ...safeUser } = user;
return safeUser;
```

## React Patterns

### Function Components Only
```typescript
// ✅ Always use function components
export const Component: FC<Props> = ({ prop1, prop2 }) => {
  return <div>{prop1}</div>;
};
```

### Proper State Management
```typescript
// Client state → Zustand
// Server state → React Query/SWR
// Form state → React Hook Form
```

## Testing Requirements

### Minimum 80% Coverage
- Unit tests for utilities
- Integration tests for APIs
- Component tests for UI
- E2E for critical paths

## Environment Variables

### Never Hardcode Secrets
```typescript
// ❌ Bad
const apiKey = "sk_live_abc123";

// ✅ Good
const apiKey = process.env.STRIPE_SECRET_KEY;
if (!apiKey) throw new Error('Missing STRIPE_SECRET_KEY');
```

## Error Handling

### Always Use Try-Catch
```typescript
export async function handler(req: Request, res: Response) {
  try {
    const result = await riskyOperation();
    res.json({ success: true, data: result });
  } catch (error) {
    console.error('Operation failed:', error);
    res.status(500).json({ 
      success: false, 
      error: 'Internal server error' 
    });
  }
}
```

## Quick Checks

Before committing, always verify:
- [ ] No `any` types
- [ ] All inputs validated
- [ ] Errors handled
- [ ] Tests passing
- [ ] No hardcoded secrets
- [ ] TypeScript compiles