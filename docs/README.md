# Documentation

Welcome to the Meal Planning & Grocery Optimization App documentation.

## Quick Navigation

### For Product Owners

| Document                                                                               | Purpose                                      |
| -------------------------------------------------------------------------------------- | -------------------------------------------- |
| [DEVELOPMENT_PLAN.md](DEVELOPMENT_PLAN.md)                                             | Overall development methodology and workflow |
| [product-backlog/sprint-01/sprint-goals.md](product-backlog/sprint-01/sprint-goals.md) | Current sprint status                        |
| [product-backlog/README.md](product-backlog/README.md)                                 | Full product backlog                         |
| [decisions/po-decisions.md](decisions/po-decisions.md)                                 | Decision log and pending items               |

### For AI Agents

| Document                                                             | Purpose                           |
| -------------------------------------------------------------------- | --------------------------------- |
| [DEVELOPMENT_PLAN.md](DEVELOPMENT_PLAN.md)                           | How to work within this structure |
| [product-backlog/sprint-01/tasks/](product-backlog/sprint-01/tasks/) | Individual task specifications    |
| [technical-specs/](technical-specs/)                                 | Data models, API specs            |
| [templates/task-template.md](templates/task-template.md)             | Template for new tasks            |

### Source Documents

| Document                                                                                         | Description                                |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------ |
| [internal/Cahier des charges interne.pdf](internal/Cahier%20des%20charges%20interne.pdf)         | Complete functional specification (French) |
| [internal/Feasibility_Analysis_CAD_Revised.docx](internal/Feasibility_Analysis_CAD_Revised.docx) | Technical and economic feasibility study   |
| [internal/Presention-produit-subvention.pdf](internal/Presention-produit-subvention.pdf)         | Product presentation for grants            |

## Documentation Structure

```
docs/
├── README.md                          # This file
├── DEVELOPMENT_PLAN.md               # Main development guide
│
├── product-backlog/                  # All user stories and sprints
│   ├── README.md                    # Backlog overview
│   ├── sprint-01/                   # Current sprint
│   │   ├── sprint-goals.md         # Sprint objectives
│   │   ├── user-stories.md         # Detailed stories
│   │   ├── tasks/                  # Task specifications
│   │   │   ├── task-001-database-setup.md
│   │   │   ├── task-002-user-model.md
│   │   │   └── ...
│   │   └── daily-logs/             # Progress updates
│   ├── sprint-02/                   # Next sprint (planned)
│   └── archive/                     # Completed sprints
│
├── technical-specs/                  # Technical documentation
│   ├── data-models.md              # Database schemas
│   ├── api-specification.md        # API endpoints
│   └── deployment-guide.md         # Deployment instructions
│
├── ui-ux/                           # Design documentation
│   ├── wireframes/                 # UI mockups
│   └── user-flows.md               # User journey maps
│
├── decisions/                        # Architecture decisions
│   ├── adr-001-tech-stack.md       # Why FastAPI/React
│   └── po-decisions.md             # Product decisions log
│
├── templates/                        # Reusable templates
│   └── task-template.md            # New task template
│
└── internal/                        # Source documents (read-only)
    ├── Cahier des charges interne.pdf
    ├── Feasibility_Analysis_CAD_Revised.docx
    └── Presention-produit-subvention.pdf
```

## Workflow Summary

### Sprint Cycle (2 weeks)

1. **Planning** (Day 1-2) — PO and AI agents review and commit to sprint goals
2. **Development** (Day 3-10) — AI agents pick up tasks and work through them
3. **Review** (Day 11-12) — PO reviews completed work, feedback incorporated
4. **Demo & Retrospective** (Day 13-14) — Sprint review and next sprint planning

### Daily Activity

**AI Agents**:

1. Check `sprint-XX/sprint-goals.md` for context
2. Pick a task from `tasks/` with status "Todo"
3. Update task to "In Progress"
4. Do the work, updating progress log
5. Submit for review when done

**Product Owner**:

1. Check `daily-logs/` for progress updates
2. Review tasks marked "Review"
3. Make decisions and record in `decisions/po-decisions.md`
4. Approve completed tasks

## Getting Started

### For New AI Agents

1. Read [DEVELOPMENT_PLAN.md](DEVELOPMENT_PLAN.md) — especially the "AI Agent Instructions" section
2. Review [product-backlog/sprint-01/sprint-goals.md](product-backlog/sprint-01/sprint-goals.md)
3. Pick your first task from [product-backlog/sprint-01/tasks/](product-backlog/sprint-01/tasks/)
4. Start coding!

### For Product Owner

1. Review [DEVELOPMENT_PLAN.md](DEVELOPMENT_PLAN.md) — especially the "Progress Tracking" section
2. Check current sprint status: [product-backlog/sprint-01/sprint-goals.md](product-backlog/sprint-01/sprint-goals.md)
3. Review any pending decisions in [decisions/po-decisions.md](decisions/po-decisions.md)
4. Check daily logs in [product-backlog/sprint-01/daily-logs/](product-backlog/sprint-01/daily-logs/)

## Key Principles

1. **User Story Driven** — All work traces back to a user story from the Cahier des charges
2. **Documentation First** — Tasks are documented before coding starts
3. **Daily Logs** — AI agents record progress daily for transparency
4. **PO Involvement** — Product Owner reviews at each stage
5. **Minimal but Complete** — MVP focus, no feature creep

---

Last updated: 2025-04-08
