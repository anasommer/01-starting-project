# UX/UI Review Checklist

> Run this checklist before every design handoff and after every dev build.  
> Medical software standard: aim for zero Critical and High issues before release.

---

## Screen / Feature
**Name:**  
**Review type:** [ ] Design review  [ ] Dev build review  [ ] Both  
**Reviewed by:**  
**Date:**  
**Figma link:**  
**Build link (if applicable):**

**Status:** [ ] Pass — ready for next phase  [ ] Fail — issues logged below

---

## 1. Clinical Workflow Fit

| # | Check | Pass | Fail | Notes |
|---|---|---|---|---|
| 1.1 | Matches the real clinical workflow (verified with a midwife/clinician) | | | |
| 1.2 | Most common task can be completed in ≤3 clicks | | | |
| 1.3 | Critical information is visible without scrolling | | | |
| 1.4 | Emergency/alert information is immediately visible | | | |
| 1.5 | No irreversible actions without confirmation dialog | | | |
| 1.6 | Autosave or draft state prevents data loss | | | |
| 1.7 | Norwegian clinical terminology used (not literal English translations) | | | |

---

## 2. Usability (Nielsen's Heuristics)

| # | Heuristic | Check | Pass | Fail | Notes |
|---|---|---|---|---|---|
| 2.1 | Visibility of system status | User always knows what state the system is in (loading, saved, error) | | | |
| 2.2 | Match with real world | Language and concepts match clinical practice in Norway | | | |
| 2.3 | User control & freedom | Easy undo, back, cancel at every step | | | |
| 2.4 | Consistency & standards | Follows Partus design system and platform conventions | | | |
| 2.5 | Error prevention | Risky actions require confirmation; impossible inputs prevented | | | |
| 2.6 | Recognition over recall | User doesn't have to remember info between screens | | | |
| 2.7 | Flexibility & efficiency | Frequent tasks have shortcuts; power users are not slowed down | | | |
| 2.8 | Aesthetic & minimalist | No irrelevant information competing with clinical data | | | |
| 2.9 | Help users recover from errors | Error messages are specific, human-readable, actionable | | | |
| 2.10 | Help & documentation | Complex workflows have inline help or tooltips | | | |

---

## 3. Accessibility (WCAG 2.1 AA — required for Norwegian health software)

| # | Check | Pass | Fail | Notes |
|---|---|---|---|---|
| 3.1 | Text contrast ≥ 4.5:1 (normal text), ≥ 3:1 (large text, UI components) | | | |
| 3.2 | All interactive elements have visible focus indicator | | | |
| 3.3 | All interactive elements reachable by keyboard only | | | |
| 3.4 | Tab order is logical and matches visual order | | | |
| 3.5 | All images have meaningful alt text (or empty alt for decorative) | | | |
| 3.6 | All form inputs have a visible label (not only placeholder) | | | |
| 3.7 | Error messages are associated with the input field | | | |
| 3.8 | Color is not the only way to convey information (add icon/text) | | | |
| 3.9 | Modals/dialogs trap focus correctly and return focus on close | | | |
| 3.10 | Touch targets ≥ 44×44px (if used on tablet) | | | |
| 3.11 | No content that flashes > 3 times per second | | | |
| 3.12 | Screen reader tested with NVDA or similar (for critical flows) | | | |

---

## 4. Forms & Data Entry

| # | Check | Pass | Fail | Notes |
|---|---|---|---|---|
| 4.1 | Required fields clearly marked | | | |
| 4.2 | Validation fires at the right time (not before user finishes typing) | | | |
| 4.3 | Error messages appear next to the field, not only at top | | | |
| 4.4 | All dropdown options present and in correct Norwegian | | | |
| 4.5 | Clinical ranges validated (warn if abnormal, block if impossible) | | | |
| 4.6 | Date format is dd.mm.yyyy consistently | | | |
| 4.7 | Decimal separator is comma (Norwegian locale) | | | |
| 4.8 | Empty/null states handled gracefully (show "—" or "Ukjent", not blank) | | | |
| 4.9 | Long text fields have visible character count if there is a limit | | | |
| 4.10 | Pre-filled data clearly marked as pre-filled | | | |

