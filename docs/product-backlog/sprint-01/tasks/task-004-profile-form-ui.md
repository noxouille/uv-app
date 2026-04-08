# TASK-004: Profile Form UI

**Story**: US-001  
**Status**: 🔴 Todo  
**Assignee**: —

---

## Goal

Create step-by-step profile creation form (SvelteKit PWA).

---

## Acceptance Criteria

- [ ] Welcome screen with clear value proposition
- [ ] Step 1: Household composition
- [ ] Step 2: Dietary preferences & restrictions
- [ ] Step 3: Budget & time constraints
- [ ] Step 4: Cooking mode selection
- [ ] Step 5: Review & confirm
- [ ] Progress indicator
- [ ] Form validation with inline errors
- [ ] Data persists between steps
- [ ] Mobile-responsive design

---

## Technical Approach

**Stack**: SvelteKit 5 + Tailwind CSS + Superforms + Zod

**Components**:

```
lib/components/profile/
├── ProfileWizard.svelte
├── ProgressIndicator.svelte
└── steps/
    ├── HouseholdStep.svelte
    ├── DietaryStep.svelte
    ├── BudgetTimeStep.svelte
    ├── CookingModeStep.svelte
    └── ReviewStep.svelte
```

**State Management**:

- Use Svelte 5 Runes (`$state`) for form data
- Store data between steps
- Submit via Superforms for validation

**PWA Requirements**:

- Responsive (mobile-first)
- Touch-friendly inputs
- Works offline (progressive enhancement)

---

## Dependencies

- TASK-003: Profile API

---

## Progress

| Date | Status      | Notes |
| ---- | ----------- | ----- |
| —    | Not started | —     |
