# Starter Template — Richmond Workforce Analysis
## Vibe Coding for Healthcare Professionals Workshop | March 14, 2026

> **Paste this entire file into a fresh Claude Code session.** Claude will generate 5 files in ~15 minutes. No edits needed.
>
> **Prerequisites**: Claude Code installed via `winget install Anthropic.ClaudeCode` (Windows) or `brew install claude-code` (macOS).

---

# Generate My Project Scaffolding

I've opened this project folder (**richmond-workforce-analysis**) in VS Code. Generate the 5 files listed below in the current directory — do not create a subfolder. The `project_management/` folder already exists with tracking templates.

## My Project

- **Name**: richmond-workforce-analysis
- **Goal**: Download BLS employment data for Richmond, identify growing and declining industries, and generate charts and a summary report
- **Language**: Python (pandas, plotly, matplotlib, requests)
- **Data Source**: BLS Quarterly Census of Employment and Wages (QCEW) API — public, no API key needed
- **Key Reference**: Richmond MSA FIPS code is 40060. Use current QCEW Open Data Access docs at https://www.bls.gov/cew/additional-resources/open-data/
- **Important**: BLS changed QCEW MSA data format in December 2025 — column layouts may differ from older tutorials

## What to Generate (5 Files Only)

### 1. CLAUDE.md (40-60 lines)
Project memory file at the root. Include:
- Project name and one-sentence description
- Tech stack (Python, pandas, plotly, requests)
- Folder structure (data/raw, data/processed, figures, reports, notebooks, src)
- An IMPORTANT block telling Claude to read the skill before starting any analysis
- 2 critical gotchas: QCEW format changed Dec 2025; always cite sources with dates and geography
- Context tips: use `/clear` between tasks, Plan Mode for complex work (Shift+Tab×2)
- A Python environment section: all packages installed in `.venv/` virtual environment, every library must have an entry in `requirements.txt` with pinned version (e.g., `pandas==2.2.3`), run `pip freeze | grep -i <package>` after installing to get exact version
- A project management section referencing `project_management/` — at session start read TASKS.md and WORK_PROGRESS.md; at session end update WORK_PROGRESS.md and TASKS.md status; all entries date-stamped (YYYY-MM-DD)

### 2. .claude/skills/workforce-analysis/SKILL.md
```yaml
---
name: workforce-analysis
description: Analyze Richmond MSA workforce data from BLS public APIs. Use when asked about employment trends, industry growth, wage data, or economic development for the Richmond area.
allowed-tools: Read, Write, Bash, Grep, Glob
---
```
Include these analysis steps:
1. Download QCEW data for Richmond MSA (FIPS 40060) for the most recent 3 years
2. Calculate year-over-year employment change by industry (NAICS sector)
3. Identify top 10 growing and top 10 declining industries
4. Generate visualizations: bar chart of growth rates, treemap of industry composition
5. Save outputs as CSV (data/processed/) and PNG (figures/)
6. Write a brief narrative summary (reports/) citing sources with dates

Quality standards: always include national comparison, flag data suppression, use plain language.

### 3. .claude/agents/research-analyst.md
```yaml
---
name: research-analyst
description: Workforce research analyst for Richmond MSA employment data. Use for BLS data analysis, industry trends, and economic development questions.
tools: Read, Write, Bash, Grep, Glob
model: sonnet
---
```
System prompt: You are a workforce research analyst. Expertise in BLS data (QCEW, OEWS, CES). Communication style: professional but accessible, lead with insight then evidence, plain language, always contextualize numbers (e.g., "12% growth, compared to 3% nationally"). Constraints: never present correlation as causation, never extrapolate without flagging, always cite sources.

### 4. .claude/rules/data-ethics.md
Rules for this project:
- All data must be publicly available (BLS APIs are public and free)
- Never include individual names or PII in outputs
- Aggregate results to jurisdiction level or higher
- Use hedging language for uncertain findings ("suggests" not "proves")
- Always state data source, date range, and geography
- Distinguish AI-generated analysis from verified facts

### 5. Folder Structure
Create these empty directories:
Create these empty directories in the current folder (do not nest inside a subfolder):
```
data/raw/
data/processed/
figures/
reports/
notebooks/
src/
```
Note: `project_management/` already exists — do not overwrite it.

## Design Principles
- CLAUDE.md is the map, not the encyclopedia — keep it under 60 lines
- The skill defines HOW to do the analysis — all BLS endpoints, FIPS codes, and steps are here
- The agent defines WHO you are — communication style and constraints
- The rule defines what you must NEVER do — data ethics guardrails
- Use real API endpoints and FIPS codes — no placeholders

## Generate All 5 Files Now
Start with CLAUDE.md. Everything specific to Richmond workforce analysis — no generic content, no TODOs.
