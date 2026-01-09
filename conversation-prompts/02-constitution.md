# Phase 2: Constitution Prompt

> **Agent:** `speckit.constitution` <br> **Output:** `.specify/memory/constitution.md`

---

## What is a Constitution?

The constitution defines **non-negotiable principles** that guide all development. Think of it as your project's "rules of engagement" — standards that every feature must follow.

A good constitution covers:
- **Code Quality** — Type strict mode, component patterns, file limits
- **Testing Discipline** — What needs tests, test-first requirements
- **UX Consistency** — Design system, loading states, error handling
- **Performance** — Bundle size limits, response time targets
- **Data & Privacy** — Storage approach, security requirements

---

## Greenfield Project Prompt

For new projects, create a constitution from your brainstorm:

```
Read docs/brainstorm.md and create a constitution for this project.

Focus on these areas (skip unnecessary ones depending on type of project):

## Code Quality Standards
- Type configuration (strict mode, specific flags)
- Component patterns (isolation, max file length, custom hooks)
- Code organization principles

## Testing Discipline
- What absolutely needs tests (data layer, algorithms, forms)
- Testing patterns (colocated tests, test-first for what)
- What can skip tests (simple UI, prototypes)

## User Experience Consistency
- Styling approach (Tailwind only, design tokens)
- Required states (loading, error, empty)
- Accessibility requirements (keyboard nav, ARIA)
- Responsive requirements (breakpoints, mobile-first)

## Performance Requirements
- Bundle size limits (e.g., <500KB gzipped)
- Load time targets (e.g., <2s initial load)
- Interaction response (e.g., <100ms for filtering)

## Data & Privacy
- Storage approach (local-first, cloud sync)
- User data ownership
- What data is never sent to servers

## Technology Constraints
- Required stack (from brainstorm)
- Deviation policy (how to justify new dependencies)

## Quality Gates
- What must pass before merge (lint, types, tests, build)

Base this on:
- Technical decisions from the brainstorm
- Best practices for the chosen stack
- The scale/scope of the project (personal tool vs public app)

Make requirements specific and measurable. Avoid vague terms like 
"should be fast" — use "must respond in <100ms" instead.
```

---

## Brownfield Project Prompt

For existing projects, derive the constitution from current patterns:

```
Analyze the existing codebase and create a constitution that captures established patterns.

E.g for a TypeScript project, examine:
- tsconfig.json for TypeScript settings
- ESLint/Prettier config for code standards
- Existing test files for testing patterns
- package.json for tech stack
- Component files for UI patterns
- README for documented standards

Create a constitution that:
1. Documents what's already being followed
2. Doesn't impose new arbitrary rules
3. Captures implicit conventions as explicit principles
4. Notes any inconsistencies that need resolution

For each principle, cite where it's currently implemented 
(e.g., "see src/components/Button.tsx for pattern").
```

---

## Constitution Sections Reference

### I. Code Quality Standards

Examples vary by language:

**TypeScript/JavaScript:**
```markdown
- **TypeScript Strict Mode**: All code MUST compile with `strict: true`
- **No any**: Explicit types required; `any` only with documented justification
- **Component Isolation**: Single-purpose components; split "X and Y" into separate components
- **Custom Hooks**: Business logic in hooks; components render only
- **Max File Length**: 200 lines soft limit; 300 lines requires refactor
- **No Dead Code**: Unused exports and commented code prohibited
```

**Python:**
```markdown
- **Type Hints**: All functions MUST have type annotations
- **Strict Linting**: Code MUST pass `mypy --strict` and `ruff` checks
- **Single Responsibility**: One class/function per purpose
- **Max Function Length**: 50 lines soft limit
- **Docstrings**: All public functions require docstrings
```

**Go:**
```markdown
- **go vet/staticcheck**: All code MUST pass static analysis
- **Error Handling**: All errors MUST be handled explicitly
- **Interface Segregation**: Small, focused interfaces
- **Package Organization**: Clear separation of concerns
```

### II. Testing Discipline

```markdown
- **Test-First for Data**: Database operations, algorithms, state machines
- **Unit Tests**: Every module with business logic needs tests
- **Edge Cases**: Empty states, validation errors, boundary conditions
- **Test Collocation**: Tests near source files (e.g., `*.test.ts`, `*_test.py`, `*_test.go`)
- **Real Dependencies**: Use test databases/fixtures, minimize mocks
```

### III. UX Consistency

```markdown
- **Design System**: Tailwind CSS only; no custom CSS except theming
- **Loading States**: Every async operation shows loading feedback
- **Error States**: Failures show actionable messages, never silent
- **Keyboard Navigation**: All interactive elements keyboard-accessible
- **Responsive**: 320px to 1920px; no horizontal scroll
- **Destructive Actions**: Require confirmation or provide undo
```

### IV. Performance

```markdown
- **Bundle Size**: <500KB gzipped production build
- **Initial Load**: <2s on 4G connection
- **Interactions**: <100ms for filtering, searching, navigation
- **Images**: Lazy load below fold; WebP format
```

### V. Data & Privacy

```markdown
- **Local-First**: Data stored in IndexedDB by default
- **User Ownership**: Export all data in standard format
- **No Tracking**: No analytics without explicit consent
- **Secure Defaults**: HTTPS only; sanitize all inputs
```

### VI. Technology Stack

Example for a TypeScript project:
```markdown
| Layer | Required | Version |
|-------|----------|----------|
| Framework | React | ^19.0.0 |
| Language | TypeScript | ^5.0.0 (strict) |
| Build | Vite | ^5.0.0 |
| Styling | Tailwind CSS | ^3.0.0 |
| Testing | Vitest + RTL | Latest |
```

Example for a Python project:
```markdown
| Layer | Required | Version |
|-------|----------|----------|
| Framework | FastAPI | ^0.100.0 |
| Language | Python | ^3.11 |
| ORM | SQLAlchemy | ^2.0.0 |
| Testing | pytest | Latest |
| Linting | ruff + mypy | Latest |
```

### VII. Quality Gates

Define what must pass before code is merged. Examples:

**JavaScript/TypeScript:**
```markdown
All PRs MUST pass:
1. `npm run lint` — Zero errors
2. `npm run typecheck` — Zero errors  
3. `npm test` — All tests pass
4. `npm run build` — Successful build
```

**Python:**
```markdown
All PRs MUST pass:
1. `ruff check .` — Zero errors
2. `mypy .` — Zero type errors
3. `pytest` — All tests pass
4. `coverage report` — Minimum 80% coverage
```

**Go:**
```markdown
All PRs MUST pass:
1. `go vet ./...` — Zero errors
2. `golangci-lint run` — Zero errors
3. `go test ./...` — All tests pass
4. `go build` — Successful build
```

---

## Tips

1. **Be specific** — "Fast" is meaningless; "<100ms" is testable
2. **Start strict** — You can relax rules; adding them later is hard
3. **Match scope** — Weekend project ≠ enterprise standards
4. **Reference examples** — Point to files that show the pattern
5. **Version it** — Add version number for future amendments
