# Vibe Coding for Professionals

## Building AI Workflows with Claude Code

### Workshop Reference Guide

**Dr. Dayanjan Wijesinghe**
**Ms. Mora Alabi, PharmD Candidate**

AI Ready RVA | VCU School of Pharmacy
March 14, 2026

---

> **💡 About This Document**
>
> This guide provides a complete walkthrough of the Claude Code project architecture, three use cases with skill and agent templates, and a Streamlit demo application. All directory structures follow Anthropic's recommended conventions for Claude Code projects. Updated with verified errata as of workshop morning.

---

## Workshop Agenda

Saturday, March 14, 2026 | 10:00 AM – 2:00 PM | VCU School of Pharmacy

| Time | Session | What You'll Experience |
|------|---------|----------------------|
| 10:00 – 10:15 | Welcome and Introductions | Meet your fellow attendees, overview of the day, and why moving beyond the chat interface matters |
| 10:15 – 10:45 | The Workflow Harness | Understand the 5 components that make AI repeatable: CLAUDE.md, skills, agents, rules, and folder structure |
| 10:45 – 11:15 | Live Demo: The Full Pipeline | Watch a complete workflow: brainstorming in Claude Code, building a skill, generating a Colab notebook through the Google Drive junction, and interpreting results — all using Richmond workforce data |
| 11:15 – 12:15 | Hands-On: Build Your First Project | Open your starter project in VS Code, paste BUILD-THIS-PROJECT.md into Claude Code, and build your first agent, skill, and rule files. Personalized help from Dr. Wijesinghe and Ms. Alabi |
| 12:15 – 12:45 | Lunch Break | Informal discussion, compare what you've built, ask questions |
| 12:45 – 1:45 | Hands-On: Extend and Iterate | Refine your project based on what worked and what didn't. Add a second skill, improve your agent, or connect to the Google Drive junction. See the iterative loop in action |
| 1:45 – 2:00 | Show and Tell + Next Steps | Share what you built, see how others approached it, Q&A, resources for continuing on your own |

> **💡 What to Have Ready**
>
> VS Code installed and open, Claude Code authenticated in your terminal (type "claude" to verify), and a Google account for the Drive junction demo. If you're not set up yet, let us know during introductions and we'll help you get started.

---

## Section 1: Core Concepts

### What Is a Claude Code Project?

A Claude Code project is a structured directory that gives AI persistent memory, reusable skills, specialized agents, and behavioral rules. Instead of repeating instructions every session, you encode your workflows as Markdown files that Claude Code reads automatically. Think of it as writing onboarding documents for an AI team member — once written, they persist across every session.

**The key insight:** most of this is plain Markdown. If you can write a clinical protocol, a grant narrative, or an onboarding document for a new hire, you can build a Claude Code project. The AI reads your instructions the same way that new team member would.

### The Three-Layer Architecture

The workflow demonstrated in this workshop operates across three layers:

| Layer | Tool | Purpose |
|-------|------|---------|
| Think | VS Code + Claude Code | Brainstorm, plan, write, interpret |
| Compute | Google Colab via Drive | Data download, ML, heavy analysis |
| Interpret | Claude Code (return loop) | Analyze outputs, draft reports, iterate |

Claude Code serves as the single orchestration point. You stay in your VS Code terminal and direct work across all three layers. Claude Code generates Colab notebooks, pushes them through the Google Drive junction, and pulls results back for interpretation. You never switch tools.

### The Google Drive Junction

The "junction" is a shared Google Drive folder that bridges your local VS Code environment and Google Colab's cloud compute:

1. Claude Code writes a Colab notebook (.ipynb) based on your skill instructions.
2. The notebook is saved to a designated Google Drive folder.
3. You open and run the notebook in Google Colab (free GPU/TPU access).
4. Outputs (CSV files, charts, model results) are saved back to Google Drive.
5. Claude Code reads those outputs and helps you interpret, report, or iterate.

> **💡 No Server Required**
>
> This architecture requires zero infrastructure setup. Google Drive is the glue. You don't need to deploy anything, configure servers, or manage databases. Everything runs on free tools.

---

## Section 2: Anatomy of a Claude Code Project

Claude Code uses a specific directory convention defined by Anthropic. Understanding this structure is essential — it's what makes skills discoverable, agents invocable, and rules automatically loaded. Everything lives under a `.claude/` directory in your project root, alongside a `CLAUDE.md` file.

### Official Project Structure

