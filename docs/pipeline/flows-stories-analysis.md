# User Flows, User Stories & UX/UI Analysis
### How they connect and how to create them for Partus modules

---

## How these three things connect

```
USER FLOWS                USER STORIES              UX/UI ANALYSIS
────────────              ────────────              ──────────────
"What does the            "What does the            "Does the design
user DO, step             user NEED and             actually support
by step?"                 WHY?"                     the flows and
    ↓                         ↓                     stories well?"
Draw BEFORE               Write BEFORE              Run AFTER
designing                 designing                 designing

→ Feeds the              → Feeds the               → Feeds the
  functional spec           acceptance criteria       iteration cycle
  (Section 3)              and ticket definition      and dev tickets
                           (Sections 3 + 7)           (Sections 6 + 7)
```

**Rule:** If you skip user flows, you design screens with no sense of how the
user arrives or leaves. If you skip user stories, acceptance criteria are vague.
If you skip UX analysis, problems reach the dev build.

---

## Part 1 — User Flows

### What a user flow is

A user flow maps every step a user takes to complete a goal — including
decision points, error paths, and alternative paths. Not just the happy path.

**A complete user flow has:**
- Entry point (how the user gets here)
- Each step the user takes
- Each decision point (yes/no, condition)
- Error/exception paths
- Exit points (success, cancel, timeout)

### Types of flows to create per module

| Flow type | When to create it | Example |
|---|---|---|
| **Happy path** | Always | Midwife fills all fields, approves record |
| **Error/recovery path** | When there are required fields or validations | Midwife tries to approve with missing fields |
| **Alert/warning path** | When there are clinical warnings | ONEWS elevated — what does midwife do? |
| **Conditional path** | When fields appear/hide based on other values | Apgar 5 min < 7 → Apgar 10 min becomes required |
| **Role-based path** | When different roles see different things | Doctor vs. midwife view |
| **Edge case path** | For rare but important scenarios | Twin birth, emergency delivery, no vannavgang |

### Claude prompt to generate user flows

```
I am designing [module name] in Partus (Norwegian electronic birth journal,
used by midwives in hospital maternity wards).

Here is the functional spec: [paste Section 3 of master spec]
Here is the field map: [paste Section 4]

Generate user flows as Mermaid flowcharts for:
1. Happy path (all fields filled, successful approval)
2. Error recovery path (required fields missing, user guided to fix them)
3. [Any specific conditional flow from the field map]

For each flow:
- Start from the real entry point (not just "open screen")
- Include every decision point
- Show what happens on each branch
- End at a clear exit state
- Keep it to one page per flow — combine trivial steps
```

### How to turn a Mermaid flow into a Figma flow

