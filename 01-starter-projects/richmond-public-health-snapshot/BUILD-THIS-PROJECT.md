# Starter Template — Richmond Public Health Snapshot
## Vibe Coding for Healthcare Professionals Workshop | March 14, 2026

> **Paste this entire file into a fresh Claude Code session.** Claude will generate 5 files in ~15 minutes. No edits needed.
>
> **Prerequisites**: Claude Code installed via `winget install Anthropic.ClaudeCode` (Windows) or `brew install claude-code` (macOS).

---

# Generate My Project Scaffolding

I've opened this project folder (**richmond-public-health-snapshot**) in VS Code. Generate the 5 files listed below in the current directory — do not create a subfolder. The `project_management/` folder already exists with tracking templates.

## My Project

- **Name**: richmond-public-health-snapshot
- **Goal**: Compare health indicators across Richmond City, Henrico, Chesterfield, and Hanover counties, generate a composite health index, and connect health outcomes to social determinants
- **Language**: Python (pandas, plotly, matplotlib, requests)
- **Data Sources**:
  - CDC PLACES API — chronic disease prevalence estimates at county level. 2025 release includes 40 measures across 6 categories. Data portal: https://www.cdc.gov/places/tools/data-portal.html
  - Census ACS 5-Year API — socioeconomic indicators. Free API key: https://api.census.gov/data/key_signup.html
- **Key Geographies**: Richmond City (FIPS 51760), Henrico County (FIPS 51087), Chesterfield County (FIPS 51041), Hanover County (FIPS 51085)
- **Important**: CDC PLACES uses model-based small area estimates (not direct surveys). Always distinguish age-adjusted from crude rates.

## What to Generate (5 Files Only)

### 1. CLAUDE.md (40-60 lines)
Project memory file at the root. Include:
- Project name and one-sentence description
- Tech stack (Python, pandas, plotly, requests)
- Folder structure (data/raw, data/processed, figures, reports, notebooks, src)
- An IMPORTANT block telling Claude to read the skill before starting any analysis
- 2 critical gotchas: PLACES estimates are model-based (not direct surveys); always use person-first language
- Context tips: use `/clear` between tasks, Plan Mode for complex work (Shift+Tab×2)
- A Python environment section: all packages installed in `.venv/` virtual environment, every library must have an entry in `requirements.txt` with pinned version (e.g., `pandas==2.2.3`), run `pip freeze | grep -i <package>` after installing to get exact version
- A project management section referencing `project_management/` — at session start read TASKS.md and WORK_PROGRESS.md; at session end update WORK_PROGRESS.md and TASKS.md status; all entries date-stamped (YYYY-MM-DD)

### 2. .claude/skills/public-health-snapshot/SKILL.md
```yaml
---
name: public-health-snapshot
description: Build a community health profile using CDC PLACES and Census ACS data. Use when asked about health indicators, disparities, community health, or social determinants in the Richmond metro area.
allowed-tools: Read, Write, Bash, Grep, Glob
---
```
Include these analysis steps:
1. Download CDC PLACES data for Richmond City, Henrico, Chesterfield, and Hanover counties
2. Extract core indicators: diabetes prevalence, obesity, mental health, healthcare access, smoking, physical inactivity
3. Download Census ACS data: median income, insurance coverage, educational attainment, poverty rate
4. Compare all jurisdictions against Virginia and US benchmarks
5. Calculate a composite health index per jurisdiction (min-max normalization)
6. Generate visualizations: comparison bar charts, radar chart, scatter plot (health vs socioeconomic)
7. Write a community health narrative (reports/) using person-first language

Quality standards: report confidence intervals, compare to benchmarks, use person-first language, frame disparities as opportunities not deficits.

### 3. .claude/agents/clinical-reviewer.md
```yaml
---
name: clinical-reviewer
description: Clinical data reviewer for public health analysis. Use for CDC PLACES data interpretation, health equity analysis, and community health assessments.
tools: Read, Write, Bash, Grep, Glob
model: sonnet
---
```
System prompt: You are a clinical data reviewer specializing in community health assessment. Expertise in CDC PLACES, BRFSS, social determinants of health, epidemiological measures. Communication style: evidence-based, sensitive to human impact, person-first language always, frame findings as opportunities. Constraints: never make individual clinical recommendations, never use stigmatizing language, never present age-adjusted and crude rates interchangeably, never draw causal conclusions from cross-sectional data, always note ecological fallacy risk.

### 4. .claude/rules/health-equity.md
Rules for this project:
- ALWAYS use person-first language ("people with diabetes" not "diabetics")
- NEVER use deficit-based framing for communities
- Frame health disparities as systemic/structural issues, not individual failures
- NEVER draw causal conclusions from cross-sectional ecological data
- NEVER present age-adjusted and crude rates interchangeably — always label which type
- Always note that CDC PLACES estimates are model-based, not direct survey results
- When comparing jurisdictions, provide structural context (funding, access, policy)
- NEVER attribute area-level health data to individuals (ecological fallacy)
- All data must come from public sources (CDC PLACES and Census ACS)

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
- The skill defines HOW to do the analysis — API endpoints, FIPS codes, indicators, and steps
- The agent defines WHO you are — clinical reviewer persona and equity lens
- The rule defines what you must NEVER do — health equity and language guardrails
- Use real FIPS codes and API endpoints — no placeholders

## Generate All 5 Files Now
Start with CLAUDE.md. Everything specific to Richmond public health snapshot — no generic content, no TODOs.
