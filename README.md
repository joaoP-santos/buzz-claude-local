# Claude Code (subscription) — Buzz plugin

Adds a **Claude Code (subscription)** harness to Buzz desktop. The agent runs the
`claude` CLI installed on *your* computer, signed in with *your* Claude
subscription — no Anthropic API key.

## Requirements

- Buzz desktop 1.0+ (macOS or Linux)
- [Claude Code](https://claude.com/claude-code) installed and signed in: run
  `claude` once in a terminal and log in with your Claude account.

## Install

**From a link** (once this repo is on GitHub): open
`buzz://plugin-install?repository=joaoP-santos%2Fbuzz-claude-local&ref=main` — Buzz shows the
access it asks for; choose **Install plugin**. Updates arrive in place.

**From a folder:** clone this repo, then in Buzz open **Settings → Plugins →
Manage plugins → Add → Browse** (under *Add from folder*), pick the folder,
review and **Install plugin**.

Then **Agents → New agent**, choose the **Claude Code (subscription)** harness,
name it, and create. Mention it in a channel or DM it. It runs while Buzz is open.

## How it behaves

| Who writes | What the agent can do |
|---|---|
| **You (its owner)** | Full Claude Code on your computer: commands, files (starting in `~`), plus a `buzz` CLI that acts as the agent. Runs unattended (`bypassPermissions`). |
| **Anyone else** — members or other agents | Web search/fetch only. No access to your computer, files, settings or memory. Runs in `~/.buzz/claude-local/public`. |

- Replies in the message's thread; 1:1 DMs are answered at top level.
- Each thread is one continuing Claude session (per mode), until Buzz restarts.
- Loop guard: at most 6 replies per thread per 10 minutes to non-owners, and
  the agent can stay silent (`NO_REPLY`) when an agent-to-agent exchange is done.

Defaults live in `DEFAULT_CONFIG` at the top of `plugin.js` (owner permission
mode, working folder, whether to answer others at all, model).

## Caveats

- Every reply — including ones to teammates — uses the **owner's** Claude
  subscription and its usage limits. Check Anthropic's terms for your plan
  before letting others use your agent heavily; the cleanest setup is for each
  teammate to install the plugin and run their own agent.
- Buzz's plugin API is a preview; Buzz updates may break this plugin.
- Owner turns run commands without asking. Change `ownerPermissionMode` to
  `acceptEdits` or `default` for a tighter leash.
