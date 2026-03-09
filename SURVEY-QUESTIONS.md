# Survey Questions Reference

**EMS Protocol Format Survey**
Grand County EMS / Foothills RETAC
Qualitative Protocol Format Preference Research

---

## Overview

This document describes every question presented to respondents in the EMS Protocol Format Survey. The survey has four sections:

1. **General Instructions** — displayed once before any questions
2. **Demographics** — 10 questions collected before comparisons begin
3. **Pairwise Comparisons** — 15 forced-choice comparisons of protocol format pairs
4. **Closing Comments** — one open-text field after all comparisons

All demographic responses and comparison choices are submitted automatically to a Google Sheet at the conclusion of the survey. No respondent action is required beyond clicking Submit.

---

## Section 1 — General Instructions

Displayed as a static screen before the demographics section. Respondents cannot skip this screen.

> *Before you begin, please note: You will be comparing six different protocol or guideline formats, all covering the same clinical topic — allergic reaction and anaphylaxis. Each format is shown as a static image.*
>
> *One format uses hyperlinks to access medication dosing information — those links are not functional in this survey. A note will appear when that format is displayed to explain how dosing is normally accessed.*
>
> *You may tap or click any image to enlarge it for closer review. Use the + / − controls or pinch to zoom.*

---

## Section 2 — Demographics

Ten questions collected before comparisons begin. Questions Q1 through Q9 are required. Q10 is optional open text.

---

### Q1 — Years of Experience
**Variable:** `exp_years`
**Type:** Single-select picklist
**Required:** Yes

**Question text:**
> How many total years have you worked or volunteered in EMS?

**Response options:**
- Less than 1 year
- 1–2 years
- 3–4 years
- 5–7 years
- 8–10 years
- 11–15 years
- 16–20 years
- 21 or more years

---

### Q2 — Certification Level
**Variable:** `cert_level`
**Type:** Single-select picklist
**Required:** Yes

**Question text:**
> What is your current EMS certification level?

**Response options:**
- EMT
- AEMT
- Paramedic
- Other
- Non-clinical (e.g., administrator, coordinator, educator)

---

### Q3 — Primary Role
**Variable:** `primary_role`
**Type:** Single-select picklist
**Required:** Yes

**Question text:**
> What best describes your primary role in EMS?

**Response options:**
- Provider
- Supervisor
- Officer
- Medical Director / Physician
- Educator / Training Officer
- Administrator / Coordinator

---

### Q4 — Agency Type
**Variable:** `agency_type`
**Type:** Single-select picklist
**Required:** Yes

**Question text:**
> Select the option that best describes the highest population density area your agency serves.

**Response options:**
- Rural / Frontier (low population density, longer transport times)
- Urban / Suburban (cities and surrounding communities)

---

### Q5 — Response Structure
**Variable:** `response_type`
**Type:** Single-select picklist
**Required:** Yes

**Question text:**
> Which best describes your agency's primary operational model?

**Response options:**
- Fire-based
- Private / Contract Service
- Government / Third-service (standalone EMS, not fire-based)
- Hospital-based
- Other

**Note:** Government / Third-service refers to a dedicated government EMS agency that operates independently from the fire department, such as a county or municipal EMS department. Private / Contract Service covers both for-profit and non-profit agencies operating under contract.

---

### Q6 — Employment Status
**Variable:** `pay_status`
**Type:** Single-select picklist
**Required:** Yes

**Question text:**
> What best describes your employment status? If you work for multiple agencies, answer for the agency where you work the most hours.

**Response options:**
- Paid (career / full-time)
- Paid (part-time)
- Volunteer

---

### Q7 — Agency Call Volume
**Variable:** `call_volume`
**Type:** Single-select picklist
**Required:** Yes

**Question text:**
> Approximately how many EMS calls does your agency respond to per day on average?

**Response options:**
- Less than 1 call per day (fewer than ~150 calls per year)
- 1–2 calls per day (roughly 150–600 calls per year)
- 2–7 calls per day (roughly 600–2,500 calls per year)
- More than 7 calls per day (more than ~2,500 calls per year)

---

### Q8 — Protocol Use — Ranked
**Variables:** `use_rank1`, `use_rank2`, `use_rank3`
**Type:** Select-and-rank — respondent assigns 1st, 2nd, and 3rd to their top three choices from the list using individual dropdowns. Each rank can only be used once.
**Required:** Yes (at least 1st must be selected; 2nd and 3rd are strongly encouraged)

**Question text:**
> How do you primarily use your agency's protocols or guidelines?
> Rank your top 3 from the list below — select 1st, 2nd, and 3rd from the dropdowns. Each rank can only be used once.

**Response options and short codes recorded in data:**

| Option Label | Short Code |
|---|---|
| As preparation before a shift or call type (to review how your medical director has defined treatment; you seek deeper clinical understanding elsewhere) | `prep` |
| As a quick reference during or after a call (to confirm dosing, criteria, or specific steps) | `reference` |
| As a checklist during patient care (to ensure you complete all required steps) | `checklist` |
| As a scope of practice reference (to confirm what you are authorized to do) | `scope` |
| As a comprehensive learning or teaching document (the protocol is your primary source of clinical knowledge, functioning like a textbook) | `learning` |
| As a documentation reference (to support or justify PCR documentation) | `documentation` |
| As a teaching tool when training or precepting others (using the protocol as the basis for instruction) | `precepting` |

