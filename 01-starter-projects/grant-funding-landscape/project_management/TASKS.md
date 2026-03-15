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
- [ ] Required packages installed (pandas, plotly, matplotlib, requests, wordcloud)
- [ ] NIH Reporter API test call returns data
- [ ] Google Drive junction configured (if using Colab)

---

### T-002: Query NIH Reporter API
**Status**: Not Started
**Priority**: High
**Created**: YYYY-MM-DD
**Depends On**: T-001

**Acceptance Criteria**:
- [ ] API query retrieves Virginia institution awards for last 3 fiscal years
- [ ] Pagination handled correctly (500 results/page)
- [ ] Sub-queries used if results exceed 10,000 ceiling
- [ ] Raw JSON responses saved to data/raw/

---

### T-003: Aggregate Funding Data
**Status**: Not Started
**Priority**: Medium
**Created**: YYYY-MM-DD
**Depends On**: T-002

**Acceptance Criteria**:
- [ ] Funding aggregated by institution (top 20)
- [ ] Funding aggregated by NIH institute (NHLBI, NCI, NIMH, etc.)
- [ ] Institution name variations resolved
- [ ] Processed data saved to data/processed/

---

### T-004: Keyword and Strategic Analysis
**Status**: Not Started
**Priority**: Medium
**Created**: YYYY-MM-DD
**Depends On**: T-003

**Acceptance Criteria**:
- [ ] Keyword frequency analysis on project titles/abstracts (top 50 terms)
- [ ] Funding gaps and opportunities identified
- [ ] Grant mechanisms matched to opportunity areas (R01, R21, K-awards)
- [ ] Strategic findings documented

---

### T-005: Generate Visualizations and Report
**Status**: Not Started
**Priority**: Medium
**Created**: YYYY-MM-DD
**Depends On**: T-003, T-004

**Acceptance Criteria**:
- [ ] Funding by institution bar chart generated
- [ ] Funding by NIH institute chart generated
- [ ] Keyword cloud generated
- [ ] Strategic summary report written in reports/
- [ ] All outputs cite fiscal year and data retrieval date

---

## Backlog

_Add future tasks here._

## Completed

_Move tasks here when done._
