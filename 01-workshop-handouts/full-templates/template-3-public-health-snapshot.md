# Project Documentation Generator v2.2 — PRE-FILLED TEMPLATE
## Use Case 3: Richmond Public Health Snapshot
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

**Project Name**: richmond-public-health-snapshot
**Description**: Build a community health profile for the Richmond, Virginia metropolitan area using CDC PLACES and Census ACS data. Compare health indicators across Richmond City, Henrico, Chesterfield, and Hanover counties, generate a composite health index, and produce reports that connect health outcomes to social determinants.
**Primary Goal**: Create a repeatable analysis that downloads CDC PLACES chronic disease prevalence data and Census socioeconomic data, generates comparison visualizations, and produces a community health assessment report suitable for public health planning.
**Timeline**: 4 weeks
**Target Output**: Community health assessment report with CSV data files, comparison charts, radar plots, composite health index scores, and a Streamlit interactive dashboard

### Technical Stack

**Primary Language**: Python
**Core Libraries/Frameworks**:
- pandas (data manipulation)
- plotly (interactive visualizations — radar charts, scatter plots)
- matplotlib (static charts)
- requests (CDC PLACES API and Census API calls)
- geopandas (optional — geographic health mapping)
- streamlit (interactive dashboard)

**Special Models/Architectures**: N/A — not applicable for this project type

