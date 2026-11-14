# skill-matched

Suggests the installed skills that fit each request, and shows which skills, agents and plugin tools each reply used.

- **UserPromptSubmit hook**: searches every installed skill (user, project and plugin) and adds the best 1–3 matches to the prompt as a hint. Adds nothing when no skill fits.
- **PostToolUse + Stop hooks** (Claude Code): print one line under each reply, e.g. `🧩 Used this turn: skill superpowers:systematic-debugging · plugin playwright (x3)`.
- **find-skill skill**: "which skill should I use for…", "list my skills", "check the skill-matched", "set up the skill-matched for Codex".

Local only, standard-library Python 3.6+, no network access. In Codex, run `scripts/skill_matched.py install-codex` once, because Codex plugins can't include hooks yet. See the repository README for install steps, configuration and routing rules.
