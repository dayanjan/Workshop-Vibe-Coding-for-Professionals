# Project Documentation Generator v2.2 — PRE-FILLED TEMPLATE
## Use Case 1: Richmond Workforce Analysis
## Vibe Coding for Healthcare Professionals Workshop | March 14, 2026

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

**Project Name**: richmond-workforce-analysis
**Description**: Analyze the Richmond, Virginia metropolitan area workforce landscape using Bureau of Labor Statistics public APIs. Download employment data, calculate industry growth trends, generate visualizations, and produce narrative reports accessible to non-data-scientists.
**Primary Goal**: Build a repeatable analysis pipeline that downloads BLS data for the Richmond MSA, identifies growing and declining industries, and generates publication-ready charts and summaries.
**Timeline**: 4 weeks
**Target Output**: Analysis report with CSV data files, PNG visualizations, and a Streamlit interactive dashboard

### Technical Stack

**Primary Language**: Python
**Core Libraries/Frameworks**:
- pandas (data manipulation)
- plotly (interactive visualizations)
- matplotlib (static charts)
- requests (BLS API calls)
- streamlit (interactive dashboard)

**Special Models/Architectures**: N/A — not applicable for this project type

**APIs and External Services**:
- BLS Quarterly Census of Employment and Wages (QCEW) API
- BLS Occupational Employment and Wage Statistics (OEWS) API
- BLS Current Employment Statistics (CES) API

**Data Sources**:
- BLS public APIs (no API key required for most endpoints)
- Richmond MSA FIPS code: 40060
- NAICS industry classification codes

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
- Estimated runtimes: Setup 2 min | Analysis 5 min | Visualization 3 min

**Sync/Workflow**:
- [x] Google Drive Desktop (auto-sync to Colab)
- [x] Git-based workflow
- [ ] Direct file management
- [ ] CI/CD pipeline

### Project Structure

Leave blank — use the default **Research / Analysis** folder structure, plus:
```
richmond-workforce-analysis/
├── notebooks/
│   ├── 01_data_download.ipynb
│   ├── 02_analysis.ipynb
│   └── 03_visualization.ipynb
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

**Primary Success Criteria**: Successfully download BLS QCEW data for Richmond MSA, calculate year-over-year employment change by industry, and produce a report with clear visualizations.
**Quantitative Metrics**: Data covers at least 3 years; top 10 growing and declining industries identified; at least 4 publication-quality charts generated.
**Qualitative Goals**: Reports are understandable by non-data-scientists; all findings cite data sources with dates and geography; national comparisons included where available.

### Domain and Context

**Domain**: Workforce Economics / Regional Economic Development
**Your Experience Level**: Beginner — learning Python and data analysis as I go
**Special Considerations**: All data must be publicly available (no PII/PHI). Findings should use plain language. Always distinguish between correlation and causation. Frame findings for a policy/workforce development audience.

### Known Challenges

**Technical Challenges**: BLS API response formats can be inconsistent; data suppression for small sample sizes; understanding NAICS codes and industry hierarchy. Note: BLS changed the presentation of MSA data in QCEW in December 2025 — CSV formats may differ from older tutorials found online.
**Data Challenges**: BLS data lags by ~9 months; some industry categories have suppressed values; annual vs. quarterly data alignment.
**Environment Challenges**: Google Drive sync timing between local edits and Colab availability.
**External Dependencies**: None — all BLS APIs are public and free. No API key needed for QCEW. Use the current Open Data Access docs at https://www.bls.gov/cew/additional-resources/open-data/

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
- The IMPORTANT block (see below) — the engine of progressive disclosure
- List of docs/ files with 1-line descriptions
- 2-3 critical gotchas that apply to EVERY task
- Context management reminders: use /clear between unrelated tasks, start complex work in Plan Mode (Shift+Tab×2), use /effort high for complex planning
- Reference to MEMORY.md for session history
- Note that Claude Code also has auto memory (`/memory` to manage) — complements MEMORY.md

**MUST NOT include:**
- Detailed setup instructions (belongs in docs/setup.md)
- Code style guides (Claude learns from your codebase — use linters and hooks instead)
- Long command references (belongs in docs/)
- Architecture deep dives (belongs in docs/architecture.md)
- Debugging guides (belongs in docs/gotchas.md)

**Required: The IMPORTANT block (customize for my project):**
```markdown
## IMPORTANT: Read Before Working
Before starting any task, identify which docs below are relevant and read them first.
- `docs/setup.md` — Environment setup, BLS API access, Google Drive junction
- `docs/architecture.md` — Three-layer architecture (Think → Compute → Interpret)
- `docs/gotchas.md` — BLS data quirks, NAICS codes, suppression rules
- `docs/colab-workflow.md` — Notebook structure, Drive mounting, output handling
- `docs/conventions.md` — Code patterns, naming, and context management

