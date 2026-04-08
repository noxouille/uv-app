# Backlog Guide

## Content Hierarchy

This document explains how content is organized across the backlog for clarity.

---

## 📊 Separation of Concerns

| Level       | Location                    | Content                         | Audience  | Size         |
| ----------- | --------------------------- | ------------------------------- | --------- | ------------ |
| **Process** | `DEVELOPMENT_PLAN.md`       | How we work, methodology        | Everyone  | ~200 lines   |
| **Sprint**  | `sprint-XX/sprint-goals.md` | What we're building this sprint | PO + Team | ~80 lines    |
| **Story**   | `sprint-XX/user-stories.md` | WHAT: Requirements & acceptance | PO + Devs | ~150 lines   |
| **Task**    | `sprint-XX/tasks/*.md`      | HOW: Implementation details     | Devs (AI) | ~50-70 lines |

---

## 📝 Content Guidelines

### User Stories (WHAT)

**Include**:

- User persona, goal, benefit
- Acceptance criteria (testable)
- Business rules
- Links to tasks

**Exclude**:

- Implementation details
- Technical stack decisions
- File structure
- Code examples

**Example**:

```markdown
## US-001: Create Profile

**As a** user  
**I want to** create a profile  
**So that** recommendations match my needs

### Acceptance Criteria

- [ ] User can specify household size
- [ ] System validates required fields

### Business Rules

- At least 1 adult required
```

### Tasks (HOW)

**Include**:

- Technical approach
- File structure
- Key implementation notes
- Dependencies
- Testing checklist

**Exclude**:

- User-facing requirements (those are in stories)
- Business justification

**Example**:

```markdown
## TASK-001: Database Setup

**Story**: US-001

### Goal

Set up database infrastructure.

### Acceptance Criteria

- [ ] Connection configured
- [ ] Migrations initialized

### Technical Approach

- SQLAlchemy 2.0 + Alembic
- SQLite for MVP

### Files
```

config/database.py
database/base.py

```

---

## 🎯 For Product Owners

Read in this order:
1. `DEVELOPMENT_PLAN.md` — Understand the process
2. `sprint-XX/sprint-goals.md` — See current sprint objectives
3. `sprint-XX/user-stories.md` — Review requirements
4. `decisions/po-decisions.md` — Track decisions

Skip the `tasks/` folder — that's implementation detail for developers.

---

## 🤖 For AI Agents

Read in this order:
1. `sprint-XX/sprint-goals.md` — Context
2. `sprint-XX/user-stories.md` — Requirements
3. `sprint-XX/tasks/TASK-XXX.md` — Your specific task
4. `technical-specs/` — Architecture patterns

Update as you work:
- Task file: Progress status
- `daily-logs/`: What you did today

---

## 📁 File Organization

```

product-backlog/
├── README.md # Backlog overview (high-level)
│
├── sprint-01/ # Current sprint
│ ├── sprint-goals.md # Sprint objectives (~80 lines)
│ ├── user-stories.md # Requirements (~150 lines)
│ │
│ ├── tasks/ # Implementation details
│ │ ├── task-001-_.md # ~50-70 lines each
│ │ ├── task-002-_.md
│ │ └── ...
│ │
│ └── daily-logs/ # Progress updates
│ └── YYYY-MM-DD.md
│
└── sprint-02/ # Next sprint
└── ...

```

---

## ✅ Quality Checklist

### User Story Quality

- [ ] Clear "As a / I want / So that"
- [ ] Acceptance criteria are testable
- [ ] No implementation details
- [ ] Business rules documented
- [ ] Links to related tasks

### Task Quality

- [ ] Clear goal statement
- [ ] Acceptance criteria are technical
- [ ] File structure documented
- [ ] Dependencies listed
- [ ] Progress log updated

---

## 🔄 Workflow

```
PO creates/reviews stories
↓
PO approves story requirements
↓
AI agent picks task from story
↓
AI implements (updates task)
↓
PO reviews (acceptance criteria)
↓
Story marked done

```

---

*Keep stories focused on WHAT users need.*
*Keep tasks focused on HOW we build it.*

```
AI implements (updates task)
         ↓
PO reviews (acceptance criteria)
         ↓
Story marked done
```

---

*Keep stories focused on WHAT users need.*  
*Keep tasks focused on HOW we build it.*