1. Copy the Mermaid code → paste at [mermaid.live](https://mermaid.live) to preview
2. In Figma: use **Autoflow** plugin to auto-draw arrows between your existing frames
3. Or: export the Mermaid diagram as SVG → paste into Figma as a reference layer
4. Present the Figma flow to stakeholders alongside the prototype

### User flow template (text format — faster than Mermaid for first draft)

```
FLOW: [name]
Entry point: [how does the user get here?]

1. User [action]
   → System [response]

2. User [action]
   → IF [condition]: go to step 3
   → IF NOT [condition]: go to step 5

3. User [action]
   → System [response]

4. [continue...]

ERROR PATH A: [what triggers this]
   → System shows [what]
   → User must [what]
   → Return to step [N]

EXIT: [success state / cancel state]
```

---

## Part 2 — User Stories

### What a user story is

A user story captures a user need from the user's perspective, not the system's.
It is NOT a task description ("add a field") — it is a need ("I need to see X
so I can do Y").

**Format:**
```
As a [specific role],
I want to [do something specific],
so that [I achieve this outcome].
```

### What makes a good user story in medical software

| Good | Bad |
|---|---|
| "As a midwife, I want to see which required fields are missing at a glance so that I can complete the record before the doctor arrives" | "As a user, I want to fill in the form" |
| "As a supervising midwife, I want to see who registered each section and when so that I can verify the audit trail" | "As a user, I want audit logging" |
| "As a midwife during active labor, I want the system to save my progress automatically so that an emergency call doesn't cause data loss" | "As a user, I want autosave" |

**Key:** Name the role precisely. Name the context (during active labor, during admission). Name the real outcome (not "so that it works" but "so that I can hand over to the night shift without data loss").

### Acceptance criteria

Write these in testable bullet points. Every criterion must be verifiable by QA.

```
Story: As a midwife, I want to be guided directly to a missing required field
       so that I don't have to scroll to find it.

Acceptance criteria:
- [ ] Clicking the alert banner scrolls to and focuses the first missing required field
- [ ] The missing field has a visible red border and "Mangler" label
- [ ] The field count in the alert banner matches the actual number of unfilled required fields
- [ ] After filling the field, the banner updates without page reload
- [ ] If all required fields are filled, the banner disappears
- [ ] "Fullfør og godkjenn" button becomes enabled only when 0 required fields remain
```

### Claude prompt to generate user stories

```
I am designing [module name] in Partus (Norwegian birth journal).

Primary users: [list roles]
Functional spec: [paste Section 3]
Field map: [paste Section 4]
Known pain points with the old module: [describe]

Generate user stories covering:
1. The main task (happy path)
2. Error handling and recovery
3. Each conditional behavior in the field map
4. Role-based access differences
5. Clinical edge cases (from the field map edge cases section)
6. Time pressure scenarios (midwives work under interruption and urgency)

For each story, include:
- As a / I want / so that
- 4-6 acceptance criteria (testable bullet points)
- Priority: Must have / Should have / Nice to have
- Story points estimate
```

### Claude prompt to derive stories from a Jira ticket

```
Here is a Jira ticket for Partus: [paste ticket]

Convert this into proper user stories.
The primary user is a midwife in a Norwegian hospital maternity ward.
For each story: As a / I want / so that + acceptance criteria.
Flag anything in the ticket that is a TECHNICAL task, not a user story
(technical tasks belong in the dev ticket, not the user story).
```

### Claude prompt to derive stories from an old Delphi module

```
Here is the old Delphi module for [module name] in Partus: [describe/screenshot]

Write user stories for the REFACTORED version of this module.
Don't write stories for features that should be removed.
Add stories for improvements based on modern obstetric practice.
Flag each story as: Existing functionality / Improvement / New.
```

---

## Part 3 — UX/UI Analysis

### What UX/UI analysis is (and is not)

**It is:** A structured review of the design against real user needs, clinical
workflow, usability heuristics, and accessibility standards.

**It is not:** A personal opinion about colors or layout preferences.

### The four lenses for Partus

Every screen should be reviewed through all four:

```
1. CLINICAL LENS          2. USABILITY LENS
   Does it match the         Nielsen's 10 heuristics
   real clinical workflow?   Error prevention matters
   Norwegian terminology?    most in medical software
   Safety-critical paths?

3. ACCESSIBILITY LENS     4. DATA INTEGRITY LENS
   WCAG 2.1 AA              Are all fields mapped?
   Required for Norwegian    Validations correct?
   health software           Edge cases handled?
   Color-blind users         MFR compliance?
```

### Running a UX analysis with Claude

**Quick analysis (paste screenshot):**
```
This is a screen from Partus, a Norwegian electronic birth journal.
[paste screenshot]

Analyze through these four lenses:
1. Clinical workflow: Does the layout match how a midwife actually works?
   Flag any sequence that forces unnatural steps.
2. Usability (Nielsen): Focus on error prevention, visibility of system status,
   and recognition over recall.
3. Accessibility: WCAG 2.1 AA. Focus on color contrast, form labels,
   error messages, and color-only states.
4. Data integrity: Do you see any fields that look like they might be missing
   validation, have inconsistent states, or have clinical range issues?

Rate each issue: Critical / High / Medium / Low
For Critical and High issues, suggest a specific fix.
```

**Deep analysis (paste spec + screenshot):**
```
Here is the master spec for [module name]: [paste]
Here is the current design: [paste screenshot]

Run a gap analysis:
1. Are all fields from Section 4 (field map) present in the design?
2. Are all user stories from Section 3 supported by the design?
3. Are all error states designed (not just the happy path)?
4. Are all conditional fields correctly shown/hidden?
5. Does the visual hierarchy match the clinical priority of information?
Flag anything missing or inconsistent.
```

### When to run UX analysis

| Moment | Type | Who |
|---|---|---|
| After first Figma Make draft | Quick review (Claude Chat + screenshot) | You |
| After manual refinement | Full analysis (Claude Chat + spec + screenshot) | You |
| Before customer prototype review | Gap analysis (all four lenses) | You |
| After customer feedback | Regression check (did fixes introduce new issues?) | You |
| Before dev handoff | Final sign-off (Section 6 of master spec) | You + clinical stakeholder for Critical items |

### UX analysis findings format

When logging findings in Section 6 of the master spec:

| # | Severity | Lens | Finding | Fix | Status |
|---|---|---|---|---|---|
| 1 | Critical | Data integrity | Progress counter shows "9 av 21" but section badges show 18+14=32 | Reconcile counter to single source of truth | Open |
| 2 | High | Accessibility | Yellow "Ikke registrert" state uses color only — no icon | Add ⚠ icon to yellow field state | Open |

---

## Putting it all together in the master spec

| Section | What goes in it |
|---|---|
| Section 3 — Functional Spec | User flows (text format or Mermaid) |
| Section 3 — User flows | One flow per main scenario |
| Section 3 — Business rules | Conditional logic from the flows |
| Sections 3+7 | User stories + acceptance criteria (stories in spec, ACs in tickets) |
| Section 6 — UX Review | UX/UI analysis findings table |
| Section 7 — Dev Tickets | One ticket per user story (or group of small stories) |
| Section 8 — Test Cases | Derived from acceptance criteria |

**Claude prompt to turn user stories into test cases:**
```
Here are the user stories and acceptance criteria for [module name]: [paste]

Convert the acceptance criteria into test cases.
For each acceptance criterion, write:
- TC-[module]-[number]: [title]
- Preconditions
- Test steps
- Expected result
- Test data (use Norwegian clinical values)

Add one negative test per story (what happens if the user does it wrong).
```
