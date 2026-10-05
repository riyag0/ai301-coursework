# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

riyag0

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63#issuecomment-5984720700

Plan
My reproduction confirmed that test_readme_with_all_quality_signals uses a README fixture with a word count of 51, while the test expects:

assert data["word_count"] > 100
and:
assert data["word_count_category"] == "comprehensive"

The test is currently marked xfail(strict=True) for issue #63, so it reports XFAIL rather than a normal failure.

Proposed change
I plan to:

Update the README fixture in tests/unit/test_readme_scorer.py with realistic content so that it reaches at least 500 words, the threshold required for the "comprehensive" category
Keep the existing word_count > 100 and "comprehensive" assertions
Remove the issue README scorer test fixture is too short for its own word-count assertion #63 xfail marker so the corrected test can pass normally
Keep the change limited to the unit test rather than modifying the production README scoring logic
Verification
I will rerun:

pytest tests/unit/test_readme_scorer.py -v -m unit

Before the fix, test_readme_with_all_quality_signals reports XFAIL. After the fix, I expect it to report PASSED, with the rest of the README scorer unit tests continuing to pass.

The main risk is that extending the fixture could affect another quality signal in the test, so I will preserve the existing fixture content and signals while adding only the content needed to represent the intended comprehensive README case.


---

## Your branch

**Branch**

fix/63-readme-word-count

**Evidence**

Before:

Command:
pytest tests/unit/test_readme_scorer.py -v -m unit

Output:
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals XFAIL
22 passed, 1 xfailed in 1.72s

After:

Command:
pytest tests/unit/test_readme_scorer.py -v -m unit

Output:
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals PASSED
23 passed in 1.03s

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

agreement: 19/20 scored items  (bar: 18/20: PASS)
agreement: 19/20 scored items  (bar: 18/20: PASS)
agreement: 18/20 scored items  (bar: 18/20: PASS)
agreement: 19/20 scored items  (bar: 18/20: PASS)

**Package analysis**

pkg-09

Rubric decision: reject
Gold label: accept

The final eval shows "pkg-09 clear-accept      accept reject  NO  failed: Diagnosis matches evidence"

My rubric rejected pkg-09 because it failed the "Diagnosis matches evidence" check. The gold label was accept, so this was the one disagreement in my final 19/20 run. The rubric read the package as not sufficiently connecting the proposed diagnosis to the reproduction evidence, even though the gold label considered the plan acceptable.


**Check rationale**

Diagnosis matches evidence "The diagnosis names a cause tied to a specific file or component, and that cause accounts for everything the repro evidence actually showed. It does not contradict or ignore a result the evidence reported." I wrote this check to require the diagnosis to be grounded in the actual reproduction evidence rather than simply repeating the issue's description. This matters because reproduction can reveal results that differ from the original issue report, such as a test reporting XFAIL instead of a normal failure. I wanted the check to accept a diagnosis only when the proposed cause explains the observed evidence and does not ignore or contradict those results.

**Trade-offs**

The "Diagnosis matches evidence" check trades some recall for stricter evidence grounding. In the final evaluation, pkg-09 had a gold label of accept but my rubric rejected it because it failed this check. I accept this tradeoff because the check helps prevent plans from passing when their diagnosis is not sufficiently supported by the reproduction evidence. The final rubric still achieved 19/20 agreement, with all other scored packages matching their gold labels.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
