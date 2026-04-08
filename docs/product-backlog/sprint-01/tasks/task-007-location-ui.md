# TASK-007: Location UI

**Story**: US-002  
**Status**: 🔴 Todo  
**Assignee**: —

---

## Goal

Create UI for location input and zone validation.

---

## Acceptance Criteria

- [ ] Postal code input with format validation
- [ ] Real-time format feedback
- [ ] Zone validation check (async)
- [ ] Travel distance selector
- [ ] Store preferences multi-select
- [ ] Out-of-zone messaging

---

## Technical Approach

**Components**:

```
lib/components/location/
├── LocationStep.svelte
├── PostalCodeInput.svelte
├── DistanceSelector.svelte
└── StoreSelector.svelte
```

**Validation Flow**:

1. Format validation (client-side regex)
2. Debounced zone API call
3. Show loading/checkmark/error states

**UX**:

- Auto-format postal code (uppercase, insert space)
- Show "Zone desservie" or "Zone non desservie"
- Out-of-zone: show waitlist signup option

---

## Dependencies

- TASK-006: Geocoding service
- TASK-004: Profile form (for integration)

---

## Progress

| Date | Status      | Notes |
| ---- | ----------- | ----- |
| —    | Not started | —     |
