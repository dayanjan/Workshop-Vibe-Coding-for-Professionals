# grant-funding-landscape

Analyzes federal health research funding patterns for Virginia institutions using the NIH Reporter API to identify strategic opportunities and trends.

## Tech Stack

Python 3.11+ | pandas | plotly | matplotlib | requests | wordcloud

## Folder Structure

```
grant-funding-landscape/
├── data/
│   ├── raw/          # JSON responses from NIH Reporter API
│   └── processed/    # Cleaned CSVs and aggregated tables
├── figures/          # Bar charts, trend lines, keyword clouds (PNG + HTML)
├── reports/          # Strategic summaries and gap analyses
├── notebooks/        # Jupyter notebooks for exploratory analysis
├── src/              # Reusable query, processing, and visualization modules
└── .claude/
    ├── skills/       # Workflow templates
    ├── agents/       # Delegated analyst personas
    └── rules/        # Guardrails for grant data integrity
```

## IMPORTANT

> This project has a skill that handles the full analysis pipeline.
> See `.claude/skills/grant-landscape/SKILL.md` for the step-by-step workflow.
> When asked to analyze grants, funding trends, or investigator strategy,
> Claude Code will automatically use this skill.

## Key API Details

- **NIH Reporter API:** https://api.reporter.nih.gov/
- **Endpoint:** /v2/projects/search (POST)
- **Authentication:** No API key required
- **Pagination:** Max 500 results/page, 10,000 ceiling per query

## Gotchas

1. **API pagination can silently truncate results.** The NIH Reporter
   `/v2/projects/search` endpoint returns a maximum of 500 results per page.
   The total result ceiling is 10,000 per query. If your search matches more
   than 10,000 projects, you must break it into sub-queries — typically by
   splitting across fiscal years, NIH institutes, or activity codes. Always
   check the `meta.total` field in the response to confirm you captured all
   results.

2. **Institution names vary across fiscal years.** Virginia institutions
   appear under different names across fiscal years. For example, "Virginia
   Commonwealth University" may also appear as "VCU" or "Medical College of
   Virginia." The University of Virginia can appear as "University of Virginia"
   or "UVA." Always normalize institution names during processing and verify
   counts against NIH Reporter's web interface for a known institution-year
   pair.

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

- Use `/clear` between analysis tasks to free up context window space.
  Each NIH Reporter response can be large, and you want room for visualization
  and summary work.
- Use **Plan Mode** (press Shift+Tab twice) before starting a multi-step
  analysis. This lets you review the query strategy before Claude Code
  begins pulling data and generating figures.
- When re-running queries, check `data/raw/` first — previously fetched
  data may already cover your fiscal years and institutions.