```
my-project/
├── CLAUDE.md              ← Project memory (auto-read at startup)
├── CLAUDE.local.md        ← Personal overrides (gitignored)
├── .claude/
│   ├── settings.json      ← Permissions, model, hooks config
│   ├── settings.local.json← Personal settings (gitignored)
│   ├── rules/             ← Behavioral rules & guardrails
│   │   ├── healthcare-ethics.md
│   │   ├── data-privacy.md
│   │   └── output-standards.md
│   ├── skills/            ← Reusable workflows (each in own dir)
│   │   ├── workforce-analysis/
│   │   │   ├── SKILL.md       ← Required: YAML frontmatter + instructions
│   │   │   ├── templates/
│   │   │   └── examples/
│   │   ├── literature-review/
│   │   ├── grant-landscape/
│   │   └── public-health-snapshot/
│   ├── agents/            ← Specialized sub-agents
│   │   ├── research-analyst.md
│   │   ├── grant-writer.md
│   │   └── clinical-reviewer.md
│   └── .mcp.json          ← External tool integrations
├── data/
├── figures/
├── reports/
└── notebooks/
```

At the user level (applies to all your projects):

```
~/.claude/
├── CLAUDE.md          ← Your global preferences (all projects)
└── skills/            ← Skills available in every project
```

> **💡 Hierarchy and Precedence**
>
> Claude Code reads CLAUDE.md files recursively from your working directory up to the root. More specific locations take precedence: local > project > global. Your project's CLAUDE.md overrides ~/.claude/CLAUDE.md for project-specific rules. CLAUDE.local.md is for personal preferences that shouldn't be shared with a team.

### Component 1: CLAUDE.md (Project Memory)

This is the most important file. Claude Code automatically reads CLAUDE.md at the project root when it starts. It tells the AI what the project is, what conventions to follow, and where to find its skills and agents. Keep it concise and high-signal — Anthropic recommends keeping CLAUDE.md under 200 lines, with 20–80 lines being ideal for most projects.

```markdown
# CLAUDE.md

## Project
Richmond Workforce Analysis for AI Ready RVA workshop.

## Key Conventions
- Save all Colab notebooks to Google Drive: AI_Workshop/notebooks/
- Save all outputs to Google Drive: AI_Workshop/outputs/
- Follow rules in .claude/rules/ at all times
- When uncertain, ask me rather than guessing
- Use plain language accessible to non-data-scientists

## Common Commands
- Run analysis: use the workforce-analysis skill
- Switch agents: use /research-analyst or /grant-writer
- Generate notebook: save .ipynb to Drive notebooks/ folder
```

> **⚠️ Keep CLAUDE.md Lean**
>
> CLAUDE.md is loaded into context every session. Don't dump everything here. Use it for project-level orientation and conventions. Detailed procedures go in skills. Behavioral constraints go in rules. Domain expertise goes in agents. Each component has its proper home.

### Component 2: Skills (.claude/skills/)

Skills are reusable workflows that define how to do specific tasks. Each skill lives in its own directory under `.claude/skills/` and must contain a `SKILL.md` file. The SKILL.md file has two parts: YAML frontmatter (between `---` markers) that tells Claude when to use the skill, and Markdown content with the actual instructions.

Skills load on demand — Claude reads them when relevant, not at startup. This means you can have dozens of skills without bloating your context. Claude can also discover skills automatically based on their description in the frontmatter, or you can invoke them explicitly with `/skill-name`. Keep SKILL.md under 500 lines; move detailed reference material to separate files within the skill directory.

Additional frontmatter options include: `allowed-tools` (grant the agent specific tool access when the skill is active), `model` (specify which Claude model to use), `disable-model-invocation: true` (only you can invoke the skill, not Claude autonomously), and `user-invocable: false` (only Claude can invoke it, useful for background knowledge).

#### Skill Example: Workforce Analysis

`.claude/skills/workforce-analysis/SKILL.md`

```yaml
---
name: workforce-analysis
description: Analyze Richmond MSA workforce data from BLS
  public APIs. Use when asked about employment trends,
  industry growth, or wage data for the Richmond area.
---
```

```markdown
## Objective
Analyze Richmond MSA workforce data from BLS public APIs.

## Data Sources
- BLS Quarterly Census of Employment and Wages (QCEW)
- BLS Occupational Employment and Wage Statistics (OEWS)
- BLS Current Employment Statistics (CES)
- Richmond MSA FIPS code: 40060

## Important: QCEW Data Format Update (Dec 2025)
BLS changed the presentation of MSA data in QCEW as of
December 2025. The CSV column layout and area codes may
differ from pre-2025 examples. Use the current QCEW Open
Data Access docs: https://www.bls.gov/cew/additional-resources/open-data/

## Analysis Requirements
1. Download the most recent available QCEW data for
   Richmond MSA (FIPS: 40060)
2. Calculate year-over-year employment change by industry
3. Identify top 10 growing and declining industries
4. Generate visualizations: bar charts for growth,
   treemap for industry composition
5. Save all outputs as CSV and PNG to the outputs/ folder

## Output Format
- Summary statistics as CSV
- Visualizations as PNG files
- Brief narrative summary as markdown

## Quality Standards
- Always cite data sources with dates and geography
- Include national comparison when available
- Flag data suppression or known limitations
```

