# TASK-002: User Profile Model

**Story**: US-001  
**Status**: 🔴 Todo  
**Assignee**: —

---

## Goal

Create database model and validation schemas for user profile.

---

## Acceptance Criteria

- [ ] `UserProfile` SQLAlchemy model with all fields
- [ ] Pydantic schemas: `Create`, `Update`, `Response`
- [ ] Enum types defined
- [ ] Database migration created
- [ ] Unit tests for validation

---

## Technical Approach

**Fields to Implement**:

- Household: `adults_count`, `children_count`, `children_ages`
- Dietary: `diet_type` (enum), `cuisine_preferences`
- Restrictions: `allergies`, `intolerances`, `avoid_foods`
- Budget: `weekly_budget`, `budget_strictness`
- Time: `cooking_time` (enum), `cooking_days`
- Mode: `cooking_mode` (enum)

**Files**:

```
models/
├── __init__.py
├── enums.py              # DietType, CookingTime, CookingMode
└── user_profile.py       # SQLAlchemy model

schemas/
├── __init__.py
└── user_profile.py       # Pydantic schemas
```

**Enums**:

- `DietType`: omnivore, vegetarian, vegan, pescatarian, flexitarian
- `CookingTime`: quick, medium, elaborate
- `CookingMode`: daily, batch

---

## Dependencies

- TASK-001: Database setup

---

## Progress

| Date | Status      | Notes |
| ---- | ----------- | ----- |
| —    | Not started | —     |
