# Completed Examples

These folders show exactly what your project should look like **after** Claude Code processes a starter template. Use them to check your work or as a reference if you get stuck.

## What's Inside Each Folder

Each completed example contains the 5 files that Claude Code generates from a starter template:

```
project-name/
├── CLAUDE.md                          ← Project memory (auto-loaded every session)
├── .claude/
│   ├── skills/skill-name/SKILL.md     ← Analysis workflow with steps and data sources
│   ├── agents/agent-name.md           ← Specialist persona and constraints
│   └── rules/rule-name.md             ← Behavioral guardrails
├── data/
│   ├── raw/                           ← Downloaded source data goes here
│   └── processed/                     ← Cleaned analysis-ready data goes here
├── figures/                           ← Charts and visualizations go here
├── reports/                           ← Narrative summaries go here
├── notebooks/                         ← Jupyter/Colab notebooks go here
└── src/                               ← Python source code goes here
```

## The Three Examples

| Folder | Skill | Agent | Rule |
|--------|-------|-------|------|
| `richmond-workforce-analysis/` | workforce-analysis | research-analyst | data-ethics |
| `grant-funding-landscape/` | grant-landscape | grant-writer | grant-integrity |
| `richmond-public-health-snapshot/` | public-health-snapshot | clinical-reviewer | health-equity |

## How to Use These

- **During the workshop**: Compare your Claude-generated output to these examples
- **If stuck**: Copy a completed example folder, open it in VS Code, and start Claude Code — it will read the CLAUDE.md and be ready to work immediately
- **To learn**: Read the SKILL.md and agent files to understand how skills and agents are structured

## Note

These are the **starter** output (5 files). The full templates in `03-reference-materials/full-templates/` generate ~28 files including docs, multiple skills, hooks, commands, and a memory system.
