# Universal Design & Dev Pipeline — Partus / Medical UI Projects

> For: Midwife + Frontend Dev at a Norwegian medical software company  
> Stack: Angular · Figma · Claude (Chat / Projects / Code) · Jira

---

## The 6-Phase Pipeline

```
[1] DISCOVER  →  [2] DESIGN  →  [3] MAP FIELDS  →  [4] PROTOTYPE  →  [5] SPEC  →  [6] REVIEW
  Jira/stories     Figma Make       Field list        Live prototype    Dev handoff    UX audit
  + Claude Chat    + guidelines     + validation       Figma links       template       checklist
```

Each phase has a Claude mode and a Figma mode. Use them together, not separately.

---

## Phase 1 — Discover (Jira ticket → shared understanding)

**Your inputs:** Jira ticket, user story from clinician/midwife, screenshot of old screen

**Claude Chat — what to paste in:**
```
Context: I work on Partus, an electronic pregnancy and birth journal used by
Norwegian clinics. I am a midwife and frontend dev.

Ticket: [paste Jira ticket or user story]
Old screen: [paste screenshot or describe it]

Help me:
1. Rewrite this as a clear UX problem statement
2. List all edge cases specific to clinical use
3. Identify what data fields are involved
4. Flag any Norwegian health regulation concerns (GDPR, Norm for informasjonssikkerhet)
5. Suggest 2-3 UX approaches
```

**Figma:** Open your company library. Note which existing components apply.

**Output of this phase:**
- Problem statement (1-2 sentences)
- List of affected data fields (seed for Phase 3)
- Component audit (what exists vs. what needs creating)

---

## Phase 2 — Design (Figma Make → refine → guideline check)

### Step 2a — Generate with Figma Make
Prompt formula:
```
[Screen name] for a medical birth journal app used by Norwegian midwives.
Clinic: hospital maternity ward. User: midwife at a computer workstation.
Style: [your company library name, e.g. "Partus Design System"].
Show: [specific fields from Phase 1 output].
Tone: clinical, calm, high information density, high contrast.
```

### Step 2b — Refine with Claude Chat
After screenshotting the Figma Make output:
```
Here is a Figma Make output for [screen name] in Partus.
Our design guidelines say: [paste key rules from your Figma library]
Issues I already see: [list them]

Review for:
- Consistency with medical software UX conventions
- Norwegian language/locale concerns (dates dd.mm.yyyy, decimal commas)
- Accessibility (WCAG 2.1 AA — required for Norwegian health software)
- Clinical workflow fit: midwife needs [specific task] done in under N clicks
- Missing fields from this list: [paste field list]
```

### Step 2c — Edit manually in Figma
Focus edits on:
- Swap generated components for your actual library components
- Fix any spacing/grid drift
- Apply correct typography tokens
- Add real Norwegian clinical labels (not English placeholders)

### Figma plugins for this phase:
| Plugin | Use |
|---|---|
| **Design Lint** | Auto-check against your library before handing off |
| **Contrast** / **A11y Annotation Kit** | WCAG check — critical for health software |
| **Similayer** | Select all layers of same type to batch-rename |
| **Token Studio** | Apply your design tokens consistently |
| **Iconify** | Find clinical icons (heart rate, calendar, etc.) |
| **Content Reel** | Fill with realistic Norwegian names, dates, values |

---

## Phase 3 — Map Fields (the most critical phase for medical software)

> Every input, display value, dropdown, and calculation must be documented
> before a single component is built. Clinical errors trace back to field gaps.

**Use the template:** `docs/templates/field-mapping.md`

**Claude Chat prompt to bootstrap the field map:**
```
I am designing [screen name] in Partus (birth journal, Norwegian clinics).
From the design and Jira ticket, I identified these fields: [paste list]

For each field, help me document:
- Field type (text, number, date, dropdown, radio, checkbox, calculated)
- If dropdown: all options with Norwegian labels + codes
- Validation rules (required, min/max, regex, clinical range)
- Data source (manual entry / sync from [system] / calculated from [fields])
- Where this value writes to (which module/table/FHIR resource)
- Edge cases (null handling, unknown, refused, not applicable)
```

**Claude Code prompt when the map is done:**
```
Here is the field map for [screen name]: [paste table]
I am building this in Angular 18 with reactive forms.
Generate:
1. The FormGroup definition with all validators
2. A reusable validation service for the clinical range rules
3. TypeScript interfaces for the data model
```

---

## Phase 4 — Prototype (live, showable to customers)

### Option A — Figma native prototype (fastest)
- Connect frames with interactions in Figma
- Use "Overlay" for modals/dialogs
- Use variables for dropdown state
- Share with: Present link (view only) → paste in Jira ticket or email to clinician

