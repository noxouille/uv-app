# TASK-008: Auth System (Stretch)

**Story**: US-011  
**Status**: 🔴 Todo  
**Assignee**: —

---

## Goal

Implement user registration and login.

---

## Acceptance Criteria

- [ ] Registration endpoint
- [ ] Login endpoint
- [ ] Password hashing (bcrypt)
- [ ] JWT token generation
- [ ] Protected route middleware

---

## Technical Approach

**Models**: Separate `User` (auth) from `UserProfile` (preferences)

**Libraries**:

- `passlib[bcrypt]` — Password hashing
- `python-jose` — JWT tokens

**Endpoints**:

```
POST /auth/register
POST /auth/login
POST /auth/refresh
```

**Security**:

- Min password: 8 characters
- HTTPS required in production
- Rate limiting on auth endpoints

---

## Notes

- Stretch goal — defer if behind schedule
- MVP can use anonymous profiles

---

## Progress

| Date | Status      | Notes                            |
| ---- | ----------- | -------------------------------- |
| —    | Not started | Defer until other tasks complete |
