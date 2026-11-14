---
name: find-skill
description: Search the installed skills and plugin commands for the best match to a task, list everything installed, or set up / check the skill-matched. Use when the user asks "which skill should I use", "what skills or plugins do I have", "is there a skill for X", wants to compare overlapping skills, or asks to install, check or turn off the skill-matched.
argument-hint: "[task description] | list | doctor | install-codex"
---

# Find a skill

Request: $ARGUMENTS

The matcher script is `scripts/skill_matched.py` in this plugin, two folders up from this file
(`<folder of this SKILL.md>/../../scripts/skill_matched.py`; in Claude Code that is
`${CLAUDE_SKILL_DIR}/../../scripts/skill_matched.py`). Run it with `python3` (on Windows, `python`).
Pass `--runtime codex` when you are running in Codex, otherwise `--runtime claude`.

| Request | Command |
|---|---|
| a task ("review my code before I push") | `skill_matched.py query --runtime <rt> "<the task>"` |
| `list`, "what do I have" | `skill_matched.py list --runtime <rt>` |
| `doctor`, "is the matcher working" | `skill_matched.py doctor` |
| `install-codex`, "turn on the matcher in Codex" | `skill_matched.py install-codex`, then tell the user to restart Codex |
| "turn the matcher off in Codex" | `skill_matched.py uninstall-codex` |

For a task:
1. Run the query. Scores are keyword matches, not a verdict.
2. Read the top candidates' descriptions, apply any skill routing rules in CLAUDE.md / AGENTS.md, and recommend **one** skill, or a combination with what each part does.
3. Say plainly when nothing fits. Working without a skill is fine.

For `list`, group the output by plugin (the part before `:`) and keep it short.
