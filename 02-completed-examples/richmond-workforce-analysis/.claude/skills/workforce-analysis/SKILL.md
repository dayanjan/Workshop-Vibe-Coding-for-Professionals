---
name: workforce-analysis
description: Analyze Richmond MSA workforce data from BLS public APIs. Use when asked about employment trends, industry growth, wage data, or economic development for the Richmond area.
allowed-tools: Read, Write, Bash, Grep, Glob
---

# Workforce Analysis Workflow

Follow these steps when asked to analyze Richmond-area employment or industry data.

## Step 1: Download QCEW Data

Pull Quarterly Census of Employment and Wages data for the Richmond MSA (FIPS 40060) covering
at least the most recent 3 years available. Use the BLS open-data flat files or API endpoints
documented at https://www.bls.gov/cew/additional-resources/open-data/.

- Download annual average files for each year.
- Save untouched files to `data/raw/` with names like `qcew_40060_2023.csv`.
- Log the download date and URL in a comment at the top of any processing script.

**Note:** The BLS restructured MSA file organization in December 2025. Verify the current
file layout before constructing download URLs for 2025-Q4+ data.

## Step 2: Calculate Year-over-Year Employment Change

- Load raw files into pandas DataFrames.
- Filter to the Richmond MSA (area_fips 40060) and desired ownership code (typically 0 for all).
- Group by 2-digit NAICS industry code.
- Calculate year-over-year absolute and percentage change in average monthly employment.
- Save the merged, calculated DataFrame to `data/processed/richmond_employment_change.csv`.

## Step 3: Identify Top Growing and Declining Industries

- Rank industries by percentage employment change over the full time window.
- Extract the top 10 growing and top 10 declining industries.
- Flag any industries with data suppression (disclosure codes) — note these in output.
- Cross-reference NAICS codes with sector names for readable labels.

## Step 4: Generate Visualizations

Create at minimum two charts:

1. **Horizontal bar chart** of year-over-year employment growth rates for the top 10
   growing and top 10 declining industries. Use green for growth, red for decline.
   Include a title, axis labels, and a source citation line at the bottom.

2. **Treemap** of current industry composition by employment share. Size rectangles
   by total employment, color by growth rate. Use plotly for interactivity.

Save static versions as PNG to `figures/` (e.g., `figures/growth_rates_bar.png`,
`figures/industry_treemap.png`). Save interactive HTML versions alongside if using plotly.

## Step 5: Write Narrative Summary

Write a 1-2 page summary in `reports/richmond_workforce_summary.md` that includes:

- An executive summary paragraph with the headline finding.
- A table of the top 5 growing and top 5 declining industries with numbers.
- Context: how Richmond compares to national trends for the same period.
- Caveats about data suppression, seasonal adjustment, or revision status.
- Full source citation: "Source: Bureau of Labor Statistics, Quarterly Census of
  Employment and Wages, [date range], Richmond MSA (FIPS 40060). Retrieved [date]."

## Quality Standards

- **National comparison:** Where possible, note whether Richmond's trends diverge from
  or mirror national patterns. Pull national totals from the same QCEW dataset.
- **Data suppression:** If BLS suppresses values for confidentiality, flag those
  industries clearly rather than silently dropping them.
- **Plain language:** Write for a policy audience. Avoid jargon. Define acronyms on
  first use (e.g., "NAICS — North American Industry Classification System").
- **Reproducibility:** Every number in the report should be traceable back to a file
  in `data/processed/` or a cell in a notebook in `notebooks/`.