#### Skill Example: Literature Review

`.claude/skills/literature-review/SKILL.md`

```yaml
---
name: literature-review
description: Conduct a structured literature review on a
  specified topic using PubMed and Google Scholar. Use when
  asked to review evidence, find papers, or summarize research.
---
```

```markdown
## Process
1. Clarify the research question with the user
2. Develop search terms (MeSH terms + keywords)
3. Search PubMed API for relevant articles (last 5 years)
4. Screen titles and abstracts for relevance
5. Summarize top 15-20 articles in structured format
6. Identify themes, gaps, and contradictions
7. Generate a narrative synthesis

## Output Format
- Search strategy documentation (terms, databases, filters)
- Article summary table (author, year, design, key findings)
- Thematic analysis with supporting citations
- Identified gaps suitable for future research

## Quality Standards
- Prioritize systematic reviews and RCTs when available
- Note study limitations alongside findings
- Flag potential publication bias
```

#### Skill Example: Grant Landscape Analysis

`.claude/skills/grant-landscape/SKILL.md`

```yaml
---
name: grant-landscape
description: Analyze federal health research funding using
  NIH Reporter API. Use when asked about grants, funding
  trends, or research opportunities in Virginia.
---
```

```markdown
## Objective
Analyze federal health research funding awarded to Virginia
institutions using NIH Reporter API.

## Data Sources
- NIH Reporter API (https://api.reporter.nih.gov/)
- Fields: project title, PI, institution, funding amount,
  NIH institute, fiscal year, study section

## Analysis Requirements
1. Query NIH Reporter for all active awards to Virginia
   institutions in the last 3 fiscal years
2. Aggregate total funding by institution and by NIH
   institute (e.g., NHLBI, NCI, NIMH)
3. Identify trending research topics via keyword frequency
4. Compare Virginia funding to national benchmarks
5. Generate: funding by institution, by NIH institute,
   and trend lines over time

## Output Format
- Aggregated data as CSV
- Visualizations as PNG
- Top 20 funded institutions table
- Keyword frequency analysis
```

#### Skill Example: Public Health Snapshot

`.claude/skills/public-health-snapshot/SKILL.md`

```yaml
---
name: public-health-snapshot
description: Build a community health profile using CDC
  PLACES and Census data. Use when asked about health
  indicators, disparities, or community health in Richmond.
---
```

```markdown
## Data Sources
- CDC PLACES API (chronic disease prevalence estimates)
  Note: The 2025 PLACES release includes 40 measures across
  6 categories including health-related social needs (new in
  2024). See https://www.cdc.gov/places/methodology/index.html
- Census ACS 5-Year (socioeconomic indicators)

## Analysis Requirements
1. Download CDC PLACES data for Richmond City and
   surrounding counties (Henrico, Chesterfield, Hanover)
2. Extract: diabetes, obesity, mental health, access to
   care, smoking rates, physical inactivity (core set)
   Consider additional measures from the expanded 40-measure
   set, especially health-related social needs
3. Compare Richmond metro to Virginia and US averages
4. Pull ACS data for income, insurance, education
5. Generate composite health index per jurisdiction
6. Visualizations: comparison bars, radar chart, scatter

## Output Format
- Health indicators summary as CSV
- Comparison charts as PNG
- Composite index scores as CSV
```

> **💡 Skills Can Bundle Supporting Files**
>
> A skill directory can contain more than SKILL.md. You can include templates/ for output formats, examples/ for few-shot samples, data-dictionaries/ for domain terminology, and scripts/ for executable code. Claude reads these on demand when the skill is invoked. This keeps your context lean while providing deep expertise when needed.

### Skill Supporting Files

Each skill directory can contain supporting files that Claude reads when the skill is invoked. These keep detailed reference material out of the main SKILL.md while making it available on demand.

#### Templates (Output Format Specs)

`.claude/skills/workforce-analysis/templates/analysis-report.md`