For complex multi-file work: start in Plan Mode (Shift+Tab×2), create a task list, then switch to Normal Mode to execute. Use /effort high for analytical decisions.
```

---

#### 2. MEMORY.md — The Index (50-100 lines MAXIMUM)

Lightweight index pointing to detailed logs. NOT a history dump.

Structure:
- Current Status (one line: phase + what's next)
- Recent Sessions table (Date | Focus | Key Outcome)
- Key Decisions (links to memory/decisions/adr-NNN.md)
- Critical Gotchas Discovered (cross-session learnings)
- For Details section pointing to memory/ subfolders

---

#### 3. ATOMIC_PLAN.md — Initial Task Breakdown

Break my project into atomic tasks for the first 2 weeks. Each task has: unique ID (AT-XXX), action-oriented title, status (Backlog/In Progress/Done), epic, dependencies, 3-5 acceptance criteria, actual commands needed, done criteria.

**Epics for this project:**
- E1: Environment Setup (Drive junction, packages, BLS API test)
- E2: Data Pipeline (QCEW download, parsing, cleaning)
- E3: Analysis (YoY change, top industries, national comparison)
- E4: Visualization (bar charts, treemap, scatter plot)
- E5: Reporting (narrative summary, Streamlit dashboard)

Include a dependency overview showing which tasks can run in parallel.

**IMPORTANT**: Include this note at the top of ATOMIC_PLAN.md:
```markdown
## Using This Plan
For complex work, start in Plan Mode (Shift+Tab×2) and ask Claude to create
a native Task List from this plan. Native task lists persist across context
compaction and support dependency tracking. Toggle the task list with Ctrl+T.
```

---

#### 4. WORK_PROGRESS.md — Progress Dashboard

Milestone timeline, sprint status, success metrics dashboard, completed/in-progress/blocked summary, open questions.

---

### TIER 2: Progressive Disclosure Docs (docs/)

Each file is self-contained. Claude reads them independently when relevant.

---

#### 5. docs/setup.md — Environment Setup
- Python environment setup (venv or conda)
- Package installation: `pip install pandas plotly matplotlib requests streamlit`
- Google Drive junction setup: create AI_Workshop/notebooks/ and AI_Workshop/outputs/ folders
- BLS API test: curl command to verify QCEW endpoint responds (use current Open Data Access: https://www.bls.gov/cew/additional-resources/open-data/)
- Colab Drive mount verification
- Sandbox configuration: recommend running /sandbox and enabling auto-allow mode
- Verification checklist ("run X and expect Y")

---

#### 6. docs/architecture.md — System Design
- ASCII diagram of the three-layer architecture: Think (VS Code + Claude Code) → Compute (Colab via Drive) → Interpret (Claude Code return loop)
- Data flow: BLS API → raw CSV → cleaned DataFrame → analysis outputs → visualizations → report
- Component descriptions for each notebook
- Google Drive junction explanation

---

#### 7. docs/gotchas.md — Known Pitfalls
- 10-15 pitfalls specific to BLS APIs, pandas, plotly, and Colab
- Each: Symptom | Cause | Fix
- Include: BLS data suppression, NAICS hierarchy confusion, QCEW vs CES vs OEWS differences, date formatting, Drive sync delays, Colab session timeouts
- Include: QCEW MSA data presentation changed December 2025 — column layouts and area coding may differ from pre-2025 examples
- Space for new gotchas to be added

---

#### 8. docs/conventions.md — Code Patterns and Context Management

**Code conventions section:**
- Naming: snake_case for files and functions, UPPER_CASE for constants
- Data conventions: always include MSA FIPS in filenames, always timestamp outputs
- Commit message format: "feat: ...", "fix: ...", "data: ..."

**Context management section:**
- Start each task from a clean git state
- Use /clear between unrelated tasks
- Start complex analysis in Plan Mode (Shift+Tab×2)
- Effort levels: /effort low (quick lookups) | /effort medium (default on Opus 4.6 — may need /effort high for complex analysis) | /effort high (methodology design, architecture decisions)
- Compact proactively at ~70% context usage
- Name sessions with /rename early for easy /resume later
- Use /rewind to undo changes if Claude goes off track

**Workflow section:**
- Default workflow: Explore → Plan → Implement → Commit
- For analysis: brainstorm questions → generate notebook → run in Colab → interpret outputs
- For monitoring: use /loop to check if Colab notebook has finished

---

#### 9. docs/colab-workflow.md — Colab + Google Drive Workflow (conditional: Research with notebooks)
- Standard notebook structure (setup cell, imports, data download, analysis, visualization, save outputs)
- Drive mounting pattern
- How to save outputs back to Drive for Claude Code to read
- Checkpoint strategy for long-running notebooks
- Memory management tips for free Colab tier

---

#### 10. docs/plans/ directory

Create an empty `docs/plans/.gitkeep` directory. This is where Plan Mode saves structured plans when configured via settings.json.

---

### TIER 3: Agent Skills (.claude/skills/)

Each skill is a directory with SKILL.md containing YAML frontmatter and markdown instructions.

---

#### 11. Notebook Creator Skill (conditional: Research/Analysis with notebooks)

**Path**: `.claude/skills/notebook-creator/SKILL.md`

```yaml
---
name: notebook-creator
description: Create Jupyter/Colab notebooks with project-standard structure for BLS workforce analysis. Use when creating new notebooks, analysis scripts, or Colab files for the Richmond MSA project.
allowed-tools: Read, Write, Bash, Grep, Glob
---
```

Standard notebook template with: Drive mounting cell, imports (pandas, plotly, matplotlib, requests), BLS API helper functions, output saving to Drive, and cleanup. Use actual BLS endpoints and Richmond MSA FIPS code.

---

#### 12. Workforce Analysis Skill

**Path**: `.claude/skills/workforce-analysis/SKILL.md`

```yaml
---
name: workforce-analysis
description: Analyze Richmond MSA workforce data from BLS public APIs. Use when asked about employment trends, industry growth, wage data, or economic development questions for the Richmond area.
allowed-tools: Read, Write, Bash, Grep, Glob
---
```

Include:
- Data sources: QCEW (FIPS 40060), OEWS, CES
- Analysis steps: download → clean → calculate YoY change → identify top/bottom industries → generate viz
- Output format: CSV summaries, PNG charts, markdown narrative
- Quality standards: cite sources with dates, include national comparison, flag suppression
- Reference to data dictionary and report template

Also create supporting files:
- `.claude/skills/workforce-analysis/templates/analysis-report.md` — Executive summary, background, methods, findings, recommendations structure
- `.claude/skills/workforce-analysis/examples/good-summary.md` — Example with specific numbers, comparisons, nuance
- `.claude/skills/workforce-analysis/examples/bad-summary.md` — Vague example without data
- `.claude/skills/workforce-analysis/data-dictionary.md` — MSA, QCEW, OEWS, NAICS definitions, Richmond NAICS codes, data quirks

---

#### 13. Atomic Planner Skill (all project types)

**Path**: `.claude/skills/atomic-planner/SKILL.md`
Also create `.claude/skills/atomic-planner/references/task-template.md`

```yaml
---
name: atomic-planner
description: Break features into atomic tasks (1-3 hours, single-purpose, testable). Use when planning new work, sprints, or decomposing complex analysis tasks. Also creates native Task Lists for Plan Mode integration.
---
```

---

#### 14. Session Closer Skill (all project types)

**Path**: `.claude/skills/session-closer/SKILL.md`

```yaml
---
name: session-closer
description: Update project memory after a work session. Use at end of session, or when asked to log progress, save learnings, update memory, or close session.
allowed-tools: Read, Write, Grep, Glob
---
```

Process: create session log → update MEMORY.md → record gotchas → update WORK_PROGRESS.md → suggest CLAUDE.md improvements.

---

#### 15. Python Debugger Skill

**Path**: `.claude/skills/python-debugger/SKILL.md`

```yaml
---
name: python-debugger
description: Debug Python errors including pandas DataError, API connection failures, plotly rendering issues, and Colab runtime errors. Use when encountering errors, crashes, or unexpected behavior.
allowed-tools: Read, Bash, Grep, Glob
---
```

Include common error patterns for pandas, requests, plotly, and Colab-specific issues.

---

### TIER 4: Hooks (.claude/settings.json)

---

#### 16. .claude/settings.json

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit|MultiEdit",
        "hooks": [
          {
            "type": "command",
            "command": "bash -c 'FILE=$(jq -r \".tool_input.file_path\" <<< \"$(cat)\"); if [[ \"$FILE\" == *.py ]]; then black --quiet \"$FILE\" 2>/dev/null; fi; exit 0'"
          }
        ]
      }
    ],
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "echo 'Claude needs attention' | tee /dev/stderr"
          }
        ]
      }
    ],
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "bash -c 'CMD=$(jq -r \".tool_input.command\" <<< \"$(cat)\"); for p in \"rm -rf /\" \"rm -rf ~\" \"DROP TABLE\" \"TRUNCATE\" \"--force\" \"push.*--force\"; do if echo \"$CMD\" | grep -qiE \"$p\"; then echo \"BLOCKED: dangerous command pattern detected\" >&2; exit 2; fi; done; exit 0'"
          }
        ]
      }
    ],
    "SessionEnd": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"Session ended at $(date)\" >> .claude/session-log.txt",
            "async": true
          }
        ]
      }
    ],
    "PreCompact": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "bash -c 'mkdir -p .claude/backups && cp -f MEMORY.md .claude/backups/MEMORY-$(date +%Y%m%d-%H%M%S).md 2>/dev/null; exit 0'",
            "async": true
          }
        ]
      }
    ]
  },
  "plansDirectory": "./docs/plans"
}
```

