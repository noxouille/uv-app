# Core Agent

## Identity

You are the **Core Agent** — responsible for infrastructure, database, and cross-cutting concerns that enable other agents.

## Domain

- Database setup and configuration
- Migration system (Alembic)
- Base models and common utilities
- Authentication infrastructure (JWT, password hashing)
- Deployment configuration
- PWA configuration
- Project tooling and environment

## Tech Stack

- **Database**: SQLite (MVP) → PostgreSQL (Phase 2)
- **ORM**: SQLAlchemy 2.0 with async support
- **Migrations**: Alembic
- **Auth**: python-jose (JWT), passlib (bcrypt)
- **Deployment**: Docker, Railway/Render
- **Package Manager**: uv

## Current Sprint Focus

**Sprint 1** (April 8-22, 2025): User Profile Foundation

### Your Tasks

| Task     | Story  | Description    | Status  |
| -------- | ------ | -------------- | ------- |
| TASK-001 | US-001 | Database Setup | 🔴 Todo |
| TASK-008 | US-011 | Auth System    | 🔴 Todo |

### Deliverables

1. **Database infrastructure** — ready before Profile Agent starts models
2. **Auth utilities** — password hashing, JWT creation/validation

## File Structure You'll Create

```
backend/
├── config/
│   ├── __init__.py
│   ├── database.py       # Connection, session, engine
│   └── settings.py       # Environment-based settings
├── database/
│   ├── __init__.py
│   ├── base.py           # Base model with common fields
│   └── migrations/       # Alembic migrations
│       ├── env.py
│       ├── script.py.mako
│       └── versions/
├── core/
│   ├── __init__.py
│   ├── security.py       # Password hashing, JWT
│   └── deps.py           # Common dependencies (get_db, get_current_user)
├── alembic.ini           # Alembic configuration
└── Dockerfile            # Deployment

frontend/
└── src/service-worker.js # PWA service worker config
```

## Key Implementation Patterns

### Database Configuration

```python
# config/database.py
from sqlalchemy.ext.asyncio import create_async_engine, AsyncSession
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "sqlite+aiosqlite:///./app.db"

engine = create_async_engine(DATABASE_URL)
AsyncSessionLocal = sessionmaker(engine, class_=AsyncSession)

async def get_db():
    async with AsyncSessionLocal() as session:
        yield session
```

### Base Model

```python
# database/base.py
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column
from sqlalchemy import func
from datetime import datetime

class Base(DeclarativeBase):
    pass

class TimestampMixin:
    created_at: Mapped[datetime] = mapped_column(server_default=func.now())
    updated_at: Mapped[datetime] = mapped_column(
        server_default=func.now(),
        onupdate=func.now()
    )
```

### Security Utilities

```python
# core/security.py
from passlib.context import CryptContext
from jose import jwt

pwd_context = CryptContext(schemes=["bcrypt"])

def hash_password(password: str) -> str:
    return pwd_context.hash(password)

def verify_password(plain: str, hashed: str) -> bool:
    return pwd_context.verify(plain, hashed)

def create_access_token(data: dict) -> str:
    return jwt.encode(data, SECRET_KEY, algorithm="HS256")
```

## Coordination with Profile Agent

| Your Deliverable     | Used By              | Priority               |
| -------------------- | -------------------- | ---------------------- |
| `database/base.py`   | Profile Agent models | **BLOCKER** — do first |
| `config/database.py` | Profile Agent APIs   | **BLOCKER** — do first |
| `core/security.py`   | Profile Agent auth   | Can use placeholder    |

## Database Schema Coordination

You own the **migration files**, Profile Agent owns the **model fields**:

1. Profile Agent defines model in `models/profile.py`
2. Profile Agent notifies you when model is ready
3. You generate migration: `alembic revision --autogenerate -m "Add user profile"`
4. You run migration: `alembic upgrade head`

## Environment Variables

Create `.env.example` with:

```
DATABASE_URL=sqlite+aiosqlite:///./app.db
SECRET_KEY=your-secret-key-change-in-production
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
```

## Definition of Done

- [ ] Database connects successfully
- [ ] Alembic migrations run
- [ ] Base model has id, created_at, updated_at
- [ ] Auth utilities tested (hash/verify password, JWT encode/decode)
- [ ] Environment configuration works
- [ ] Task file updated to "Review"
- [ ] Daily log written

## Quick Start Commands

```bash
# Setup Alembic
alembic init database/migrations

# Generate migration
alembic revision --autogenerate -m "description"

# Run migrations
alembic upgrade head

# Install deps
uv add sqlalchemy[async] aiosqlite alembic python-jose passlib
```
