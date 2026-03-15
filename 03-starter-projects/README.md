# Starter Projects

Each folder is a standalone project. Pick one, open it in VS Code, and let Claude Code build it out.

## How to Use

1. **Download** (or copy) one of the project folders below to your computer
2. **Open the folder in VS Code** — File → Open Folder → select the project folder
3. **Start Claude Code** — open the terminal in VS Code (Ctrl+`) and type `claude`, or use the Claude Code VS Code extension
4. **Copy the contents of `BUILD-THIS-PROJECT.md`** and paste it into Claude Code
5. **Wait ~15 minutes** — Claude will generate 5 files and your folder structure
6. **Start working** — ask Claude to run the analysis, refine the agent, or add a skill

## The Three Projects

| Folder | Data Source | What You'll Build |
|--------|-----------|-------------------|
| `richmond-workforce-analysis/` | BLS QCEW API | Employment trends and industry growth charts for Richmond MSA |
| `grant-funding-landscape/` | NIH Reporter API | Funding analysis and strategic positioning for Virginia researchers |
| `richmond-public-health-snapshot/` | CDC PLACES + Census ACS | Community health profile with composite index for Richmond metro |

## What Claude Will Generate (5 Files)

Each starter template produces the same 5-file structure — the minimum needed to demonstrate the full Claude Code pattern:

| File | Purpose | Analogy |
|------|---------|---------|
| `CLAUDE.md` | Project memory — auto-loaded every session | Project charter |
| `.claude/skills/*/SKILL.md` | Reusable workflow with steps and data sources | Standard operating procedure |
| `.claude/agents/*.md` | Specialist persona with expertise and constraints | Job description |
| `.claude/rules/*.md` | Behavioral guardrails (what to never do) | Compliance manual |
| Folder structure | Where data, outputs, and code live | Filing system |

## Want to See the Expected Output?

Check `04-completed-examples/` in the parent directory — those folders show exactly what your project should look like after Claude builds it out.

## Ready for More?

After the workshop, use the full templates in `01-workshop-handouts/full-templates/` to generate a complete project with docs, multiple skills, hooks, slash commands, and a memory system (~28 files).
