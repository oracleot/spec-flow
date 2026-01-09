# Phase 4: Plan Prompt

> **Agent:** `speckit.plan`
> **Output:** `plan.md`, `research.md`, `data-model.md`, `quickstart.md`, `contracts/`

---

## What is a Technical Plan?

The plan defines **how** to build what the spec describes. It includes:
- Technology stack with rationale
- Architecture decisions
- Data model with relationships
- Project structure
- Research on best practices
- Setup instructions

---

## The Framework Decision

Before running the plan command, consider whether you even need a framework, and which one fits your language ecosystem.

### Use Minimal/Standard Library When:
- Simple scripts or utilities
- CLI tools with straightforward logic
- Learning/tutorial projects
- Performance-critical applications where overhead matters
- Small APIs with few endpoints

### Use a Framework When:
- Complex application structure needed
- ORM/database abstractions helpful
- Authentication, middleware, routing patterns
- Team familiarity with framework
- Ecosystem benefits (plugins, community, tooling)

### Framework Selection Tools

**JavaScript/TypeScript Frontend Projects:**
Use [Stack Match](https://stack-match.as93.net/) to compare React, Vue, Svelte, Angular, etc.

For greenfield projects where you're unsure about framework choice, use [Stack Match](https://stack-match.as93.net/) to make a data-driven decision.

Map your constitution constraints to Stack Match priorities:

| Constitution Constraint | Stack Match Priority | Weight |
|------------------------|---------------------|--------|
| Bundle <500KB gzipped | Bundle Size | 8-10 |
| <100ms interactions | Performance | 8-10 |
| Long-term maintenance | Viability | 7-9 |
| Need for plugins | Ecosystem | 6-8 |

Document the evaluation in `research.md`.

**Backend/Full-Stack Projects (Any Language):**
Use [TechEmpower Web Framework Benchmarks](https://www.techempower.com/benchmarks/) to compare 300+ frameworks across Python, Go, Rust, Java, C#, PHP, Ruby, and more.

**Language-Specific Considerations:**
- **Python**: FastAPI vs Django vs Flask (see TechEmpower)
- **Go**: Gin vs Echo vs Fiber vs Chi (all performant; choose by API style)
- **Rust**: Actix-web vs Axum vs Rocket
- **Java/Kotlin**: Spring Boot vs Quarkus vs Micronaut
- **C#**: ASP.NET Core (compare minimal APIs vs MVC)
- **Ruby**: Rails vs Sinatra
- **PHP**: Laravel vs Symfony

---

## Greenfield Project Prompt

```
Read docs/brainstorm.md, the spec, and the constitution.
Create a technical implementation plan.

Technology preferences:
- [Framework preference, e.g., "React 19 with TypeScript"]
- [Build tool, e.g., "Vite"]
- [Styling, e.g., "Tailwind CSS"]
- [Storage, e.g., "IndexedDB via Dexie.js"]
- [Testing, e.g., "Vitest + React Testing Library"]

Architecture principles:
- Prefer simplicity over abstraction
- Only use vanilla HTML/CSS/JS if the app is simple enough
- Start with recommended approach, justify deviations
- Local-first data storage
- PWA for offline support (if applicable)

For the research phase:
- Document best practices for chosen stack
- Explain key architectural decisions with rationale
- Note alternatives considered and why rejected

For the data model:
- Define all entities from the spec
- Include field types and constraints
- Document relationships and indexes
- Include validation rules

Project structure should:
- Place source code at project root (not nested folder)
- Use standard conventions for chosen stack
- Colocate tests with source files
- Keep clear separation of concerns

Create quickstart.md with step-by-step setup instructions.
```

---

## Brownfield Project Prompt

```
Read the spec and analyze the existing codebase.
Create a technical plan that integrates with current architecture.

Analyze existing:
- package.json for dependencies
- tsconfig.json for TypeScript settings
- Project structure and patterns
- Existing components and hooks
- Data layer implementation

Create a plan that:
1. Uses existing tech stack (don't introduce new frameworks)
2. Follows established patterns in the codebase
3. Reuses existing components where possible
4. Extends existing data models appropriately
5. Maintains consistency with current architecture

For research, document:
- Which existing components to reuse
- Which patterns to follow
- Any necessary additions (justified)

Skip quickstart.md (project already set up).
```

---

## Minimal/Simple App Prompt

For simple apps that might not need a framework:

```
Read the brainstorm and spec. This is a simple app.

Evaluate whether we actually need a framework:
- Can this be built with vanilla HTML/CSS/JS?
- What's the minimum viable tech stack?
- What complexity would justify a framework?

If vanilla is sufficient:
- Plan for single HTML file + CSS + JS modules
- Use native browser APIs (fetch, localStorage/IndexedDB)
- No build step required

If framework is needed, explain:
- Why vanilla is insufficient
- What specific benefits the framework provides
- Minimum additional dependencies

Prefer the simplest solution that meets requirements.
```

---

## Plan Sections Reference

### Technical Context

Adjust based on your project's language and stack:

**TypeScript/React Example:**
```markdown
**Language/Version**: TypeScript ^5.0.0 (strict mode)
**Primary Dependencies**: React ^19.0.0, Vite ^5.0.0, Tailwind ^3.0.0
**Storage**: IndexedDB via Dexie.js ^4.0.0
**Testing**: Vitest + React Testing Library
**Target Platform**: Modern browsers (Chrome, Firefox, Safari, Edge)
**Project Type**: Single-page web application (PWA)
```

**Python/FastAPI Example:**
```markdown
**Language/Version**: Python ^3.11
**Primary Dependencies**: FastAPI ^0.100.0, SQLAlchemy ^2.0.0, Pydantic ^2.0.0
**Storage**: PostgreSQL via asyncpg
**Testing**: pytest + pytest-asyncio
**Target Platform**: Linux containers (Docker)
**Project Type**: REST API backend
```

**Go Example:**
```markdown
**Language/Version**: Go ^1.21
**Primary Dependencies**: Gin ^1.9.0, GORM ^1.25.0
**Storage**: PostgreSQL via pgx
**Testing**: go test + testify
**Target Platform**: Linux (compiled binary)
**Project Type**: Microservice API
```

### Project Structure

Structure varies by language convention:

**TypeScript/React:**
```markdown
src/
├── components/     # UI components
│   └── ui/         # Base components (Button, Card, etc.)
├── hooks/          # Custom React hooks
├── lib/            # Utilities and database
├── types/          # TypeScript interfaces
├── pages/          # Route components
└── App.tsx

Test files colocated: `Component.tsx` → `Component.test.tsx`
```

**Python/FastAPI:**
```markdown
app/
├── api/            # Route handlers
├── models/         # SQLAlchemy models
├── schemas/        # Pydantic schemas
├── services/       # Business logic
├── db/             # Database utilities
└── main.py
tests/              # Test directory
```

**Go:**
```markdown
cmd/
└── server/         # Main entry point
internal/
├── handlers/       # HTTP handlers
├── models/         # Data models
├── repository/     # Database layer
└── services/       # Business logic

Test files colocated: `handler.go` → `handler_test.go`
```

### Research Document

```markdown
## Research: [Feature Name]

### [Technology] Decision

**Decision**: Use [technology] with [pattern]

**Rationale**: [Why this choice is best]

**Alternatives Considered**:
- [Alternative 1]: [Why rejected]
- [Alternative 2]: [Why rejected]

### Implementation Pattern

[Code example with explanation]
```

### Data Model Document

```markdown
## Entity: [Name]

| Field | Type | Required | Default | Constraints |
|-------|------|----------|---------|-------------|
| id | string | Yes | auto-gen | UUID |
| name | string | Yes | - | max 200 chars |
| createdAt | Date | Yes | auto-set | - |

**Indexes**: id (primary), name, createdAt
**Relationships**: [Links to other entities]
**Validation**: [Rules for each field]
```

---

## Quality Checklist

Before moving to Phase 5, verify:

- [ ] Tech stack matches constitution constraints
- [ ] Research documents key decisions with rationale
- [ ] Data model covers all entities from spec
- [ ] Project structure is clear and conventional
- [ ] Constitution check passes (all gates verified)
- [ ] Quickstart has complete setup instructions
- [ ] No unnecessary complexity or over-engineering

---

## Tips

1. **Question the defaults** — Does this app actually need React?
2. **Document decisions** — Future you will thank you
3. **Check the constitution** — Stack must meet constraints
4. **Keep it flat** — Avoid deep nesting in project structure
5. **Start simple** — You can always add complexity later
