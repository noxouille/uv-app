# Product Owner Decision Log

This document records important product decisions made during development.

---

## Decision Template

| Field                  | Description                  |
| ---------------------- | ---------------------------- |
| **Date**               | When the decision was made   |
| **Decision**           | What was decided             |
| **Context**            | Why the decision was needed  |
| **Options Considered** | Alternatives evaluated       |
| **Impact**             | How this affects the project |
| **Reversible?**        | Can this be changed later?   |

---

## Decisions

### 2025-04-08: Use SQLite for MVP Database

| Field                  | Value                                                                       |
| ---------------------- | --------------------------------------------------------------------------- |
| **Date**               | 2025-04-08                                                                  |
| **Decision**           | Use SQLite for the MVP database, migrate to PostgreSQL in Phase 2           |
| **Context**            | Need a database solution that requires minimal setup for MVP development    |
| **Options Considered** | SQLite (zero config), PostgreSQL (production-ready), MySQL                  |
| **Impact**             | Simplifies development and deployment for MVP; will require migration later |
| **Reversible?**        | Yes — migration path documented                                             |

---

### 2025-04-08: Focus on Quebec for Initial Launch

| Field                  | Value                                                                                            |
| ---------------------- | ------------------------------------------------------------------------------------------------ |
| **Date**               | 2025-04-08                                                                                       |
| **Decision**           | Initial serviceable zone limited to Quebec major cities (Montreal, Quebec City, Laval, Gatineau) |
| **Context**            | From Cahier des charges and Feasibility Analysis — need to ensure data quality for promotions    |
| **Options Considered** | National launch (high risk), Ontario only, Quebec only                                           |
| **Impact**             | Narrower market initially but better user experience; French language support prioritized        |
| **Reversible?**        | Yes — will expand to other provinces in Phase 2                                                  |

---

### 2025-04-08: Defer Authentication to Sprint 2 (Stretch)

| Field                  | Value                                                                   |
| ---------------------- | ----------------------------------------------------------------------- |
| **Date**               | 2025-04-08                                                              |
| **Decision**           | Make user authentication optional for MVP; profiles can be device-local |
| **Context**            | Speed up MVP delivery; auth adds complexity                             |
| **Options Considered** | Auth required from start, auth optional, no auth at all                 |
| **Impact**             | Faster Sprint 1; need migration path for anonymous profiles later       |
| **Reversible?**        | Yes — can add auth without breaking existing profiles                   |

---

## Pending Decisions

| Topic                  | Options                         | Status                      | Target Date |
| ---------------------- | ------------------------------- | --------------------------- | ----------- |
| ~~Frontend framework~~ | ~~React vs Vue~~                | ✅ **Decided: SvelteKit 5** | 2025-04-08  |
| CSS framework          | Tailwind vs Bootstrap vs custom | Pending PO input            | 2025-04-09  |
| Hosting provider       | Railway vs Render vs Heroku     | Pending PO input            | 2025-04-15  |

---

## How to Add a Decision

1. Copy the decision template
2. Fill in all fields
3. Add to the Decisions section above
4. If reversing a previous decision, note it in the Reversible field
