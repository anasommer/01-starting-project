# Design & Dev Pipeline — Partus
### For a team lead writing functional + design specs, iterating with customers, handing off to devs

---

## The honest reality

Your inputs are never the same. Sometimes you have a Jira ticket. Sometimes a user story from a clinician. Sometimes just a screenshot of an old Delphi form. Sometimes just your own idea. Sometimes all of the above, sometimes none.

**The pipeline has one rule: everything for one module lives in one document.**

Use the master spec template: `docs/templates/master-module-spec.md`
Copy it once per module. It follows you from first input to dev tickets.

---

## What the pipeline actually looks like

```
ANY INPUT
(Delphi module / Jira ticket / user story / your idea)
        ↓
[1] CAPTURE  — fill the top of the master spec
        ↓
[2] FIELD MAP  — before touching Figma, list every input + validation
        ↓
[3] DESIGN  — Figma, using the field map as your source of truth
        ↓
[4] PROTOTYPE → CUSTOMER  — iterate, log feedback in the master spec
        ↓
[5] UX REVIEW  — inline checklist in the master spec
        ↓
[6] TICKETS + ESTIMATES  — slice the spec into Jira tickets with story points
        ↓
[7] TEST CASES  — generate from the accepted spec
```

You can go back to any step. The change log at the bottom of the master spec tracks what changed and when.

---

## Starting from different inputs

### Starting from an old Delphi module

This is the most common case. Paste this into Claude Chat:

```
I am refactoring an old Delphi module in Partus (Norwegian electronic birth
journal). Here is the old module:

[Paste: screenshot / describe the form, its fields, behaviors, and what it does]

Help me:
1. Extract every field as a table: label, type, current validation, data source
2. Flag fields that are likely outdated or candidates for removal
3. Flag data that might have moved to another module or system
4. Suggest what new fields might be needed based on modern obstetric practice
5. Note any Norwegian clinical terminology that should be updated

Do NOT suggest a new design yet. Just help me understand what exists.
```

Then paste Claude's output into Section 2 of the master spec and start editing it.

---

### Starting from a Jira ticket or user story

```
I am working on Partus (Norwegian electronic birth journal).
Here is the input:

[Paste: Jira ticket / user story]

Help me turn this into a functional spec with:
1. Problem statement (one sentence: who needs to do what, and why)
2. Scope: what is included and explicitly what is NOT included
3. Affected modules / screens
4. Initial field list (just names and types — I will validate these next)
5. Open questions I need to answer before designing
```

---

### Starting from your own idea

```
I have an idea for a new feature in Partus (Norwegian electronic birth journal
used by midwives in hospital clinics).

My idea: [describe it in plain language]

Help me:
1. Frame it as a user story: "As a [user], I need to [do X] so that [outcome]"
2. Ask me 5 clarifying questions I should answer before speccing this out
3. Flag any similar features that likely already exist in birth journal systems
4. List the minimum fields this would need
```

---

## The master spec as a living document

The master spec has a **Decision Log** and a **Change Log**.

- Every time you make a significant decision, add a line to the Decision Log (date, what, why).
- Every time the customer review changes something, add a line and mark the affected sections with `[updated: date]`.
- This gives you the overview without maintaining multiple versions.

When you are lost and don't know what has changed, paste the spec intro Claude and ask:

```
Here is my current master spec for [module]: [paste spec]

I've been iterating with the customer. Help me:
1. Summarize what has been decided vs. still open
2. Find any inconsistencies between sections
3. List what I still need to complete before handing off to devs
```

---

## Figma — where and when

**Do the field map first. Always.** Opening Figma before the field map is the biggest time waster — you design something and then discover a field you forgot.

Once the field map is done:
- Open your Partus library in Figma
- Use Figma Make to generate a first draft (use the field map as your prompt)
- Edit manually to match your library components
- Share the Figma prototype link directly with the customer — no need to export or email

Figma Make prompt formula for medical forms:
```
A form for [module name] in a Norwegian electronic birth journal (Partus).
Used by a midwife at a hospital workstation.
Fields: [paste your field list from the field map section]
Style: clinical, high information density, calm, [your library name].
Show default state and one error state.
```

---

## Files in this docs folder

```
docs/
├── pipeline/
│   └── PIPELINE.md              ← you are here
└── templates/
    ├── master-module-spec.md    ← THE document — copy once per module
    ├── tickets-and-estimates.md ← how to turn a finished spec into Jira tickets
    ├── field-mapping.md         ← detailed reference (already in master spec)
    ├── dev-specs.md             ← detailed reference (already in master spec)
    └── ux-checklist.md          ← detailed reference (already in master spec)
```

The three detailed templates at the bottom are reference material.
In practice, everything lives in the master module spec.
