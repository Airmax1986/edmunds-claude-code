# Project Context

## Tech Stack
- **Frontend**: React 18, TypeScript 5.3+, Tailwind CSS 3.4+, Zustand
- **Backend**: Node.js 20+, Express 5, TypeScript
- **Database**: Xano (via Snappy MCP)
- **Auth**: Supabase Auth or Xano JWE tokens
- **Testing**: Vitest, React Testing Library, Playwright

## Available Commands
```bash
# Edmund's Commands (14)
/component-new      # React components
/page-new          # Next.js pages  
/api-new           # API endpoints
/api-test          # Test APIs
/api-protect       # Add auth/validation
/feature-plan      # Plan features
/code-explain      # Explain code
/code-optimize     # Optimize performance
/docs-generate     # Generate docs
/types-gen         # TypeScript types

# Our Additions
/xano-mcp          # Secure Xano operations
/best-practices    # Production patterns
```

## Project Structure
```
src/
├── frontend/
│   ├── components/    # React components
│   ├── pages/        # Page components
│   ├── hooks/        # Custom hooks
│   ├── stores/       # Zustand stores
│   └── lib/          # Utilities
├── backend/
│   ├── api/          # API routes
│   ├── services/     # Business logic
│   ├── middleware/   # Auth, validation
│   └── lib/          # Shared utilities
└── shared/
    └── types/        # Shared TypeScript types
```

## Quick Start

### Create a Feature
```bash
# 1. Plan it
/feature-plan user dashboard

# 2. Backend API
/api-new dashboard stats endpoint

# 3. Database
/xano-mcp create dashboard_stats table

# 4. Frontend
/component-new Dashboard component

# 5. Test it
/api-test dashboard endpoint
```

## Development Workflow

1. **Always use TypeScript** - No `any` types
2. **Validate everything** - Use zod schemas
3. **Test as you go** - Minimum 80% coverage
4. **Security first** - Never expose keys
5. **Document changes** - Update this file

## Environment Variables
```bash
# .env.local
XANO_WORKSPACE_ID=xxx
SNAPPY_OAUTH_TOKEN=xxx
SUPABASE_URL=xxx
SUPABASE_ANON_KEY=xxx
```

## Git Workflow
```bash
git checkout -b feat/feature-name
# Make changes
git commit -m "feat: add feature"
git push origin feat/feature-name
# Create PR
```