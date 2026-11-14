---
name: bilingual-study-pack
description: Build an exam study pack from the user's own lecture slides, notes and past papers — complete, copyable model answers in the exam's language, plus short trap and memory notes in the user's own language (e.g. 繁體中文／廣東話, 简体中文, Español), optionally as a printable PDF. Use when the user asks for revision notes, a cheat sheet, model answers, past-paper practice or a study pack for a course.
argument-hint: "[course or topic] [optional: notes language] [optional: pdf]"
---

# Bilingual study pack

Build a study pack for: $ARGUMENTS

**Languages.** Answers go in the exam's language (default English). Notes go in the user's own language: use the one they named, otherwise the language they are writing to you in. If that is the same as the exam language, write the notes in it too.

## 1. Ground everything in the supplied material
- Read every slide deck, past paper and marking scheme the user gives (extract text from PDF/PPTX with whatever document tools are available). If none were supplied, ask for them first. Never invent syllabus content.
- List the topics covered and map each past-paper question to its source (deck + slide or page number).
- If an answer needs something that isn't in the material, mark it **[outside the material]** rather than silently filling it in.

## 2. Model answers (the part they copy into the exam)
For each topic or past-paper question:
- **Question / topic.** Restate it exactly.
- **Model answer.** Complete, exam-ready, in the structure markers reward (definition → explanation → example → conclusion; show working for calculations; label diagrams). Match the mark allocation: roughly one distinct point per mark.
- **Keywords.** The terms a marker looks for, in bold.
- **Source.** The deck and page it comes from.

Keep answers copyable: plain prose and simple lists, no decorative formatting inside answers.

## 3. Notes in the user's language
After each answer, add a short block:
- **Common traps.** Typical mistakes and misreadings of the question.
- **Memory hook.** A quick mnemonic or one-line summary, if it helps.
- Keep technical terms in the exam language, with a gloss in the notes language the first time, e.g. 「死結 (deadlock)」.

The notes are for understanding only. Never replace the answer with them.

## 4. Output
- Default: one Markdown document ordered by topic, ending with a **quick-revision table** (topic | key point | trap).
- For a printable PDF or cheat sheet:
  - Use a font stack that covers both languages (for CJK, e.g. `"PingFang TC", "Noto Sans CJK TC", "Microsoft JhengHei", sans-serif`).
  - Respect any page limit (e.g. "one A4 sheet, double-sided").
  - **Before delivering,** render each page to an image and check it: page count within the limit, no clipped text or overflowing tables, and every character displays (no □ boxes). Fix and re-render if any check fails.
- End with a short list of what was covered and anything left out or uncertain.
