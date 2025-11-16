---
name: mcp-setup
description: Configure all MCP servers for maximum automation
---

# MCP Server Setup - Full Automation

## Quick Install All Essential MCPs

```bash
# 1. Install MCP packages
npm install -g \
  @modelcontextprotocol/server-filesystem \
  @modelcontextprotocol/server-github \
  @modelcontextprotocol/server-postgres \
  @modelcontextprotocol/server-playwright
```

## Configuration

Create `.mcp/config.json`:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-filesystem", 
               "--allowed-directories", "/Users/maximilian/Documents"]
    },
    "github": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-github"],
      "env": { 
        "GITHUB_TOKEN": "${GITHUB_TOKEN}"
      }
    },
    "postgres": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-postgres"],
      "env": { 
        "DATABASE_URL": "${DATABASE_URL}"
      }
    },
    "playwright": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-playwright"]
    },
    "xano": {
      "type": "http",
      "url": "wss://mcp.snappy.ai/v1/stream",
      "headers": { 
        "Authorization": "Bearer ${SNAPPY_OAUTH_TOKEN}"
      }
    }
  }
}
```

## What Each MCP Enables

### Filesystem MCP
- Direct file operations (10x faster than commands)
- Bulk file updates
- Search across codebase

### GitHub MCP  
- Create branches/PRs programmatically
- Manage issues
- Trigger workflows

### PostgreSQL MCP
- Direct SQL queries
- Schema migrations
- Performance analysis

### Playwright MCP
- E2E test generation
- Visual regression testing
- Browser automation

## Usage Examples

### With Filesystem MCP
"Update all React components to use new design tokens"
→ MCP updates 50 files in seconds

### With GitHub MCP
"Create a PR with these changes"
→ Branch, commit, PR created automatically

### With PostgreSQL MCP
"Optimize slow queries in the dashboard"
→ Direct EXPLAIN ANALYZE and index creation

### With Playwright MCP
"Generate E2E tests for the checkout flow"
→ Complete test suite auto-generated