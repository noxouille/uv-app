# TASK-001: Database Setup

**Story**: US-001  
**Status**: 🔴 Todo  
**Assignee**: —

---

## Goal

Set up database infrastructure for the application.

---

## Acceptance Criteria

- [ ] Database connection configured
- [ ] Migration system (Alembic) initialized
- [ ] Base model with common fields (id, created_at, updated_at)
- [ ] Environment-based configuration
- [ ] Connection pooling

---

## Technical Approach

**Stack**: SQLAlchemy 2.0 + Alembic + SQLite (MVP)

**Files to Create**:

```
config/database.py          # Connection & session management
database/base.py            # Base model class
database/migrations/        # Alembic migrations
```

**Key Implementation**:

- Use `create_engine()` with SQLite for MVP
- `SessionLocal` for dependency injection
- `Base` model with auto-timestamping

**Environment**: `DATABASE_URL` variable (defaults to SQLite)

---

## Testing

- [ ] Can connect to database
- [ ] Can run initial migration
- [ ] Session dependency works in FastAPI

---

## Progress

| Date | Status      | Notes |
| ---- | ----------- | ----- |
| —    | Not started | —     |
