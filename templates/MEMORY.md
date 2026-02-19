# MEMORY.md — AI Context & Architectural Decisions
# Keep this file updated. Writing it forces you to understand why things work the way they do.

---

## Project Overview

**Project name:** [your-project]
**Purpose:** [One sentence on what this system does]
**Primary language(s):** [e.g., Python 3.11, TypeScript 5.x]
**Stage:** [MVP / Production / Legacy]

---

## Architecture Decisions

> Record the WHY, not just the WHAT. AI can read code — it can't read your reasoning.
> Examples below use TypeScript/Node.js conventions — adapt to your stack.

| Decision | Choice Made | Why (not an alternative) |
|----------|-------------|--------------------------|
| Auth pattern | JWT in httpOnly cookies | XSS protection; localStorage ruled out |
| DB access | Repository pattern (`src/repos/`) | Testability + single query surface |
| Error handling | `AppError` class only, no raw throws | Consistent error shapes for API consumers |
| State management | [your choice] | [your reason] |
| API layer | [your choice] | [your reason] |

---

## Security Constraints (AI must respect these)

- **Never** store sensitive data in localStorage or sessionStorage
- **Never** log PII, tokens, or credentials — even in dev/debug paths
- **Never** write raw SQL — all queries go through `[your ORM/repo layer]`
- Auth checks happen at `[middleware location]`, not inside route handlers
- Secrets are injected via environment — no hardcoding, no `.env` committed

---

## Data Layer

**Database:** [PostgreSQL / MySQL / MongoDB / etc.]
**ORM / Query builder:** [Prisma / TypeORM / SQLAlchemy / etc.]
**Migration tool:** [Flyway / Alembic / Liquibase / etc.]

**Critical patterns:**
- All queries go through: `[path/to/repos/]`
- Transactions must wrap: [list multi-step operations]
- Soft deletes are used on: [list entities] — never hard delete these
- Pagination default: [cursor / offset], page size: [n]

---

## Testing Conventions

| Test type | Tool | Location | Notes |
|-----------|------|----------|-------|
| Unit | [Jest / Pytest / etc.] | `tests/unit/` | No I/O; mock everything |
| Integration | [Testcontainers / etc.] | `tests/integration/` | Real DB, no mocks |
| E2E | [Playwright / Cypress] | `tests/e2e/` | Against staging only |

**Rule:** AI-generated code paths must have 100% test coverage before merge.

---

## Deployment & Infrastructure

- **Deploy strategy:** [Blue-green / Rolling / Canary]
- **CI/CD:** [GitHub Actions / Azure DevOps / etc.] — pipeline at `[path]`
- **Environments:** `dev` → `staging` → `prod` (never skip staging)
- **Feature flags:** [tool name] — use before shipping anything experimental
- **Rollback procedure:** [brief description or link to runbook]

---

## AI-Free Zones (Human-written code only)

The following paths are too consequential for cognitive debt. AI may draft; a human must own and rewrite.

- `[src/auth/]` — Authentication & authorization
- `[src/payments/]` — Payment processing
- `[src/data/deletion.ts]` — Data deletion logic
- `[src/migrations/]` — All migration scripts
- `[Add your critical paths here]`

---

## Naming Conventions

| Context | Convention | Example |
|---------|------------|---------|
| Files | kebab-case | `user-profile.service.ts` |
| Classes | PascalCase | `UserProfileService` |
| Functions | camelCase | `getUserProfile()` |
| Constants | UPPER_SNAKE | `MAX_RETRY_ATTEMPTS` |
| DB tables | snake_case | `user_profiles` |
| Env vars | UPPER_SNAKE | `DATABASE_URL` |

---

## Key Business Rules AI Must Know

> Things that are non-obvious and would cause bugs if ignored.

- [Rule 1 — e.g., "A user can belong to multiple orgs but only have one active session per org"]
- [Rule 2 — e.g., "Invoices are immutable after 24h; create a credit note instead"]
- [Rule 3 — e.g., "Deleted users retain their data for 90 days per compliance requirements"]
- [Add more as your team discovers edge cases that confused AI output]

---

## Changelog

| Date | Author | Change |
|------|--------|--------|
| YYYY-MM-DD | [name] | Initial creation |
| | | |

---
*Maintained by the team. If the AI gives you wrong output, check here first — then update this file.*

---
*Part of the [Cognitive Debt Prevention Kit](https://github.com/kesslernity/cognitive-debt-prevention-kit) by [Kesslernity](https://kesslernity.com)*
