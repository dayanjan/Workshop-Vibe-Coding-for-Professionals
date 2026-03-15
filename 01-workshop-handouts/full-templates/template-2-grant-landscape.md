# Project Documentation Generator v2.2 — PRE-FILLED TEMPLATE
## Use Case 2: Grant Funding Landscape Analysis
## Vibe Coding for Professionals Workshop | March 14, 2026

> **How to use this template**: Copy this entire file and paste it into a fresh Claude Code session. Claude will generate a complete project scaffolding with all the skills, agents, rules, and hooks you need. No edits required — just paste and go.
>
> **Prerequisites**: Claude Code installed via `brew install claude-code` (macOS) or `winget install Anthropic.ClaudeCode` (Windows). The old `npm install -g @anthropic-ai/claude-code` method is deprecated. Docs: https://code.claude.com/docs/en/overview

---

# Generate Complete Project Scaffolding

I need you to create a modern Claude Code project scaffolding system using progressive disclosure, Agent Skills, Custom Subagents, Hooks, Plan Mode integration, Sandbox mode, and optimized context management.

---

## SECTION A: MY PROJECT DETAILS

### Project Type

**Select ONE primary type** (this controls which conditional sections are generated):

- [ ] ML / Data Science
- [ ] Web App
- [ ] API / Backend
- [ ] CLI Tool
- [ ] Automation / Scripts
- [x] **Research / Analysis** — data analysis, visualization, reports, papers

### Basic Information

**Project Name**: grant-funding-landscape
**Description**: Analyze federal health research funding awarded to Virginia institutions using the NIH Reporter API. Map funding by institution and NIH institute, identify trending research topics, compare Virginia to national benchmarks, and generate strategic reports for investigators seeking funding opportunities.
**Primary Goal**: Build a repeatable pipeline that queries NIH Reporter, aggregates funding data, and produces strategic analysis to help researchers identify funding opportunities and position grant applications.
**Timeline**: 4 weeks
**Target Output**: Analysis report with funding data CSVs, trend visualizations, keyword frequency analysis, and a strategic positioning summary for new investigators

### Technical Stack

**Primary Language**: Python
**Core Libraries/Frameworks**:
- pandas (data manipulation and aggregation)
- plotly (interactive funding visualizations)
- matplotlib (static charts)
- requests (NIH Reporter API calls)
- wordcloud (keyword frequency visualization)
- streamlit (optional interactive dashboard)

**Special Models/Architectures**: N/A — not applicable for this project type

