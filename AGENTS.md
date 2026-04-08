# AGENTS.md

This document provides essential information for AI coding agents working on this project.

## Project Overview

This is a **Meal Planning & Grocery Optimization Application** — a Progressive Web App (PWA) that helps Canadian households plan meals, generate shopping lists, and optimize grocery purchases based on local promotions.

- **Project Name**: almea
- **Language**: Python 3.11+ (backend), TypeScript/React (frontend)
- **Architecture**: PWA with FastAPI backend
- **Target Market**: Canada (initially Quebec)
- **Package Manager**: [uv](https://github.com/astral-sh/uv)
- **Build System**: Hatchling
- **License**: Apache License 2.0

## Project Structure

```
.
├── app.py                          # Main application entry point (to be developed)
├── pyproject.toml                  # Project configuration
├── uv.lock                        # Locked dependency versions
├── utils/                         # Utility modules
│   ├── __init__.py
│   └── logger.py                  # Loguru-based logging
├── test/                          # Test files
│   └── example_logging.py
├── docs/                          # Documentation (see docs/README.md)
│   ├── DEVELOPMENT_PLAN.md        # Main development guide
│   ├── product-backlog/           # User stories and sprints
│   ├── technical-specs/           # Architecture docs
│   ├── decisions/                 # ADRs and PO decisions
│   ├── templates/                 # Task templates
│   └── internal/                  # Source documents (PDFs)
├── README.md
├── LICENSE
└── .gitignore
```

## AI Agent Configuration

This project uses **specialized AI agents** organized by domain. Each agent has its own context file in `docs/agents/`.

### Available Agents

| Agent             | Focus                                     | Context File                             |
| ----------------- | ----------------------------------------- | ---------------------------------------- |
| **Profile Agent** | User profiles, auth, geographic zones     | `docs/agents/profile-agent/AGENTS.md`    |
| **Core Agent**    | Database, infrastructure, cross-cutting   | `docs/agents/core-agent/AGENTS.md`       |

### How to Spawn Agents

```bash
# From project root

# Spawn Profile Agent (for profile-related tasks)
kimi spawn -d docs/agents/profile-agent "Implement TASK-002: User Profile Model"

# Spawn Core Agent (for infrastructure tasks)
kimi spawn -d docs/agents/core-agent "Implement TASK-001: Database Setup"
```

The `-d` flag tells Kimi Code to use that directory's `AGENTS.md` as additional context.

### Agent Task Assignments (Sprint 1)

| Task                        | Assigned Agent                            |
| --------------------------- | ----------------------------------------- |
| TASK-001: Database Setup    | Core Agent                                |
| TASK-002: User Profile Model| Profile Agent                             |
| TASK-003: Profile API       | Profile Agent                             |
| TASK-004: Profile Form UI   | Profile Agent                             |
| TASK-005: Location Model    | Profile Agent                             |
| TASK-006: Geocoding Service | Profile Agent                             |
| TASK-007: Location UI       | Profile Agent                             |
| TASK-008: Auth System       | Core Agent (backend) + Profile Agent (UI) |

---

## Quick Start for AI Agents

### 1. Read the Development Plan

👉 **Start here**: [docs/DEVELOPMENT_PLAN.md](docs/DEVELOPMENT_PLAN.md)

This document explains:

- How sprints are organized
- How to pick up and work on tasks
- How to report progress
- The definition of done

### 2. Check Current Sprint

👉 **Current sprint**: [docs/product-backlog/sprint-01/sprint-goals.md](docs/product-backlog/sprint-01/sprint-goals.md)

See what we're building right now and pick a task to work on.

### 3. Understand the Requirements

Source documents (in `docs/internal/`):

- **Cahier des charges interne.pdf** — Complete functional specification (French)
- **Feasibility_Analysis_CAD_Revised.docx** — Technical and economic analysis
- **Presention-produit-subvention.pdf** — Product presentation

## Development Workflow

### Sprint-Based Development

We work in **2-week sprints** following this structure:

```
Sprint N
├── sprint-goals.md          # What we're building
├── user-stories.md          # Detailed requirements
├── tasks/                   # Individual task specs
│   ├── task-001-*.md
│   ├── task-002-*.md
│   └── ...
├── daily-logs/              # Progress updates
│   └── YYYY-MM-DD.md
└── retrospective.md         # Post-sprint review
```

### How to Work on a Task

1. **Find a task** in `docs/product-backlog/sprint-XX/tasks/`
2. **Check status**: Look for "Todo" tasks
3. **Update status**: Change to "In Progress" in the task file
4. **Create branch**: `git checkout -b feature/task-XXX-short-name`
5. **Do the work**: Follow the acceptance criteria
6. **Update progress**: Add entries to the task's Progress Log
7. **Write tests**: Ensure acceptance criteria are met
8. **Update status**: Change to "Review" when done
9. **Create PR**: Link to the user story

### Daily Log

When you work on the project, add an entry to the daily log:

```markdown
# Daily Log — YYYY-MM-DD

## Completed

- [x] What you finished

## In Progress

- What you're working on

## Blockers

- Any issues needing PO attention

## Notes for PO

- Questions or decisions needed
```

## Technology Stack

### Backend

| Component   | Choice                                 |
| ----------- | -------------------------------------- |
| Framework   | FastAPI                                |
| Database    | SQLite (MVP) → PostgreSQL (production) |
| ORM         | SQLAlchemy 2.0                         |
| Migrations  | Alembic                                |
| Auth        | JWT + passlib                          |
| HTTP Client | httpx                                  |

### Frontend

| Component  | Choice                            |
| ---------- | --------------------------------- |
| Framework  | SvelteKit 5 + TypeScript          |
| Styling    | Tailwind CSS                      |
| State      | Svelte 5 Runes (`$state`)         |
| Forms      | Superforms + Zod                  |
| Build Tool | Vite + PWA Plugin                 |

### Core Dependencies

- **loguru** (~0.7.3) — Logging
- **pydantic** — Data validation
- **sqlalchemy** — Database ORM
- **alembic** — Database migrations

## Code Style Guidelines

### Python Style

- **Line length**: 88 characters
- **Quotes**: Use double quotes for strings
- **Indentation**: 4 spaces
- **Type hints**: Encouraged
- **Imports**: Sorted automatically by ruff

Example:

```python
from fastapi import APIRouter, Depends
from sqlalchemy.orm import Session

from config.database import get_db
from models.user_profile import UserProfile
from schemas.user_profile import UserProfileCreate

router = APIRouter(prefix="/profiles", tags=["profiles"])

@router.post("", response_model=UserProfileResponse, status_code=201)
def create_profile(
    profile: UserProfileCreate,
    db: Session = Depends(get_db)
) -> UserProfileResponse:
    """Create a new user profile."""
    logger.info("Creating profile", adults_count=profile.adults_count)
    # Implementation
```

### Logging Conventions

Always use `loguru`:

```python
from utils import logger

# Basic logging
logger.info("Operation completed")

# Structured logging
logger.info("Profile created", profile_id=profile_id, diet_type=diet_type)

# Error logging
logger.error("Database connection failed", error=str(e))

# Exception handling
@logger.catch
def risky_operation():
    pass
```

## Build and Development Commands

### Environment Setup

```bash
# Create virtual environment
uv venv

# Activate environment
source .venv/bin/activate  # Linux/macOS

# Install dependencies
uv pip install -e .
```

### Install Additional Dependencies

```bash
# Backend dependencies
uv pip install fastapi uvicorn sqlalchemy alembic pydantic httpx

# Add to pyproject.toml for persistence
```

### Linting and Formatting

```bash
# Format code with ruff
ruff format .

# Check linting
ruff check .

# Fix auto-fixable issues
ruff check --fix .
```

### Running the Application

```bash
# Development server
uv run uvicorn app:app --reload

# Run tests
uv run pytest
```

## Definition of Done

### For Tasks

- [ ] Code implemented following project style
- [ ] Unit tests written and passing
- [ ] Manual testing completed
- [ ] Task file updated with progress
- [ ] Status changed to "Review"

### For User Stories

- [ ] All acceptance criteria met
- [ ] Feature works on mobile (PWA)
- [ ] PO has reviewed and accepted
- [ ] Story file updated with "Done" status

### For Sprints

- [ ] All "Must" stories completed
- [ ] Sprint demo completed
- [ ] Retrospective documented
- [ ] Next sprint planned

## Common Patterns

### Database Model Pattern

```python
# models/user_profile.py
from sqlalchemy import Column, Integer, String, Float, JSON, Enum
from database.base import BaseModel

class DietType(str, Enum):
    OMNIVORE = "omnivore"
    VEGETARIAN = "vegetarian"

class UserProfile(BaseModel):
    __tablename__ = "user_profiles"

    adults_count = Column(Integer, default=1)
    diet_type = Column(Enum(DietType), default=DietType.OMNIVORE)
    allergies = Column(JSON, default=list)
```

### Pydantic Schema Pattern

```python
# schemas/user_profile.py
from pydantic import BaseModel, Field

class UserProfileCreate(BaseModel):
    adults_count: int = Field(default=1, ge=1, le=10)
    diet_type: DietType = DietType.OMNIVORE
    allergies: list[str] = Field(default_factory=list)

class UserProfileResponse(UserProfileCreate):
    id: int
    created_at: datetime

    class Config:
        from_attributes = True
```

### API Endpoint Pattern

```python
# api/v1/endpoints/profiles.py
from fastapi import APIRouter, Depends, HTTPException
from sqlalchemy.orm import Session

from config.database import get_db
from models.user_profile import UserProfile
from schemas.user_profile import UserProfileCreate, UserProfileResponse

router = APIRouter(prefix="/profiles", tags=["profiles"])

@router.post("", response_model=UserProfileResponse, status_code=201)
def create_profile(
    profile: UserProfileCreate,
    db: Session = Depends(get_db)
):
    db_profile = UserProfile(**profile.model_dump())
    db.add(db_profile)
    db.commit()
    db.refresh(db_profile)
    return db_profile
```

## Important Notes

### For JavaScript/Node.js Work (SvelteKit)

- **Use `bun` instead of `npm`** for all JS/Node operations
- `bun install` instead of `npm install`
- `bun run dev` to start development server
- `bun run build` to create production build
- `bun run preview` to preview production build

### SvelteKit Project Structure

```
frontend/
├── src/
│   ├── lib/                    # Shared code
│   │   ├── components/         # Svelte components (.svelte)
│   │   ├── schemas/            # Zod validation schemas
│   │   └── stores/             # Svelte 5 runes state (.svelte.ts)
│   ├── routes/                 # File-based routing
│   │   ├── +layout.svelte      # Root layout
│   │   ├── +page.svelte        # Page component
│   │   └── +page.server.ts     # Server-side logic
│   ├── app.html                # HTML template
│   └── app.d.ts                # TypeScript declarations
├── static/                     # Static assets
│   └── manifest.json           # PWA manifest
├── svelte.config.js            # Svelte configuration
├── vite.config.ts              # Vite + PWA config
└── tailwind.config.js          # Tailwind CSS config
```

### Security

1. Use `.env` files for secrets (already in `.gitignore`)
2. Never commit the `.venv/` directory
3. Log files go to `logs/` (gitignored)
4. Hash all passwords with bcrypt
5. Use HTTPS in production

### When in Doubt

1. Check [docs/DEVELOPMENT_PLAN.md](docs/DEVELOPMENT_PLAN.md)
2. Look at existing task files for examples
3. Ask the Product Owner (update daily log with questions)
4. Prefer simplicity — MVP first, polish later

---

## Document Maintenance

- **Last updated**: 2025-04-08
- **Owner**: AI Agents / Product Owner
