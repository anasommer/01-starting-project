# Field Mapping Template

> Copy this file for each screen or feature. Filename: `field-mapping-[screen-name].md`  
> Fill in before design is finalized. Review with dev before handoff.

---

## Screen / Feature
**Name:**  
**Jira ticket:**  
**Module in Partus:**  
**Last updated:**  
**Status:** [ ] Draft  [ ] In Review  [ ] Approved

---

## Overview
Brief description of what this screen does and who uses it.

**Primary user:** (e.g. Midwife, Doctor, Secretary)  
**Clinical context:** (e.g. During active labor, At admission, Post-delivery)  
**Key workflow:** (what the user is trying to accomplish)

---

## Field Map

> Legend for Source/Destination:
> - `MANUAL` = user enters directly
> - `CALC` = calculated from other fields (list which)
> - `SYNC:[system]` = synced from/to another system (e.g. SYNC:DIPS, SYNC:HIS, SYNC:FHIR)
> - `READ-ONLY` = displayed only, not editable
> - `PREFILL:[source]` = pre-filled but editable

| # | Field Label (NO) | Field Label (EN) | Type | Required | Options / Range | Validation | Source | Writes To | Notes |
|---|---|---|---|---|---|---|---|---|---|
| 1 | | | | | | | | | |
| 2 | | | | | | | | | |
| 3 | | | | | | | | | |

### Field Types Reference
`text` `textarea` `number` `decimal` `date` `time` `datetime` `dropdown` `multi-select` `radio` `checkbox` `toggle` `calculated` `read-only` `file-upload`

---

## Dropdown Options Detail

> For every dropdown/radio/multi-select field above, list all options here.

### Field: [Field name]
| Code | Norwegian label | English label | Notes |
|---|---|---|---|
| | | | |

### Field: [Field name]
| Code | Norwegian label | English label | Notes |
|---|---|---|---|
| | | | |

---

## Validation Rules

> List clinical validation rules that go beyond "required" or "max length".

| Field | Rule | Error message (NO) | Severity |
|---|---|---|---|
| | | | Warning / Error / Block |
| | | | Warning / Error / Block |

**Severity levels:**
- `Block` — Cannot save/proceed (e.g. impossible clinical value)
- `Error` — Must fix before submit (e.g. required field)
- `Warning` — Can proceed but shown alert (e.g. value outside normal range, confirm?)

### Clinical Range Rules
> Document normal ranges and alert thresholds for numeric clinical fields.

| Field | Normal range | Alert threshold | Action on alert |
|---|---|---|---|
| | | | |

---

## Data Sources & Integrations

| Field | Source system | Sync direction | Sync trigger | Notes |
|---|---|---|---|---|
| | | IN / OUT / BOTH | On save / Real-time / Manual | |

---

## States & Edge Cases

| Field | State | Behavior |
|---|---|---|
| [field] | Empty / null | Show placeholder or dash |
| [field] | Not applicable (N/A) | Hide field or show "Ikke aktuelt" |
| [field] | Unknown / not recorded | Show "Ukjent" option |
| [field] | Refused by patient | Show "Pasient ønsker ikke å oppgi" |

---

## Calculated Fields

> For each calculated field, document the exact formula.

### [Calculated field name]
**Formula:** `[formula or plain language description]`  
**Inputs:** `[field A]`, `[field B]`  
**Output type:** number / date / text  
**Edge case (null input):** [what happens if one input is missing]

---

## Locale & Formatting

| Field | Format | Example |
|---|---|---|
| All dates | dd.mm.yyyy | 14.03.2025 |
| All times | HH:mm | 09:30 |
| All decimals | Comma separator | 3,5 kg |
| Phone numbers | Norwegian format | +47 123 45 678 |

---

## Accessibility Notes

| Field | Note |
|---|---|
| | ARIA label needed if icon-only |
| | Error message must be announced by screen reader |
| | Color-only status needs text alternative |

---

## Open Questions

| # | Question | Owner | Status |
|---|---|---|---|
| 1 | | | Open / Answered |
| 2 | | | Open / Answered |

---

## Claude Prompt to Fill This Template

```
I am filling in the field mapping template for [screen name] in Partus
(Norwegian electronic birth journal, used by midwives in hospital clinics).

Here is what I know so far:
- Jira ticket summary: [paste]
- Old screen description: [describe or paste screenshot]
- Fields I've identified so far: [list]

Help me complete the field map. For each field, suggest:
1. Norwegian and English labels
2. Field type
3. Whether it should be required
4. Any dropdown options (use Norwegian clinical terminology)
5. Validation rules and clinical ranges
6. Most likely data source (manual entry, or common Norwegian health systems: DIPS, Helseplattformen, FHIR R4)
7. Any edge cases relevant to obstetrics/maternity care

Flag anything you are unsure about so I can verify with clinical staff.
```
