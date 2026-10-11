# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Plan fidelity | The diff's changed files and behavior read against the plan's scope, approach, and Deviations, plus the PR description read against both the plan and diff | Pass if every substantive change in the diff is covered by the plan or an honestly recorded deviation, and the PR description accurately represents what the diff implements. An honestly disclosed planned shortfall may still pass. Fail when the diff silently adds, omits, or contradicts planned work or the description materially misrepresents the implementation | required |
| Test evidence | The test evidence read against the plan's test plan and the repo's required checks, with the PR description's testing claims read against the recorded outputs | Pass if the evidence shows the observable results for the planned verification and records the repo's required checks with their actual outcomes. A failing or unavailable check may still pass when its outcome and reason are honestly recorded. Fail when required verification was silently omitted or the evidence does not support the claimed result | required |
| Diff quality | The branch's diff's changed files and hunks read against the issue and the plan's stated implementation boundary | Pass if the diff is focused on the issue and contains no unrelated changes, debugging artifacts, accidental files, commented out debris, or other changes that unnecessarily obscure review of the intended fix | required |
| Standards and comms | The PR title and description read against the repo facts block's PR template, contribution requirements, and applicable disclosure asks, with factual claims checked against the diff and test evidence | Pass if the PR satisfies the repository's applicable submission requirements and disclosures and its outgoing claims are supported by the package. A requirement that does not apply does not cause failure. Fail when an applicable template, contribution, or disclosure requirement is ignored or materially contradicted | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only if every required check passes. Reject if any required check fails or is unclear. An unclear grade counts as fail because a required outcome that cannot be verified from the package is not ready to submit. Preferred checks, if any are added later, never change the verdict.
