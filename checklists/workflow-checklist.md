# Vibe Code Workflow Checklist

> Use this checklist to track progress through the development workflow.
> Copy this file to your project's `docs/` folder.

---

## Project: [Name]
**Started:** YYYY-MM-DD  
**Current Phase:** [ ]

---

## Greenfield Workflow

### Phase 0: Setup
- [ ] Created project folder
- [ ] Ran `specify init <name> --ai copilot`
- [ ] Opened in VS Code
- [ ] Copied custom agents from toolkit (optional)

### Phase 1: Brainstorm
- [ ] Had conversation in Plan Mode
- [ ] Asked about MVP scope
- [ ] Identified edge cases
- [ ] Created `docs/brainstorm.md`
- [ ] Reviewed brainstorm quality

**Brainstorm Quality Check:**
- [ ] Clear problem statement
- [ ] Defined target user
- [ ] Prioritized features (MVP vs future)
- [ ] At least one user flow
- [ ] Technical direction identified
- [ ] Open questions listed

### Phase 2: Constitution
- [ ] Ran `/speckit.constitution`
- [ ] Reviewed code quality standards
- [ ] Reviewed testing requirements
- [ ] Reviewed UX standards
- [ ] Reviewed performance targets
- [ ] Constitution matches project scope

### Phase 3: Specification
- [ ] Ran `/speckit.specify`
- [ ] User stories have acceptance criteria
- [ ] Functional requirements are testable
- [ ] Non-functional requirements have metrics
- [ ] Edge cases identified
- [ ] Key entities defined

### Phase 3.5: Clarify (Optional)
- [ ] Ran `/speckit.clarify`
- [ ] Answered clarifying questions
- [ ] Spec updated with clarifications
- [ ] No critical ambiguities remaining

### Phase 4: Plan
- [ ] Evaluated framework need (minimal vs framework)
- [ ] Used appropriate framework comparison tool:
  - [ ] Stack Match (for JavaScript/TypeScript frontend)
  - [ ] TechEmpower Benchmarks (for backend, any language)
- [ ] Ran `/speckit.plan`
- [ ] Research documents decisions
- [ ] Data model covers all entities
- [ ] Project structure defined
- [ ] Constitution check passes
- [ ] Quickstart is complete

### Phase 4.5: Checklist (Optional)
- [ ] Ran `/speckit.checklist` for [domain]
- [ ] Reviewed checklist items
- [ ] Requirements are complete
- [ ] Requirements are clear
- [ ] No critical gaps

### Phase 5: Tasks
- [ ] Ran `/speckit.tasks`
- [ ] Tasks cover all requirements
- [ ] Tasks are properly sequenced
- [ ] Dependencies are noted

### Phase 5.5: Analyze (Optional)
- [ ] Ran `/speckit.analyze`
- [ ] No critical issues
- [ ] Coverage is adequate
- [ ] No terminology drift
- [ ] Constitution compliance verified

### Phase 6: Implement
- [ ] Pre-scaffolded project (if needed)
- [ ] Ran `/speckit.implement`
- [ ] All tasks completed
- [ ] Linting passes (language-specific)
- [ ] Type checking passes (if applicable)
- [ ] Tests pass
- [ ] Build succeeds

### Phase 7: QA
- [ ] Ran `/dami.qa`
- [ ] Type check passes
- [ ] Lint passes
- [ ] Unit tests pass
- [ ] E2E tests pass
- [ ] User flows validated
- [ ] User guide generated

### Phase 8: Learn
- [ ] Ran `/dami.learn`
- [ ] Reviewed learning materials
- [ ] Can explain architecture
- [ ] Understand key patterns
- [ ] Know how data flows

---

## Brownfield Workflow

### Phase 0: Setup
- [ ] Navigated to project folder
- [ ] Ran `specify init . --ai copilot`
- [ ] Copied custom agents from toolkit (optional)

### Phase 1: Constitution
- [ ] Ran `/speckit.constitution`
- [ ] Constitution reflects existing patterns
- [ ] No new arbitrary rules imposed
- [ ] Inconsistencies noted for resolution

### Phase 2: Specification
- [ ] Ran `/speckit.specify`
- [ ] Feature scope is focused
- [ ] Integration points identified
- [ ] Existing components referenced

### Phase 2.5: Clarify (Optional)
- [ ] Ran `/speckit.clarify`
- [ ] Ambiguities resolved
- [ ] Spec updated

### Phase 3: Plan
- [ ] Ran `/speckit.plan`
- [ ] Uses existing tech stack
- [ ] Follows existing patterns
- [ ] Reuses existing components
- [ ] Data model extends appropriately

### Phase 3.5: Checklist (Optional)
- [ ] Ran `/speckit.checklist`
- [ ] Requirements validated

### Phase 4: Tasks
- [ ] Ran `/speckit.tasks`
- [ ] Tasks integrate with existing code

### Phase 4.5: Analyze (Optional)
- [ ] Ran `/speckit.analyze`
- [ ] No conflicts with existing code

### Phase 5: Implement
- [ ] Ran `/speckit.implement`
- [ ] Feature works
- [ ] Existing tests still pass
- [ ] New tests added

### Phase 6: QA
- [ ] Ran `/dami.qa`
- [ ] Feature validated
- [ ] No regressions

### Phase 7: Learn
- [ ] Ran `/dami.learn`
- [ ] Understand new code

---

## Notes

[Add any project-specific notes here]
