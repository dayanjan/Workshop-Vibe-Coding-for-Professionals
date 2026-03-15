# Vibe Coding for Healthcare Professionals

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)

**Building Repeatable AI Workflows with Claude Code**

Workshop materials from the [AI Ready RVA](https://aireadyrva.com) session at VCU School of Pharmacy, Laboratory of Digital Health — March 14, 2026.

## What Happened

13 professionals — from healthcare and pharmacy to finance, government IT, and consulting — built their first AI workflow harnesses in 60 minutes using Claude Code. Zero coding experience required.

The breakthrough moment: attendees pasted a single template (`BUILD-THIS-PROJECT.md`) into Claude Code, which generated a complete project scaffolding (CLAUDE.md, skill, agent, rule, and folder structure). After restarting Claude Code, the generated CLAUDE.md loaded automatically — and the AI remembered everything.

## Quick Start

1. **Install Claude Code**: `winget install Anthropic.ClaudeCode` (Windows) or `brew install claude-code` (macOS)
2. **Pick a starter project** from `starter-projects/` and open the folder in VS Code
3. **Start Claude Code** — open the terminal (Ctrl+\`) and type `claude`
4. **Copy the contents of `BUILD-THIS-PROJECT.md`** and paste it into Claude Code
5. **Wait ~15 minutes** — Claude generates your project, then restart Claude Code so it loads the new CLAUDE.md

## Repository Contents

| Directory | What's Inside | How to Use |
|-----------|--------------|------------|
| `starter-projects/` | 3 standalone project folders, each with a `BUILD-THIS-PROJECT.md` template | Pick one, open in VS Code, paste template into Claude Code |
| `completed-examples/` | What each project looks like after Claude builds it (CLAUDE.md, skill, agent, rule) | Compare your output or use as a fallback |
| `reference-materials/full-templates/` | Full v2.2 templates (~500-600 lines, ~28 files each) | Take-home for deeper projects |
| `reference-materials/workshop-guide/` | Complete workshop reference guide (.md, .docx, .pdf) | Comprehensive walkthrough of Claude Code project architecture |
| `presentation/` | Opening presentation slides | 30-minute overview of the workflow harness concept |

## The Three Use Cases

| Use Case | Data Source | Agent | What It Builds |
|----------|-----------|-------|----------------|
| Richmond Workforce Analysis | BLS QCEW API | research-analyst | Employment trends, industry growth charts |
| Grant Funding Landscape | NIH Reporter API | grant-writer | Funding analysis, strategic positioning for investigators |
| Public Health Snapshot | CDC PLACES + Census ACS | clinical-reviewer | Community health profile, composite health index |

All three use the same 5-file harness pattern. Different data, different agents — same architecture.

## The 5-File Harness

Every starter template generates exactly 5 things:

| File | Purpose | Analogy |
|------|---------|---------|
| `CLAUDE.md` | Project memory — auto-loaded every session | Onboarding doc for a new team member |
| `.claude/skills/*/SKILL.md` | Step-by-step workflow | Standard Operating Procedure |
| `.claude/agents/*.md` | Specialist persona with expertise and constraints | Job description + scope of practice |
| `.claude/rules/*.md` | Guardrails the AI cannot break | Compliance requirements |
| Folder structure | Where data, outputs, and code live | Filing system |

> "Think of it as writing onboarding documents for an AI team member — once written, they persist across every session." — Anthropic, Claude Code Documentation

## Prerequisites

- [VS Code](https://code.visualstudio.com/)
- [Claude Code](https://code.claude.com/docs/en/overview) — requires Anthropic API key or Claude Pro/Max subscription
- Google Account (optional — for Google Drive junction and Colab)

## Workshop Team

- **Dr. Dayanjan S. Wijesinghe** — AI Ready RVA, VCU School of Pharmacy, Laboratory of Digital Health
- **Ms. Mora Alabi, PharmD Candidate** — VCU School of Pharmacy

## Resources

- [Claude Code Documentation](https://code.claude.com/docs/en/overview)
- [Claude Code Skills](https://code.claude.com/docs/en/skills)
- [Claude Code Subagents](https://code.claude.com/docs/en/sub-agents)
- [BLS QCEW Open Data](https://www.bls.gov/cew/additional-resources/open-data/)
- [NIH Reporter API](https://api.reporter.nih.gov/)
- [CDC PLACES](https://www.cdc.gov/places/)

## License

© 2026 Dayanjan S. Wijesinghe. Licensed under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/).

You are free to share and adapt these materials for non-commercial purposes with attribution.
