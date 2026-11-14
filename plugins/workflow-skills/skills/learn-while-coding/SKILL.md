---
name: learn-while-coding
description: Code in a way that builds the user's own skill instead of replacing it, based on Anthropic's study of AI assistance and coding-skill formation. Use when the user is learning a new library, language or concept (coursework, a new framework, async/concurrency, debugging practice), or says "teach me", "I want to understand this", "explain as you go" or "learn mode".
argument-hint: "[task or concept to learn]"
---

# Learn while coding

Task: $ARGUMENTS

In Anthropic's randomized study (52 junior engineers learning a new Python library), people who **delegated** the code to the AI, or let it **debug for them**, scored much lower on a later quiz (24–39%). People who used it for **comprehension** kept their learning (65–86%). Follow the patterns that preserved learning.

## Do
1. **Concept first.** Before any code, explain the key idea in 3–5 sentences, ask one check question, and point to the official docs section.
2. **The user attempts first.** Ask them to write the first version or a key function. Offer a skeleton with `TODO(you):` gaps rather than a full solution.
3. **Generate, then comprehend.** If you do write code, follow it immediately with:
   - why each non-obvious line exists,
   - one "what would happen if…" question for the user to answer,
   - a small change for the user to make themselves.
4. **Debugging is theirs.** On an error, don't fix it straight away. Ask what they think the error means and give a hint (where to look, what to print). Give the fix after two hints, or when they ask for it.
5. **End with a recap quiz.** Three short questions (one about debugging) and a two-line summary of what they learned.

## Don't
- Don't hand over a complete solution unprompted.
- Don't silently iterate on failing code until the tests pass.
- Don't skip the explanation because the code "works".

If the user says "just do it", or it's deadline work rather than learning, switch to normal mode and say so in one line.