```markdown
## Report Structure

### Executive Summary (150-200 words)
- Key finding in one sentence
- 2-3 supporting data points
- Primary recommendation

### Background
- Why this analysis matters
- What data was used and its timeframe

### Methods
- Data sources with URLs
- Analysis approach (keep non-technical)
- Limitations or caveats

### Findings
- Organize by theme, not chronologically
- Lead each subsection with the insight, then evidence
- Include one visualization per major finding

### Recommendations
- Numbered, actionable, specific
- Each tied to a finding above
```

#### Examples (Few-Shot Learning)

Examples are one of the most powerful components. By showing what good output looks like — and what bad output looks like — you calibrate quality more effectively than pages of instructions.

**Good example:**

```
"Healthcare employment in the Richmond MSA grew 10.2% between
2023 and 2025, adding approximately 4,600 jobs. This outpaced
the national healthcare growth rate of 6.1% over the same
period. Growth was concentrated in ambulatory care services
(NAICS 621), which accounted for 62% of new positions.
However, hospitals (NAICS 622) saw flat employment,
suggesting a shift toward outpatient care models consistent
with national trends."
```

*Why this is good:* Leads with specific finding and magnitude, provides national comparison, breaks down aggregate into meaningful subcategories, notes an important nuance, connects data to a broader trend.

**Bad example:**

```
"Healthcare employment has been growing in Richmond. The
numbers show positive trends across several indicators."
```

*Why this is bad:* No specific numbers or percentages, no time period specified, no comparison or context, vague language, states the obvious without adding insight.

#### Data Dictionaries (Domain Terminology)

```markdown
## Key Terms
- MSA: Metropolitan Statistical Area
- Richmond MSA FIPS: 40060
- QCEW: Quarterly Census of Employment and Wages
- OEWS: Occupational Employment and Wage Statistics
- NAICS: North American Industry Classification System

## Common NAICS Codes for Richmond
- 62: Healthcare and Social Assistance
- 52: Finance and Insurance
- 54: Professional, Scientific, and Technical Services
- 92: Government

## Data Quirks
- BLS suppresses data when sample size is too small
- QCEW uses establishment counts, not headcounts
- Annual averages lag by ~9 months
- QCEW MSA data format changed Dec 2025 (see BLS notices)
```

### Component 3: Agents (.claude/agents/)

Agents are specialized sub-agents that Claude Code can spawn for focused tasks. Each agent is a Markdown file in `.claude/agents/` with YAML frontmatter (between `---` markers) that defines metadata, followed by the system prompt in Markdown. When invoked, the agent runs in its own isolated context — separate from the main conversation — and returns its results. Think of agents as different hats your AI wears.

You can create agents manually as Markdown files, or use the `/agents` command for an interactive guided setup.

#### Built-in Agents (Always Available)

Before creating custom agents, know that Claude Code ships with three built-in agents you can use immediately without creating any files:

| Agent | Model | Tools | Use For |
|-------|-------|-------|---------|
| Explore | Haiku (fast) | Read, Grep, Glob, Bash (read-only) | Fast codebase search, file analysis, answering questions about existing code |
| Plan | Sonnet | Read, Grep, Glob, Bash | Research during Plan Mode, analyzing dependencies before making changes |
| General-purpose | Sonnet | All tools | Complex multi-step tasks that Claude delegates automatically |

> **⚠️ Don't Recreate Built-in Agents**
>
> A common mistake is creating a custom "researcher" or "explorer" agent that duplicates the built-in Explore agent. The built-in version is faster (Haiku), safer (read-only), and already integrated. Only create custom agents for domain-specific expertise that the built-in agents don't have.

#### Agent: Research Analyst

`.claude/agents/research-analyst.md`

```yaml
---
name: research-analyst
description: Workforce research analyst for Richmond MSA
  employment data. Use for BLS data analysis, industry
  trends, and economic development questions.
model: sonnet
tools: Read, Grep, Glob, Bash, Write
---
```

```markdown
You are a workforce research analyst helping professionals
understand employment trends in the Richmond, Virginia
metropolitan area.

## Expertise
- Bureau of Labor Statistics data (QCEW, OEWS, CES, JOLTS)
- Regional economic development patterns
- Statistical analysis and data visualization
- Translating data into actionable insights

## Communication Style
- Professional but accessible
- Assume the reader is intelligent but not a data scientist
- Lead with the insight, then show the evidence
- Use plain language; define technical terms on first use
- When presenting numbers, always include context
  (e.g., "12% growth, compared to 3% nationally")

## Decision Rules
- Always cite data sources with dates and geography
- Flag when data may be outdated or have known limitations
- If a finding is surprising, double-check the underlying data
- Present options with trade-offs, not single answers
- Default to conservative interpretations of ambiguous data

## Constraints
- Never make predictions without stating assumptions
- Never present correlation as causation
- Never extrapolate beyond the data without flagging it
```

