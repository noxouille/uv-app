# Data Models Specification

This document defines the core data models for the application.

---

## Entity Relationship Diagram

```
┌─────────────────┐       ┌──────────────────┐
│      User       │1─────1│   UserProfile    │
├─────────────────┤       ├──────────────────┤
│ id (PK)         │       │ id (PK)          │
│ email           │       │ user_id (FK)     │
│ hashed_password │       │ adults_count     │
│ is_active       │       │ children_count   │
│ created_at      │       │ children_ages    │
└─────────────────┘       │ diet_type        │
                          │ allergies        │
                          │ weekly_budget    │
                          │ cooking_time     │
                          │ cooking_mode     │
                          │ postal_code      │
                          │ latitude         │
                          │ longitude        │
                          │ max_travel_dist  │
                          │ preferred_stores │
                          │ created_at       │
                          │ updated_at       │
                          └──────────────────┘
```

---

## User Model

```python
class User(Base):
    __tablename__ = "users"

    id: Mapped[int] = mapped_column(primary_key=True)
    email: Mapped[str] = mapped_column(String(255), unique=True, index=True)
    hashed_password: Mapped[str] = mapped_column(String(255))
    is_active: Mapped[bool] = mapped_column(default=True)
    created_at: Mapped[datetime] = mapped_column(server_default=func.now())

    # Relationships
    profile: Mapped["UserProfile"] = relationship(back_populates="user", uselist=False)
```

---

## UserProfile Model

```python
class UserProfile(Base):
    __tablename__ = "user_profiles"

    # Primary Key
    id: Mapped[int] = mapped_column(primary_key=True)

    # Foreign Key (optional for MVP - anonymous users)
    user_id: Mapped[Optional[int]] = mapped_column(ForeignKey("users.id"), nullable=True)

    # Household
    adults_count: Mapped[int] = mapped_column(default=1)
    children_count: Mapped[int] = mapped_column(default=0)
    children_ages: Mapped[Optional[list[int]]] = mapped_column(JSON, nullable=True)

    # Dietary
    diet_type: Mapped[DietType] = mapped_column(default=DietType.OMNIVORE)
    cuisine_preferences: Mapped[Optional[list[str]]] = mapped_column(JSON, nullable=True)

    # Restrictions
    allergies: Mapped[list[str]] = mapped_column(JSON, default=list)
    intolerances: Mapped[list[str]] = mapped_column(JSON, default=list)
    avoid_foods: Mapped[list[str]] = mapped_column(JSON, default=list)

    # Budget
    weekly_budget: Mapped[Optional[float]] = mapped_column(nullable=True)
    budget_strictness: Mapped[str] = mapped_column(default="flexible")

    # Time
    cooking_time: Mapped[CookingTime] = mapped_column(default=CookingTime.MEDIUM)
    cooking_days: Mapped[list[str]] = mapped_column(JSON, default=list)

    # Mode
    cooking_mode: Mapped[CookingMode] = mapped_column(default=CookingMode.DAILY)

    # Location
    postal_code: Mapped[Optional[str]] = mapped_column(String(10), nullable=True)
    latitude: Mapped[Optional[float]] = mapped_column(nullable=True)
    longitude: Mapped[Optional[float]] = mapped_column(nullable=True)
    max_travel_distance_km: Mapped[int] = mapped_column(default=10)
    preferred_stores: Mapped[list[str]] = mapped_column(JSON, default=list)

    # Metadata
    created_at: Mapped[datetime] = mapped_column(server_default=func.now())
    updated_at: Mapped[Optional[datetime]] = mapped_column(onupdate=func.now())

    # Relationships
    user: Mapped[Optional["User"]] = relationship(back_populates="profile")
```

---

## Enums

```python
from enum import Enum

class DietType(str, Enum):
    OMNIVORE = "omnivore"
    VEGETARIAN = "vegetarian"
    VEGAN = "vegan"
    PESCATARIAN = "pescatarian"
    FLEXITARIAN = "flexitarian"

class CookingTime(str, Enum):
    QUICK = "quick"        # < 30 minutes
    MEDIUM = "medium"      # 30-60 minutes
    ELABORATE = "elaborate"  # > 60 minutes

class CookingMode(str, Enum):
    DAILY = "daily"
    BATCH = "batch"

class StoreChain(str, Enum):
    LOBLAWS = "loblaws"
    SOBEYS = "sobeys"
    METRO = "metro"
    IGA = "iga"
    MAXI = "maxi"
    SUPER_C = "super_c"
    PROVIGO = "provigo"
    COOP = "coop"
    COSTCO = "costco"
    WALMART = "walmart"
```

---

## JSON Schema Examples

### User Profile (API Response)

```json
{
  "id": 1,
  "adults_count": 2,
  "children_count": 1,
  "children_ages": [8],
  "diet_type": "vegetarian",
  "cuisine_preferences": ["italian", "asian"],
  "allergies": ["nuts", "gluten"],
  "intolerances": ["lactose"],
  "avoid_foods": ["mushrooms"],
  "weekly_budget": 150.0,
  "budget_strictness": "flexible",
  "cooking_time": "medium",
  "cooking_days": ["mon", "tue", "wed", "thu", "fri"],
  "cooking_mode": "daily",
  "postal_code": "H2X 1Y4",
  "latitude": 45.5019,
  "longitude": -73.5674,
  "max_travel_distance_km": 10,
  "preferred_stores": ["loblaws", "metro"],
  "created_at": "2025-04-08T12:00:00Z",
  "updated_at": null
}
```

---

## Database Indexes

```sql
-- For user lookups
CREATE INDEX ix_users_email ON users(email);

-- For location-based queries (Phase 2)
CREATE INDEX ix_user_profiles_location ON user_profiles(latitude, longitude)
WHERE latitude IS NOT NULL AND longitude IS NOT NULL;

-- For postal code lookups
CREATE INDEX ix_user_profiles_postal_code ON user_profiles(postal_code);
```
