# Tickets & Estimates Guide

> Use this when you are ready to slice a finished spec into Jira tickets.
> The ticket table in Section 7 of your master spec is where tickets live.
> This file explains the process and gives you the prompts.

---

## When to create tickets

Only slice into tickets when:
- [ ] Field map is complete and signed off (Section 4)
- [ ] Customer prototype review is done (Section 5)
- [ ] UX review passes with no Critical or High issues (Section 6)
- [ ] Open questions are answered (or explicitly deferred)

Creating tickets too early is the main reason tickets need to be rewritten mid-sprint.

---

## How to slice a spec into tickets

**Rule: one ticket = one thing a dev can ship independently.**

Do not write:
- "Implement backend for admission form" (too vague, too big)
- "Fix everything in the old Delphi module" (no scope)

Do write:
- "Build risk factor section of admission form — frontend + validation"
- "Add FHIR sync for maternal blood type field"
- "Migrate admission_form table: remove deprecated fields, add new columns"

### Ticket types for a Delphi refactor project

| Type | What it covers |
|---|---|
| `Frontend` | Angular component, template, form, UI states |
| `API` | New or changed endpoint, business logic |
| `Data` | DB migration, data mapping from old to new structure |
| `Integration` | Sync with external system (DIPS, FHIR, HIS) |
| `Test` | E2E test, integration test, test data setup |

---

## Generating tickets with Claude

Paste this into Claude Code or Claude Chat when your spec is complete:

```
Here is my completed master spec for [module name] in Partus:

[paste your master-module-spec.md — or at minimum sections 3, 4, and the field map]

Create Jira tickets from this spec. For each ticket:

1. Title — short, action verb, specific (not "implement form")
2. Type — Frontend / API / Data / Integration / Test
3. User story — "As a [role], I want to [do X] so that [outcome]"
4. Acceptance criteria — bullet list, each item testable by QA
5. Technical notes — Angular 18 patterns, which service/component, any gotchas
6. Story point estimate — Fibonacci (1/2/3/5/8/13) with one-line reasoning
7. Depends on — which ticket must be done first (use ticket titles)

Rules:
- No ticket larger than 8 points. Split 13-point work first, then estimate.
- Data migration tickets before API tickets. API tickets before Frontend tickets.
- Group by sprint-ready order.
- Flag anything unclear in the spec that would block a dev from starting.
```

---

## Story point estimation

Use Fibonacci. When in doubt, round up.

| Points | Meaning | Delphi refactor examples |
|---|---|---|
| **1** | Trivial. No logic, no state. | Rename a label. Toggle a field to read-only. |
| **2** | Small, well-understood. One component, no integration. | Display-only field. Static dropdown with no DB link. |
| **3** | Standard. One component with state + validation. | Single form field with validation, error state, save. |
| **5** | Medium. Multiple components or one integration point. | Form section (3-5 fields) with API read. New dropdown synced from DB. |
| **8** | Large. Cross-cutting change or meaningful uncertainty. | Full form refactor (5+ fields). New field with FHIR sync. Data migration + API. |
| **13** | Too big. Split before estimating. | Always split. |

### Adjustment factors for medical software

Add 1-2 points if:
- The ticket touches a field that syncs to an external system (DIPS, HIS, FHIR)
- The ticket requires clinical validation (range rules, obstetric logic)
- The ticket involves a data migration from the old Delphi structure
- The business rule is ambiguous and needs clinical sign-off mid-sprint

---

## Jira ticket format

When copying into Jira, use this structure:

```
[TICKET TITLE]

User story:
As a [role], I want to [action] so that [outcome].

Acceptance criteria:
- [ ] [Specific, testable criterion]
- [ ] [Another criterion]
- [ ] [Edge case handled]
- [ ] WCAG 2.1 AA: [specific accessibility requirement]
- [ ] Norwegian locale: dates dd.mm.yyyy, decimal comma

Technical notes:
- Component: [file path if known]
- Uses: [service name, API endpoint]
- Angular patterns: [any specifics]

Story points: [N]
Depends on: [ticket title or "none"]

Spec reference: [module name] spec, Section [N]
```

---

## Handling estimates under pressure

When a stakeholder asks for estimates before the spec is done:

```
I have a partial spec for [module name]. It is not complete yet.
Here is what I know: [paste what you have]

Give me a rough range estimate (not a precise number) for the full module.
State what assumptions you are making.
List the 3 biggest unknowns that could change the estimate significantly.
```

Use this output to give a range ("likely 25-40 story points") rather than a false precise number. Commit to a precise estimate only when the spec is complete.

---

## Test cases from tickets

Once tickets are written, add test cases to Section 8 of the master spec. Use:

```
Here are the Jira tickets for [module name]: [paste ticket list]
Here is the field map: [paste Section 4]

Generate test cases. For each ticket that has acceptance criteria, create:
- Happy path test case
- At least one negative test (invalid input, missing required field, wrong role)
- One edge case if the field map has null/unknown/refused states for relevant fields

Format:
TC-[module]-[number] | Title | Preconditions | Steps | Expected result | Test data
```

---

## Sprint planning tip

After generating tickets, ask Claude:

```
Here are my tickets for [module name] with story point estimates:
[paste ticket table from Section 7]

Our sprint velocity is approximately [N] points.
Suggest a sprint-by-sprint delivery order that:
1. Gets something visible to the customer as early as possible
2. Respects technical dependencies (data before API before frontend)
3. Flags any ticket that needs clinical sign-off before it can start
```
