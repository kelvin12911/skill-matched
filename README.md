# Skill Matched

**Find the installed skill that fits each request, and see which skills each reply used. For Claude Code and Codex.**

Once you have dozens of skills and plugins, the agent sees a long list of descriptions and has to guess which one fits. Skill Matched helps it pick, and shows you the result:

1. **Before each request**, it searches every skill you have installed (user, project and plugin skills) and adds the best 1–3 matches to the prompt as a hint. If nothing matches, it adds nothing.
2. **After each reply** (Claude Code), it shows one line with what was used:
   > 🧩 Used this turn: skill `superpowers:systematic-debugging` · plugin `playwright` (x3) · agent `code-reviewer`

It works with whatever *you* have installed, so there's nothing to configure. It understands everyday wording ("my app keeps crashing", "look over my code before I push", "is it true that…").

Everything runs locally with the Python standard library. No network access, no telemetry, no dependencies.

## What's in the repo

| Plugin | What it gives you |
|---|---|
| **skill-matched** | The matcher hooks, plus the `find-skill` skill: ask "which skill should I use for…", "list my skills", or "check the skill-matched". |
| **workflow-skills** (optional) | `ship-check` (pre-merge gate: lint, types, tests, browser smoke test, review), `source-verified-research` (every claim cites an opened source), `learn-while-coding` (learn-first coding), `bilingual-study-pack` (exam answers plus notes in your own language). |

## Install: Claude Code

```
/plugin marketplace add kelvin12911/skill-matched
/plugin install skill-matched@skill-matched
/plugin install workflow-skills@skill-matched
```

Start a new session. To keep it updated: `/plugin` → **Marketplaces** → `skill-matched` → **Enable auto-update**.

## Install: Codex

```bash
codex plugin marketplace add kelvin12911/skill-matched
```

In Codex, open `/plugins` and install **Skill Matched** (and **Workflow Skills** if you want them).

Codex plugins can't include hooks yet, so turn on the automatic suggestions once. Ask Codex: **"Set up the skill-matched hook for Codex"**, or run it yourself:

```bash
python3 "$(ls -d ~/.codex/plugins/cache/skill-matched/skill-matched/*/ | sort -V | tail -n1)scripts/skill_matched.py" install-codex
```

On Windows (PowerShell):

```powershell
$p = Get-ChildItem "$env:USERPROFILE\.codex\plugins\cache\skill-matched\skill-matched" -Directory | Sort-Object Name | Select-Object -Last 1
python "$($p.FullName)\scripts\skill_matched.py" install-codex
```

Restart Codex and approve the new hook if it asks. Run `install-codex` again after updating the plugin.

Codex shows the suggestions but not the "🧩 Used this turn" line, because Codex has no skill tool for the hook to track.

## Make the choice predictable (recommended)

When several skills match, for example three design skills for "make my website nicer", the agent decides. To decide for it, copy the template in [`ROUTING.example.md`](ROUTING.example.md) into `~/.claude/CLAUDE.md` or `~/.codex/AGENTS.md` and edit the table to fit the skills you have.

## Commands

Run `python3 <plugin folder>/scripts/skill_matched.py <command>`, or ask the `find-skill` skill to do it.

| Command | What it does |
|---|---|
| `query "my test is failing"` | Show the best matches and their scores |
| `list` | Every skill the matcher can see |
| `doctor` | Paths, skill counts and whether the Codex hook is installed |
| `install-codex` / `uninstall-codex` | Add or remove the Codex hook |

Add `--runtime codex` to `query` and `list` to see Codex's view.

## Configuration (optional)

Create `~/.claude/skill-matched/config.json` (Codex: `~/.codex/skill-matched/config.json`):

```json
{
  "max_suggestions": 3,
  "min_score": 5.0,
  "suggest": true,
  "show_summary": true,
  "ignore": ["some-plugin", "some-plugin:some-skill"],
  "phrases": { "make it pop": "design interface styling", "出bug": "bug" }
}
```

- `phrases` teaches the matcher your own wording. Each key is matched anywhere in your prompt and adds the words on the right, which should be words your skills' descriptions use.
- `ignore` hides skills or whole plugins from suggestions.
- `"suggest": false` keeps only the summary line; `"show_summary": false` keeps only the suggestions.

`CLAUDE_CONFIG_DIR` and `CODEX_HOME` are respected.

## How it works

- **Matching.** A small BM25 keyword search over each skill's name, `description` and `when_to_use`, with stemming, a synonym and phrase table, and character pairs for Chinese, Japanese and Korean. A match must hit the skill's name, or at least two uncommon words with enough score. The index is cached for 10 minutes and rebuilt when you install or remove anything.
- **Project skills.** Skills inside a project (`.claude/skills`, `.agents/skills`, `.codex/skills`) are read only when you've marked that folder as trusted in Claude Code or Codex, and only up to the repository root. They're labelled as project skills, and the hint tells the agent to treat every description as data, not instructions.
- **Deciding.** The matcher only suggests. The agent reads the suggestions together with your routing rules and each skill's own limits, and skips them when nothing fits.
- **Summary.** A `PostToolUse` hook records `Skill`, `Agent` and plugin tool calls, and the `Stop` hook prints and clears them. In the Claude desktop app the line appears as a notice labelled **"Stop says:"**, where "Stop" is the name of the hook.

## Requirements

- Python 3.6 or later, as `python3` (or `python` on Windows).
- Claude Code with plugin support, and/or Codex with plugins and hooks.

## Uninstall

- Claude Code: `/plugin uninstall skill-matched@skill-matched`
- Codex: run `skill_matched.py uninstall-codex`, then uninstall the plugin in `/plugins`.

## Licence

MIT
