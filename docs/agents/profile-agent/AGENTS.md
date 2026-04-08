# Profile Agent

## Identity

You are the **Profile Agent** — responsible for the complete user profile experience.

## Domain

- User profiles (household, dietary preferences, budget, time constraints)
- Authentication flows (registration, login)
- Geographic zones (postal codes, geocoding, travel distance)
- Profile creation UI (step-by-step wizard)

## Tech Stack

### Backend

- **Framework**: FastAPI
- **ORM**: SQLAlchemy 2.0 (with `Mapped[]` syntax)
- **Schemas**: Pydantic v2
- **Auth**: JWT tokens, password hashing (handled by Core Agent infrastructure)

### Frontend

- **Framework**: SvelteKit 5
- **Styling**: Tailwind CSS
- **Forms**: Superforms + Zod validation
- **State**: Svelte 5 Runes (`$state`, `$derived`)

## Current Sprint Focus

**Sprint 1** (April 8-22, 2025): User Profile Foundation

### Your Tasks

| Task     | Story  | Description        | Status  |
| -------- | ------ | ------------------ | ------- |
| TASK-002 | US-001 | User Profile Model | 🔴 Todo |
| TASK-003 | US-001 | Profile API        | 🔴 Todo |
| TASK-004 | US-001 | Profile Form UI    | 🔴 Todo |
| TASK-005 | US-002 | Location Model     | 🔴 Todo |
| TASK-006 | US-002 | Geocoding Service  | 🔴 Todo |
| TASK-007 | US-002 | Location UI        | 🔴 Todo |

### Dependencies on Core Agent

- TASK-001 (Database Setup) — wait for `database/base.py` and `config/database.py`
- TASK-008 (Auth System) — wait for auth utilities, use placeholder if needed

## File Structure You'll Create

```
backend/
├── models/
│   ├── user.py           # User model (linked to auth)
│   ├── profile.py        # UserProfile model
│   └── location.py       # Location/geocoding models
├── schemas/
│   ├── profile.py        # Pydantic schemas
│   └── location.py
├── api/
│   ├── profiles.py       # /api/v1/profiles endpoints
│   └── zones.py          # /api/v1/zones endpoints
└── services/
    └── geocoding.py      # Geocoding service

frontend/
└── src/lib/components/profile/
    ├── ProfileWizard.svelte
    ├── ProgressIndicator.svelte
    └── steps/
        ├── HouseholdStep.svelte
        ├── DietaryStep.svelte
        ├── BudgetTimeStep.svelte
        ├── CookingModeStep.svelte
        └── ReviewStep.svelte
```

## Key Implementation Patterns

### SQLAlchemy 2.0 Model

```python
from sqlalchemy.orm import Mapped, mapped_column
from database.base import Base

class UserProfile(Base):
    __tablename__ = "user_profiles"

    id: Mapped[int] = mapped_column(primary_key=True)
    adults_count: Mapped[int] = mapped_column(default=1)
    # ... use Mapped[] syntax
```

### FastAPI Endpoint

```python
from fastapi import APIRouter, Depends
from sqlalchemy.ext.asyncio import AsyncSession
from config.database import get_db

router = APIRouter(prefix="/api/v1/profiles")

@router.post("/")
async def create_profile(
    data: ProfileCreate,
    db: AsyncSession = Depends(get_db)
):
    ...
```

### SvelteKit Superform

```svelte
<script>
  import { superForm } from "sveltekit-superforms";

  let { data } = $props();
  const { form, enhance, errors } = superForm(data.form);
</script>
```

## User Stories Reference

### US-001: Create User Profile

- Household composition (adults, children, ages)
- Dietary preferences (diet type, cuisines)
- Restrictions (allergies, avoid foods)
- Budget constraints (weekly budget)
- Time constraints (cooking time, days available)
- Cooking mode (daily vs batch)

### US-002: Set Geographic Zone

- Canadian postal code input (format: A1A 1A1)
- Geocoding to coordinates
- Max travel distance (1, 5, 10, 15, 25 km)
- Service zone validation (Montreal, Quebec City, Laval, Gatineau)

## Coordination with Core Agent

| Situation                | Action                                               |
| ------------------------ | ---------------------------------------------------- |
| Need database connection | Use `config.database.get_db()` (Core Agent provides) |
| Need base model          | Import from `database.base` (Core Agent provides)    |
| Need auth utilities      | Wait for Core Agent or use placeholder               |
| Modifying shared config  | Notify Core Agent, update both AGENTS.md             |
| Need database connection | Use `config.database.get_db()` (Core Agent provides) |
| Need base model          | Import from `database.base` (Core Agent provides)    |
| Need auth utilities      | Wait for Core Agent or use placeholder               |
| Modifying shared config  | Notify Core Agent, update both AGENTS.md             |

## Definition of Done

- [ ] Code implemented
- [ ] Type hints throughout
- [ ] Error handling with proper HTTP status codes
- [ ] Mobile-responsive UI
- [ ] Task file updated to "Review"
- [ ] Daily log written
