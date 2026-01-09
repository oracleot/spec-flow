# Phase 3: Specify Prompt

> **Agent:** `speckit.specify`
> **Output:** `specs/001-feature/spec.md`

---

## What is a Specification?

The specification defines **what** to build (not how). It includes:
- User stories with acceptance criteria
- Functional requirements (what the system must do)
- Non-functional requirements (quality attributes)
- Edge cases and error handling
- Success criteria (how we know it's done)

---

## Greenfield Project Prompt

For new projects, create the spec from your brainstorm:

```
Read docs/brainstorm.md and create a comprehensive feature specification 
for the MVP.

Structure the spec with:

## User Scenarios & Testing
For each core feature, create user stories with:
- As a [user], I want to [action], so that [benefit]
- Priority (P1 = must have, P2 = should have, P3 = nice to have)
- Acceptance criteria (Given/When/Then format)
- Independent test description

## Edge Cases
List what happens when:
- Required data is missing
- User provides invalid input
- External services fail
- Storage is full or unavailable
- Concurrent operations conflict

## Functional Requirements
Format: FR-001: System MUST/SHOULD [action] [condition]
- Be specific and testable
- Use MUST for required, SHOULD for preferred
- Include all CRUD operations
- Cover all user interactions

## Non-Functional Requirements
- Performance targets (load time, response time)
- Accessibility requirements (WCAG level)
- Browser/device support
- Offline capabilities
- Security requirements

## Success Criteria
Measurable outcomes that indicate the feature works:
- User can complete [action] in under [time]
- Data persists across [condition]
- System handles [edge case] gracefully

## Key Entities
List the main data objects with:
- Name and description
- Key attributes
- Relationships to other entities

Focus on the MVP scope identified in the brainstorm.
Make requirements specific enough to test.
Flag anything that needs clarification as "NEEDS CLARIFICATION".
```

---

## Brownfield Project Prompt

For adding features to existing projects:

```
I want to add [FEATURE DESCRIPTION] to this project.

Context:
- [Why this feature is needed]
- [How it relates to existing functionality]
- [Any constraints or integration points]

Create a feature specification that:
1. Defines user stories with acceptance criteria
2. Lists functional requirements
3. Identifies integration points with existing code
4. Notes edge cases specific to this feature
5. Defines success criteria

Keep the scope focused on this specific feature.
Reference existing entities/components where relevant.
```

---

## Specification Sections Reference

### User Stories Format

```markdown
### User Story 1 - [Short Name] (Priority: P1)

As a [user type], I want to [action], so that [benefit].

**Why this priority**: [Justification]

**Independent Test**: [How this can be tested in isolation]

**Acceptance Criteria**:

1. **Given** [context], **When** [action], **Then** [result]
2. **Given** [context], **When** [action], **Then** [result]
3. **Given** [context], **When** [action], **Then** [result]
```

### Functional Requirements Format

```markdown
## Functional Requirements

- **FR-001**: System MUST allow users to [action] with [parameters]
- **FR-002**: System MUST persist [data] in [storage]
- **FR-003**: System MUST validate [input] before [action]
- **FR-004**: System MUST display [feedback] when [condition]
- **FR-005**: System SHOULD [optional behavior] when [condition]
```

### Non-Functional Requirements Format

```markdown
## Non-Functional Requirements

### Performance
- **NFR-001**: Page MUST load in under 2 seconds on 4G connection
- **NFR-002**: Search results MUST appear in under 100ms

### Accessibility
- **NFR-003**: All interactive elements MUST be keyboard accessible
- **NFR-004**: MUST meet WCAG 2.1 Level AA

### Reliability
- **NFR-005**: App MUST work offline after initial load
- **NFR-006**: Data MUST persist across browser sessions
```

### Edge Cases Format

```markdown
## Edge Cases

- What happens when user submits form with missing required fields?
- How does the system handle very long text inputs?
- What happens if storage quota is exceeded?
- How are duplicate entries handled?
- What happens when filtering returns zero results?
```

### Success Criteria Format

```markdown
## Success Criteria

- **SC-001**: Users can [action] in under [time]
- **SC-002**: [Data] persists across page refreshes
- **SC-003**: [Operation] completes without errors
- **SC-004**: UI remains responsive with [load] data
- **SC-005**: All [requirement type] triggers appropriate [feedback]
```

---

## Quality Checklist

Before moving to Phase 4, verify:

- [ ] All MVP features have user stories
- [ ] Each user story has acceptance criteria
- [ ] Functional requirements are specific and testable
- [ ] Edge cases are identified
- [ ] Non-functional requirements have measurable targets
- [ ] Key entities are defined
- [ ] No vague terms like "fast", "intuitive", "robust"
- [ ] NEEDS CLARIFICATION items are flagged for Phase 3.5

---

## Tips

1. **Focus on behavior, not implementation** — "User can filter" not "Filter uses useState"
2. **Make it testable** — If you can't write a test, it's not specific enough
3. **Prioritize ruthlessly** — P1 is MVP, P2/P3 can wait
4. **Name things consistently** — Same entity name everywhere
5. **Flag unknowns** — It's okay to have NEEDS CLARIFICATION items
