---
name: ship-check
description: Pre-merge gate for the current branch — run the project's lint, type check and tests, smoke-test the changed user flow in a real browser when the project has a UI, review the diff, and report pass/fail with evidence. Use when the user says "ship check", "ready to merge?", "check before PR" or "before I push", or has just finished a feature.
argument-hint: "[optional: flow to smoke-test, e.g. 'sign up, then reload the page']"
---

# Ship check

Flow to smoke-test (if given): $ARGUMENTS

Run every step; don't stop at the first failure. Never report a step as passing without its command output.

1. **Scope.** `git status` and `git diff --stat <base>...HEAD` (base = the default branch). Note what changed and which user flows it touches.
2. **Find the project's own commands.** Read package.json scripts, pyproject.toml, Makefile, Cargo.toml, CI config and so on. Use those; don't invent new ones.
3. **Static checks.** Lint and type check (e.g. `npm run lint`, `tsc --noEmit`, `ruff`, `mypy`/`pyright`, `cargo clippy`).
4. **Tests.** Run the suite, or the affected subset if the full suite is slow (say so). Flag changed code that has no tests.
5. **Browser smoke test** (projects with a UI only). Start the dev server and walk the changed flow end to end, or the flow in the arguments, with whatever browser tool is available (a Playwright plugin or MCP, a built-in browser). Check that state survives a reload and that error states show what the user should see. Capture a screenshot and console errors. If no browser tool is available, say so and skip.
6. **Review.** Review the diff for real bugs (use a code-review skill or command if one is installed). Separate bugs from style nits.
7. **Report.** A table: step | result (✅ / ❌ / ⚠️ skipped) | evidence (command + key output line). Then a short list of blockers to fix before merge.

Don't commit, push or open a PR unless the user asks.
