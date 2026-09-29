# Setup chapter decisions

Eli said the original Setup page was "completely wrong": it told participants to
export `GATEWAY_URL`, `GATEWAY_KEY` and `ANTHROPIC_*` variables by hand. Clinic
participants never do that. They work on the NMFS Openscapes JupyterHub and run
a shared script that gets a key, installs Claude Code and sets everything.

The steps Eli specified, in order:

1. Log in to GitHub.
2. Go to https://nmfs-openscapes.2i2c.cloud/.
3. Start a server with 4 GB.
4. Open a terminal.
5. Run `~/shared/workshop/claude-agent-coders` and enter the workshop code.
   **Say no to trusting the folder**, then close Claude Code. The first run starts
   in the home directory, and its only job is to install Claude Code and save
   the key. This looks odd but is deliberate.
6. `gh auth login`.
7. Create a repo in the participant's own account from the template
   `nmfs-opensci/NOAA-quarto-book` (`gh repo create ... --template ... --clone`).
8. In a new terminal, `cd` into that repo and run `claude-agent-coders`. Trust it
   this time.

Details:

- The script path is `~/shared/workshop/claude-agent-coders`. An older
  `~/shared/agent-coders/claude-tester` also exists on the hub; it is not the one
  to document.
- The short name `claude-agent-coders` only works in terminals opened after the
  first run (the script adds `~/.local/bin` to PATH in login files).
- Budget checks use `claude-agent-coders --budget`; a new workshop uses `--reset`.
  The `curl .../key/info` recipe was removed from the book because hub users
  have no `GATEWAY_*` variables.
- The model table follows `~/agent-coders-issuer/models.yaml`; `deepseek-v3.2`
  was dropped from the gateway.
- Source of truth for these steps: `~/agent-coders-issuer/docs/hub-quickstart.md`.
