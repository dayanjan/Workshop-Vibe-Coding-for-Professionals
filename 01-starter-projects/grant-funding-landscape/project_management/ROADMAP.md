# Roadmap

> **Convention**: When checking off items, append the completion date: `- [x] Item (2026-03-14)`. When adding new items, include the date added.

## Phase 1: Setup
- [ ] Create Python environment and install dependencies
- [ ] Test NIH Reporter API connectivity (/v2/projects/search)
- [ ] Set up Google Drive junction (if using Colab)
- [ ] Verify folder structure is ready

## Phase 2: Data Pipeline
- [ ] Query NIH Reporter for Virginia institutions, last 3 fiscal years
- [ ] Handle pagination (500/page, 10K ceiling)
- [ ] Parse nested JSON responses
- [ ] Resolve institution name variations
- [ ] Save cleaned data to data/processed/

## Phase 3: Funding Analysis
- [ ] Aggregate by institution (top 20)
- [ ] Aggregate by NIH institute
- [ ] Calculate trend lines over fiscal years
- [ ] Identify funding concentration vs gaps

## Phase 4: Strategic Analysis
- [ ] Run keyword frequency on titles and abstracts
- [ ] Match funding gaps to grant mechanisms (R01, R21, K-awards)
- [ ] Identify opportunities for new investigators
- [ ] Note current FOAs relevant to identified gaps

## Phase 5: Reporting
- [ ] Generate funding visualizations
- [ ] Generate keyword cloud
- [ ] Write strategic summary with actionable recommendations
- [ ] Save all outputs to figures/ and reports/

## Stretch Goals
- [ ] Build Streamlit interactive dashboard
- [ ] Add USAspending.gov data for broader federal context
- [ ] Compare Virginia to peer states