**Claude Chat prompt for prototype planning:**
```
I need to prototype [flow name] for a Norwegian midwife.
The flow covers: [paste steps]
Key interactions: [list them]
What Figma prototype connections do I need? List frame-by-frame.
```

### Option B — Anima plugin (HTML/CSS live preview)
- For stakeholders who want to click through in a browser
- Generates basic HTML from your Figma frame
- Good for simple read-only reviews, not for complex form logic

### Option C — Angular prototype (when you need real form logic)
Ask Claude Code:
```
Here is my Figma design for [screen] and my field map: [paste both]
Generate an Angular standalone component with:
- The complete template matching the layout
- Reactive form with all validations from the field map
- Mock data service returning [paste example data]
- No backend calls, just local state
This is a prototype only — correctness over completeness.
```

---

## Phase 5 — Dev Specs (handoff to devs)

**Use the template:** `docs/templates/dev-specs.md`

### Figma Dev Mode
Before handing off:
1. Run Design Lint — fix all errors
2. Check every layer has a semantic name (not "Frame 247")
3. Add annotation layer with: field names, states (default/error/disabled), notes
4. Mark components as "Ready for dev" in Figma status

### Claude Code prompt for spec generation:
```
Here is my completed Figma design for [screen], my field map, and the
component inventory:

[paste Figma frame description or component list]
[paste field map]

Generate the dev spec in this format:
- Component breakdown (which Angular components to create/reuse)
- Props/inputs for each component
- API contract (what endpoints are needed, request/response shapes)
- State management notes
- Angular routing changes needed
- Accessibility requirements
```

### Figma plugins for this phase:
| Plugin | Use |
|---|---|
| **Zeplin** or **Figma Dev Mode** | CSS, spacing, asset export |
| **Measure** | Auto-generate spacing annotations |
| **Figma Tokens (Token Studio)** | Export tokens as CSS/JSON for devs |
| **Autoflow** | Generate user flow diagrams for spec doc |

---

## Phase 6 — UX/UI Review & QA

**Use the template:** `docs/templates/ux-checklist.md`

**Claude Chat prompt for heuristic review:**
```
Review this design [describe or paste screenshot] against Nielsen's 10 heuristics
adapted for medical software. Additional context:
- Norwegian clinical setting, hospital maternity ward
- Primary user: midwife under time pressure
- Data is patient-sensitive (GDPR, Norwegian health law)
- Must work on: [desktop / tablet / specific device]
Flag issues as: Critical (patient safety) / High (workflow blocker) / Medium / Low
```

**Claude Chat prompt for accessibility audit:**
```
Review this design for WCAG 2.1 AA compliance.
Pay special attention to:
- Color contrast (especially for status indicators — red/green for clinical alerts)
- Focus order for keyboard navigation
- Form labels and error messages in Norwegian
- Touch target sizes (if used on tablet in clinical setting)
```

---

## Claude Modes — When to Use What

| Mode | Best for | Example |
|---|---|---|
| **Claude Chat** | Brainstorming, UX analysis, writing copy, reviewing designs | "Review my field map for gaps" |
| **Claude Projects** | Maintaining context across sessions for one project | Create a Project for Partus, add your guidelines, field maps, and design decisions as files |
| **Claude Code** | Generating Angular components, form validators, interfaces | "Generate the reactive form for this field map" |

### Setting up a Claude Project for Partus:
1. Create a new Project in Claude called "Partus"
2. Upload as project files:
   - Your company UI design guidelines (PDF or paste key rules)
   - Your completed field maps
   - Your component inventory
   - Key architectural decisions
3. Every new conversation in this Project has full context automatically

---

## Quick Reference — Prompts by Situation

| Situation | Where | Prompt start |
|---|---|---|
| New Jira ticket | Claude Chat | "I have a new Jira ticket for Partus. Context: [guidelines]. Ticket: ..." |
| Old screen to refactor | Claude Chat | "Here is a screenshot of the old Partus screen for [X]. Help me identify UX problems and plan a refactor..." |
| Generate component | Claude Code | "Generate an Angular 18 standalone component for [X] matching this Figma design and field map..." |
| Figma Make review | Claude Chat | "Review this Figma Make output against our design guidelines..." |
| Write user story | Claude Chat | "Write a user story for a Norwegian midwife needing to [task] in Partus..." |
| Check field map | Claude Chat | "Review this field map for [screen]. Flag missing validations or edge cases for clinical use..." |
| Generate dev spec | Claude Code | "Generate a dev spec for [screen] based on this field map and component list..." |

---

## Files in This Docs Folder

```
docs/
├── pipeline/
│   └── PIPELINE.md          ← you are here (the hub)
└── templates/
    ├── field-mapping.md     ← copy per screen, fill in
    ├── dev-specs.md         ← copy per feature, fill in
    └── ux-checklist.md      ← run before every handoff
```
