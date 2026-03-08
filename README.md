# ems-protocol-format-survey

This tool supports qualitative research into EMS protocol format preferences among prehospital providers. Respondents view two protocol formats side by side and select which they find more usable, readable, or preferable — repeated across all possible pairs. Choices are tallied using a win-count method to produce a final preference ranking. Responses are submitted automatically to a Google Sheet via Google Apps Script. Designed for zero-cost deployment on GitHub Pages.

---

## Table of Contents

- [How It Works](#how-it-works)
- [Repository Structure](#repository-structure)
- [Adding or Updating Protocols](#adding-or-updating-protocols)
- [Protocol File Naming Convention](#protocol-file-naming-convention)
- [Google Sheets & Apps Script Setup](#google-sheets--apps-script-setup)
- [Deploying to GitHub Pages](#deploying-to-github-pages)
- [Sharing the Survey](#sharing-the-survey)
- [Analyzing Results in Google Sheets](#analyzing-results-in-google-sheets)
- [Ranking Method](#ranking-method)
- [Researcher Notes](#researcher-notes)

---

## How It Works

The survey uses a **forced-choice pairwise comparison** design. Each protocol format is shown alongside every other format exactly once. The respondent chooses which format they prefer. At the end, the tool calculates a ranking based on the number of head-to-head wins each format accumulated.

With **N** protocol formats, respondents complete **N × (N − 1) / 2** comparisons:

| Formats | Pairs |
|---------|-------|
| 3 | 3 |
| 4 | 6 |
| 5 | 10 |
| 6 | 15 |

Pair order is randomized for each respondent to reduce order bias.

When a respondent submits, their responses are sent automatically to a Google Sheet via Google Apps Script. No action is required from the respondent after submission. The researcher accesses all responses directly in Google Sheets.

---

## Repository Structure

```
ems-protocol-format-survey/
├── index.html              ← Survey application (single file, no dependencies)
├── README.md               ← This file
└── protocols/
    ├── format-01_algorithmic-flowchart_p01.png
    ├── format-01_algorithmic-flowchart_p02.png
    ├── format-02_text-narrative_p01.png
    ├── format-03_decision-table_p01.png
    └── ...
```

All protocol images live in the `protocols/` folder. The survey HTML references them by relative path and requires no server-side code.

---

## Protocol File Naming Convention

Use this naming pattern for all protocol image files:

```
format-##_description-slug_p##.png
```

**Examples:**

```
format-01_algorithmic-flowchart_p01.png
format-01_algorithmic-flowchart_p02.png
format-02_text-narrative_p01.png
format-03_decision-table_p01.png
format-03_decision-table_p02.png
format-03_decision-table_p03.png
```

**Rules:**
- `format-##` — two-digit zero-padded number; keeps files sorted in file explorers and maps directly to protocol slots in the HTML
- `description-slug` — lowercase, hyphen-separated, human-readable label; used during development and version control review
- `_p##` — two-digit zero-padded page number; required for multi-page protocols; single-page protocols still use `_p01`
- Extension: always `.png` (preferred) or `.jpg`
- No spaces, no special characters, no uppercase

---

## Adding or Updating Protocols

### Preparing Image Files

Convert all protocol documents to **PNG images** before adding them to this repository. Do not use PDF files directly in the deployed version — images render faster, work on all mobile browsers, and embed cleanly.

**Recommended conversion tools (all free):**
- **Adobe Acrobat Reader** (Windows/Mac): File → Export To → Image → PNG
- **Preview** (Mac): Open PDF → File → Export → PNG
- **ImageMagick** (command line): `magick convert -density 150 protocol.pdf format-01_name_p%02d.png`
- **Snagit** or any screenshot tool: capture each page at high resolution (150 dpi minimum)

**Image quality guidelines:**
- Resolution: 150 dpi minimum; 200 dpi recommended for readability
- Width: 1200–1700 pixels wide produces good results at survey display size
- Format: PNG preferred; JPG acceptable at quality 85 or higher
- Do not compress aggressively — respondents need to read the protocol content

### Adding Files to the Repository

1. Place new image files in the `protocols/` folder following the naming convention above
2. Open `index.html` in a text editor
3. Locate the `PROTOCOL CONFIGURATION` section near the top of the `<script>` block
4. Update the `protocols` array with the new format names and file paths (see inline comments in the HTML)
5. Commit and push — GitHub Pages updates automatically within 1–2 minutes

### Removing or Replacing a Protocol

1. Delete or replace the image files in `protocols/`
2. Update the `protocols` array in `index.html` to match
3. Commit and push

---

## Google Sheets & Apps Script Setup

This is a one-time setup that connects the survey to your Google Sheet.

### What You Need
- A Google account
- The `Code.gs` script (contents provided separately)
- The deployed Apps Script Web App URL hard-coded into `index.html`

### Steps

1. Go to [sheets.google.com](https://sheets.google.com) → create a new sheet named **EMS Protocol Survey**
2. Click **Extensions → Apps Script**
3. In the editor, delete all existing code in `Code.gs` → paste the contents of the provided Apps Script code
4. Click **Save**
5. Click **Deploy → New deployment**
   - Type: **Web app**
   - Description: EMS Protocol Survey
   - Execute as: **Me**
   - Who has access: **Anyone**
   - Click **Deploy** → authorize when prompted
6. Copy the Web App URL
7. Open `index.html` in a text editor → find the line `let APPS_SCRIPT_URL = ''` → paste the URL between the quotes
8. Save and upload the updated `index.html` to GitHub

**Important:** After any code change to `Code.gs`, always create a **New deployment** rather than updating the existing one, to ensure the latest code is live.

### What Gets Recorded Per Respondent

Each submission writes one row to the Google Sheet containing: Respondent ID, timestamp, all four demographic fields, every pairwise choice and optional comment, and a final rank for each protocol format.

---

## Deploying to GitHub Pages

### First-Time Setup

1. **Create a GitHub account** at [github.com](https://github.com) if you do not have one (free)
2. **Create a new repository** named `ems-protocol-format-survey`
   - Set visibility to **Public**
   - Do not initialize with a README (you will upload this one)
3. **Upload files:**
   - Click **Add file → Upload files**
   - Upload `index.html` and `README.md`
   - Create the `protocols/` folder by uploading at least one image with the path `protocols/your-file.png`
4. **Enable GitHub Pages:**
   - Go to **Settings → Pages**
   - Under *Source*, select **Deploy from a branch**
   - Select branch: `main`, folder: `/ (root)`
   - Click **Save**
5. After 1–2 minutes, your survey is live at:
   `https://YOUR-USERNAME.github.io/ems-protocol-format-survey/`

### Updating After Initial Deployment

Upload changed files directly through the GitHub web interface, or use the GitHub Desktop app (free, no command line required) for bulk file management. Changes go live within 1–2 minutes of each commit.

---

## Sharing the Survey

Share the GitHub Pages URL directly with respondents. No login is required. The survey runs entirely in the respondent's browser.

**Recommended distribution language:**

> This survey is part of a research study on EMS protocol format preferences. It will take approximately 10–15 minutes. You will view pairs of protocol formats and select which you find more usable or readable. Your responses are submitted automatically — no download or email is required. Your responses are anonymous.

**Note:** Responses are transmitted automatically to a secure Google Sheet when the respondent clicks Submit. No action is required from the respondent after that point.

---

## Analyzing Results in Google Sheets

All responses are collected automatically in your Google Sheet — one row per respondent. No aggregation of separate files is needed.

### Sheet Structure

Each row contains: Respondent ID, timestamp (Mountain Time), demographics (4 fields), every pairwise choice and optional comment in individual columns, and a final rank for each protocol format.

### Calculating Group-Level Rankings

Use a **COUNTIF** formula to count total wins for each protocol across all respondents. The chosen protocol name is recorded in each `Pair#_Chosen` column:

```
=COUNTIF(C:ZZ, "Protocol Name Here")
```

Run this for each protocol format to get aggregate win counts, then rank by total wins descending.

### Analyzing Comments

The `Pair#_Comment` columns contain optional free-text rationale for each choice. These are suitable for qualitative thematic coding alongside the quantitative rankings.

### Analyzing by Demographic Subgroup

Filter or use pivot tables on the `CertificationLevel`, `AgencyType`, or `ResponseType` columns to compare rankings across subgroups — for example, paramedics vs. EMTs, or rural vs. urban agencies.

---

## Ranking Method

Rankings are calculated using a **win-count (Condorcet-style)** method. Each protocol receives one point for every head-to-head comparison in which it was chosen. The protocol with the most wins ranks first.

In the case of a tie in win count, tied protocols should be considered equivalent in the respondent's preference for that session. Across aggregated data, ties at the individual level typically resolve when group totals are summed.

This method is appropriate for ordinal preference research and is consistent with standard pairwise comparison methodology used in health services and usability research.

---

## Researcher Notes

- **IRB / research ethics:** Verify whether your institution requires IRB review for this type of anonymous provider survey before distributing.
- **Sample size:** For qualitative preference research, 15–30 respondents per subgroup of interest is generally sufficient to identify consistent patterns.
- **Pair randomization:** Pair order is randomized per respondent session to reduce primacy and recency bias. Protocol left/right position is not currently randomized; consider this a limitation if positional bias is a concern.
- **Mobile compatibility:** The survey is functional on mobile devices but the side-by-side comparison layout is best experienced on a tablet or desktop. Consider noting this in your distribution message.
- **Protocol content neutrality:** Ensure that protocol images shown to respondents represent realistic but de-identified or fictional clinical content to prevent content-driven preferences from confounding format-driven preferences.

---

*Developed for Grand County EMS / Foothills RETAC qualitative protocol format research.*
