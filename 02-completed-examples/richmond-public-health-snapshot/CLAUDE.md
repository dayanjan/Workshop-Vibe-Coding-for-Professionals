# richmond-public-health-snapshot

Community health profile comparing Richmond City, Henrico, Chesterfield, and Hanover counties using CDC PLACES and Census ACS data.

## Tech Stack

Python 3.11+ | pandas | plotly | matplotlib | requests

## Folder Structure

```
richmond-public-health-snapshot/
├── data/
│   ├── raw/               # Untouched API downloads (PLACES JSON, ACS tables)
│   └── processed/         # Cleaned CSVs ready for analysis
├── figures/               # PNG and HTML chart outputs
├── reports/               # Written narratives and summaries
├── notebooks/             # Jupyter notebooks for exploration
├── src/                   # Reusable Python modules
└── .claude/
    ├── skills/            # Workflow templates
    ├── agents/            # Delegated analyst personas
    └── rules/             # Guardrails for health equity
```

## IMPORTANT

> This project has a skill that knows how to build the full analysis pipeline.
> Ask Claude Code: "Build the public health snapshot" or "Run the PLACES analysis"
> and it will follow the step-by-step workflow in `.claude/skills/public-health-snapshot/SKILL.md`.

## Key Geographies

| Jurisdiction | FIPS Code |
|---|---|
| Richmond City | 51760 |
| Henrico County | 51087 |
| Chesterfield County | 51041 |
| Hanover County | 51085 |

## Gotchas

1. **PLACES data are model-based small area estimates, not direct survey results.**
   CDC PLACES uses multilevel regression and poststratification (MRP) applied to BRFSS data.
   Do not describe these as "survey findings" or "reported rates." Always note the
   estimation methodology when presenting results.

2. **Always use person-first language.**
   Write "people with diabetes," not "diabetics." Write "people experiencing obesity,"
   not "obese people." Write "people who smoke," not "smokers." This applies to all
   narratives, chart labels, axis titles, and code comments.

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

- Run `/clear` between major tasks to free up context window
- Use **Plan Mode** (press Shift+Tab twice) to preview what Claude will do before it runs
- The clinical-reviewer agent (`.claude/agents/clinical-reviewer.md`) can review outputs
  for epidemiological accuracy and person-first language compliance
