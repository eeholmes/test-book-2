# Handoff — 2026-09-28

## What was done

First draft of the Agent Coders Clinic participant guide — a Quarto book with 12 chapters across 4 parts. All content written, all PRs merged to main, book renders cleanly.

### Book structure (12 chapters)

1. **Welcome & Overview** (`index.qmd`)
2. **Setup & Connection** (`content/setup.qmd`) — adapted from participant-quickstart.md
3. **Models & Budget** (`content/models-and-budget.qmd`)
4. **What Is Agentic Coding?** (`content/what-is-agentic-coding.qmd`) — concepts only
5. **How to Work with an Agent** (`content/how-to-work-with-an-agent.qmd`) — workflow discipline with Mermaid flowchart
6. **Activity: Edit a Quarto Book** (`content/activity-repo-analysis.qmd`) — 3-phase hands-on exercise
7. **Skills 100: Telling the Agent How You Work** (`content/skills-100.qmd`) — global CLAUDE.md with copy-paste prompt
8. **Skills 101: Clear–Handoff–Notes** (`content/skills-101.qmd`)
9. **Skills 102: SKILLS.md** (`content/skills-102.qmd`)
10. **Skills 103: Checking the Agent's Work** (`content/skills-103.qmd`) — verification via domain knowledge, real data, breaking things
11. **Tool Comparison** (`content/tool-comparison.qmd`)
12. **Troubleshooting** (`content/troubleshooting.qmd`)

### Key decisions made

- HTML output only for now (dropped PDF/docx until content stabilizes)
- `/resume` acknowledged but discouraged — handoff notes preferred, especially for gaps and team handoffs
- Verification (Skills 103) framed honestly: you're the domain expert, not the code reviewer. Give the agent real data and constraints, let it break its own work.
- Skills 100 uses a copy-paste prompt so participants don't have to write CLAUDE.md by hand
- Activity is the template itself (NOAA-quarto-book) — participants fork, clone, and practice the full clear/handoff/notes cycle

## What's left

- **Review and polish** — first drafts throughout, could tighten prose and check consistency
- **Eli's intro content** — chapter 4 has a placeholder mention of Eli's ~20 min intro; may need updating once his material is ready
- **Activity repos** — chapter 6 says "pick a public repo" but doesn't suggest specific ones
- **Skills 102 examples** — SKILLS.md chapter has generic examples, could use project-specific ones
- **Skills 103** — marked as a bit of a placeholder, could expand with concrete worked examples
- **Test the full activity flow** — walk through the 3-phase exercise end-to-end before the clinic
- **`notes/plan.md`** is now outdated — reflects the original plan, not the current state

## Source material

- Participant quickstart: https://github.com/nmfs-opensci/agent-coders-clinics/blob/main/docs/participant-quickstart.md
- Template repo participants will fork: https://github.com/nmfs-opensci/NOAA-quarto-book
