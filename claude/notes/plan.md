# Documentation Plan: Agent Coders Clinic — Participant Guide

## What This Is

A Quarto book for participants of the NMFS Openscapes "agent coders" clinics. Clinics run on a sandboxed JupyterHub. Participants use AI coding agents (Claude Code, OpenCode, Copilot CLI, Gemini CLI, etc.) through a shared LiteLLM gateway — no AWS account or AI subscription needed.

**Audience:** NOAA/NMFS scientists and staff, mixed experience levels. Some have used agentic tools; for others this is brand new. That's fine.

**Scope:** Participant-facing only. Organizer/infra docs stay in the source repo. No connection to private or confidential NOAA code — this is a learning environment.

---

## Proposed Book Sections

### Part 1: Getting Started

1. **Welcome & Overview** (`index.qmd`)
   - What the clinic is
   - What you'll do: learn a workflow for working with AI coding agents
   - The sandboxed JupyterHub environment

2. **Setup & Connection** (`content/setup.qmd`)
   - Gateway URL + personal key (from organizer)
   - Setting environment variables
   - Connecting your tool (Claude Code, OpenCode, Copilot CLI)
   - Verifying it works
   - Adapted from `participant-quickstart.md`

3. **Models & Budget** (`content/models-and-budget.qmd`)
   - Available models and relative costs
   - Switching models and when to use which
   - Checking remaining budget
   - Making your budget last

### Part 2: What Is Agentic Coding?

4. **What It Is** (`content/what-is-agentic-coding.qmd`)
   - Eli's intro (~20 min): what is an "agentic harness" (Claude Code, Copilot CLI, Gemini CLI, OpenCode, etc.)
   - How it differs from chat-based AI or autocomplete
   - The agent loop: prompt → read/search → edit → run → repeat
   - These tools give the model access to your filesystem, terminal, and git

5. **Group Activity: Repo Reproducibility Analysis** (`content/activity-repo-analysis.qmd`)
   - The activity: point an agent at a public GitHub repo and have it analyze reproducibility
   - What to ask, what to look for
   - Discussion prompts for the group

### Part 3: Agent Skills

6. **Agent Skills 101: The Clear-Handoff-Notes Workflow** (`content/skills-101.qmd`)
   - **The core habit**: `/clear` to reset context, handoff notes to preserve it
   - Why: agents don't remember between sessions. Huge memory files are not the answer — instead, keep a lightweight `notes/` directory with what the agent needs to pick up where it left off.
   - The workflow:
     1. Start a task — agent reads `notes/` for context
     2. Do the work
     3. Before ending — tell the agent to write a handoff note to `notes/`
     4. `/clear` (or close the session)
     5. Next session — agent reads `notes/` and continues
   - What goes in handoff notes: what was done, what's next, any decisions made
   - What does NOT go in handoff notes: entire file contents, code dumps, things the agent can just read from the repo
   - Branches and PRs as a secondary concept: a natural complement to this workflow, but the clear/handoff/notes cycle is the essential habit

7. **Agent Skills 102: SKILLS.md** (`content/skills-102.qmd`)
   - What SKILLS.md is and what it does
   - Writing reusable skills for your project
   - Examples

### Part 4: Reference

8. **Tool Comparison** (`content/tool-comparison.qmd`)
   - Quick-reference: Claude Code vs. OpenCode vs. Copilot CLI vs. Gemini CLI
   - Key commands for each

9. **Troubleshooting** (`content/troubleshooting.qmd`)
   - Budget exceeded / key expired
   - Connection errors
   - Agent not reading files
   - Open-model quirks

---

## Content Sources

- `docs/participant-quickstart.md` from `nmfs-opensci/agent-coders-clinics` — setup, models, troubleshooting
- Eli's intro material (to be incorporated)
- Clinic exercises (repo reproducibility activity)

## Open Questions

- What public GitHub repo(s) for the reproducibility analysis activity?
- Does Eli have slides or notes to reference for the "What It Is" section?
- Specific SKILLS.md examples to include?
