---
name: source-verified-research
description: Research a question where every claim must trace to a source that was actually opened — official docs for cloud, API and framework behaviour, original papers for academic work (literature reviews, proposals, theses). Use when the user asks for researched findings, citations, a literature review, or whether a technical claim is true ("is it true that…", "fact-check this").
argument-hint: "[research question]"
---

# Source-verified research

Question: $ARGUMENTS

## Rules
1. **Open every source you cite.** Use web search to find candidates and a fetch/browser tool to read them. A search snippet is not a source. If a page can't be opened, say so and don't cite it.
2. **Prefer primary sources.**
   - Cloud, API and framework claims → the vendor's official docs for the *version in use* (check the lockfile or dependency file; use a docs tool such as Context7 if one is installed).
   - Academic claims → the original paper (arXiv, ACL Anthology, publisher page), not a blog summary. Use secondary sources only to find primaries.
3. **Record what each source actually supports**: a short paraphrase plus the section or page. Never attribute a claim to a source that doesn't contain it.
4. **Verify citation details** against the source itself: authors, title, year, venue, DOI/URL. Flag anything you couldn't confirm.
5. **Separate fact from inference.** Mark your own reasoning as *inference*. Mark conflicting sources as *disputed* and show both.

## For papers
For each paper, capture these where reported (write "not reported" otherwise; never guess):
- Task and setting (domain, population, language, region — note anything specific to the user's target setting)
- Dataset(s) and **train/validation/test split**
- **Baseline(s)** compared against
- **Evaluation metric(s)** and headline result
- Limitations the authors state

## Output
1. **Answer.** A direct answer in a few sentences, with inline numbered citations [1].
2. **Evidence table.** claim | source # | what it supports | confidence (high / medium / low).
3. **Paper table** (if papers). paper | dataset & split | baseline | metric | result.
4. **References.** Full verified citations with URLs; mark any unverified field.
5. **Gaps.** What couldn't be found or verified, and what to search next.
