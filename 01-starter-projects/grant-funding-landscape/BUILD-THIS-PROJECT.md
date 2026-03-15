# Starter Template — Grant Funding Landscape Analysis
## Vibe Coding for Healthcare Professionals Workshop | March 14, 2026

> **Paste this entire file into a fresh Claude Code session.** Claude will generate 5 files in ~15 minutes. No edits needed.
>
> **Prerequisites**: Claude Code installed via `winget install Anthropic.ClaudeCode` (Windows) or `brew install claude-code` (macOS).

---

# Generate My Project Scaffolding

I've opened this project folder (**grant-funding-landscape**) in VS Code. Generate the 5 files listed below in the current directory — do not create a subfolder. The `project_management/` folder already exists with tracking templates.

## My Project

- **Name**: grant-funding-landscape
- **Goal**: Query NIH Reporter for Virginia health awards, aggregate by institution and NIH institute, identify trending topics, and produce a strategic report for investigators seeking funding
- **Language**: Python (pandas, plotly, matplotlib, requests, wordcloud)
- **Data Source**: NIH Reporter API (https://api.reporter.nih.gov/) — public REST API, no API key needed
- **Key Endpoints**: /v2/projects/search (POST with JSON criteria), /v2/projects (GET by project number)
- **Important**: API returns max 500 results per page with a 10,000 result ceiling per query — must break large queries into sub-queries using fiscal_year or award_amount ranges

## What to Generate (5 Files Only)

### 1. CLAUDE.md (40-60 lines)
Project memory file at the root. Include:
- Project name and one-sentence description
- Tech stack (Python, pandas, plotly, requests, wordcloud)
- Folder structure (data/raw, data/processed, figures, reports, notebooks, src)
- An IMPORTANT block telling Claude to read the skill before starting any analysis
- 2 critical gotchas: API pagination (500/page, 10K ceiling); institution name variations across years
- Context tips: use `/clear` between tasks, Plan Mode for complex work (Shift+Tab×2)
- A Python environment section: all packages installed in `.venv/` virtual environment, every library must have an entry in `requirements.txt` with pinned version (e.g., `pandas==2.2.3`), run `pip freeze | grep -i <package>` after installing to get exact version
- A project management section referencing `project_management/` — at session start read TASKS.md and WORK_PROGRESS.md; at session end update WORK_PROGRESS.md and TASKS.md status; all entries date-stamped (YYYY-MM-DD)

### 2. .claude/skills/grant-landscape/SKILL.md
```yaml
---
name: grant-landscape
description: Analyze federal health research funding using NIH Reporter API. Use when asked about grants, funding trends, research opportunities, or investigator strategy for Virginia institutions.
allowed-tools: Read, Write, Bash, Grep, Glob
---
```
Include these analysis steps:
1. Query NIH Reporter for all active awards to Virginia institutions, last 3 fiscal years
2. Handle pagination (500 results/page) and sub-query if results exceed 10,000
3. Aggregate total funding by institution and by NIH institute (e.g., NHLBI, NCI, NIMH)
4. Run keyword frequency analysis on project titles and abstracts (top 50 terms)
5. Generate visualizations: funding by institution bar chart, funding by NIH institute, keyword cloud
6. Write a strategic summary (reports/) identifying gaps and opportunities for new investigators

Quality standards: verify FOA currency, match strengths to mechanisms (R01, R21, K-awards), flag eligibility issues.

### 3. .claude/agents/grant-writer.md
```yaml
---
name: grant-writer
description: Grant writing strategist for federal funding analysis. Use for NIH grant strategy, funding opportunity analysis, and investigator positioning.
tools: Read, Write, Bash, Grep, Glob
model: sonnet
---
```
System prompt: You are a grant writing strategist. Expertise in NIH mechanisms (R01, R21, K-awards, T32, P-series), federal databases, and strategic positioning. Communication style: direct and strategic, mirror funded application language, active voice, concise. Constraints: never fabricate preliminary data or citations, never guarantee funding outcomes, always verify FOAs are current, state career-stage assumptions when recommending mechanisms.

### 4. .claude/rules/grant-integrity.md
Rules for this project:
- NEVER fabricate preliminary data, citations, or study results
- NEVER guarantee funding outcomes or success rates
- Always verify that referenced funding opportunity announcements (FOAs) are current
- Clearly distinguish strategic suggestions from eligibility requirements
- State assumptions about career stage and institutional support when recommending mechanisms
- All data must come from public sources (NIH Reporter is public and free)
- Always cite fiscal year and data retrieval date

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
- The skill defines HOW to do the analysis — API endpoints, pagination logic, analysis steps
- The agent defines WHO you are — grant strategist persona and constraints
- The rule defines what you must NEVER do — grant integrity guardrails
- Use real API endpoints — no placeholders

## Generate All 5 Files Now
Start with CLAUDE.md. Everything specific to NIH grant funding landscape — no generic content, no TODOs.
