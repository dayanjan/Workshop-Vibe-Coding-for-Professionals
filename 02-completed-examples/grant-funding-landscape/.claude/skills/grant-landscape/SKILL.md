---
name: grant-landscape
description: Analyze federal health research funding using NIH Reporter API. Use when asked about grants, funding trends, research opportunities, or investigator strategy for Virginia institutions.
allowed-tools: Read, Write, Bash, Grep, Glob
---

# Grant Funding Landscape Analysis

Follow these steps when analyzing NIH funding for Virginia institutions.

## Step 1: Query NIH Reporter

Query the NIH Reporter API at `https://api.reporter.nih.gov/v2/projects/search` (POST) for Virginia institutions across the last 3 fiscal years (FY2023, FY2024, FY2025).

Request body structure:
```json
{
  "criteria": {
    "org_states": ["VA"],
    "fiscal_years": [2025],
    "include_active_projects": true
  },
  "offset": 0,
  "limit": 500
}
```

Target institutions include University of Virginia, Virginia Commonwealth University, Virginia Tech, Inova Health System, Eastern Virginia Medical School, and George Mason University.

## Step 2: Handle Pagination and Sub-Querying

Each response returns up to 500 results. Use the `meta.total` field to determine how many pages to fetch. Loop with increasing `offset` values (0, 500, 1000, ...).

If `meta.total` exceeds 10,000 for any query, split into sub-queries by:
- Individual fiscal years
- Specific NIH institutes (e.g., NHLBI, NCI, NIMH, NIAID, NIGMS)
- Activity codes (R01, R21, K08, K23, T32, P30, P50, U01)

Save raw JSON responses to `data/raw/` with filenames like `va_fy2025_page1.json`.

## Step 3: Aggregate by Institution and NIH Institute

Build a consolidated DataFrame with columns:
- `project_num`, `fiscal_year`, `org_name`, `pi_name`, `project_title`
- `abstract_text`, `award_amount`, `activity_code`, `ic_name`
- `project_start_date`, `project_end_date`, `foa_number`

Normalize institution names (map variants to canonical names). Aggregate total and median award amounts by institution and by NIH institute (NHLBI, NCI, NIMH, NIAID, NIGMS, NIDDK, NICHD, NINDS, NEI, NIDA, etc.).

Save processed data to `data/processed/va_grants_consolidated.csv`.

## Step 4: Keyword Frequency Analysis

Extract the top 50 terms from project titles and abstracts using TF-IDF or simple frequency counts. Remove standard stopwords and common grant boilerplate terms (e.g., "study," "research," "project," "aim," "propose").

Group keyword frequencies by NIH institute to reveal topic clustering. Save keyword table to `data/processed/keyword_frequencies.csv`.

## Step 5: Visualizations

Generate and save to `figures/`:

1. **Institution bar chart** (`institution_funding.png`): Total award dollars by institution, stacked or grouped by fiscal year. Use plotly for interactive HTML version.

2. **NIH institute chart** (`nih_institute_breakdown.png`): Award counts and total dollars by NIH institute for Virginia as a whole. Horizontal bar chart sorted by total funding.

3. **Keyword cloud** (`keyword_cloud.png`): Word cloud from title/abstract terms, sized by frequency. Use matplotlib and wordcloud library. Generate separate clouds per top-funded NIH institute if requested.

4. **Trend lines** (`funding_trends.html`): Interactive plotly line chart showing funding over fiscal years by institution or institute.

## Step 6: Strategic Summary

Write a narrative report to `reports/funding_landscape_summary.md` that includes:

- Total funding flowing to Virginia institutions and year-over-year change
- Top-funded institutions and their primary NIH institute partners
- Emerging keyword themes that signal growing research areas
- Gaps: NIH institutes with low Virginia representation relative to national averages
- Opportunity areas: FOAs with few Virginia applicants, growing mechanism types
- Recommendations for investigators at different career stages (early, mid, senior)

## Quality Checks

- Verify that all referenced FOA numbers are current (not expired) by checking dates
- Match awards to correct mechanisms: R01 (research), R21 (exploratory), K08/K23 (career development), T32 (training), P30/P50 (center), U01 (cooperative agreement)
- Flag eligibility constraints (new investigator, ESI status, specific institution types)
- Cross-check total counts against NIH Reporter web interface for at least one institution-year pair
- Always note the data retrieval date and fiscal years covered