**APIs and External Services**:
- CDC PLACES API (chronic disease prevalence estimates at county/tract level — 2025 release includes 40 measures across health outcomes, prevention, risk behaviors, disabilities, health status, and health-related social needs)
- Census ACS 5-Year API (socioeconomic indicators)
- Census API key required (free, instant — https://api.census.gov/data/key_signup.html)

**Data Sources**:
- CDC PLACES: diabetes, obesity, mental health, healthcare access, smoking, physical inactivity prevalence (starting set — 40 total measures available in the 2025 release, including 7 health-related social needs measures added in 2024)
- Census ACS 5-Year: median income, insurance coverage, educational attainment, poverty rate
- Geographies: Richmond City (FIPS 51760), Henrico County (FIPS 51087), Chesterfield County (FIPS 51041), Hanover County (FIPS 51085), Virginia state, US national

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
- Estimated runtimes: Setup 2 min | Data download 5 min | Analysis 5 min

**Sync/Workflow**:
- [x] Google Drive Desktop (auto-sync to Colab)
- [x] Git-based workflow
- [ ] Direct file management
- [ ] CI/CD pipeline

### Project Structure

Leave blank — use the default **Research / Analysis** folder structure, plus:
```
richmond-public-health-snapshot/
├── notebooks/
│   ├── 01_cdc_places_download.ipynb
│   ├── 02_census_acs_download.ipynb
│   ├── 03_health_analysis.ipynb
│   └── 04_composite_index.ipynb
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

**Primary Success Criteria**: Successfully download CDC PLACES and Census ACS data for Richmond metro jurisdictions, compare health indicators across localities, generate a composite health index, and produce a report connecting health outcomes to social determinants.
**Quantitative Metrics**: At least 6 health indicators compared across 4 jurisdictions plus state and national benchmarks (40 measures available in PLACES 2025 — expand as needed); composite index scores calculated; at least 5 publication-quality visualizations including radar chart and scatter plot.
**Qualitative Goals**: Reports use person-first language; findings frame disparities as opportunities not deficits; all health indicators contextualized with socioeconomic data; report suitable for a community health needs assessment.

### Domain and Context

**Domain**: Public Health / Community Health Assessment / Health Equity
**Your Experience Level**: Beginner — learning Python and data analysis as I go
**Special Considerations**: Must use person-first language throughout. Never make individual clinical recommendations. Distinguish between age-adjusted and crude rates. Frame health disparities constructively. Connect findings to social determinants of health framework. Never draw causal conclusions from cross-sectional data.

### Known Challenges

**Technical Challenges**: CDC PLACES API response format (CSV vs JSON options); Census API query syntax for specific variables; aligning PLACES measure definitions across years; creating composite indices from different scales.
**Data Challenges**: CDC PLACES uses model-based small area estimates (not direct surveys) — the 2025 release methodology uses BRFSS data, ACS data, and Census population counts with Monte Carlo simulation; age-adjusted vs crude rate confusion; different time periods for PLACES vs ACS data; suppression for small geographies; not all states participate in every BRFSS module so some health-related social needs measures may have gaps.
**Environment Challenges**: Google Drive sync timing between local edits and Colab availability; Census API key management.
**External Dependencies**: Census API key (free, instant signup at https://api.census.gov/data/key_signup.html). CDC PLACES API is public and free — data portal at https://www.cdc.gov/places/tools/data-portal.html

### Collaboration

**Working Style**: Solo (workshop learning project)
**Version Control**: Git
**Branch Strategy**: Main only

---

## SECTION B: WHAT TO GENERATE

Generate all of the following. Follow the design principles in Section C exactly.

---

### TIER 1: Core Files

---

#### 1. CLAUDE.md — The Map (60-100 lines MAXIMUM)

**MUST include:**
- Project name + 1-2 sentence description
- Tech stack (one line)
- Abbreviated folder structure (5-10 lines max)
- Current phase / status (one line)
- The IMPORTANT block (see below)
- List of docs/ files with 1-line descriptions
- 2-3 critical gotchas: age-adjusted vs crude rates, PLACES model-based estimates vs direct survey, person-first language
- Context management reminders
- Reference to MEMORY.md
- Note that Claude Code also has auto memory (`/memory` to manage) — complements MEMORY.md

**Required: The IMPORTANT block:**
```markdown
## IMPORTANT: Read Before Working
Before starting any task, identify which docs below are relevant and read them first.
- `docs/setup.md` — Environment setup, CDC PLACES API, Census API key, Google Drive junction
- `docs/architecture.md` — Three-layer architecture (Think → Compute → Interpret)
- `docs/gotchas.md` — PLACES data caveats, Census API quirks, rate type confusion, equity framing
- `docs/colab-workflow.md` — Notebook structure, Drive mounting, output handling
- `docs/conventions.md` — Code patterns, naming, person-first language requirements, context management

For complex multi-file work: start in Plan Mode (Shift+Tab×2), create a task list, then switch to Normal Mode to execute. Use /effort high for methodology and equity framing decisions.
```

---

#### 2. MEMORY.md — The Index (50-100 lines MAXIMUM)

Standard lightweight index structure.

---

#### 3. ATOMIC_PLAN.md — Initial Task Breakdown

**Epics for this project:**
- E1: Environment Setup (Drive junction, packages, Census API key, test both APIs)
- E2: Data Pipeline — CDC PLACES (download Richmond metro data, parse, clean)
- E3: Data Pipeline — Census ACS (download socioeconomic indicators, parse, clean)
- E4: Health Analysis (compare across jurisdictions, state/national benchmarks, radar charts)
- E5: Composite Index (normalize indicators, weight, calculate composite scores)
- E6: Social Determinants (merge health + socioeconomic data, scatter plots, correlation analysis)
- E7: Reporting (community health assessment narrative, dashboard)

Include Plan Mode usage note at top.

---

#### 4. WORK_PROGRESS.md — Progress Dashboard

---

### TIER 2: Progressive Disclosure Docs (docs/)

---

#### 5. docs/setup.md — Environment Setup
- Python environment setup
- Package installation: `pip install pandas plotly matplotlib requests geopandas streamlit`
- Census API key signup: https://api.census.gov/data/key_signup.html
- Store key in .env file (add .env to .gitignore)
- CDC PLACES API test: curl example for measure data endpoint (data portal: https://www.cdc.gov/places/tools/data-portal.html — use SODA API for programmatic access)
- Census ACS API test: curl example for Virginia county income data
- Google Drive junction setup
- Sandbox configuration
- Verification checklist

---

#### 6. docs/architecture.md — System Design
- Three-layer architecture diagram
- Data flow: CDC PLACES API + Census ACS API → raw data → cleaned DataFrames → merged dataset → analysis → visualizations → community health report
- Two parallel data pipelines that merge at the analysis stage
- Google Drive junction explanation

---

#### 7. docs/gotchas.md — Known Pitfalls
- Age-adjusted vs crude rates (NEVER present interchangeably)
- CDC PLACES uses model-based small area estimates, not direct survey data
- The 2025 PLACES release expanded to 40 measures (from 36 in 2023) — verify measure IDs match the release year you're querying
- Not all states participate in every BRFSS module, so some newer measures (health-related social needs) may have geographic gaps
- Census ACS margins of error (always check MOE for small geographies)
- FIPS code formatting (leading zeros matter)
- Variable name lookup for Census API (use the variables list endpoint)
- PLACES measure IDs vs descriptive names
- Different time periods: PLACES release year vs data year vs ACS vintage year
- Person-first language requirements (see conventions.md)
- Composite index normalization: min-max vs z-score implications
- Ecological fallacy: never attribute area-level findings to individuals

---

#### 8. docs/conventions.md — Code Patterns and Context Management

**Code conventions section:**
- Naming: snake_case, include FIPS codes in filenames, always timestamp outputs
- Data conventions: always carry FIPS, jurisdiction name, and data year through pipelines
- Language conventions: person-first language in ALL outputs ("people with diabetes" not "diabetics")
- Framing conventions: frame disparities as opportunities, never deficit framing

**Context management section (standard v2.2):**
- /clear between tasks, Plan Mode for complex work, /rewind, /compact
- Effort levels: /effort low (quick lookups) | /effort medium (Opus 4.6 default) | /effort high (methodology design, equity framing decisions)

**Workflow section:**
- Default: Explore → Plan → Implement → Commit
- For analysis: define indicators → download data → clean/merge → analyze → visualize → report

---

#### 9. docs/colab-workflow.md — Colab + Google Drive Workflow
Standard notebook structure with CDC PLACES and Census ACS API helper functions, output saving.

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
description: Create Jupyter/Colab notebooks for CDC PLACES and Census ACS health analysis. Use when creating new notebooks or analysis scripts for the Richmond public health project.
allowed-tools: Read, Write, Bash, Grep, Glob
---
```

Template with Drive mounting, imports, CDC PLACES and Census API helpers, FIPS lookup functions, output saving.

---

#### 12. Public Health Snapshot Skill

**Path**: `.claude/skills/public-health-snapshot/SKILL.md`

```yaml
---
name: public-health-snapshot
description: Build a community health profile using CDC PLACES and Census ACS data. Use when asked about health indicators, disparities, community health, social determinants, or health equity in the Richmond metro area.
allowed-tools: Read, Write, Bash, Grep, Glob
---
```

Include:
- Data sources: CDC PLACES API (chronic disease prevalence), Census ACS 5-Year (socioeconomic)
- Geographies: Richmond City (51760), Henrico (51087), Chesterfield (51041), Hanover (51085)
- Health indicators: diabetes, obesity, mental health, healthcare access, smoking, physical inactivity
- Socioeconomic indicators: median income, insurance coverage, education, poverty rate
- Analysis steps: download → clean → compare across jurisdictions → benchmark vs state/national → composite index → social determinants scatter → narrative report
- Output format: health indicators CSV, comparison charts, radar chart, composite scores CSV, scatter plots, markdown narrative
- Quality standards: always report confidence intervals, compare to benchmarks, cross-reference health + socioeconomic data, use person-first language, frame as opportunities

Also create supporting files:
- `.claude/skills/public-health-snapshot/templates/health-assessment.md` — Executive summary, health indicators, social determinants, composite index, recommendations
- `.claude/skills/public-health-snapshot/examples/good-finding.md` — Example using person-first language, benchmarks, nuance, actionable framing
- `.claude/skills/public-health-snapshot/examples/bad-finding.md` — Example with deficit framing, no context, causal language from cross-sectional data
- `.claude/skills/public-health-snapshot/data-dictionary.md` — CDC PLACES measures (40 in 2025 release across 6 categories), Census ACS variables, FIPS codes for Richmond metro, rate types (age-adjusted vs crude), confidence intervals, BRFSS module participation notes

---

#### 13. Atomic Planner Skill (standard)

---

#### 14. Session Closer Skill (standard)

---

#### 15. Python Debugger Skill

**Path**: `.claude/skills/python-debugger/SKILL.md`

```yaml
---
name: python-debugger
description: Debug Python errors including API connection failures, Census API query syntax errors, pandas merge issues, plotly rendering problems, and Colab runtime errors. Use when encountering errors, crashes, or unexpected behavior.
allowed-tools: Read, Bash, Grep, Glob
---
```

Include common errors for Census API (bad variable names, FIPS formatting), CDC PLACES response parsing, and pandas merge/join pitfalls.

---

### TIER 4: Hooks (.claude/settings.json)

---

#### 16. .claude/settings.json

Same 5-hook structure as previous templates (PostToolUse formatter, Notification, PreToolUse security, SessionEnd logging, PreCompact backup). Python/black formatter.

---

### TIER 5: Custom Agents (.claude/agents/)

---

#### 17. Clinical Data Reviewer Agent

**Path**: `.claude/agents/clinical-reviewer.md`

```yaml
---
name: clinical-reviewer
description: Clinical data reviewer for public health analysis. Use proactively for CDC PLACES data interpretation, health equity analysis, community health assessments, social determinants, and disparity identification.
tools: Bash, Read, Write, Grep, Glob
model: sonnet
permissionMode: acceptEdits
skills: public-health-snapshot
---
```

System prompt should include:
- Expertise in CDC PLACES and BRFSS datasets, social determinants of health frameworks, epidemiological measures (prevalence, incidence, rates), health equity analysis
- Communication style: evidence-based and measured, sensitive to human impact, person-first language always, frame findings as opportunities not deficits
- Decision rules: always report confidence intervals, compare to state and national benchmarks, cross-reference health with socioeconomic data
- Constraints: NEVER make individual clinical recommendations, NEVER use stigmatizing language, NEVER present age-adjusted and crude rates interchangeably, NEVER draw causal conclusions from cross-sectional data

---

#### 18. Test Writer Agent (standard)

---

### TIER 6: Slash Commands (.claude/commands/)

#### 19-21. Standard commands: next-task.md, complete-task.md, status.md

---

### TIER 7: Utility Scripts, Config, and Templates

---

#### 22. .gitignore — Python + Colab customized. Include .env for Census API key.
#### 23. README.md
#### 24. requirements.txt
```
pandas>=2.0
plotly>=5.0
matplotlib>=3.7
requests>=2.28
geopandas>=0.14
streamlit>=1.30
python-dotenv>=1.0
black>=23.0
```

#### 25. memory/ folder structure (standard)

---

### Rules (.claude/rules/)

#### 26. .claude/rules/healthcare-ethics.md
- NEVER make individual clinical recommendations or diagnoses
- NEVER suggest treatment plans for specific patients
- NEVER present AI analysis as substitute for clinical judgment
- NEVER use identifiable patient data in any analysis
- All data must be publicly available or de-identified
- Distinguish AI-generated content from verified facts
- Use hedging language ("suggests" not "proves")
- When health data affects real communities, frame with empathy
- Acknowledge when a question is beyond data analysis scope

#### 27. .claude/rules/data-privacy.md
- Public data (BLS, CDC, Census): can be used freely
- Never include individual names in outputs
- Aggregate all results to jurisdiction level or higher
- When sample sizes are small, suppress to prevent identification

#### 28. .claude/rules/output-standards.md
- Self-check: numbers match source, percentages correct, date ranges stated, no unsupported claims
- Non-specialist readability requirement
- Technical terms defined on first use
- Visualizations have clear labels and titles
- Limitations and caveats stated

#### 29. .claude/rules/health-equity.md (additional rule for this project)
- ALWAYS use person-first language ("people with diabetes" not "diabetics", "people experiencing homelessness" not "the homeless")
- NEVER use deficit-based framing for communities ("underserved" is acceptable; "deficient" or "lacking" is not)
- ALWAYS frame health disparities as systemic/structural issues, not individual failures
- NEVER draw causal conclusions from cross-sectional ecological data
- NEVER present age-adjusted and crude rates interchangeably — always label which type
- ALWAYS note that CDC PLACES estimates are model-based, not direct survey results (methodology uses BRFSS, ACS, and Census data with MRP and Monte Carlo simulation)
- When comparing jurisdictions, provide structural context (funding, access, policy) not just numbers
- NEVER attribute area-level health data to individuals (ecological fallacy)

---

## SECTION C: DESIGN PRINCIPLES

Same 8 principles as previous templates (Progressive Disclosure, Context Efficiency, Deterministic Over Advisory, Let Native Systems Work, Specialist Agents, Be Specific, Build for Growth, Project-Type Awareness).

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
- [ ] All code uses Python + pandas + plotly + CDC PLACES + Census APIs — zero placeholders
- [ ] .claude/rules/ contains healthcare-ethics.md, data-privacy.md, output-standards.md, health-equity.md
- [ ] Person-first language used in ALL example outputs and templates
- [ ] Only Research/Analysis conditional sections generated

---

## BEGIN GENERATION

Create all files now, starting with CLAUDE.md. Everything specific to Richmond public health community assessment — no generic placeholders, no TODOs.

Start with CLAUDE.md.
