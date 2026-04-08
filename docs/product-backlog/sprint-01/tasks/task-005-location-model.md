# TASK-005: Location Model Extension

**Story**: US-002  
**Status**: 🔴 Todo  
**Assignee**: —

---

## Goal

Extend UserProfile with location fields.

---

## Acceptance Criteria

- [ ] Add location fields to UserProfile model
- [ ] Canadian postal code validation
- [ ] Update Pydantic schemas
- [ ] Database migration
- [ ] Unit tests

---

## Technical Approach

**Fields to Add**:

- `postal_code` (string, validated)
- `latitude` (float, nullable)
- `longitude` (float, nullable)
- `max_travel_distance_km` (int, default 10)
- `preferred_stores` (JSON list)

**Validation**:

- Regex: `^[A-Za-z]\d[A-Za-z]\s?\d[A-Za-z]\d$`
- Normalize to uppercase with space: `A1A 1A1`

**Store Options**: Loblaws, Sobeys, Metro, IGA, Maxi, Super C, Provigo, Coop, Costco, Walmart

---

## Dependencies

- TASK-002: User profile model

---

## Progress

| Date | Status      | Notes |
| ---- | ----------- | ----- |
| —    | Not started | —     |
