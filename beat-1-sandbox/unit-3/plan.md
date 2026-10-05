## Plan for Issue #63

## Diagnosis

The issue is caused by the README fixture in tests/unit/test_readme_scorer.py being too short for the expectations in test_readme_with_all_quality_signals. 

My Unit 2 reproduction confirmed that the fixture contains 51 words, matching the issue's reported assert 51 > 100.

The test expects:
assert data["word_count"] > 100
assert data["word_count_category"] == "comprehensive"

The reproduction also showed that the test is currently marked XFAIL, rather than appearing as a normal failure:
"Test output shows the test marked XFAIL, not a plain failure: tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals XFAIL 22 passed, 1 xfailed in 2.84s"

The test currently carries this marker:
@pytest.mark.xfail(
    strict=True,
    reason = "issue #63: README scorer fixture is too short for its own word-count assertion"
)

This evidence indicates that the fixture does not contain enough README content to satisfy the test's own > 100 word count assertion and reach the expected comprehensive category. The xfail marker currently prevents this known issue from appearing as a normal test failure.

## Scope

I will update the README fixture used by test_readme_with_all_quality_signals with realistic README content so that it reaches at least 500 words, which is the threshold required by the scorer for the "comprehensive" category. This will also satisfy the existing word_count > 100 assertion.

I will also remove the issue #63 xfail marker once the underlying fixture problem is fixed.

I will not change the production README scoring logic or lower the existing word count expectation. The reproduction evidence points to the test fixture itself as the source of the mismatch.

## Files to Touch
- tests/unit/test_readme_scorer.py

I expect the implementation to remain limited to this file because both the affected fixture and the issue #63 xfail marker are associated with this unit test.

## Approach
1. Locate the README fixture used by test_readme_with_all_quality_signals
2. Preserve its existing quality signals while extending the README text with realistic content
3. Ensure the updated fixture contains at least 500 words so that it reaches the "comprehensive" category while also satisfying the word_count > 100 assertion
4. Keep the existing assertions for word_count > 100 and word_count_category == "comprehensive"
5. Remove the issue #63 xfail marker so that the corrected test can pass normally
6. Rerun the README scorer unit tests
7. Review the diff to confirm that the change remains limited to the test fixture and its associated expected failure handling

## Test Plan

I will rerun the same command used during the Unit 2 reproduction:
pytest tests/unit/test_readme_scorer.py -v -m unit

Before the fix, my reproduction produced:
tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals XFAIL
22 passed, 1 xfailed in 2.84s

After this fix, I expect test_readme_with_all_quality_signals to report
PASSED rather than XFAIL.

I will verify that the existing assertions succeed:
assert data["word_count"] > 100
assert data["word_count_category"] == "comprehensive"

I will also verify that the rest of tests/unit/test_readme_scorer.py continues to pass.

The xfail handling is part of the test plan because my Unit 2 reproduction found:
"The fix will also need to remove or update the xfail marker, since strict=True means an unexpected pass after the fix would itself cause a failure."

Therefore, a successful result should have the corrected test passing normally rather than unexpectedly passing while still marked with xfail(strict=True).

## Risks and Unknowns


The reproduction established that the fixture currently contains 51 words. Repository inspection confirms that the scorer categorizes 100-499 words as "adequate" and requires at least 500 words for "comprehensive". I will therefore extend the fixture to at least 500 words while preserving its existing quality signals. 

The main risk is that adding content could unintentionally affect another quality signal exercised by the test, so I will verify all existing assertions after the change.

## Deviations

The implementation followed the plan as written. I updated only tests/unit/test_readme_scorer.py, extended the README fixture so that it meets the comprehensive word-count threshold, removed the issue #63 xfail marker, and did not change the production README scoring logic. The reproduction test changed from XFAIL with 22 passed and 1 xfailed to passed with all 23 tests passing. No deviations from the planned implementation were necessary.
