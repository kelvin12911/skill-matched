# Skill routing rules (template)

Copy the section below into `~/.claude/CLAUDE.md` (Claude Code) or `~/.codex/AGENTS.md` (Codex). The matcher finds candidate skills, and these rules decide which one wins when several match.

**Delete the rows for skills you don't have, and add your own.** Skill names are the ones `find-skill list` prints.

---

## Using installed skills
- Before starting a task, check the available skills (and any "Skill matcher" suggestions added to the prompt) for one that genuinely fits. If one fits, use it first. If several fit, use the table below. If none fits, just do the task — never force a skill.
- Respect each skill's own limits.
- If I name a skill, use that one.

## Routing table
| Task | Use |
|---|---|
| Bug, failing test, unexpected behaviour | `superpowers:systematic-debugging` |
| New feature or bugfix code | `superpowers:test-driven-development` |
| Planning something new, unclear requirements | `superpowers:brainstorming`, then `superpowers:writing-plans` |
| Before saying "done", "fixed" or "passing" | `superpowers:verification-before-completion` |
| Before merging | `workflow-skills:ship-check` |
| Deep pull-request review | `/pr-review-toolkit:review-pr` |
| Library or framework API question | a docs tool (e.g. Context7) for the version in the lockfile |
| Claims that need sources, papers, literature review | `workflow-skills:source-verified-research` |
| I say I want to learn or understand something | `workflow-skills:learn-while-coding` |
| Course revision, exam answers, cheat sheets | `workflow-skills:bilingual-study-pack` |
| PDF / Word / Excel / PowerPoint files | the matching document skill (`pdf`, `docx`, `xlsx`, `pptx`) |
| "Which skill should I use?" / "what do I have?" | `skill-matched:find-skill` |

In Codex, skills from this repo appear without the plugin prefix (for example `ship-check`, `find-skill`).