---

### TIER 5: Custom Agents (.claude/agents/)

---

#### 17. Research Analyst Agent

**Path**: `.claude/agents/research-analyst.md`

```yaml
---
name: research-analyst
description: Workforce research analyst for Richmond MSA employment data. Use proactively for BLS data analysis, industry trends, economic development questions, and data interpretation tasks.
tools: Bash, Read, Write, Grep, Glob
model: sonnet
permissionMode: acceptEdits
skills: workforce-analysis
---
```

System prompt should include:
- Expertise in BLS data (QCEW, OEWS, CES, JOLTS)
- Communication style: professional but accessible, lead with insight then evidence, plain language, always include context for numbers
- Decision rules: cite sources, flag limitations, double-check surprising findings, present options not single answers, conservative interpretation
- Constraints: never predict without stating assumptions, never present correlation as causation, never extrapolate without flagging

---

#### 18. Test Writer Agent (all project types)

**Path**: `.claude/agents/test-writer.md`

```yaml
---
name: test-writer
description: Test creation specialist. Writes unit tests for data processing functions and API calls. Use proactively after code changes or when test coverage is needed.
tools: Read, Write, Edit, Bash, Grep, Glob
model: haiku
permissionMode: acceptEdits
---
```

---

### TIER 6: Slash Commands (.claude/commands/)

