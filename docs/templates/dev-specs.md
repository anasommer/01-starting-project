# Dev Spec Template

> Copy this file for each feature/screen handed off to developers.  
> Filename: `dev-specs-[screen-name].md`  
> Complete after design is approved and field map is signed off.

---

## Feature / Screen
**Name:**  
**Jira ticket:**  
**Figma link:** (frame-specific link, not just file link)  
**Field map:** `docs/templates/field-mapping-[name].md`  
**Designer:** (your name)  
**Dev lead:**  
**Spec created:**  
**Status:** [ ] Draft  [ ] Ready for dev  [ ] In dev  [ ] Done

---

## Summary

One paragraph describing what this feature is, why it exists, and what user problem it solves.

**Affected users:** (Midwife / Doctor / Secretary / All)  
**Clinical workflow context:** (when/where in the patient journey this appears)

---

## Design Assets

| Asset | Link / Location | Notes |
|---|---|---|
| Figma frames | | Include all states |
| Figma prototype | | Clickable flow |
| Icons / illustrations | | Export specs |
| Design tokens | | From Token Studio export |

### Figma Frame Index
| Frame name | URL | Description |
|---|---|---|
| Default state | | |
| Empty state | | |
| Error state | | |
| Loading state | | |
| Success/confirmation | | |
| Mobile / tablet (if applicable) | | |

---

## Component Breakdown

> List every Angular component needed. Specify new vs. reuse from library.

| Component | Status | Parent | Description |
|---|---|---|---|
| `<app-[name]>` | NEW / REUSE / MODIFY | AppComponent | |
| `<app-[name]>` | NEW / REUSE / MODIFY | | |

### New Components Detail

#### `<app-[component-name]>`
**File:** `src/app/[module]/[component]/[component].component.ts`  
**Purpose:**  
**Inputs ([@Input](https://angular.dev/api/core/Input)):**
```typescript
@Input() [name]: [type];  // description
```
**Outputs ([@Output](https://angular.dev/api/core/Output)):**
```typescript
@Output() [name] = new EventEmitter<[type]>(); // description
```
**Internal state:** (describe key state the component manages)

---

## Form & Fields

> Reference the completed field map. Summarize key points for devs here.

**Form type:** Reactive / Template-driven  
**Form group name:** `[formGroupName]`

### Key Validators
```typescript
// Example — expand as needed
this.form = this.fb.group({
  fieldName: ['', [Validators.required, Validators.maxLength(100)]],
  clinicalValue: [null, [Validators.min(0), Validators.max(999)]],
});
```

### Custom Validators Needed
| Validator | Rule | Error key | Error message (NO) |
|---|---|---|---|
| | | | |

---

## API Contract

> List every endpoint this feature touches.

### GET — [description]
```
GET /api/v1/[endpoint]
Query params: [list if any]
```
**Response shape:**
```typescript
interface [ResponseType] {
  // list fields
}
```

### POST / PUT — [description]
```
POST /api/v1/[endpoint]
```
**Request body:**
```typescript
interface [RequestType] {
  // list fields
}
```
**Success response:** `201` / `200` with `[shape]`  
**Error cases:** `400` (validation), `409` (conflict), `403` (permissions)

---

## State Management

**Where is state held:** Component local / Service / NgRx store  
**Service file:** `src/app/[module]/[name].service.ts`  

| State | Type | Initial value | Updated when |
|---|---|---|---|
| | | | |

---

## Routing

| Action | Route | Guard needed |
|---|---|---|
| Navigate to this screen | `/partus/[route]` | AuthGuard |
| Back navigation | | |

---

## Accessibility Requirements

> These are non-negotiable for Norwegian health software.

- [ ] All form inputs have visible labels (not just placeholder)
- [ ] Error messages are associated with inputs via `aria-describedby`
- [ ] All interactive elements reachable by keyboard (Tab order documented below)
- [ ] Color is not the only indicator of state (add icon or text for clinical alerts)
- [ ] Minimum touch target: 44x44px (if used on tablet)
- [ ] Focus is managed on modal open/close
- [ ] WCAG 2.1 AA contrast ratio: 4.5:1 for text, 3:1 for large text and UI

**Tab order:**
1. [First focusable element]
2. [Second]
3. ...

**Screen reader announcements:**
| Trigger | What should be announced |
|---|---|
| Form submit error | "Skjemaet inneholder feil. [N] felt må fylles ut." |
| Successful save | "[Record name] er lagret." |
| Loading state | "Laster inn data..." |

---

## Error Handling

| Scenario | UI behavior | Message to user (NO) |
|---|---|---|
| API timeout | Show retry button | "Noe gikk galt. Prøv igjen." |
| Validation error | Inline error under field | [field-specific] |
| Concurrent edit conflict | Block save, show alert | "Journalen er oppdatert av en annen bruker. Last inn på nytt." |
| No data / empty state | Show empty state illustration | "Ingen registreringer enda." |

---

## Clinical / Business Rules

> Rules that must be implemented, not just validated in the form.

| Rule | Trigger | Action |
|---|---|---|
| | | |

---

## Permissions

| Role | Can view | Can edit | Can delete |
|---|---|---|---|
| Midwife | ✓ | ✓ | |
| Doctor | ✓ | ✓ | |
| Secretary | ✓ | | |
| Read-only | ✓ | | |

---

## Testing Notes

> For QA and dev.

### Happy path
1. [Step by step: what a successful interaction looks like]

### Edge cases to test
- [ ] [Edge case 1]
- [ ] [Edge case 2]

### Data scenarios to test
| Scenario | Test data | Expected result |
|---|---|---|
| | | |

---

## Open Items / Blockers

| # | Item | Owner | Due |
|---|---|---|---|
| 1 | | | |

---

## Claude Code Prompt to Generate Angular Code from This Spec

```
I have a completed dev spec for [screen name] in Partus (Angular 18, Norwegian
electronic birth journal).

Spec summary:
- Components needed: [list]
- Form fields and validators: [paste from spec]
- API endpoints: [paste from spec]
- Accessibility requirements: [paste key ones]

Generate:
1. The Angular standalone component(s) with template
2. The reactive FormGroup with all validators
3. The service with typed HTTP methods
4. TypeScript interfaces for request/response models
5. A stub test file for the main component

Use Angular 18 patterns: standalone components, inject(), signals where appropriate.
No NgRx — use service + BehaviorSubject for now.
Use Norwegian strings for all user-facing text.
```
