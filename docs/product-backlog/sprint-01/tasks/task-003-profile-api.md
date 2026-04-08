# TASK-003: Profile API Endpoints

**Story**: US-001  
**Status**: 🔴 Todo  
**Assignee**: —

---

## Goal

Implement REST API for profile management.

---

## Acceptance Criteria

- [ ] `POST /api/v1/profiles` — Create profile
- [ ] `GET /api/v1/profiles/me` — Get profile
- [ ] `PUT /api/v1/profiles/me` — Update profile
- [ ] Input validation with clear errors
- [ ] Proper HTTP status codes
- [ ] Unit tests

---

## Technical Approach

**Router**: `api/v1/endpoints/profiles.py`

**Endpoints**:

```python
POST   /profiles          → Create (201)
GET    /profiles/me       → Read (200)
PUT    /profiles/me       → Update (200)
```

**Implementation Notes**:

- Use FastAPI dependency injection for DB session
- Validate with Pydantic schemas
- Return French error messages (primary market)
- Log key operations with `loguru`

**Error Handling**:

- 400: Validation errors
- 404: Profile not found
- 422: Unprocessable entity

---

## Dependencies

- TASK-002: User model

---

## Progress

| Date | Status      | Notes |
| ---- | ----------- | ----- |
| —    | Not started | —     |
