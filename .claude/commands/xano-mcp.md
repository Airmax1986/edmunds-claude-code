---
name: xano-mcp
description: Secure Xano database operations via Snappy MCP (no API keys in code)
---

# Xano MCP - Secure Database Operations

Uses Snappy MCP to interact with Xano without exposing API keys.

## One-Time Setup

1. Visit https://mcp.snappy.ai and OAuth authenticate
2. Add this to `.vscode/mcp.json`:

```json
{
  "servers": [{
    "name": "snappy-xano",
    "type": "http",
    "url": "wss://mcp.snappy.ai/v1/stream",
    "headers": {
      "Authorization": "Bearer ${SNAPPY_OAUTH_TOKEN}"
    }
  }]
}
```

## Available Commands

### Create Table
"Create a [table_name] table with [fields]"
Example: "Create a products table with name, price, description, and stock fields"

### List Tables
"Show all Xano tables"

### Get Schema
"Show schema for [table_name] table"

### Generate CRUD
"Generate CRUD endpoints for [table_name]"

## Best Practices

1. **Never hardcode API keys** - Always use Snappy MCP OAuth
2. **Use TypeScript types** - Generate from Xano schema
3. **Implement pagination** - For large datasets
4. **Add validation** - Use zod for runtime validation

## Example Workflow

```typescript
// 1. Create table via MCP
"Create users table with email, name, role fields"

// 2. Generate TypeScript types
interface User {
  id: number;
  email: string;
  name: string;
  role: 'user' | 'admin';
  created_at: string;
}

// 3. Create service layer
class XanoService {
  async getUsers() {
    // MCP handles auth securely
    return await xano_list_tables('users');
  }
}
```