#### Agent: Grant Writing Strategist

`.claude/agents/grant-writer.md`

```yaml
---
name: grant-writer
description: Grant writing strategist for federal funding
  analysis. Use for NIH, NSF, and federal grant strategy,
  Specific Aims drafting, and funding opportunity analysis.
model: opus
tools: Read, Grep, Glob, Bash, Write
---
```

> **Workshop starter version:** The simplified starter template uses `model: sonnet` for faster generation during the hands-on session. Use `opus` for production grant writing work where quality is paramount.

```markdown
You are a grant writing strategist who helps researchers
identify funding opportunities and develop compelling
grant narratives.

## Expertise
- NIH grant mechanisms (R01, R21, K-awards, T32, P-series)
- NSF funding structures
- Federal grant databases (NIH Reporter, USAspending)
- Specific Aims page structure and narrative strategy

## Communication Style
- Direct and strategic
- Mirror the language of successful funded applications
- Use active voice and strong topic sentences
- Be concise: reviewers read hundreds of applications

## Decision Rules
- Always verify current funding opportunity announcements
- Match investigator strengths to mechanism requirements
- Flag potential conflicts with eligibility criteria early
- Prioritize significance and innovation sections

## Constraints
- Never fabricate preliminary data or citations
- Never write boilerplate that could apply to any project
- Never ignore page limits or formatting requirements
```

#### Agent: Clinical Data Reviewer

`.claude/agents/clinical-reviewer.md`

```yaml
---
name: clinical-reviewer
description: Clinical data reviewer for public health
  analysis. Use for CDC PLACES data, health equity
  analysis, and community health assessments.
model: sonnet
tools: Read, Grep, Glob
---
```

> **Workshop starter version:** The simplified starter template gives the clinical-reviewer full tool access (`Read, Write, Bash, Grep, Glob`) for ease of use during the hands-on session. The restricted tool set above is the recommended production configuration.

```markdown
You are a clinical data reviewer who analyzes public
health datasets and generates community health assessments.

## Expertise
- CDC PLACES and BRFSS datasets
- Social determinants of health frameworks
- Epidemiological measures (prevalence, incidence, rates)
- Health equity analysis and disparity identification

## Communication Style
- Evidence-based and measured
- Sensitive to the human impact behind the numbers
- Use person-first language
- Frame findings as opportunities, not deficits

## Decision Rules
- Always report confidence intervals when available
- Compare local data to state and national benchmarks
- Cross-reference health indicators with socioeconomic data

## Constraints
- Never make individual-level clinical recommendations
- Never use stigmatizing language about health conditions
- Never present age-adjusted and crude rates interchangeably
- Never draw causal conclusions from cross-sectional data
```

> **💡 One Project, Multiple Agents**
>
> Notice that the clinical-reviewer agent only has Read, Grep, and Glob tools — it can analyze but never accidentally modify files. The grant-writer uses Opus for maximum quality on high-stakes writing. These configurations are set once in the frontmatter and apply every time the agent runs. Use the /agents command to create and manage agents interactively.

### Component 4: Rules (.claude/rules/)

Rules are behavioral guardrails that apply across all skills and agents. They define what the AI must never do. While skills guide behavior and agents shape persona, rules constrain both. Files in `.claude/rules/` are automatically loaded based on path — they don't need to be explicitly referenced.

#### Rule: Healthcare Ethics

```markdown
# .claude/rules/healthcare-ethics.md

## Absolute Rules
- NEVER make individual clinical recommendations or diagnoses
- NEVER suggest treatment plans for specific patients
- NEVER present AI analysis as a substitute for clinical judgment
- NEVER use identifiable patient data in any analysis
- NEVER claim certainty about clinical outcomes

## Data Handling Rules
- All data used must be publicly available or de-identified
- Flag any dataset that might contain PII/PHI
- Do not merge datasets in ways that could re-identify individuals
- State the data source, date, and known limitations for every analysis

## Communication Rules
- Always distinguish AI-generated content from verified facts
- Use hedging language for uncertain findings ("suggests" not "proves")
- When health data affects real communities, frame with empathy
- Acknowledge when a question is beyond data analysis scope
```

#### Rule: Data Privacy

```markdown
# .claude/rules/data-privacy.md

## Data Classification
- Public data (BLS, CDC, Census): can be used freely
- Institutional data: verify de-identification before use
- Patient/individual data: NEVER process through this pipeline

## Output Rules
- Never include individual names in analysis outputs
- Aggregate all results to jurisdiction level or higher
- When sample sizes are small, suppress to prevent identification
```

#### Rule: Output Standards

