# Roadmap

> **Convention**: When checking off items, append the completion date: `- [x] Item (2026-03-14)`. When adding new items, include the date added.

## Phase 1: Setup
- [ ] Create Python environment and install dependencies
- [ ] Test BLS QCEW API connectivity
- [ ] Set up Google Drive junction (if using Colab)
- [ ] Verify folder structure is ready

## Phase 2: Data Pipeline
- [ ] Download QCEW data for Richmond MSA (FIPS 40060)
- [ ] Parse and clean raw data
- [ ] Align annual vs quarterly data
- [ ] Save cleaned data to data/processed/

## Phase 3: Analysis
- [ ] Calculate year-over-year employment change by industry
- [ ] Identify top 10 growing and declining industries
- [ ] Pull national comparison data
- [ ] Flag data suppression and known limitations

## Phase 4: Visualization
- [ ] Generate industry growth bar chart
- [ ] Generate industry composition treemap
- [ ] Generate wage-vs-growth scatter plot (stretch goal)
- [ ] Save all figures to figures/

## Phase 5: Reporting
- [ ] Write narrative summary report
- [ ] Include executive summary, findings, recommendations
- [ ] Review for plain language and source citations
- [ ] Save to reports/

## Stretch Goals
- [ ] Build Streamlit interactive dashboard
- [ ] Add OEWS wage data to analysis
- [ ] Compare Richmond to peer MSAs