---

#### 19. .claude/commands/next-task.md
Reviews ATOMIC_PLAN.md, identifies tasks with all dependencies met, recommends highest-priority available task, shows full details. Suggests Plan Mode if task is complex.

#### 20. .claude/commands/complete-task.md
Takes a task ID argument ($ARGUMENTS). Marks task done, updates progress, commits, shows next task.

#### 21. .claude/commands/status.md
Quick dashboard: current phase, sprint progress, blockers, next 3 actions, context usage.

---

### TIER 7: Utility Scripts, Config, and Templates

---

#### 22. .gitignore
Customized for Python + Colab. Include: `.claude/worktrees/`, `.claude/backups/`, `.claude/session-log.txt`, `data/raw/`, `__pycache__/`, `.ipynb_checkpoints/`, `*.pyc`

#### 23. README.md
Project overview, link to docs/setup.md, quick start steps.

#### 24. requirements.txt
```
pandas>=2.0
plotly>=5.0
matplotlib>=3.7
requests>=2.28
streamlit>=1.30
black>=23.0
```

#### 25. memory/ folder structure
- `memory/sessions/.gitkeep`
- `memory/decisions/adr-template.md`
- `memory/patterns.md`

---

### Rules (.claude/rules/) — Healthcare and Data Ethics

Also create these rule files for this project:

