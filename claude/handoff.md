# Handoff — 2026-10-03

## Latest (2026-10-03): Antigravity instructions added (Issue #12)

Added instructions for participants using Google Antigravity (`agy`) on JupyterHub via the team launcher `~/shared/agent-coders/agy-agent-coders`. Setup page now features tabsets for Claude Code vs Antigravity at steps 5 and 8. Tool Comparison and Troubleshooting updated with Antigravity details, commands, and safeguards. See `claude/notes/setup-decisions.md`.

## Previous (2026-09-29): Setup rewritten for the hub (PR #9, merged)

The old Setup page described manual gateway env vars; participants actually use the shared hub script. Setup, Troubleshooting and Models & Budget now follow the hub flow. Why and what's deliberate: `claude/notes/setup-decisions.md`.

## What was done (first draft, 2026-09-28)

First draft of the Agent Coders Clinic participant guide — a Quarto book with 12 chapters across 4 parts. All content written, all PRs merged to main, book renders cleanly.

### Book structure (12 chapters)

1. **Welcome & Overview** (`index.qmd`)
2. **Setup** (`content/setup.qmd`) — hub workflow; see `claude/notes/setup-decisions.md`
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
- **Eli's intro content** — chapter 4 has a placeholder mention of Eli's ~20 min intro; may need updating once that material is ready
- **Activity repos** — chapter 6 says "pick a public repo" but doesn't suggest specific ones
- **Skills 102 examples** — SKILLS.md chapter has generic examples, could use project-specific ones
- **Skills 103** — marked as a bit of a placeholder, could expand with concrete worked examples
- **Test the full activity flow** — walk through the 3-phase exercise end-to-end before the clinic
- **`claude/notes/plan.md`** is now outdated — reflects the original plan, not the current state
- **Walk the Setup steps on a fresh hub account** — not done yet; `/model` with an open model through Claude Code also untested
- **Tool Comparison** updated to cover both hub launchers (`claude-agent-coders` and `agy-agent-coders`)
- **Antigravity instructions (issue #12)** — drafted and integrated into `setup.qmd`, `tool-comparison.qmd`, and `troubleshooting.qmd` on branch `issue-12-antigravity-instructions`.


## Source material

- Hub participant steps (source of truth for Setup): `~/agent-coders-issuer/docs/hub-quickstart.md`
- Manual gateway setup (other tools, own machine): `~/agent-coders-issuer/docs/participant-quickstart.md`
- Current model list: `~/agent-coders-issuer/models.yaml`
- Template repo participants will fork: https://github.com/nmfs-opensci/NOAA-quarto-book
