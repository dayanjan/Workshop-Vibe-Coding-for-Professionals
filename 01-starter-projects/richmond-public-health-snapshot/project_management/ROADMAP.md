# Roadmap

> **Convention**: When checking off items, append the completion date: `- [x] Item (2026-03-14)`. When adding new items, include the date added.

## Phase 1: Setup
- [ ] Create Python environment and install dependencies
- [ ] Obtain Census API key
- [ ] Test CDC PLACES API connectivity
- [ ] Test Census ACS API connectivity
- [ ] Set up Google Drive junction (if using Colab)

## Phase 2: Data Pipeline — CDC PLACES
- [ ] Download PLACES data for 4 Richmond metro jurisdictions
- [ ] Extract 6 core health indicators
- [ ] Label age-adjusted vs crude rates
- [ ] Note that estimates are model-based (not direct surveys)
- [ ] Save cleaned data to data/processed/

## Phase 3: Data Pipeline — Census ACS
- [ ] Download ACS 5-Year for same 4 jurisdictions
- [ ] Extract socioeconomic indicators (income, insurance, education, poverty)
- [ ] Include Virginia and US benchmarks
- [ ] Check margins of error for small geographies
- [ ] Save cleaned data to data/processed/

## Phase 4: Analysis
- [ ] Compare health indicators across all jurisdictions
- [ ] Benchmark against Virginia and US averages
- [ ] Calculate composite health index (min-max normalization)
- [ ] Cross-reference health with socioeconomic data
- [ ] Identify patterns using opportunity-based framing

## Phase 5: Visualization and Reporting
- [ ] Generate comparison bar charts
- [ ] Generate radar chart
- [ ] Generate health-vs-socioeconomic scatter plot
- [ ] Write community health narrative (person-first language)
- [ ] Include confidence intervals and structural context
- [ ] Save all outputs to figures/ and reports/

## Stretch Goals
- [ ] Build Streamlit interactive dashboard
- [ ] Add geographic mapping with geopandas
- [ ] Explore additional PLACES 2025 measures (40 total)
- [ ] Include health-related social needs measures (new in 2024)
