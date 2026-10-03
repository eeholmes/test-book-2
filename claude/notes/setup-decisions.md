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

## Antigravity (agy) setup decisions (Issue #12)

Antigravity instructions are integrated alongside Claude Code in `setup.qmd` using panel tabsets for tool-specific steps (step 5 and step 8).

Why and what's deliberate:

- **Launcher over plain `agy`:** Out of the box, `agy` prompts before running *every* shell command, making normal coding impossible without constant interruptions. The team launcher at `~/shared/agent-coders/agy-agent-coders` (source: `agent-coders-clinics` repo `hub/agy-agent-coders`) pre-approves safe everyday tools (`ls`, `cat`, `grep`, `mkdir`, `touch`, `R`, `Rscript`, `quarto`, `python`, `python3`, `git`, read-only `gh`, `curl`) and sets `defaultMode: accept-edits`.
- **Gzip install fix:** Upstream install script (`curl -fsSL https://antigravity.google/cli/install.sh | bash`) fails on the hub because the server returns gzipped content uncompressed; the launcher handles installation using `curl --compressed`.
- **First start sign-in:** First start installs `agy` and prompts for Google OAuth ("click to authenticate"), followed by pasting the Google Cloud project code from Jira, and accepting 'Agent Platform'.
- **Guards:** The launcher installs an agy hook (`agy-agent-coders --hook`) blocking `git reset --hard`, force pushes without lease, `git clean -f`, and recursive deletions (`rm -r`) outside the project root. Blocked commands report `agent-coders guard:`.
- **Project folder boundary:** Users must `cd` into their project repository before starting `agy-agent-coders` because `agy` takes the launch directory as the project root and `rm -r` boundary.
- **Why approvals still appear:** Unlisted commands (copying, moving, deleting files with `rm`, `pip`, or chained commands with an unlisted segment) intentionally prompt for confirmation.
- **Hub constraints:** `agy --sandbox` fails because hub containers do not allow nested unprivileged user namespaces. Non-interactive `agy -p` stops at the first command needing confirmation.

## Setup and Activity 1 reorganization (Issue #13)

- **Setup page streamlined:** Repository creation and first agent launch were moved out of `setup.qmd` into Activity 1 (`content/activity-repo-analysis.qmd`) where participants actually work on their practice repository.
- **Tabset consistency:** In `setup.qmd`, the tool-specific setup step, "Good to know", and "If something goes wrong" all use panel tabsets separating Claude Code from Antigravity.
- **Activity 1 startup:** In `content/activity-repo-analysis.qmd`, participants create their repository from the template using `gh repo create my-quarto-book --template nmfs-opensci/NOAA-quarto-book --public --clone` and launch their chosen agent with tabbed instructions for `claude-agent-coders` vs `agy-agent-coders`. (Issue #10 moved `gh repo create` into the `gh auth login` tab; see below.)



## GitHub access via fine-grained token (Issue #10)

Eli chose (2026-10-03) to offer two options in a tabset in Activity 1, token
first (default tab): a fine-grained token scoped to the practice repo, or
`gh auth login` for people fine with the agent doing anything they can on GitHub.
Goal of the token: the agent works on the practice repo without the hub holding a
credential for private work-organization repos.

- **Considered and rejected: `gh-scoped-creds`.** It is installed on the hub and
  configured (`GH_SCOPED_CREDS_CLIENT_ID`, app
  `nmfs-openscapes-github-push-access`), but that GitHub App is owned by
  2i2c-org and has only `contents: write` + `metadata: read`, so `gh pr` /
  `gh issue` (Skills 100 workflow) would fail, and it only wires up git, not
  `gh`. A self-owned app with PR/Issues permissions would fix that; Eli chose the
  PAT instead.
- **The whole GitHub flow lives in Activity 1**, not Setup. In the token tab the
  repo is created on the website ("Use this template") *before* the token;
  `gh repo create` cannot be used there — a selected-repositories token cannot
  create repos. The `gh auth login` tab keeps `gh repo create --template --clone`.
- **Logging out matters**, not just skipping login: a stored OAuth token in
  `~/.config/gh/hosts.yml` stays readable to the agent even when `GH_TOKEN` is set.
  `gh auth logout` refuses while `GH_TOKEN` is set (checked), hence
  `env -u GH_TOKEN gh auth logout ...` in Troubleshooting.
- **Permissions:** Contents, Pull requests and Issues all read/write, because
  Skills 100's CLAUDE.md prompt has the agent create issues, open and merge PRs,
  and delete branches. Issue #10 said grant PR/Issues only if exercises use them;
  they do.
- **Launchers, not plain `claude`:** issue #10's snippet ends with `claude`; the
  guide uses `claude-agent-coders` / `agy-agent-coders`. Both `exec` the CLI, so
  `GH_TOKEN` is inherited. The agent must start in the same terminal.
- **Checked in a clean HOME:** `gh auth setup-git` works with only `GH_TOKEN`
  (no stored login) and the git credential helper hands git that token; it also
  writes an empty `helper =` that overrides other helpers for github.com.
  **Not yet checked with a real token:** clone/push, PR/issue creation, and that
  a private org repo is refused.
