# Phase 1: Brainstorm Prompt

> **Mode:** Copilot Plan Mode (conversational)
> **Output:** `docs/brainstorm.md`

---

## Starting the Conversation

Use Plan Mode (not Agent Mode) to have a back-and-forth conversation about your idea.

### Initial Prompt Template

```
I want to build [ONE SENTENCE DESCRIPTION OF YOUR IDEA].

My goals are:
- [Primary goal - what problem does this solve?]
- [Secondary goal - optional]

My constraints are:
- [Time: weekend project / month-long / ongoing]
- [Users: just me / friends & family / public]
- [Platform: web / mobile / desktop / CLI]

Help me think through this idea. Ask me clarifying questions to:
1. Refine the core value proposition
2. Identify must-have vs nice-to-have features
3. Spot potential technical challenges
4. Find edge cases I haven't considered
5. Suggest features I might be missing
```

### Example Prompts

**Personal Tool:**
```
I want to build a personal finance tracker that helps me understand where my 
money goes each month.

My goals are:
- See spending by category at a glance
- Set budgets and get alerts when overspending
- Work offline (I don't want my financial data in the cloud)

My constraints are:
- Weekend project to start, iterate over time
- Just for me
- Web app (PWA for offline)

Help me think through this idea.
```

**Learning App:**
```
I want to build an app to help me master algorithm problems for coding 
interviews using spaced repetition.

My goals are:
- Track which problems I've solved
- Get reminded to review problems before I forget
- Build a solution journal with my notes

My constraints are:
- Ongoing side project
- Just for me initially, maybe share later
- Web app, mobile-friendly

Help me think through this idea.
```

**Productivity Tool:**
```
I want to build a simple task manager that focuses on daily priorities 
instead of endless backlogs.

My goals are:
- Pick 3 priorities each morning
- Track completion streaks
- Review weekly progress

My constraints are:
- 2-week sprint
- Personal use
- Web + mobile PWA

Help me think through this idea.
```

---

## Guiding the Conversation

Plan Mode will ask you questions. Here are helpful follow-up prompts:

### Scope Refinement
```
That's a lot of features. Help me prioritize them into:
- MVP (must have for v1)
- V2 (next iteration)
- Someday (nice to have)
```

### Technical Direction
```
What are the key technical decisions I need to make for this app?
Walk me through the trade-offs.
```

### User Flows
```
Walk me through the main user flow for [core feature].
What happens step by step?
```

### Edge Cases
```
What edge cases should I consider for [specific feature]?
What could go wrong?
```

### Competition/Alternatives
```
What existing tools solve similar problems?
How would this be different/better?
```

---

## Creating the Brainstorm Document

After the conversation, switch to **Agent Mode** and use this prompt:

```
Create docs/brainstorm.md and organize our conversation into a structured 
format. Use this structure:

# [Project Name] - Product Brainstorm

## Problem Statement
What problem are we solving and for whom?

## Target User
Who is the primary user? What are their needs?

## Core Features (MVP)
Prioritized list of must-have features for v1

## Future Features (V2+)
Features for later iterations

## User Flows
Key user journeys through the app

## Technical Considerations
- Platform decisions
- Data storage approach
- Key libraries/frameworks
- Performance requirements

## Open Questions
Unresolved decisions that need more thought

## Inspiration & References
Similar products, design patterns to follow

Include insights from our conversation. Be specific rather than vague.
```

---

## Brainstorm Quality Checklist

Before moving to Phase 2, verify your brainstorm includes:

- [ ] Clear problem statement (not just features)
- [ ] Defined target user
- [ ] Prioritized feature list (MVP vs future)
- [ ] At least one detailed user flow
- [ ] Technical direction (even if rough)
- [ ] Identified edge cases
- [ ] List of open questions

---

## Tips

1. **Don't rush** — Spend at least 15-20 minutes in conversation
2. **Be honest about constraints** — Weekend project ≠ full product
3. **Start small** — A focused MVP beats a sprawling v1
4. **Capture everything** — You can always cut later
5. **Question assumptions** — "Why do I need X?" is always valid