#### 26. .claude/rules/healthcare-ethics.md
- NEVER make individual clinical recommendations or diagnoses
- NEVER present AI analysis as substitute for clinical judgment
- All data must be publicly available or de-identified
- Distinguish AI-generated content from verified facts
- Use hedging language ("suggests" not "proves")
- Frame community data with empathy

#### 27. .claude/rules/data-privacy.md
- Public data (BLS, CDC, Census): can be used freely
- Never include individual names in outputs
- Aggregate all results to jurisdiction level or higher
- Suppress small sample sizes to prevent identification

#### 28. .claude/rules/output-standards.md
- Self-check: numbers match source, percentages correct, date ranges stated, no unsupported claims
- Non-specialist readability requirement
- Technical terms defined on first use
- Visualizations have clear labels and titles
- Limitations and caveats stated

---

## SECTION C: DESIGN PRINCIPLES

### Principle 1: Progressive Disclosure
CLAUDE.md is the MAP, not the encyclopedia. Under 100 lines. Details live in docs/. The IMPORTANT block triggers Claude to read docs before working.

### Principle 2: Context Efficiency
Every CLAUDE.md line costs tokens in every session. Be ruthless. MEMORY.md is an index. Use /clear between unrelated tasks.

### Principle 3: Deterministic Over Advisory
Use hooks for rules that must never be broken. Use CLAUDE.md for guidelines.

### Principle 4: Let Native Systems Do the Work
Use built-in Explore agent for codebase research. Use Plan Mode + native Task Lists. Use /sandbox, /loop, /rewind.

### Principle 5: Specialist Agents Over Generalists
One agent per domain. Restrict tools. Use haiku for routine, sonnet for complex.

### Principle 6: Be Specific, Not Generic
All code uses my actual stack. All gotchas target my libraries. No placeholders.

### Principle 7: Build for Growth
Memory grows through session logs. Gotchas grow. New skills can be added.

### Principle 8: Project-Type Awareness
Generate only what's relevant to Research / Analysis. No API routes, no CLI commands, no web components.

---

## SECTION D: OUTPUT FORMAT

### Generation Order
1. CLAUDE.md
2. MEMORY.md
3. .claude/settings.json (hooks + plansDirectory)
4. All docs/ files (including docs/plans/.gitkeep)
5. All .claude/skills/ (each SKILL.md plus references)
6. All .claude/agents/ files
7. All .claude/commands/ files
8. All .claude/rules/ files
9. ATOMIC_PLAN.md
10. WORK_PROGRESS.md
11. .gitignore, README.md, requirements.txt
12. memory/ folder templates

### Quality Checks
- [ ] CLAUDE.md under 100 lines with IMPORTANT block
- [ ] MEMORY.md under 100 lines (index only)
- [ ] .claude/settings.json has all 5 hooks (format, notify, security, SessionEnd, PreCompact)
- [ ] Every SKILL.md has valid YAML frontmatter
- [ ] Every agent .md has valid YAML frontmatter
- [ ] NO custom researcher/explorer agent (use the built-in Explore agent)
- [ ] All code uses Python + pandas + plotly + BLS APIs — zero placeholders
- [ ] .claude/rules/ contains healthcare-ethics.md, data-privacy.md, output-standards.md
- [ ] Only Research/Analysis conditional sections generated

---

## BEGIN GENERATION

Create all files now, starting with CLAUDE.md. Everything specific to Richmond workforce analysis — no generic placeholders, no TODOs.

Start with CLAUDE.md.
