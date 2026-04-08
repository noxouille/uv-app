# Development Plan

## Meal Planning & Grocery Optimization App

> **Project**: AI-powered PWA for meal planning and grocery optimization  
> **Approach**: Lean team (Product Owner + AI Agents)  
> **Document Date**: April 2025

---

## 1. Project Overview

### Vision

Build a Progressive Web App (PWA) that helps Canadian households:

- Plan weekly meals personalized to their constraints
- Generate optimized shopping lists
- Find local grocery promotions to save money
- Choose between daily cooking and batch cooking modes

### MVP Scope (Phase 1)

| Module              | Core Features                                                                                                             |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **User Profile**    | Household composition, dietary preferences/allergies, budget, cooking time, location & radius, cooking mode (daily/batch) |
| **Menu Generation** | Weekly balanced meal plan, ingredient mutualization, manual meal replacement                                              |
| **Shopping List**   | Auto-generated from menu, editable, categorized                                                                           |
| **Promotions**      | Local promotion analysis, simple store-based recommendations                                                              |

### Phase 2 Features (Post-MVP)

- Multi-store advanced optimization
- Pantry/garde-manger management
- Nutritional recommendations
- Cost/distance/time trade-offs
- Drive/delivery integration

---

## 2. Development Methodology

### Approach: Agile Kanban + Sprints

Given the AI-agent + Product Owner lean team structure, we use:

- **2-week sprints** for focused delivery
- **Kanban board** for visual task flow (Todo → In Progress → Review → Done)
- **User Story-driven** development
- **Continuous PO review** at each stage

### Why This Works for AI + PO Teams

| Challenge                       | Solution                                         |
| ------------------------------- | ------------------------------------------------ |
| Context switching for AI agents | Clear sprint boundaries with frozen requirements |
| PO needs visibility             | Kanban board + structured status files           |
| Code quality/consistency        | Standardized templates + definition of done      |
| Traceability                    | Branch-per-feature + PR descriptions             |

---

## 3. Sprint Structure

### Directory Structure

```
docs/
├── DEVELOPMENT_PLAN.md          # This file — process & methodology
├── product-backlog/
│   ├── README.md               # Backlog overview
│   ├── sprint-01/              # Current sprint
│   │   ├── sprint-goals.md     # High-level objectives
│   │   ├── user-stories.md     # WHAT we're building (requirements)
│   │   ├── tasks/              # HOW to build it (implementation)
│   │   ├── daily-logs/         # Progress updates
│   │   └── retrospective.md
│   ├── sprint-02/              # Next sprint
│   └── archive/
├── technical-specs/            # Architecture decisions
├── decisions/                  # ADRs & PO decisions
└── templates/
```

### Sprint Lifecycle (2 Weeks)

```
Week 1                          Week 2
┌─────────────┐                ┌─────────────┐
│ Day 1-2     │                │ Day 8-10    │
│ Planning    │                │ Development │
│ + Kickoff   │                │ + Tests     │
└─────────────┘                └─────────────┘
      ↓                              ↓
┌─────────────┐                ┌─────────────┐
│ Day 3-7     │                │ Day 11-14   │
│ Development │                │ Review +    │
│ Daily logs  │                │ Demo + Next │
└─────────────┘                │ Sprint Plan │
                               └─────────────┘
```

---

## 4. Product Backlog Organization

### Content Hierarchy

| Level          | Content                                   | Audience         | Detail Level |
| -------------- | ----------------------------------------- | ---------------- | ------------ |
| **Epic**       | Major feature area (e.g., "User Profile") | PO               | High         |
| **User Story** | WHAT: Requirements & acceptance criteria  | PO + Devs        | Medium       |
| **Task**       | HOW: Implementation details               | Devs (AI Agents) | High         |

### User Story Format (WHAT)

```markdown
## US-XXX: [Title]

**As a** [user]  
**I want** [goal]  
**So that** [benefit]

### Acceptance Criteria (testable)

- [ ] User can [specific action]
- [ ] System [expected behavior]

### Notes

- Links to requirements document
- Business rules
- Out of scope items
```

**User stories focus on requirements, NOT implementation.**

### Task Format (HOW)

Tasks live in `sprint-XX/tasks/` and contain:

- Technical approach
- File structure
- Code patterns
- Dependencies
- Testing approach

---

## 5. AI Agent Workflow

### Before Starting

1. Read `sprint-XX/sprint-goals.md` for context
2. Pick a task from `tasks/` with status "Todo"
3. Create branch: `git checkout -b feature/task-XXX`
4. Update task status to "In Progress"

### While Working

1. **Update task file** with progress
2. **Write daily log** in `daily-logs/YYYY-MM-DD.md`

### When Done

1. Update task → Status: Review
2. Create PR referencing user story
3. Move to next task

### Code Standards

- Line length: 88 characters
- Double quotes for strings
- 4-space indentation
- Use `loguru` for logging
- Type hints encouraged

---

## 6. Progress Tracking for Product Owner

### Quick Status Check

| I want to...          | Go to...                                      |
| --------------------- | --------------------------------------------- |
| See sprint progress   | `sprint-XX/sprint-goals.md`                   |
| Check today's work    | `sprint-XX/daily-logs/YYYY-MM-DD.md`          |
| Review completed work | `sprint-XX/tasks/` (look for "Review" status) |
| See overall backlog   | `product-backlog/README.md`                   |

### Sprint Dashboard Template

```markdown
# Sprint X — [Name]

| Story  | Status         | Progress  |
| ------ | -------------- | --------- |
| US-001 | 🟡 In Progress | 2/4 tasks |
| US-002 | 🔴 Not Started | 0/3 tasks |

## Blockers

- None
```

---

## 7. Definition of Done

### Task Done

- [ ] Code implemented
- [ ] Tests passing
- [ ] Task file updated
- [ ] PR created

### User Story Done

- [ ] All acceptance criteria met
- [ ] PO reviewed and accepted
- [ ] Works on mobile

### Sprint Done

- [ ] All "Must" stories complete
- [ ] Demo completed
- [ ] Retrospective done

---

## 8. Quick Reference

### AI Agent Quick Start

1. Read `docs/product-backlog/sprint-01/sprint-goals.md`
2. Pick a task from `tasks/` with status "Todo"
3. Create branch: `git checkout -b feature/task-XXX`
4. Update task status → "In Progress"
5. Do the work
6. Update task status → "Review"
7. Create PR
8. Write daily log

---

> 💡 **Tip for AI Agents**: When in doubt, prioritize simplicity. Follow the existing code style and ask the PO when requirements are unclear.
