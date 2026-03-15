# Tasks

Persistent task tracking across Claude Code sessions. Update status as work progresses.

> **Convention**: All status changes and notes must include a date stamp (YYYY-MM-DD). Use `**Updated YYYY-MM-DD**:` for inline updates.

## Active Tasks

### T-001: Set Up Python Environment
**Status**: Not Started
**Priority**: High
**Created**: YYYY-MM-DD

**Acceptance Criteria**:
- [ ] Python virtual environment created (.venv)
- [ ] Required packages installed (pandas, plotly, matplotlib, requests)
- [ ] Census API key obtained (https://api.census.gov/data/key_signup.html)
- [ ] CDC PLACES API test call returns data
- [ ] Census ACS API test call returns data
- [ ] Google Drive junction configured (if using Colab)

---

### T-002: Download CDC PLACES Data
**Status**: Not Started
**Priority**: High
**Created**: YYYY-MM-DD
**Depends On**: T-001

**Acceptance Criteria**:
- [ ] PLACES data downloaded for Richmond City (FIPS 51760), Henrico (51087), Chesterfield (51041), Hanover (51085)
- [ ] Core indicators extracted: diabetes, obesity, mental health, healthcare access, smoking, physical inactivity
- [ ] Age-adjusted vs crude rates clearly labeled
- [ ] Raw data saved to data/raw/

---

### T-003: Download Census ACS Data
**Status**: Not Started
**Priority**: High
**Created**: YYYY-MM-DD
**Depends On**: T-001

**Acceptance Criteria**:
- [ ] ACS 5-Year data downloaded for all 4 jurisdictions
- [ ] Indicators: median income, insurance coverage, educational attainment, poverty rate
- [ ] Virginia and US benchmarks included
- [ ] Raw data saved to data/raw/

---

### T-004: Health Analysis and Composite Index
**Status**: Not Started
**Priority**: Medium
**Created**: YYYY-MM-DD
**Depends On**: T-002, T-003

**Acceptance Criteria**:
- [ ] All jurisdictions compared against Virginia and US benchmarks
- [ ] Composite health index calculated (min-max normalization)
- [ ] Health indicators cross-referenced with socioeconomic data
- [ ] Person-first language used throughout
- [ ] Processed data saved to data/processed/

---

### T-005: Generate Visualizations and Report
**Status**: Not Started
**Priority**: Medium
**Created**: YYYY-MM-DD
**Depends On**: T-004

**Acceptance Criteria**:
- [ ] Comparison bar charts generated
- [ ] Radar chart generated (health indicators by jurisdiction)
- [ ] Scatter plot generated (health vs socioeconomic indicators)
- [ ] Community health narrative written using person-first language
- [ ] Disparities framed as opportunities, not deficits
- [ ] All outputs saved to figures/ and reports/

---

## Backlog

_Add future tasks here._

## Completed

_Move tasks here when done._
