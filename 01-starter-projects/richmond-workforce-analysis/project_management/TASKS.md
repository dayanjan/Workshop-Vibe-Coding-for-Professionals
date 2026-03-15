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
- [ ] BLS QCEW API test call returns data
- [ ] Google Drive junction configured (if using Colab)

---

### T-002: Download BLS QCEW Data
**Status**: Not Started
**Priority**: High
**Created**: YYYY-MM-DD
**Depends On**: T-001

**Acceptance Criteria**:
- [ ] QCEW data downloaded for Richmond MSA (FIPS 40060)
- [ ] Data covers at least 3 years
- [ ] Raw CSV saved to data/raw/ with timestamp in filename
- [ ] Data format matches current QCEW Open Data Access spec (Dec 2025 update)

---

### T-003: Analyze Employment Trends
**Status**: Not Started
**Priority**: Medium
**Created**: YYYY-MM-DD
**Depends On**: T-002

**Acceptance Criteria**:
- [ ] Year-over-year employment change calculated by NAICS sector
- [ ] Top 10 growing and top 10 declining industries identified
- [ ] National comparison included for context
- [ ] Processed data saved to data/processed/
- [ ] Data suppression flagged where applicable

---

### T-004: Generate Visualizations
**Status**: Not Started
**Priority**: Medium
**Created**: YYYY-MM-DD
**Depends On**: T-003

**Acceptance Criteria**:
- [ ] Bar chart of industry growth rates generated
- [ ] Treemap of industry composition generated
- [ ] All charts have clear titles, labels, and source citations
- [ ] PNG files saved to figures/

---

### T-005: Write Summary Report
**Status**: Not Started
**Priority**: Medium
**Created**: YYYY-MM-DD
**Depends On**: T-003, T-004

**Acceptance Criteria**:
- [ ] Narrative summary written in plain language
- [ ] All findings cite data source, date range, and geography
- [ ] National comparison included
- [ ] Limitations and caveats stated
- [ ] Report saved to reports/

---

## Backlog

_Add future tasks here._

## Completed

_Move tasks here when done._
