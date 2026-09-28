# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

riyag0

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63#issuecomment-5852313550

Hi, I would like to work on this as a first contribution. The issue points to tests/unit/test_readme_scorer.py, specifically test_readme_with_all_quality_signals, where assert 51 > 100 fails against the current fixture. I will set up the dev environment per docs/SETUP.md and run the test to confirm, then report back.


**Reproduction comment**


https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63#issuecomment-5859771655

Environment
OS: Windows 11
Python: 3.14.4
pytest: 9.1.1
Repo: Fork of codepath/pathreview-ai301-fa26-s1, branch main
Setup: Created a Python venv per docs/SETUP.md, activated it, and ran pip install -e ".[dev]". Skipped the full make setup, since this bug is isolated to a Python unit test with no database or API dependency
Steps
cd into the cloned fork
py -m venv .venv
source .venv/Scripts/activate
pip install -e ".[dev]"
pytest tests/unit/test_readme_scorer.py -v -m unit
Behavior shown
Test output:
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals XFAIL 22 passed, 1 xfailed in 2.84s

The test carries this marker:
@pytest.mark.xfail(strict=True, reason="issue #63: README scorer fixture is too short for its own word-count assertion")

I confirmed the fixture's actual word count directly:
$ python/tmp/count_words.py
51

This matches the issue's stated assert 51 > 100 exactly. The assertions that would fail without the xfail marker are assert data["word_count"] > 100 and assert data["word_count_category"] == "comprehensive"

Expected vs actual
Expected: The fixture's word count should exceed 100, so the test validates comprehensive README scoring as intended.

Actual: The fixture contains exactly 51 words, so assert data["word_count"] > 100 would fail.
A maintainer has already marked the test xfail(strict=True) citing this issue, so the suite reports 22 passed, 1 xfailed rather than a plain failure.

Next, I will extend the fixture's content past 100 words and remove the xfail marker, since strict=True means an unexpected pass after the fix would itself cause a failure.


## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**


1. agreement: 15/17 scored items (Partial run)
2. agreement: 17/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in disclosure)
3. agreement: 3/3 (pkg-09, pkg-10,pkg-20)
4. agreement: 19/20 scored items  (bar: 18/20: PASS)
5. agreement: 2/2 (pkg-03, pkg-20)
6. agreement: 18/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in disclosure)
7. agreement: 20/20 scored items  (bar: 18/20: PASS)


**Package analysis**


pkg-20. Gold label: reject. My rubric's decision: accept before the revision, reject after the revision. The package is from ghostty-org/ghostty, whose AI_POLICY.md states "All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance." The candidate claim comment and repro report were otherwise well evidenced and honest, but neither one contained any AI disclosure statement. My words respect the repo's conventions check initially only tested for specificity, so it passed this package since writing was specific. After comparing my rubric's accept against the gold reject, I added an explicit disclosure clause of "If the repo's contribution policy requires disclosing AI tool use, the comment or report states that disclosure. A required disclosure that is missing fails this check, even if the rest of the writing is specific and honest." Running it again against this package after the fix produced a reject. I later narrowed this clause after pkg-03 was wrongly rejected. The pkg-03 policy only requires comments in the contributor's own words. It does not ask for a disclosure statement. The final rubric reads "This check only requires a disclosure statement when the policy explictly asks the contributor to state that AI was used." pkg-20 still rejects under this wording. Its policy explicitly asks for the tool and the extent of assistance to be stated. 

**Check rationale**

Quoting the behavior matches the issue check's current pass condition from tools/repro-check/rubric.md where it says "If the report claims reproduction succeeded, the pasted output shows the same specific behavior the issue names. If the report honestly states it could not reproduce the behavior, this check passes regardless of what the output shows." I wrote it this way after my first version of this check failed two gold labeled accept packages pkg-09 and pkg-10 that were well evidenced reports which cannot be reproduced. My original wording only checked whether the pasted output matched the issue's described behavior with no exception for an honest negative result. Splitting the condition into two sentences, one for the claimed reproductions and one for honest non reproductions, fixed both packages without weakening the check's ability to catch an actual wrong target claim.

**Trade-offs**

This check's honest cannot reproduce condition means it will not fail a report that claims no reproduction, even if that report's investigation was shallow, as long as the report does not claim more than it observed. I accept this could let a low effort report that says I couldn't reproduce can report pass in this specific check. That risk is left intentionally to separate steps are complete and easy to follow and outcome stated honestly checks, which catchs a report that has done little work to make its conclusion.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.

