# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

Where it lives:
- In an eval bundle, read the plan context block for the accepted plan's scope, files, approach, and any deviations. Compare those with the Candidate PR's diff and description
- In live mode, read `plan.md`, including `## Deviations`, and compare it with the committed branch diff from `git diff main...HEAD`. Compare the claims in `pr_draft.md` with both the plan and the diff

What good looks like:
Every substantive changed file and behavior in the diff falls within the plan's stated boundary or is covered by an honest deviation note. The PR description accurately describes what the diff actually implements. Silent drift exists when the diff does more or less than the plan without a recorded deviation, or when the description materially claims more or less than the diff delivers

## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

Where it lives:
- In an eval bundle, read the plan context block's test plan and reproduction evidence, then compare them with the Candidate PR's test evidence section and testing claims in the description. Use the repo facts block to identify repository-required checks
- In live mode, read the test plan in `plan.md`, the captured commands and output in `test_evidence.md`, and the Testing section of `pr_draft.md`. Use the repository's PR template and `docs/CONTRIBUTING.md` to identify required checks

What good looks like:
The evidence shows observable results for the planned verification, including the relevant before and after behavior, and records the actual outcomes of the repository's required checks. A failing or unavailable check can still be valid evidence when its outcome and reason are honestly recorded. A statement such as "tests pass" without observable supporting results is not enough

## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

Where it lives:
- In an eval bundle, inspect the Candidate PR's unified diff and commit list
- In live mode, inspect the committed branch diff from `git diff main...HEAD` and the commits on the branch

What good looks like:
The intended fix is visible and reviewable in the diff, and the changed files and hunks are focused on the issue. The diff contains no unrelated edits, debug leftovers, dead or commented-out code, accidental files, unnecessary formatting churn, or other debris that obscures the intended change

## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->

Where it lives:
- In an eval bundle, read the repo facts block for PR template requirements, contribution instructions, stated policies, and disclosure requirements. Compare those requirements with the Candidate PR's title and description and any relevant maintainer direction in the issue thread
- In live mode, read `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, the issue thread, and the title and description in `pr_draft.md`. Use `voice-guide.md` separately for live mode voice guidance as directed by `SKILL.md`.

What good looks like:
Every applicable repository requirement is addressed with real content, including required template sections, issue references, contribution requirements, and AI-use disclosure when required. Explicit maintainer directions that apply to the submission are addressed. Boilerplate, missing required information, or an ignored applicable repository requirement does not satisfy the standard
