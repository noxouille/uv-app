# AI Agents Directory

This directory contains agent-specific context files for Kimi Code CLI subagents.

## Available Agents

| Agent             | Directory        | Domain                                  | Current Sprint Focus       |
| ----------------- | ---------------- | --------------------------------------- | -------------------------- |
| **Profile Agent** | `profile-agent/` | User profiles, auth, geographic zones   | US-001, US-002 (Sprint 1)  |
| **Core Agent**    | `core-agent/`    | Infrastructure, database, cross-cutting | Database setup, auth infra |

## How to Spawn Agents

```bash
# From project root

# Spawn Profile Agent
kimi spawn -d docs/agents/profile-agent "Implement TASK-002: User Profile Model"

# Spawn Core Agent
kimi spawn -d docs/agents/core-agent "Implement TASK-001: Database Setup"
```

## Agent Collaboration Rules

1. **Shared Files**: Notify other agent before modifying `config/`, `database/base.py`, `pyproject.toml`
2. **Database Schema**: Core Agent owns migrations; Profile Agent defines model fields
3. **Daily Logs**: Both agents write to `docs/product-backlog/sprint-XX/daily-logs/`
4. **Task Updates**: Update task status in `docs/product-backlog/sprint-01/tasks/`

## Code Standards (All Agents)

- Line length: 88 characters
- Double quotes for strings
- 4-space indentation
- Type hints required
- Use `loguru` for logging (from `utils.logger`)
- Follow existing file patterns

## Project Context

- **Language**: Python 3.11+ (backend), TypeScript/Svelte 5 (frontend)
- **Backend**: FastAPI, SQLAlchemy 2.0, Alembic, SQLite
- **Frontend**: SvelteKit 5, Tailwind CSS, Superforms, Zod
- **Package Manager**: uv
- **Sprint**: 2-week cycles, see `docs/product-backlog/`