---

## 5. Design Consistency

| # | Check | Pass | Fail | Notes |
|---|---|---|---|---|
| 5.1 | All components are from the Partus design library | | | |
| 5.2 | No hardcoded colors (all from design tokens) | | | |
| 5.3 | Typography matches the type scale | | | |
| 5.4 | Spacing uses the spacing scale (not random pixel values) | | | |
| 5.5 | Icons are from the approved icon set | | | |
| 5.6 | Figma Design Lint shows 0 errors | | | |
| 5.7 | All layers are named semantically (no "Frame 247") | | | |
| 5.8 | All interactive states are designed: default, hover, focus, disabled, error | | | |

---

## 6. Responsive & Device

| # | Check | Pass | Fail | Notes |
|---|---|---|---|---|
| 6.1 | Tested at desktop resolution (1280px minimum) | | | |
| 6.2 | Tested at laptop resolution (1024px) | | | |
| 6.3 | Tablet layout reviewed (if used in delivery room on tablet) | | | |
| 6.4 | No horizontal scroll at any breakpoint | | | |
| 6.5 | Long Norwegian text doesn't break layout | | | |

---

## 7. Content & Language

| # | Check | Pass | Fail | Notes |
|---|---|---|---|---|
| 7.1 | All visible text is in Norwegian Bokmål | | | |
| 7.2 | Clinical terminology approved by a clinician | | | |
| 7.3 | No placeholder "Lorem ipsum" or English text left in | | | |
| 7.4 | Confirmation messages are specific ("Registrering lagret" not just "Lagret") | | | |
| 7.5 | Error messages describe what went wrong and what to do | | | |
| 7.6 | Success messages are shown but not intrusive | | | |

---

## 8. Privacy & Data Security (GDPR / Norm for informasjonssikkerhet)

| # | Check | Pass | Fail | Notes |
|---|---|---|---|---|
| 8.1 | Patient-identifiable data is not shown unnecessarily | | | |
| 8.2 | Sensitive fields are masked where appropriate | | | |
| 8.3 | No patient data exposed in URLs | | | |
| 8.4 | Audit log triggers are clear (what actions are logged) | | | |
| 8.5 | Access to sensitive sections requires appropriate role | | | |

---

## Issues Log

| # | Severity | Phase | Description | Screenshot/frame | Assigned to | Status |
|---|---|---|---|---|---|---|
| 1 | Critical / High / Medium / Low | Design / Dev | | | | Open / Fixed |
| 2 | | | | | | |

**Severity guide:**
- `Critical` — Patient safety, data loss, or GDPR risk. Block release.
- `High` — Blocks clinical workflow or fails WCAG AA. Fix before release.
- `Medium` — Friction or inconsistency. Fix before release if possible.
- `Low` — Polish item. Log and fix in next sprint.

---

## Sign-off

| Role | Name | Date | Approved |
|---|---|---|---|
| Designer | | | |
| Dev lead | | | |
| Clinical stakeholder | | | (for Critical/High items) |

---

## Claude Prompt for Assisted Review

```
I am doing a UX/UI review of [screen name] in Partus (Norwegian electronic
birth journal, used by midwives in hospital maternity wards).

[Describe the screen or paste screenshot + description]

Please review using:
1. Nielsen's 10 usability heuristics (adapted for clinical software)
2. WCAG 2.1 AA accessibility (required for Norwegian health software)
3. Medical/clinical UX best practices
4. Norwegian locale requirements (dates, decimals, language)
5. GDPR / patient data privacy considerations

Rate each issue as: Critical (patient safety) / High / Medium / Low
For each issue, suggest a specific fix.
```