**APIs and External Services**:
- NIH Reporter API (https://api.reporter.nih.gov/)
- Endpoints: /v2/projects/search, /v2/projects
- No API key required — public REST API

**Data Sources**:
- NIH Reporter API (project data: title, PI, institution, funding, NIH institute, fiscal year, study section)
- Filter: Virginia institutions, last 3 fiscal years
- Optional: USAspending.gov for broader federal funding context

### Compute and Environment

**Development Environment**:
- [x] Local machine (OS: macOS or Windows — Claude will detect)
- [x] Google Colab (Tier: Free)
- [ ] Remote server / cloud VM
- [ ] Docker / devcontainer
- [ ] Other

**GPU Required**: No

**If using Colab**:
- Recommended GPU: CPU only
- Memory requirements: 16GB (standard free tier is fine)
- Estimated runtimes: Setup 2 min | API queries 10 min | Analysis 5 min

**Sync/Workflow**:
- [x] Google Drive Desktop (auto-sync to Colab)
- [x] Git-based workflow
- [ ] Direct file management
- [ ] CI/CD pipeline

### Project Structure

Leave blank — use the default **Research / Analysis** folder structure, plus:
```
grant-funding-landscape/
├── notebooks/
│   ├── 01_nih_data_download.ipynb
│   ├── 02_funding_analysis.ipynb
│   └── 03_strategic_report.ipynb
├── src/
│   ├── analysis/
│   ├── visualization/
│   └── utils/
├── data/
│   ├── raw/
│   └── processed/
├── figures/
├── reports/
├── tests/
├── configs/
```

### Success Metrics

**Primary Success Criteria**: Successfully query NIH Reporter for all active Virginia health awards, aggregate by institution and NIH institute, and produce a strategic report identifying funding gaps and opportunities.
**Quantitative Metrics**: Data covers at least 3 fiscal years; top 20 funded institutions identified; funding broken down by at least 10 NIH institutes; keyword frequency analysis of 100+ project abstracts.
**Qualitative Goals**: Reports help a new investigator identify where to focus; strategic recommendations tied to data; all findings cite API sources with fiscal years.

### Domain and Context

**Domain**: Research Funding Strategy / Health Research Administration
**Your Experience Level**: Beginner — learning Python and data analysis as I go
**Special Considerations**: NIH Reporter API has rate limits (be respectful with requests). Grant mechanisms (R01, R21, K-awards, T32) need clear definitions. Funding amounts should be presented in context (percentages, comparisons). Never fabricate preliminary data or citations.

### Known Challenges

**Technical Challenges**: NIH Reporter API pagination (max 500 results per request, 10,000 result ceiling per query — must break into sub-queries for larger result sets); parsing nested JSON responses; matching institution names across years (name variations).
**Data Challenges**: Funding amounts may include subprojects; multi-PI grants complicate per-institution attribution; fiscal year timing vs. calendar year.
**Environment Challenges**: Google Drive sync timing between local edits and Colab availability.
**External Dependencies**: None — NIH Reporter API is public and free. No API key needed. API docs: https://api.reporter.nih.gov/

### Collaboration

**Working Style**: Solo (workshop learning project)
**Version Control**: Git
**Branch Strategy**: Main only

---

## SECTION B: WHAT TO GENERATE

Generate all of the following. Follow the design principles in Section C exactly.

The project type selected in Section A determines which conditional sections to include. Files marked **(conditional)** are only generated when they match the project type.

---

### TIER 1: Core Files

---

#### 1. CLAUDE.md — The Map (60-100 lines MAXIMUM)

This loads into every session. Every line costs tokens permanently.

**MUST include:**
- Project name + 1-2 sentence description
- Tech stack (one line)
- Abbreviated folder structure (5-10 lines max)
- Current phase / status (one line)
- The IMPORTANT block (see below)
- List of docs/ files with 1-line descriptions
- 2-3 critical gotchas: NIH Reporter pagination, institution name matching, fiscal year alignment
- Context management reminders
- Reference to MEMORY.md for session history
- Note that Claude Code also has auto memory (`/memory` to manage) — complements MEMORY.md

**Required: The IMPORTANT block:**
```markdown
## IMPORTANT: Read Before Working
Before starting any task, identify which docs below are relevant and read them first.
- `docs/setup.md` — Environment setup, NIH Reporter API access, Google Drive junction
- `docs/architecture.md` — Three-layer architecture (Think → Compute → Interpret)
- `docs/gotchas.md` — NIH Reporter API quirks, pagination, funding attribution rules
- `docs/colab-workflow.md` — Notebook structure, Drive mounting, output handling
- `docs/conventions.md` — Code patterns, naming, and context management

For complex multi-file work: start in Plan Mode (Shift+Tab×2), create a task list, then switch to Normal Mode to execute. Use /effort high for strategic analysis decisions.
```

---

#### 2. MEMORY.md — The Index (50-100 lines MAXIMUM)

Lightweight index. Current Status, Recent Sessions table, Key Decisions, Critical Gotchas, For Details pointers.

---

#### 3. ATOMIC_PLAN.md — Initial Task Breakdown

**Epics for this project:**
- E1: Environment Setup (Drive junction, packages, NIH Reporter API test)
- E2: Data Pipeline (query NIH Reporter, pagination, parse JSON, clean data)
- E3: Funding Analysis (aggregate by institution, by NIH institute, trend lines)
- E4: Strategic Analysis (keyword frequency, gap identification, mechanism matching)
- E5: Reporting (narrative summary, visualizations, strategic recommendations)

Include Plan Mode usage note at top.

---

#### 4. WORK_PROGRESS.md — Progress Dashboard

---

### TIER 2: Progressive Disclosure Docs (docs/)

---

#### 5. docs/setup.md — Environment Setup
- Python environment setup
- Package installation: `pip install pandas plotly matplotlib requests wordcloud streamlit`
- NIH Reporter API test: curl example for /v2/projects/search (docs: https://api.reporter.nih.gov/?urls.primaryName=V2.0)
- Google Drive junction setup
- Sandbox configuration
- Verification checklist

---

#### 6. docs/architecture.md — System Design
- Three-layer architecture diagram
- Data flow: NIH Reporter API → raw JSON → cleaned DataFrame → aggregations → visualizations → strategic report
- Google Drive junction explanation

---

#### 7. docs/gotchas.md — Known Pitfalls
- NIH Reporter API pagination (500 results max per page, 10,000 result ceiling per query — must break large queries into sub-queries using criteria ranges like award_amount or fiscal_year to get complete result sets)
- Rate limiting (be polite with delays between requests — bulk download available at https://reporter.nih.gov/exporter/)
- Institution name variations across years
- Multi-PI grant attribution
- Fiscal year vs calendar year confusion
- Funding amounts including/excluding subprojects
- JSON nested structure for project details
- Keyword extraction from abstracts (tokenization issues)

---

#### 8. docs/conventions.md — Code Patterns and Context Management

Same structure as v2.2 standard with project-specific naming conventions (fiscal year in filenames, institution codes). Note: Opus 4.6 defaults to medium effort — use `/effort high` for strategic analysis and methodology decisions.

---

#### 9. docs/colab-workflow.md — Colab + Google Drive Workflow
Standard notebook structure with NIH Reporter API helper functions, pagination handler, and output saving.

---

#### 10. docs/plans/.gitkeep

---

### TIER 3: Agent Skills (.claude/skills/)

---

#### 11. Notebook Creator Skill

**Path**: `.claude/skills/notebook-creator/SKILL.md`

```yaml
---
name: notebook-creator
description: Create Jupyter/Colab notebooks for NIH Reporter grant analysis. Use when creating new notebooks or analysis scripts for the funding landscape project.
allowed-tools: Read, Write, Bash, Grep, Glob
---
```

Template with Drive mounting, imports, NIH Reporter API helpers with pagination, output saving.

---

#### 12. Grant Landscape Skill

**Path**: `.claude/skills/grant-landscape/SKILL.md`

```yaml
---
name: grant-landscape
description: Analyze federal health research funding using NIH Reporter API. Use when asked about grants, funding trends, research opportunities, NIH institutes, or investigator strategy for Virginia institutions.
allowed-tools: Read, Write, Bash, Grep, Glob
---
```

Include:
- Data source: NIH Reporter API (https://api.reporter.nih.gov/)
- Query parameters: Virginia institutions, last 3 fiscal years
- Analysis steps: query → paginate → parse → aggregate by institution and institute → keyword frequency → gap analysis → strategic recommendations
- Output format: aggregated CSVs, funding charts, keyword cloud, strategic summary
- Quality standards: verify current FOAs, match strengths to mechanisms, flag eligibility issues

Also create supporting files:
- `.claude/skills/grant-landscape/templates/strategic-report.md` — Executive summary, funding landscape, opportunities, strategic recommendations
- `.claude/skills/grant-landscape/examples/good-analysis.md` — Example with specific institutions, mechanisms, strategic insight
- `.claude/skills/grant-landscape/examples/bad-analysis.md` — Vague example without actionable advice
- `.claude/skills/grant-landscape/data-dictionary.md` — NIH grant mechanisms (R01, R21, K-awards, T32, P-series), NIH institutes, fiscal year definitions, study section codes

---

#### 13. Atomic Planner Skill

**Path**: `.claude/skills/atomic-planner/SKILL.md` (standard)

---

#### 14. Session Closer Skill

**Path**: `.claude/skills/session-closer/SKILL.md` (standard)

---

#### 15. Python Debugger Skill

**Path**: `.claude/skills/python-debugger/SKILL.md`

```yaml
---
name: python-debugger
description: Debug Python errors including requests/API failures, JSON parsing errors, pandas issues, and Colab runtime errors. Use when encountering errors, crashes, or unexpected behavior.
allowed-tools: Read, Bash, Grep, Glob
---
```

---

### TIER 4: Hooks (.claude/settings.json)

---

#### 16. .claude/settings.json

Same 5-hook structure as Use Case 1 (PostToolUse formatter, Notification, PreToolUse security, SessionEnd logging, PreCompact backup). Python/black formatter.

---

### TIER 5: Custom Agents (.claude/agents/)

---

#### 17. Grant Writing Strategist Agent

**Path**: `.claude/agents/grant-writer.md`

```yaml
---
name: grant-writer
description: Grant writing strategist for federal funding analysis. Use proactively for NIH, NSF, and federal grant strategy, Specific Aims structure, funding opportunity analysis, and investigator positioning.
tools: Bash, Read, Write, Grep, Glob
model: sonnet
permissionMode: acceptEdits
skills: grant-landscape
---
```

System prompt should include:
- Expertise in NIH grant mechanisms (R01, R21, K-awards, T32, P-series), NSF structures, federal databases
- Communication style: direct and strategic, mirror language of funded applications, active voice, concise
- Decision rules: verify current FOAs, match strengths to mechanisms, flag eligibility issues early, prioritize significance and innovation
- Constraints: never fabricate preliminary data or citations, never write boilerplate, never ignore page limits

---

#### 18. Test Writer Agent (standard)

---

### TIER 6: Slash Commands (.claude/commands/)

#### 19-21. Standard commands: next-task.md, complete-task.md, status.md

---

### TIER 7: Utility Scripts, Config, and Templates

---

#### 22. .gitignore — Python + Colab customized
#### 23. README.md
#### 24. requirements.txt
```
pandas>=2.0
plotly>=5.0
matplotlib>=3.7
requests>=2.28
wordcloud>=1.9
streamlit>=1.30
black>=23.0
```

#### 25. memory/ folder structure (standard)

---

### Rules (.claude/rules/)

#### 26. .claude/rules/healthcare-ethics.md
Same as Use Case 1 — never make clinical recommendations, all data publicly available, hedge uncertain findings.

#### 27. .claude/rules/data-privacy.md
Same as Use Case 1 — public data only, aggregate results, suppress small samples.

#### 28. .claude/rules/output-standards.md
Same as Use Case 1 — self-check numbers, cite sources, plain language, flag limitations.

#### 29. .claude/rules/grant-integrity.md (additional rule for this project)
- NEVER fabricate preliminary data, citations, or study results
- NEVER claim familiarity with specific unpublished work
- NEVER guarantee funding outcomes or success rates
- Always verify that referenced funding opportunity announcements (FOAs) are current
- Clearly distinguish between strategic suggestions and eligibility requirements
- When recommending grant mechanisms, state assumptions about career stage and institutional support

---

## SECTION C: DESIGN PRINCIPLES

Same 8 principles as Use Case 1 (Progressive Disclosure, Context Efficiency, Deterministic Over Advisory, Let Native Systems Work, Specialist Agents, Be Specific, Build for Growth, Project-Type Awareness).

---

## SECTION D: OUTPUT FORMAT

### Generation Order
1. CLAUDE.md
2. MEMORY.md
3. .claude/settings.json
4. All docs/ files
5. All .claude/skills/
6. All .claude/agents/
7. All .claude/commands/
8. All .claude/rules/
9. ATOMIC_PLAN.md
10. WORK_PROGRESS.md
11. .gitignore, README.md, requirements.txt
12. memory/ folder templates

### Quality Checks
- [ ] CLAUDE.md under 100 lines with IMPORTANT block
- [ ] MEMORY.md under 100 lines
- [ ] .claude/settings.json has all 5 hooks
- [ ] Every SKILL.md has valid YAML frontmatter
- [ ] Every agent .md has valid YAML frontmatter
- [ ] NO custom researcher/explorer agent
- [ ] All code uses Python + pandas + plotly + NIH Reporter API — zero placeholders
- [ ] .claude/rules/ contains healthcare-ethics.md, data-privacy.md, output-standards.md, grant-integrity.md
- [ ] Only Research/Analysis conditional sections generated

---

## BEGIN GENERATION

Create all files now, starting with CLAUDE.md. Everything specific to NIH grant funding landscape analysis — no generic placeholders, no TODOs.

Start with CLAUDE.md.