```markdown
# .claude/rules/output-standards.md

## Self-Check Before Presenting Output
- [ ] All numbers match the source data
- [ ] Percentages are calculated correctly
- [ ] Date ranges and geographies are stated
- [ ] No claims made without supporting data
- [ ] A non-specialist could understand the main finding
- [ ] Technical terms are defined on first use
- [ ] Visualizations have clear labels and titles
- [ ] Limitations and caveats are stated
- [ ] Guardrail rules have been followed
```

> **⚠️ Rules Are Non-Negotiable**
>
> Unlike skills which guide behavior, rules constrain it. If a skill says "be creative with visualizations" but a rule says "never fabricate data," the rule wins. Always build rules before giving agents more autonomy.

### How Components Work Together

| Component | Location | Answers | Analogy |
|-----------|----------|---------|---------|
| CLAUDE.md | Project root | What is this project? | Project charter |
| Skill | .claude/skills/*/SKILL.md | How do I do this task? | Standard operating procedure |
| Agent | .claude/agents/*.md | Who am I for this task? | Job description + persona |
| Rule | .claude/rules/*.md | What must I never do? | Compliance manual |
| Template | Inside skill directory | What should output look like? | Report template |
| Example | Inside skill directory | What does good work look like? | Sample deliverables |
| Data Dict | Inside skill directory | What do these terms mean? | Glossary / codebook |

---

## Section 3: Environment Setup

### VS Code

Download from https://code.visualstudio.com/ and install for your operating system (Windows, Mac, or Linux). Recommended extensions: Python, Jupyter, Markdown Preview.

### Claude Code (Terminal Tool)

Claude Code is Anthropic's command-line AI tool that runs directly in your terminal:

```bash
# macOS (recommended)
brew install claude-code

# Windows (recommended)
winget install Anthropic.ClaudeCode

# Verify installation
claude --version

# Start Claude Code in your project directory
cd your-project-folder
claude
```

> **⚠️ npm Installation Is Deprecated**
>
> Earlier versions of this guide referenced `npm install -g @anthropic-ai/claude-code`. That method is deprecated as of March 2026. Use the native installers above — they auto-update. If you previously installed via npm, uninstall first: `npm uninstall -g @anthropic-ai/claude-code`

You will need an Anthropic API key or a Claude Pro/Max subscription to authenticate.

### Google Drive and Colab Setup

1. Create a folder in Google Drive called `AI_Workshop`.
2. Inside it, create two subfolders: `notebooks/` and `outputs/`.
3. Open Google Colab (colab.research.google.com) and verify you can mount your Drive.

### Initialize Your Project

Claude Code has a built-in `/init` command that generates a starter CLAUDE.md by scanning your project structure:

```bash
# Create your project directory
mkdir richmond-workforce && cd richmond-workforce

# Create the .claude directory structure
mkdir -p .claude/skills/workforce-analysis
mkdir -p .claude/skills/literature-review
mkdir -p .claude/skills/grant-landscape
mkdir -p .claude/skills/public-health-snapshot
mkdir -p .claude/agents
mkdir -p .claude/rules
mkdir -p data/raw data/processed figures reports notebooks src

# Start Claude Code and initialize
claude
# Then type: /init
```

---

## Section 4: Use Case Walkthroughs

### Use Case 1: Richmond Workforce Analysis

This use case demonstrates the full think-compute-interpret loop using the research-analyst agent and the workforce-analysis skill.

**Note:** BLS changed the presentation of MSA data in QCEW in December 2025. The CSV column layout or area codes may look different from pre-2025 examples found online. Use the current QCEW Open Data Access documentation at https://www.bls.gov/cew/additional-resources/open-data/

#### Brainstorm

```
You: I want to analyze the Richmond, Virginia workforce
landscape. Use the research-analyst agent. What are the
most interesting questions we could answer using publicly
available BLS data?
```

#### Generate the Notebook

```
You: Using the workforce-analysis skill, create a Colab
notebook that downloads BLS QCEW data for Richmond
and runs the full analysis. Save it to my Google Drive
notebooks/ folder.
```

Claude Code reads the SKILL.md, references the data dictionary and templates within the skill directory, and generates a complete .ipynb file with Drive mounting, API calls, analysis, and visualization — all shaped by the research-analyst agent's communication style.

#### Interpret

```
You: The notebook has finished. Read the outputs from Drive
and summarize key findings using the analysis-report
template.
```

> **💡 See the Pattern?**
>
> The agent shaped the communication style. The skill defined the analysis steps. The template structured the output. The rules in .claude/rules/ prevented overstatements. The data dictionary provided domain vocabulary. Each component played its role.

### Use Case 2: Grant Funding Landscape

Same architecture, different agent. The grant-writer agent interprets the same kind of data through a strategic lens — focused on opportunities and positioning rather than just describing trends.

```
You: Use the grant-writer agent with the grant-landscape
skill. Generate a Colab notebook that queries NIH Reporter
for Virginia health research awards.

... (after running) ...

You: Read the outputs. Which NIH institutes fund the most
research in Virginia? Where might a new investigator
find less competition?
```

Because the grant-writer agent is active, the interpretation focuses on strategic positioning and suggests specific mechanisms (R21 for exploratory, K-awards for early career) tailored to the findings.

### Use Case 3: Richmond Public Health Snapshot

The clinical-reviewer agent brings epidemiological rigor — correctly distinguishing between age-adjusted and crude rates, framing health disparities constructively, and connecting findings to social determinants frameworks.

**Note:** The 2025 PLACES release now includes 40 measures across 6 categories (up from the 6 core indicators listed in the skill). The new categories include health-related social needs. The 6 indicators in the skill template are still valid starting points, but you may want to explore the expanded set.

```
You: Use the clinical-reviewer agent with the
public-health-snapshot skill. Build a community health
profile for Richmond metro.
```

> **💡 Cross-Domain Application**
>
> These three use cases share identical architecture. The workforce skill adapts for any BLS-driven analysis. The grant skill works for NSF, DoD, or SBA funding. The public health skill works for any CDC PLACES geography. Attendees from any sector can adapt these by modifying the skill's data source and the agent's domain expertise.

---

## Pro Tips: Getting More from Claude Code

### Controlling Reasoning Depth

Claude Code gives you two ways to control how deeply it reasons before acting: the `/effort` command (preferred) and natural-language thinking keywords (still supported).

**The `/effort` command** is now the primary control. Opus 4.6 defaults to medium effort for Max and Team subscribers.

| Command | Level | When to Use |
|---------|-------|-------------|
| `/effort low` | Low | Quick lookups, simple edits, routine tasks |
| `/effort medium` | Medium (default) | Most analysis work, standard generation |
| `/effort high` | High | Complex analytical decisions, system-wide analysis, critical research design |

**Natural-language keywords** still work as a secondary method, especially mid-prompt:

| Phrase | Thinking Level | When to Use |
|--------|---------------|-------------|
| "think" | Standard | Default reasoning — most tasks |
| "think hard" | Elevated | Multi-file changes, unfamiliar data sources |
| "think harder" | High | Complex analytical decisions, methodology design |
| "ultrathink" | Maximum | System-wide analysis, critical research design |

*Example: "Think hard about which BLS data series best captures gig economy trends in Richmond, then create the analysis plan."*

> **💡 If Output Seems Less Thorough Than Expected**
>
> Opus 4.6 defaults to medium effort, not high. For complex tasks like methodology design or multi-source analysis, explicitly run `/effort high` at the start of your session.

### Auto Memory

In addition to the manual CLAUDE.md approach taught in this workshop, Claude Code now has auto memory — it automatically saves useful context (build commands, debugging insights, architecture notes, preferences) to `~/.claude/projects/<project>/memory/` without you writing anything.

- Auto memory is on by default (v2.1.59+)
- Use `/memory` to browse and manage saved memories
- The first 200 lines of auto memory are loaded at session start
- You can still use CLAUDE.md for explicit instructions — both systems work together

The manual approach (CLAUDE.md, skills, agents, rules) is still the right thing to learn because it gives you deliberate control. Auto memory handles the implicit learning that accumulates over time.

### The Four-Phase Workflow

Anthropic's recommended pattern for complex work follows four phases: Explore (understand the problem and data), Plan (design the approach), Implement (execute the work), Commit (save checkpoints). Start each session from a clean state. If a task touches multiple files or data sources, begin in exploration before jumping to implementation.

### Built-in Explore Agent

When you ask Claude Code a question about your project or data, it often delegates to the built-in Explore agent — a fast, read-only sub-agent running on Haiku. You don't need to configure this; it happens automatically. For deeper research, you can say "Use subagents to investigate this thoroughly" and Claude will delegate appropriately.

---

## Section 5: Streamlit Demo Application

The final piece demonstrates that this workflow can produce interactive applications, not just analysis files. The Streamlit app is provided as a separate Python file (`richmond_workforce_app.py`). It includes metric cards, interactive growth charts, an industry treemap, a wage-vs-growth scatter plot, and a filterable data table.

```bash
pip install streamlit pandas plotly
streamlit run richmond_workforce_app.py
```

**The key message:** you don't ask Claude Code to "build a Streamlit app." You ask it to "turn the workforce analysis into something my team can explore." The skill and agent handle the rest.

---

## Section 6: Hands-On Guide for Attendees

### Your First Project (30 Minutes)

#### Phase 1: Brainstorm (10 minutes)

1. Open VS Code and create a new folder for your project.
2. Open the terminal and type: `claude`
3. Describe a recurring task in your work. Be specific about inputs, analysis, and outputs.
4. Have a 5-minute conversation. Let Claude Code help refine the problem.

#### Phase 2: Build the Structure (15 minutes)

**Workshop shortcut:** Instead of building manually, paste the contents of `BUILD-THIS-PROJECT.md` (included in your starter project folder) into Claude Code. It will generate all 5 files automatically in about 15 minutes.

1. Ask Claude Code to create the `.claude/` directory structure.
2. Create your first agent — run `/agents` in Claude Code for guided setup, or manually write a file in `.claude/agents/` with YAML frontmatter (name, description, tools, model) and a system prompt.
3. Write your first skill in `.claude/skills/your-skill/SKILL.md` — include the YAML frontmatter with name and description, then the steps, data sources, and output format.
4. Add one rule in `.claude/rules/` — what should the AI absolutely never do in your domain?
5. Create `CLAUDE.md` at the project root with a brief project description and conventions.

#### Phase 3: Test and Iterate (5 minutes)

1. Restart Claude Code (it reads CLAUDE.md automatically).
2. Ask it to perform the task. Evaluate the output.
3. Refine the agent, skill, or rules based on what worked and what didn't.

> **💡 The Iteration Is the Learning**
>
> Your first project won't be perfect. Each refinement teaches you how to write better instructions — which is the core skill you're developing. This is not about becoming a programmer. It's about becoming an effective communicator with AI systems.

### Project Ideas by Profession

| Role | Agent + Skill Idea | Start With |
|------|-------------------|------------|
| Healthcare | Evidence reviewer agent + PubMed literature review skill | Agent defining clinical evidence standards |
| Mental Health | Community needs analyst agent + CDC PLACES skill | Rule file for sensitive health data |
| Pharmacy | Drug info specialist agent + FDA database skill | Data dictionary for pharmacology terms |
| Consulting | Market analyst agent + industry data skill | Template for client-ready reports |
| Finance | Compliance analyst agent + regulatory tracking skill | Rule file for financial advice restrictions |
| HR | Talent market analyst agent + BLS JOLTS skill | Examples of good vs. bad benchmarking |
| IT / Gov | Procurement analyst agent + RFP evaluation skill | Output standards rule with scoring rubric |
| Higher Ed | Institutional researcher agent + IPEDS skill | Context in CLAUDE.md with institutional mission |

---

## Section 7: Resources and Next Steps

### Key Links

- Claude Code docs: https://code.claude.com/docs/en/overview
- Claude Code skills: https://code.claude.com/docs/en/skills
- Claude Code memory: https://code.claude.com/docs/en/memory
- Claude Code best practices: https://code.claude.com/docs/en/best-practices
- Claude Code settings reference: https://code.claude.com/docs/en/settings
- Claude Code agent teams: https://code.claude.com/docs/en/agent-teams
- VS Code: https://code.visualstudio.com/
- Google Colab: https://colab.research.google.com/
- BLS Data: https://www.bls.gov/data/
- BLS QCEW Open Data: https://www.bls.gov/cew/additional-resources/open-data/
- NIH Reporter API: https://api.reporter.nih.gov/
- CDC PLACES: https://www.cdc.gov/places/
- Streamlit: https://streamlit.io/

### Extending Your Project

- Add new skills for adjacent tasks (e.g., add grant-writing skill to a research project).
- Chain skills: literature review → gap analysis → specific aims draft.
- Share `.claude/` directories with colleagues via Git — they're just Markdown.
- Build domain-specific skill libraries for your team.
- Create new agents for different audiences (technical report vs. executive summary).
- Use `~/.claude/CLAUDE.md` for preferences that apply to all your projects.

### The AGIL Framework

The AGIL (AI-Guided Inquiry Learning) framework, developed by Dr. Wijesinghe, uses this same architecture for education. AGIL skills guide students through structured inquiry where AI serves as a mediated learning partner. The skills define the inquiry path, the agent ensures pedagogically sound guidance, and the rules prevent the AI from simply giving answers. Contact Dr. Wijesinghe for information about implementing AGIL.

---

*Thank you for attending Vibe Coding for Professionals. The project you build today is the beginning — the real value compounds as you refine, extend, and share your workflows.*

**AI Ready RVA | March 14, 2026 | VCU School of Pharmacy**
