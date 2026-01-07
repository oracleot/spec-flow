# External Tooling & Resources

> Project-specific tool recommendations that complement the Spec Kit workflow.
> This file survives Spec Kit updates and is referenced by agents during planning phases.

## Framework Selection

> **Note:** Framework selection tools vary by language/ecosystem. Choose the appropriate tool below based on your project's technology stack.

---

### Stack Match (JavaScript/TypeScript Frontend Projects Only)

**When to Use**: At the start of `/speckit.plan` for **new JavaScript/TypeScript frontend projects** where the frontend framework is not predetermined.

**Tool**: [Stack Match](https://stack-match.as93.net/) - Data-driven frontend JavaScript framework comparison

**Supported Frameworks**: React, Vue, Svelte, Angular, Solid.js, Preact, Qwik, Alpine.js, Lit, and more.

**Integration with Constitution**:

Map your constitution constraints to Stack Match priority weights:

| Constitution Constraint | Stack Match Priority | Suggested Weight |
|------------------------|---------------------|------------------|
| Bundle <500KB gzipped | Bundle Size | 8-10 |
| Performance SLAs (<100ms ops) | Performance | 8-10 |
| Long-term maintenance | Viability | 7-9 |
| Offline-capable | N/A (manual check) | - |
| TypeScript strict mode | N/A (all modern frameworks support) | - |

**Output Format** (for research.md):

```markdown
## Framework Evaluation

**Tool**: [Stack Match](https://stack-match.as93.net/)
**Date**: [evaluation date]

### Priority Weights

| Priority | Weight | Rationale |
|----------|--------|-----------|
| Bundle Size | 9 | Constitution: <500KB gzipped |
| Performance | 8 | Constitution: <100ms filter ops |
| Viability | 7 | Long-term maintenance |
| Ecosystem | 6 | Community support needs |

### Candidates

| Framework | Match Score | Key Strengths |
|-----------|-------------|---------------|
| [Framework 1] | X% | [strengths] |
| [Framework 2] | X% | [strengths] |
| [Framework 3] | X% | [strengths] |

### Decision

**Selected**: [Framework]
**Rationale**: [Why this over alternatives - team experience, specific features, ecosystem]
```

**Skip When**:
- Brownfield project (framework already chosen)
- Spec explicitly defines the framework
- Non-JavaScript/TypeScript project (use TechEmpower or language-specific tools below)
- Non-frontend project (API, CLI, library)

---

### TechEmpower Web Framework Benchmarks (All Languages - Backend)

**When to Use**: At the start of `/speckit.plan` for **any backend/full-stack project** where you need to compare framework performance across languages.

**Tool**: [TechEmpower Benchmarks](https://www.techempower.com/benchmarks/) - Comprehensive web framework performance benchmarks

**Supported Languages**: Python, Go, Rust, Java, Kotlin, C#, PHP, Ruby, Elixir, JavaScript/Node.js, C++, and 50+ more languages.

**What It Measures**:
- JSON serialization performance
- Single/Multiple database queries
- Fortunes (HTML template rendering)
- Data updates
- Plaintext throughput

**Output Format** (for research.md):

```markdown
## Backend Framework Evaluation

**Tool**: [TechEmpower Benchmarks](https://www.techempower.com/benchmarks/)
**Date**: [evaluation date]
**Test Type**: [Fortunes / JSON / Multiple Queries]

### Requirements Mapping

| Requirement | Benchmark Priority |
|-------------|-------------------|
| High throughput | JSON serialization |
| Database-heavy | Multiple queries |
| Template rendering | Fortunes |

### Candidates ([Language])

| Framework | Requests/sec | Relative Performance |
|-----------|-------------|---------------------|
| [Framework 1] | X | 100% |
| [Framework 2] | X | Y% |
| [Framework 3] | X | Z% |

### Decision

**Selected**: [Framework]
**Rationale**: [Why this over alternatives - performance, ecosystem, team experience]
```

**Skip When**:
- Frontend-only project (use Stack Match for JS)
- Performance is not a primary concern
- Team has strong preference/experience with specific framework

---

### Language-Specific Framework Comparison Resources

For languages where Stack Match or TechEmpower don't provide sufficient guidance:

#### Python
- **Web Frameworks**: Compare Django, FastAPI, Flask, Starlette via TechEmpower benchmarks
- **Data Science**: scikit-learn vs PyTorch vs TensorFlow - depends on use case
- **Async**: FastAPI (Starlette) vs aiohttp vs Quart

#### Go
- **Web Frameworks**: Compare Gin, Echo, Fiber, Chi via TechEmpower
- **All are performant** - choose based on API design preferences

#### Rust  
- **Web Frameworks**: Actix-web, Axum, Rocket via TechEmpower
- **Consider**: Actix for max performance, Axum for async-first design

#### Java/Kotlin
- **Compare**: Spring Boot, Quarkus, Micronaut, Ktor via TechEmpower
- **Consider**: Startup time (Quarkus), ecosystem (Spring), Kotlin-native (Ktor)

#### C#/.NET
- **ASP.NET Core** is the standard; compare minimal APIs vs MVC vs Blazor based on app type

#### PHP
- **Compare**: Laravel, Symfony, Slim via TechEmpower
- **Consider**: Laravel for rapid development, Symfony for enterprise

#### Ruby
- **Rails** is dominant; consider Sinatra for micro-services

---

## Simplicity Check

### When to Use Vanilla HTML/CSS/JS

Before choosing a framework, ask:

1. **State Complexity**: Does the app have complex, interdependent state?
2. **Component Reuse**: Are there many reusable UI patterns?
3. **Real-time Updates**: Does data change frequently without page reload?
4. **Team Familiarity**: Does the team already know a framework?
5. **Ecosystem Needs**: Do you need routing, testing libraries, etc.?

**If most answers are "No"** → Consider vanilla implementation

**Vanilla is Sufficient For**:
- Static sites with minor interactivity
- Form-based apps with simple validation
- Data display with filtering/sorting
- Learning projects
- Performance-critical micro-apps

**Framework is Warranted For**:
- Complex state management
- Many interactive components
- Real-time updates
- PWA with offline-first
- Large applications with routing

---

## Future Tools

<!-- Add other external tools as discovered -->

### [Tool Name]

**When to Use**: [phase and condition]
**Purpose**: [what it helps with]
**Integration**: [how it fits the workflow]
