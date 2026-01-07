# 🔄 Spec Flow

> **Specification-driven development for the AI age.**

A structured workflow companion for building software with AI coding assistants, extending GitHub's [Spec Kit](https://github.com/github/spec-kit) methodology with practical prompts, checklists, and tooling guidance.

## Built on Spec Kit

This toolkit is built on top of **[Spec Kit](https://github.com/github/spec-kit)** — GitHub's open-source framework for specification-driven AI development. Spec Kit provides:

- **Structured agents** (`speckit.specify`, `speckit.plan`, `speckit.implement`, etc.) that guide AI assistants through a phased development process
- **Memory files** that persist project context (constitution, decisions, constraints)
- **Specification templates** that ensure requirements are clear before code is written
- **A CLI tool** (`specify`) for initializing and managing spec-driven projects

**Spec Flow** extends Spec Kit with:
- Ready-to-use prompt templates for each workflow phase
- Framework selection guidance (Stack Match, TechEmpower Benchmarks)
- Multi-language examples (not just JavaScript/TypeScript)
- Practical checklists for tracking progress
- Tips and patterns learned from real projects

## Philosophy

**"Specify first. Build with intent. Understand what you ship."**

This workflow helps you:
- **Think before you build** — Brainstorm → Spec → Plan → Build
- **Stay in control** — You understand what's being built, not just watching AI generate code
- **Build consistently** — Same high-quality process for every project
- **Learn continuously** — Custom agents help you understand what was built

---

## Quick Start

### Prerequisites

- Clone this repository
- Install Spec Kit: follow instuctions here: https://github.com/github/spec-kit

### New Project

```bash
# 1. Create project
cd ~/Projects
specify init my-awesome-app --ai copilot

# 2. Open in VS Code
code my-awesome-app

# 3. Copy toolkit extensions
cp -r path/to/spec-flow/memory/* my-awesome-app/.specify/memory/
```

Then follow the [Greenfield Workflow](#greenfield-workflow-new-projects) below.

> **Note:** This toolkit works with any programming language or framework. While examples often use JavaScript/TypeScript for illustration, the methodology applies equally to Python, Go, Rust, Java, C#, and any other stack.

---

## Workflows

### Greenfield Workflow (New Projects)

| Phase | Mode/Agent | What You Do | Output |
|-------|------------|-------------|--------|
| 0 | Terminal | `specify init <project-name> --ai copilot` | Project scaffold |
| 1 | Plan Mode | Brainstorm your idea | `docs/brainstorm.md` |
| 2 | `speckit.constitution` | Create project principles | `.specify/memory/constitution.md` |
| 3 | `speckit.specify` | Define what to build | `specs/001-feature/spec.md` |
| 3.5 | `speckit.clarify` | *(Optional)* Reduce ambiguity | Updated spec.md |
| 4 | `speckit.plan` | Technical architecture | `plan.md`, `research.md`, `data-model.md` |
| 4.5 | `speckit.checklist` | *(Optional)* Requirements QA | `checklists/*.md` |
| 5 | `speckit.tasks` | Break down into tasks | `tasks.md` |
| 5.5 | `speckit.analyze` | *(Optional)* Cross-check artifacts | Analysis report |
| 6 | `speckit.implement` | Build it | Working code |
| 7 | `qa` | Test the implementation | `qa-report.md`, `user-guide.md` |
| 8 | `learn` | Understand what was built | `learning/*.md` |

---

### Phase 0: Initialize Project

```bash
cd ~/Projects
specify init my-app --ai copilot
code my-app
```

**What it does:** Creates project structure with `.specify/`, `.github/agents/`, and templates.

---

### Phase 1: Brainstorm

**Switch to:** Copilot → **Plan Mode** (not Agent mode)

Plan mode is conversational and asks clarifying questions. Use it to refine your idea.

**Prompt Template:** See [conversation-prompts/01-brainstorm.md](conversation-prompts/01-brainstorm.md)

**Example:**
```
I want to build a personal finance tracker that helps me understand where my money goes each month. I want to see spending by category, set budgets, and get alerts when I'm overspending. It should work offline and sync when online.

Help me think through this idea. Ask me questions to clarify the scope and identify features I might be missing.
```

**After brainstorming:** Switch to **Agent Mode** and create the brainstorm file:

```
Create docs/brainstorm.md and organize our conversation into a structured product spec format. Include:
- Problem statement
- Target user
- Core features (prioritized)
- Nice-to-have features
- Technical considerations we discussed
- Open questions
```

**Output:** `docs/brainstorm.md`

---

### Phase 2: Constitution

**Switch to:** `speckit.constitution` agent

The constitution defines non-negotiable principles that guide all development.

**Prompt Template:** See [conversation-prompts/02-constitution.md](conversation-prompts/02-constitution.md)

**Example:**
```
Read docs/brainstorm.md and create a constitution focused on:
- Code quality (Type strict, component isolation)
- Testing requirements (what needs tests)
- UX consistency (offline-first, responsive)
- Performance (bundle size, load times)
- Data privacy (local-first, user owns data)
```

**Output:** `.specify/memory/constitution.md`

---

### Phase 3: Specify

**Switch to:** `speckit.specify` agent

This creates the formal feature specification with user stories and requirements.

**Prompt Template:** See [conversation-prompts/03-specify.md](conversation-prompts/03-specify.md)

**Example:**
```
Read docs/brainstorm.md and create a comprehensive feature specification.
Focus on the MVP scope we identified. Include:
- User stories with acceptance criteria
- Functional requirements
- Non-functional requirements
- Edge cases
```

**Output:** `specs/001-feature/spec.md`

---

### Phase 3.5: Clarify (Optional but recommended)

**Switch to:** `speckit.clarify` agent

This agent finds ambiguities in your spec and asks targeted questions.

**When to use:**
- Before `/speckit.plan` (catches issues early)
- When spec has vague terms like "fast", "secure", "intuitive"
- When you're unsure about edge cases

**Prompt:**
```
Review the spec and identify any ambiguities that could cause problems 
during implementation.
```

**What happens:**
1. Agent scans spec for unclear areas
2. Asks up to 5 targeted questions (one at a time)
3. Provides recommended answers for each
4. Updates spec with clarifications

**Output:** Updated `spec.md` with `## Clarifications` section

---

### Phase 4: Plan

**Switch to:** `speckit.plan` agent

This creates the technical implementation plan with architecture decisions.

**Prompt Template:** See [conversation-prompts/04-plan.md](conversation-prompts/04-plan.md)

**Example:**
```
Read docs/brainstorm.md and the spec. Create a technical plan using:
- React 19 with TypeScript (strict mode)
- Vite for build tooling
- Tailwind CSS for styling
- IndexedDB via Dexie.js for local storage
- PWA for offline support

For simple apps, prefer vanilla HTML/CSS/JS. Only use frameworks when 
complexity justifies it.
```

**Stack Match Integration (JavaScript/TypeScript projects only):**
For greenfield JavaScript/TypeScript projects where you're unsure about frontend framework choice, the agent should consult [Stack Match](https://stack-match.as93.net/) - see [memory/tooling.md](memory/tooling.md).

**For other languages:** Use [TechEmpower Web Framework Benchmarks](https://www.techempower.com/benchmarks/) for backend framework comparisons across 300+ frameworks in Python, Go, Rust, Java, C#, PHP, Ruby, and more.

**Output:** 
- `specs/001-feature/plan.md`
- `specs/001-feature/research.md`
- `specs/001-feature/data-model.md`
- `specs/001-feature/quickstart.md`
- `specs/001-feature/contracts/`

---

### Phase 4.5: Checklist (Optional)

**Switch to:** `speckit.checklist` agent

Creates "unit tests for your requirements" — validates that requirements are complete, clear, and consistent.

**When to use:**
- After `/speckit.plan`, before `/speckit.tasks`
- When requirements are complex
- For high-stakes features (auth, payments, data handling)

**Prompt:**
```
Create a UX requirements checklist for this feature. Focus on:
- Completeness (are all interactions specified?)
- Clarity (are vague terms quantified?)
- Consistency (do requirements align?)
```

**Checklist Types:**
- `ux.md` — UI/UX requirements quality
- `api.md` — API contract completeness
- `security.md` — Security requirements coverage
- `performance.md` — Performance requirements specificity

**Output:** `specs/001-feature/checklists/*.md`

**Key Concept:** Checklists test the *requirements*, not the implementation:
- ❌ "Verify button works" (tests implementation)
- ✅ "Is button behavior specified for all states?" (tests requirements)

---

### Phase 5: Tasks

**Switch to:** `speckit.tasks` agent

Breaks the plan into actionable implementation tasks.

**Prompt:**
```
(No prompt needed — it reads existing artifacts)
```

**Output:** `specs/001-feature/tasks.md`

---

### Phase 5.5: Analyze (Optional but Recommended)

**Switch to:** `speckit.analyze` agent

Cross-checks spec, plan, and tasks for inconsistencies.

**When to use:**
- After `/speckit.tasks`, before `/speckit.implement`
- When you want confidence before building
- To catch terminology drift or missing coverage

**Prompt:**
```
Analyze the spec, plan, and tasks for consistency issues.
```

**What it checks:**
- Requirements with no tasks (gaps)
- Tasks with no requirements (orphans)
- Terminology inconsistencies
- Constitution violations
- Ambiguous or duplicate requirements

**Output:** Analysis report (displayed, not saved)

---

### Phase 6: Implement

**Switch to:** `speckit.implement` agent

Executes the tasks and builds the feature.

**Prompt:**
```
Implement all tasks. Install dependencies at the project root level.
Use the existing project structure — do not create nested project folders.
```

**⚠️ Greenfield Gotcha:**
When the agent needs to scaffold a project (React, Django, Rails, etc.), it may try to create a nested folder. To avoid this:

1. **Pre-scaffold if needed:** Before running implement, manually scaffold your project:
   ```bash
   # JavaScript/TypeScript (Vite)
   npm create vite@latest . -- --template react-ts
   
   # Python (Django)
   django-admin startproject myproject .
   
   # Python (FastAPI) - create main.py at root
   # Go - run go mod init at root
   # Rust - cargo init .
   ```

2. **Or instruct the agent:**
   ```
   The project root is the working directory. Install all dependencies 
   and create all source files here. Do not create a new subfolder for 
   the app.
   ```

**Output:** Working code in your project's source directory

---

### Phase 7: QA Testing

**Switch to:** `qa` agent

Comprehensive testing: type checks, linting, unit tests, and E2E browser testing.

**Prompt:**
```
Test Phase 3 (or "all" for everything)
```

**What it does:**
1. Runs type checking (language-specific: `tsc`, `mypy`, `go vet`, etc.)
2. Runs linting (ESLint, Pylint, golangci-lint, etc.)
3. Runs unit tests (Vitest, pytest, go test, etc.)
4. Starts dev server and tests in browser (for web apps)
5. Validates user flows from spec
6. Generates QA report and user guide

**Output:**
- `specs/001-feature/qa-report.md`
- `specs/001-feature/user-guide.md`

---

### Phase 8: Learn

**Switch to:** `learn` agent

Teaches you what was built so you understand your own codebase.

**Prompt:**
```
Teach me about Phase 3
```

**What it does:**
1. Analyzes the implementation
2. Creates learning modules explaining concepts
3. Generates knowledge checks (quizzes)
4. Creates hands-on exercises
5. Builds a reference card

**Output:** `specs/001-feature/learning/`

---

## Brownfield Workflow (Existing Projects)

| Phase | Mode/Agent | What You Do |
|-------|------------|-------------|
| 0 | Terminal | `specify init . --ai copilot` |
| 1 | `speckit.constitution` | Create constitution from existing patterns |
| 2 | `speckit.specify` | Describe the new feature |
| 2.5 | `speckit.clarify` | *(Optional)* Clarify ambiguities |
| 3 | `speckit.plan` | Plan using existing tech stack |
| 3.5 | `speckit.checklist` | *(Optional)* Requirements QA |
| 4 | `speckit.tasks` | Break down into tasks |
| 4.5 | `speckit.analyze` | *(Optional)* Cross-check |
| 5 | `speckit.implement` | Build the feature |
| 6 | `dami.qa` | Test |
| 7 | `dami.learn` | Learn |

### Brownfield Constitution Prompt

```
Analyze the existing codebase and create a constitution that captures:
- Current code patterns and conventions
- Testing approach already in use
- UI/UX patterns (component library, styling)
- Existing constraints (tech stack, dependencies)

Don't impose new rules — document what's already established.
```

### Brownfield Plan Prompt

```
Read the spec and create a plan that:
- Uses the existing tech stack (don't introduce new frameworks)
- Follows established project patterns
- Integrates with existing components and hooks
- Maintains consistency with current architecture
```

---

## Toolkit Contents

```
spec-flow/
├── README.md                    # This file
├── conversation-prompts/                     # Ready-to-use prompt templates
│   ├── 01-brainstorm.md
│   ├── 02-constitution.md
│   ├── 03-specify.md
│   ├── 04-plan.md
│   └── 05-implement.md
├── templates/                   # File templates
│   └── brainstorm-template.md
├── memory/                      # Memory files to copy into projects
│   └── tooling.md
└── checklists/                  # Reference checklists
    └── workflow-checklist.md
```

---

## Quick Reference: Agent Modes

| Agent | Purpose | When to Use |
|-------|---------|-------------|
| **Plan Mode** | Conversational brainstorming | Phase 1: Ideation |
| **Agent Mode** | File creation/editing | Creating brainstorm.md |
| `speckit.constitution` | Project principles | Phase 2: Standards |
| `speckit.specify` | Feature specification | Phase 3: Requirements |
| `speckit.clarify` | Reduce ambiguity | Before planning |
| `speckit.plan` | Technical architecture | Phase 4: Design |
| `speckit.checklist` | Requirements QA | After planning |
| `speckit.tasks` | Task breakdown | Phase 5: Planning |
| `speckit.analyze` | Cross-artifact check | Before implementing |
| `speckit.implement` | Build the code | Phase 6: Execution |
| `dami.qa` | Test everything | Phase 7: Validation |
| `dami.learn` | Understand the code | Phase 8: Learning |

---

## Tips & Tricks

### 1. Don't Skip Clarify
`/speckit.clarify` catches ambiguities early. 10 minutes here saves hours of rework.

### 2. Use Checklist for Complex Features
For auth, payments, or data-sensitive features, always run `/speckit.checklist security` before implementation.

### 3. Analyze Before Implement
`/speckit.analyze` is your safety net. It catches inconsistencies between spec/plan/tasks.

### 4. Pre-Scaffold for Greenfield
If you know your target framework, scaffold it before running `/speckit.implement`:
```bash
# JavaScript/TypeScript
npm create vite@latest . -- --template react-ts

# Python
python -m venv venv && pip install fastapi uvicorn

# Go
go mod init myproject
```

### 5. Learn What You Build
Don't just vibe code and forget. Run `/dami.learn` to understand patterns used.

### 6. Keep Constitution Updated
When you make architecture decisions, update the constitution so future features stay consistent.

---

## Updating the Toolkit

```bash
cd ~/Projects/spec-flow
git pull  # if version controlled
```

To update Spec Kit:
```bash
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git
```

---

## Troubleshooting

### "Agent not found"
Make sure you copied agents to `.github/agents/` in your project.

### "Script not found"
Run `specify init . --force --ai copilot` to re-initialize Spec Kit files.

### "Implement creates nested folder"
Pre-scaffold or explicitly tell the agent to use project root.

### "Checklist items test implementation"
Checklists should test requirements quality, not implementation. Re-run with clearer instructions.

---

## Contributing

Found a better prompt? Improved workflow? 

1. Update the relevant file in `spec-flow/`
2. Test it on a real project
3. Document what changed and why

---

## License

Personal toolkit — use however you like!
