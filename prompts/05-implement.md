# Phase 6: Implement Prompt

> **Agent:** `speckit.implement`
> **Output:** Working code in `src/`

---

## The Greenfield Challenge

When building a new project, the implement agent needs to scaffold a framework (React, Vue, etc.). This can create problems:

**❌ Common Issue:**
Agent creates a nested folder structure:
```
my-project/
├── .specify/
├── my-app/          ← Nested Vite scaffold
│   ├── src/
│   ├── package.json
│   └── ...
└── specs/
```

**✅ What You Want:**
```
my-project/
├── .specify/
├── src/             ← Source at root
├── package.json     ← Config at root
└── specs/
```

---

## Solution 1: Pre-Scaffold (Recommended)

Before running `/speckit.implement`, scaffold the project yourself:

**JavaScript/TypeScript:**
```bash
# React + TypeScript + Vite
npm create vite@latest . -- --template react-ts

# Vue + TypeScript + Vite
npm create vite@latest . -- --template vue-ts

# Svelte + TypeScript + Vite
npm create vite@latest . -- --template svelte-ts

# Vanilla TypeScript
npm create vite@latest . -- --template vanilla-ts
```

**Python:**
```bash
# Create virtual environment and basic structure
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install fastapi uvicorn  # or django, flask, etc.
mkdir -p app tests
touch app/__init__.py app/main.py
```

**Go:**
```bash
# Initialize Go module
go mod init myproject
mkdir -p cmd/server internal/handlers
touch cmd/server/main.go
```

**Rust:**
```bash
# Initialize Rust project in current directory
cargo init .
```

The `.` means "scaffold in current directory".

Then run `/speckit.implement` — it will add to the existing structure.

---

## Solution 2: Explicit Prompt

If you prefer the agent to scaffold:

```
Implement all tasks according to the plan.

CRITICAL PROJECT STRUCTURE RULES:
1. This project root is the working directory
2. Install all dependencies at the root (package.json here)
3. Create source files in src/ at the root
4. Do NOT create a nested project folder
5. Do NOT run "npm create vite" with a project name
6. If scaffolding is needed, scaffold directly into the current directory

When installing dependencies:
- Run `npm init -y` if no package.json exists
- Run `npm install [packages]` at the root
- Configure vite.config.ts at the root

The file structure should match the plan.md project structure exactly.
```

---

## Implementation Prompts by Phase

### First Implementation (Full MVP)

```
Implement all tasks from tasks.md.

Follow the plan exactly. Start with:
1. Project setup and dependencies
2. Core data layer
3. Basic components
4. Integration and routing

Test each phase before moving to the next.
Write tests alongside implementation (test-first for data layer).
```

### Specific Phase Implementation

```
Implement Phase 3: [User Story Name]

Follow the tasks exactly. Create:
- [List specific components/files from tasks.md]

Ensure:
- Types are in src/types/
- Components are in src/components/
- Hooks are in src/hooks/
- Tests are colocated with source files
```

### Resume After Interruption

```
Continue implementation from where we stopped.

Last completed: [task ID or description]
Next task: [task ID from tasks.md]

Pick up from there and continue through the remaining tasks.
```

---

## Common Implementation Patterns

These are language-specific setup patterns. Use the one matching your project:

### React + Vite + Tailwind Setup (JavaScript/TypeScript)

```
Set up the project with:
1. npm init -y
2. npm install react react-dom
3. npm install -D vite @vitejs/plugin-react typescript @types/react @types/react-dom
4. npm install -D tailwindcss postcss autoprefixer
5. npx tailwindcss init -p

Create configuration files:
- vite.config.ts
- tsconfig.json (strict mode per constitution)
- tailwind.config.js
- postcss.config.js

Create entry files:
- index.html (at root)
- src/main.tsx
- src/App.tsx
- src/index.css (Tailwind directives)

Add scripts to package.json:
- "dev": "vite"
- "build": "tsc && vite build"
- "preview": "vite preview"
- "test": "vitest"
- "lint": "eslint src --ext ts,tsx"
- "typecheck": "tsc --noEmit"
```

### Adding Testing Setup

```
Add testing dependencies:
- npm install -D vitest @testing-library/react @testing-library/jest-dom
- npm install -D jsdom @types/node

Create vitest.config.ts with:
- jsdom environment
- setup file for testing-library
- include pattern for test files

Create src/tests/setup.ts with:
- import '@testing-library/jest-dom'
- [Any other global test setup]
```

### Adding Dexie for IndexedDB (JavaScript)

```
Add Dexie for local storage:
- npm install dexie dexie-react-hooks

Create src/lib/db.ts with:
- Database class extending Dexie
- Table definitions matching data model
- Version management for migrations

Create src/hooks/use[Entity].ts with:
- useLiveQuery for reactive data
- CRUD operations
- Loading/error state management
```

### Python FastAPI Setup

```
Set up the Python project with:
1. python -m venv venv && source venv/bin/activate
2. pip install fastapi uvicorn sqlalchemy alembic pydantic
3. pip install pytest pytest-asyncio httpx (dev dependencies)

Create project structure:
- app/main.py (FastAPI app entry)
- app/api/ (route handlers)
- app/models/ (SQLAlchemy models)
- app/schemas/ (Pydantic schemas)
- app/db/ (database connection)
- tests/ (pytest tests)

Create configuration files:
- pyproject.toml or requirements.txt
- alembic.ini (database migrations)
- .env.example (environment variables)
```

### Go Project Setup

```
Set up the Go project with:
1. go mod init [module-name]
2. go get github.com/gin-gonic/gin (or echo, fiber, chi)
3. go get gorm.io/gorm gorm.io/driver/postgres

Create project structure:
- cmd/server/main.go (entry point)
- internal/handlers/ (HTTP handlers)
- internal/models/ (data models)
- internal/repository/ (database layer)
- internal/services/ (business logic)

Add Makefile with common commands:
- make run, make test, make build
```

---

## Handling Implementation Issues

### Dependencies Conflict

```
There's a dependency conflict with [package].

Options:
1. Use --legacy-peer-deps flag
2. Downgrade [package] to [version]
3. Find alternative package

Recommend option [X] because [reason].
```

### File Already Exists

```
[File] already exists. Should I:
1. Overwrite with new implementation
2. Merge changes into existing file
3. Skip this file

Show me what changes would be made before proceeding.
```

### Tests Failing

```
Tests are failing for [component/function].

Show me:
1. The failing test output
2. The relevant code
3. What change would fix it

Fix the issue before continuing to next task.
```

---

## Quality Checklist During Implementation

For each phase, verify:

- [ ] All tasks for the phase are complete
- [ ] Types/schemas are properly defined
- [ ] Tests are written and passing
- [ ] Linting passes (language-specific linter)
- [ ] Type checking passes (if applicable)
- [ ] App runs without errors
- [ ] Feature works as specified

---

## Tips

1. **Pre-scaffold when possible** — Avoids nested folder issues
2. **Implement in phases** — Don't try to do everything at once
3. **Test as you go** — Catch issues early
4. **Check the terminal** — Agent should run and verify commands
5. **Review generated code** — Don't blindly accept everything
6. **Commit after each phase** — Easy to roll back if needed
