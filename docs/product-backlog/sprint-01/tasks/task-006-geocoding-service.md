# TASK-006: Geocoding Service

**Story**: US-002  
**Status**: 🔴 Todo  
**Assignee**: —

---

## Goal

Implement postal code to coordinates conversion.

---

## Acceptance Criteria

- [ ] Geocoding service created
- [ ] Canadian postal code support
- [ ] Caching to avoid repeated calls
- [ ] Zone validation (is location serviceable?)
- [ ] Error handling for invalid codes
- [ ] API endpoint: `GET /zones/validate`

---

## Technical Approach

**Service**: `services/geocoding.py`

**Provider**: Nominatim (OpenStreetMap) — free, no API key needed

- Rate limit: 1 request/sec
- Attribution required

**Zone Validation**:

- Serviceable regions: Montreal, Quebec City, Laval, Gatineau
- Check if coordinates fall within region radius

**Caching**: In-memory dict (MVP)

**API Response**:

```json
{
  "postal_code": "H2X 1Y4",
  "serviceable": true,
  "region": "Montreal",
  "message": "Service available in Montreal"
}
```

---

## Dependencies

- TASK-005: Location model

---

## Progress

| Date | Status      | Notes |
| ---- | ----------- | ----- |
| —    | Not started | —     |
