---
name: public-health-snapshot
description: Build a community health profile using CDC PLACES and Census ACS data. Use when asked about health indicators, disparities, community health, or social determinants in the Richmond metro area.
allowed-tools: Read, Write, Bash, Grep, Glob
---

# Public Health Snapshot — Analysis Pipeline

Follow these steps to build a complete community health profile for the Richmond metro area.

## Step 1: Download CDC PLACES Data

Query the CDC PLACES API for county- and city-level measures across four jurisdictions:
- Richmond City (FIPS 51760)
- Henrico County (FIPS 51087)
- Chesterfield County (FIPS 51041)
- Hanover County (FIPS 51085)

API endpoint: `https://data.cdc.gov/resource/swc5-untb.json`

Save raw JSON responses to `data/raw/places_{jurisdiction}.json`.

## Step 2: Extract Key Health Measures

From the PLACES download, extract these six indicator categories:
- **Diabetes prevalence** — people with diagnosed diabetes (age-adjusted %)
- **Obesity** — people experiencing obesity, BMI >= 30 (age-adjusted %)
- **Mental health** — people reporting frequent mental distress, 14+ days/month (age-adjusted %)
- **Healthcare access** — people without health insurance, ages 18-64 (crude %)
- **Smoking** — people who currently smoke (age-adjusted %)
- **Physical inactivity** — people reporting no leisure-time physical activity (age-adjusted %)

Clean and reshape into a tidy DataFrame. Save to `data/processed/places_measures.csv`.

## Step 3: Download Census ACS Socioeconomic Data

Using the Census ACS 5-Year API (`https://api.census.gov/data/2022/acs/acs5`), pull:
- **Median household income** (B19013_001E)
- **Health insurance coverage** (B27001 table)
- **Educational attainment** — bachelor's degree or higher (B15003 table)
- **Poverty rate** (B17001 table)

for all four jurisdictions plus Virginia statewide.

Save to `data/processed/acs_socioeconomic.csv`.

## Step 4: Benchmark Comparisons

Compare each jurisdiction against:
- Virginia statewide averages (from ACS and PLACES state-level data)
- US national benchmarks (from PLACES national estimates)

Flag any jurisdiction where a measure is more than 2 percentage points above the state average. Frame these as opportunities for investment, not deficits.

Save comparison table to `data/processed/benchmark_comparison.csv`.

## Step 5: Composite Health Index

Build a composite health index for each jurisdiction:
1. Select the six PLACES measures from Step 2
2. Apply min-max normalization across the four jurisdictions (0 = best, 1 = worst)
3. Calculate an unweighted average to produce a single composite score
4. Rank jurisdictions

Save to `data/processed/composite_index.csv`.

## Step 6: Visualizations

Generate three main visualizations:

### 6a. Jurisdiction Comparison Bar Chart
Grouped bar chart showing all six PLACES measures side by side for each jurisdiction. Include Virginia and US benchmark lines. Save to `figures/jurisdiction_comparison.png` and `figures/jurisdiction_comparison.html`.

### 6b. Radar Chart
One radar chart overlaying all four jurisdictions across the six health measures. Normalize so that outward = worse health outcome. Save to `figures/radar_health_profile.png`.

### 6c. Health vs. Socioeconomic Scatter
Scatter plot with median household income on the x-axis and composite health index on the y-axis. Label each jurisdiction. Add a trend annotation if appropriate. Save to `figures/health_vs_income_scatter.png`.

**Chart standards:**
- Use person-first language in all labels and titles
- Label whether rates are age-adjusted or crude
- Include data source footnotes on every chart
- Use colorblind-friendly palettes

## Step 7: Community Health Narrative

Write a 500-800 word summary to `reports/community_health_narrative.md` that includes:
- Overview of the Richmond metro health landscape
- Key findings for each jurisdiction
- Structural and systemic context for any observed disparities
- Opportunities for community health investment
- Data limitations section noting that PLACES uses model-based estimates

**Writing standards:**
- Person-first language throughout
- Opportunity framing, not deficit framing
- No causal claims from this cross-sectional ecological data
- Note ecological fallacy: area-level data do not describe individuals

## Quality Checklist

Before finalizing, verify:
- [ ] All rates clearly labeled as age-adjusted or crude — never mixed in the same comparison
- [ ] Confidence intervals included where available from PLACES
- [ ] Virginia and US benchmarks present in comparison outputs
- [ ] Person-first language in every narrative, label, and comment
- [ ] Opportunity framing used — no deficit-based descriptions
- [ ] PLACES methodology noted as model-based small area estimates
- [ ] No causal language (use "associated with," not "caused by")
- [ ] Ecological fallacy disclaimer included in narrative
- [ ] All data sourced from public APIs — no proprietary data