**Data recorded:** The short code of the option ranked 1st is stored in `use_rank1`, 2nd in `use_rank2`, 3rd in `use_rank3`. Unranked options are not recorded.

---

### Q9 — Protocol Reference Frequency
**Variable:** `protocol_frequency`
**Type:** Single-select picklist
**Required:** Yes

**Question text:**
> How often do you reference your agency's protocols or guidelines?

**Response options:**
- Daily or almost daily
- Weekly
- Monthly
- A few times per year
- Rarely or never

---

### Q10 — Protocol Use — Open Text
**Variable:** `use_other`
**Type:** Open text
**Required:** No

**Question text:**
> Is there anything about how you use your protocols or guidelines that isn't captured above?

---

## Section 3 — Pairwise Comparisons

Respondents complete 15 forced-choice comparisons — one for each unique pairing of the six protocol formats. Pair order is fixed but left/right display position of each format is randomized per respondent to reduce positional bias.

For each comparison, respondents may:
- Tap or click any image to enlarge it (zoom in/out supported)
- Scroll through multi-page protocols within the panel
- Leave an optional comment explaining their choice
- Navigate back to a previous pair to change their selection

Progress is shown throughout (e.g., "Comparison 3 of 15").

---

### Protocol Formats

| Format ID | Display Label | Pages |
|---|---|---|
| `format-01_linear-algorithm` | Linear Algorithm | 1 |
| `format-02_column-algorithm` | Column Algorithm | 2 |
| `format-03_narrative-outline` | Narrative Outline | 2 |
| `format-04_structured-outline` | Structured Outline | 2 |
| `format-05_narrative-reference` | Narrative Reference | 5 |
| `format-06_colorcoded-sidebar` | Color-Coded Sidebar | 4 |

All formats display the same clinical topic: **Allergic Reaction / Anaphylaxis**.

---

### Comparison Pairs

All 15 pairs are hardcoded. The table below shows the fixed pairing; left/right display order is randomized per respondent.

| Pair | Format A | Format B |
|---|---|---|
| 01 | Linear Algorithm | Column Algorithm |
| 02 | Linear Algorithm | Narrative Outline |
| 03 | Linear Algorithm | Structured Outline |
| 04 | Linear Algorithm | Narrative Reference |
| 05 | Linear Algorithm | Color-Coded Sidebar |
| 06 | Column Algorithm | Narrative Outline |
| 07 | Column Algorithm | Structured Outline |
| 08 | Column Algorithm | Narrative Reference |
| 09 | Column Algorithm | Color-Coded Sidebar |
| 10 | Narrative Outline | Structured Outline |
| 11 | Narrative Outline | Narrative Reference |
| 12 | Narrative Outline | Color-Coded Sidebar |
| 13 | Structured Outline | Narrative Reference |
| 14 | Structured Outline | Color-Coded Sidebar |
| 15 | Narrative Reference | Color-Coded Sidebar |

---

### Data Recorded Per Pair

| Variable | Description |
|---|---|
| `pair_XX_formatA` | Display label of the left-side format |
| `pair_XX_formatB` | Display label of the right-side format |
| `pair_XX_formatA_key` | File identifier of the left-side format |
| `pair_XX_formatB_key` | File identifier of the right-side format |
| `pair_XX_chosen` | Display label of the chosen format |
| `pair_XX_chosen_key` | File identifier of the chosen format |
| `pair_XX_comment` | Optional free-text comment explaining the choice |

---

### Per-Pair Comment Field

**Type:** Open text, optional
**Prompt displayed to respondent:**
> What influenced your choice for this comparison? (format, layout, readability, usability…)

---

## Section 4 — Closing Comments

Displayed after all 15 comparisons are complete, before the Submit button.

**Variable:** `closing_comments`
**Type:** Open text
**Required:** No

**Question text:**
> Based on the protocols presented, do you have any additional information to add?

---

## Data Collected Per Submission

The following fields are written to the Google Sheet for each completed submission:

| Field | Source |
|---|---|
| `respondentId` | Auto-generated unique ID per session |
| `timestamp` | ISO 8601 timestamp of submission |
| `deviceType` | Auto-detected: mobile, tablet, or desktop |
| `screenWidth` | Browser screen width in pixels |
| `exp_years` | Q1 |
| `cert_level` | Q2 |
| `primary_role` | Q3 |
| `agency_type` | Q4 |
| `response_type` | Q5 |
| `pay_status` | Q6 |
| `call_volume` | Q7 |
| `use_rank1` | Q8 — 1st ranked protocol use |
| `use_rank2` | Q8 — 2nd ranked protocol use |
| `use_rank3` | Q8 — 3rd ranked protocol use |
| `protocol_frequency` | Q9 |
| `use_other` | Q10 |
| `closing_comments` | Section 4 closing field |
| `totalPairs` | Always 15 |
| `pair_01` through `pair_15` | All comparison data (7 fields each) |
| `rank_[FormatLabel]` | Final win-count rank for each of the 6 formats |

---

## Ranking Method

At the end of the survey, each format's rank is calculated by counting the number of head-to-head comparisons it won. The format with the most wins ranks first. This win-count (Condorcet-style) method is appropriate for ordinal preference research and is consistent with standard pairwise comparison methodology used in health services and usability research.

Each format competes in 5 comparisons (once against each of the other 5 formats). Maximum possible wins per format: 5.

---

*Developed for Grand County EMS / Foothills RETAC qualitative protocol format research.*
*Clinical topic used in all format examples: Allergic Reaction / Anaphylaxis.*
