# richmond-workforce-analysis

Analyze Richmond, Virginia MSA workforce trends using Bureau of Labor Statistics public QCEW data.

## Tech Stack

Python 3.11+ | pandas | plotly | matplotlib | requests

## Folder Structure

```
richmond-workforce-analysis/
├── data/
│   ├── raw/          # Untouched BLS downloads (CSV/JSON)
│   └── processed/    # Cleaned, merged analysis-ready files
├── figures/          # PNG and HTML charts
├── reports/          # Written narrative summaries
├── notebooks/        # Jupyter notebooks for exploration
├── src/              # Reusable Python modules
└── .claude/
    ├── skills/       # Workflow templates
    ├── agents/       # Delegated analyst personas
    └── rules/        # Guardrails for data ethics
```

## IMPORTANT

> Before starting any analysis, read the workforce-analysis skill at
> `.claude/skills/workforce-analysis/SKILL.md` — it contains the full
> step-by-step workflow for pulling BLS data, running calculations,
> generating charts, and writing reports.

## Key Data Parameters

- **Richmond MSA FIPS:** 40060
- **Data source:** BLS Quarterly Census of Employment and Wages (QCEW)
- **API docs:** https://www.bls.gov/cew/additional-resources/open-data/
- **NAICS codes:** 2-digit for sector overview, 3-digit for detail

## Gotchas

1. **QCEW MSA format changed December 2025.** The BLS restructured how
   MSA-level files are organized in their flat-file downloads. Scripts
   written before this change will break on 2025-Q4+ data. Always check
   the current file layout at the open-data page before downloading.

2. **Always cite sources with dates and geography.** Every table, chart,
   or claim must state the data source (e.g., "BLS QCEW"), the time
   period (e.g., "2023-Q1 through 2025-Q3"), and the geography
   (e.g., "Richmond MSA, FIPS 40060"). Reviewers and policymakers
   will not trust uncited numbers.

## Project Management (`project_management/`)

All entries must be date-stamped (YYYY-MM-DD).

| File | When to READ | When to WRITE |
|------|-------------|---------------|
| `TASKS.md` | Session start — check active/blocked tasks | When creating, starting, completing, or blocking a task |
| `WORK_PROGRESS.md` | Session start — see where we left off | Session end — log what was done, blockers, next goals |
| `ROADMAP.md` | When planning or prioritizing | When a milestone is completed or rescheduled |
| `CHANGELOG.md` | Before making changes | After any commit that changes project outputs |
| `DECISIONS.md` | Before structural changes | When making a non-obvious design choice (new ADR) |

## Python Environment

- All packages MUST be installed in a virtual environment (`.venv/`) — never install globally
- Create: `python -m venv .venv` then activate before installing
- Every library MUST have an entry in `requirements.txt` with pinned version (e.g., `pandas==2.2.3`)
- After installing: `pip freeze | grep -i <package>` to get exact version, add to `requirements.txt`

## Context Tips

- Run `/clear` between unrelated tasks to keep the context window focused.
- Use **Plan Mode** (press Shift+Tab twice) when you want Claude to outline
  an approach before writing code — useful for complex multi-step analyses.
- Keep raw data files in `data/raw/` and never modify them in place.
