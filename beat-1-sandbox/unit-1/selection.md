# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
issue-select: grade these candidate first issues: <https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54>  <https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63>  <https://github.com/codepath/pathreview-ai301-fa26-s1/issues/56>

I'll load the issue-select skill to grade these against its rubric.

● Skill(issue-select)
Successfully loaded skill

  Read 3 files

All three are in the scoped repo. Gathering evidence.

  Ran 11 shell commands

All three are in the scoped repo (codepath/pathreview-ai301-fa26-s1), so all three are valid candidates. Evidence gathered live via the public GitHub API (today: 2026-09-19).

Shared repo facts: archived: false, last push 2026-09-16T21:48:27Z (3 days ago); the 5 newest main commits are all by Andrew Burke, newest 2026-09-16. Repo has zero PRs (search type:pr → total_count: 0), so no issue can have a linked PR. docs/CONTRIBUTING.md (189 lines) contains no mention of AI, Claude, Copilot, LLM, or generated code; there is no AI_POLICY.md, and no CONTRIBUTING.md in .github/ — silence, which passes.

Ranked read-out

Accepted, in fit order:

1. #56 — Structural chunker silently drops documents that contain no headings — best fit: it's the RAG ingestion path, which is squarely the AI-engineering + data-processing work you said you want to strengthen, and the fix (chunk as one block / fall back) is a bounded change with a named failing test, test_document_with_no_headings.
2. #54 — Resume section detection fails on text with leading whitespace — Python regex/parsing in the ingestion pipeline, with a copy-pasteable repro and three named failing tests; data-processing fit, but less AI-specific than #56.
3. #63 — README scorer test fixture is too short for its own word-count assertion — testing fit and the safest of the three, but the smallest learning payoff: extending a fixture or correcting one assertion.

Rejected: none.

Per-check detail (identical structure across the three; only scope evidence differs):

- Maintainer is active — pass: newest main commit 2026-09-16, 3 days ago, well inside 90.
- Repo in use — pass: "archived": false, "pushed_at": "2026-09-16T21:48:27Z", inside 180 days.
- Scope fits a newcomer — pass for all three: each is a single cohesive bug with a repro block and named failing tests; none is an umbrella issue, none has any comments (so no unresolved design debate), none has a closed/abandoned linked PR, none is a usage question, none waits on an undecided input.
- Nobody else is already on it — pass for all three: "assignees": [], "assignee": null, "comments": 0, and the repo has no PRs at all.
- AI assisted contributions allowed — pass: no AI ban anywhere in the contribution docs; the repo's own commits carry Co-Authored-By: Claude Opus 5.

One note on the Path Review house rule: it exists to stop classmate claim comments from blocking you, but here it never had to fire — all three issues have zero comments.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/56",
    "checks": [
      {"name": "Maintainer is active", "grade": "pass", "evidence": "Newest main commit by Andrew Burke dated 2026-09-16, 3 days before today (2026-09-19), within 90 days."},
      {"name": "Repo in use", "grade": "pass", "evidence": "\"archived\": false and \"pushed_at\": \"2026-09-16T21:48:27Z\", within 180 days of today."},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Single bounded bug: \"StructuralChunker.chunk() returns an empty list for any document without markdown headings\" with a repro and one named failing test; 0 comments, no linked PRs, not an umbrella issue."},
      {"name": "Nobody else is already on it", "grade": "pass", "evidence": "\"assignees\": [], \"comments\": 0, and repo-wide PR search returns \"total_count\": 0 so no linked PR exists."},
      {"name": "AI assisted contributions allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI/Claude/Copilot/LLM/generated mentions and no AI policy file exists; repo commits are themselves Co-Authored-By Claude."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54",
    "checks": [
      {"name": "Maintainer is active", "grade": "pass", "evidence": "Newest main commit by Andrew Burke dated 2026-09-16, 3 days before today (2026-09-19), within 90 days."},
      {"name": "Repo in use", "grade": "pass", "evidence": "\"archived\": false and \"pushed_at\": \"2026-09-16T21:48:27Z\", within 180 days of today."},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Single bounded regex bug in _detect_sections() with a runnable repro and three named failing tests; 0 comments, no design debate, no abandoned PRs."},
      {"name": "Nobody else is already on it", "grade": "pass", "evidence": "\"assignees\": [], \"comments\": 0, and repo-wide PR search returns \"total_count\": 0 so no linked PR exists."},
      {"name": "AI assisted contributions allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI/Claude/Copilot/LLM/generated mentions and no AI policy file exists; repo commits are themselves Co-Authored-By Claude."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63",
    "checks": [
      {"name": "Maintainer is active", "grade": "pass", "evidence": "Newest main commit by Andrew Burke dated 2026-09-16, 3 days before today (2026-09-19), within 90 days."},
      {"name": "Repo in use", "grade": "pass", "evidence": "\"archived\": false and \"pushed_at\": \"2026-09-16T21:48:27Z\", within 180 days of today."},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "One test fixture vs. assertion mismatch (\"assert 51 > 100 fails\") in a single test file; 0 comments, no umbrella structure, no abandoned PRs."},
      {"name": "Nobody else is already on it", "grade": "pass", "evidence": "\"assignees\": [], \"comments\": 0, and repo-wide PR search returns \"total_count\": 0 so no linked PR exists."},
      {"name": "AI assisted contributions allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI/Claude/Copilot/LLM/generated mentions and no AI policy file exists; repo commits are themselves Co-Authored-By Claude."}
    ],
    "verdict": "accept"
  }
]

✻ Brewed for 1m 27s · done 11:06 AM
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. agreement: 16/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in policy)
2. agreement: 17/20 scored items  (bar: 18/20: below the bar)
3. agreement: 18/20 scored items  (bar: 18/20: PASS)
4. agreement: 19/20 scored items  (bar: 18/20: PASS)
5. agreement: 19/20 scored items  (bar: 18/20: PASS)
6. agreement: 20/20 scored items  (bar: 18/20: PASS)


**Issue analysis**

issue-20 was a gold label reject before I fixed my scope fits a newcomer check, my rubric produced this disagreement: issue-20  reject  accept   NO     graded accept. The issue asked to add company logo shape to the toolbar in excalidraw but the issue body stated logo asset TBD and left part of the implementation surface undecided. My check initially only tested for umbrella issues and unresolved design debates, so it passed this issue since there was no maintainer dispute and no core internals statement. After comparing my rubric's accept against the gold reject, I added a new failure condition for an undecided input the assignee cannot supply themselves, such as an unspecified asset. Rerunning against this issue after the fix produced  issue-20  reject  reject   yes which matched the gold.

**Check rationale**

The scope fits a newcomer check's current pass condition from tools/issue-select/rubric.md "Fails only if issue is an umbrella/tracking issue whose sub items are meant to be split into separate issues, not a single cohesive feature or doc topic broken into checklist or the thread shows an unresolved design debate with no maintainer decision, including cases where contributors are reverse engineering undocumented external behavior with no settled spec or maintainer states the fix touches core internals or it is a pure usage/support question or the issue depends on a specific undecided input the assignee cannot supply themselves, such as an unspecified asset (e.g. a logo, image, or file marked TBD) or an undecided cross package boundary, or the issue has two or more closed/abandoned linked PRs, or the thread shows two or more separate contributors each claiming the issue and then going stale/unresponsive, signaling real difficulty despite apparent simplicity." I wrote it this way because a single narrow test missed several distinct ways a first issue can quietly fail to be bounded such as an unresolved implementation input, reverse engineering an undocumented external spec, and a pattern of repeated contributor abandonment.


**Trade-offs**

This check does not fail an issue for having a checklist, multiple related sub tasks on one topic, or the reporter's own suggested implementation approaches. I added that carve out after this same wording before I narrowed it which wrongly rejected issue-01 and issue-19, both gold labeled accept despite multi part descriptions. I also required two or more separate contributors abandoning the issue after a broader version wrongly caught issue-09. I accept this check could still miss an issue where a single contributor's abandoned attempt shows high difficulty.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. Issue #63 fits my interests and time available since this is my first open source contribution. I wanted something I could realistically finish without getting stuck.
2. My rubric's verdict correctly showed the issue is unclaimed, the repo is active, and the fix is small and bounded. What the rubric couldn't weigh was my own comfort level for doing open source contribution for the first time. My skill ranked #56 higher for skill building value but I chose #63 anyways because I wanted to focus on learning the actual contribution process before tackling a more demanding issue. 
3. I expect this to be low difficulty. It looks like a one line fix to a test fixture or assertion value, so most of the challenge will be setting up the dev environment and following the repo's contribution steps correctly.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
