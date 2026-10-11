# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->

1. Read the issue and its thread first. Note the stated bug, any maintainer-confirmed facts, and the repo's contribution policy
2. Read the plan next, including its Deviations section. Note the planned scope, files to change, approach, test plan, and any recorded deviations
3. Read the branch diff next. Note every changed file and substantive change, and compare them against the plan and its Deviations
4. Read the test evidence. Note the commands that were run, their observable results, the Unit 2 repro before and after, and the repo's required checks
5. Read the candidate PR title and description last. Note what it claims changed, the issue it references, its testing claims, any disclosed shortfalls or deviations, and any required disclosures

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->

- Plan fidelity: Pull the plan's scope, approach, and Deviations. Record them alongside the diff's changed files and substantive changes. Record whether every change is covered by the plan or an honestly recorded deviation, whether planned work was omitted, and whether the PR description accurately represents the implementation
- Test evidence: Pull the plan's test plan and the recorded test evidence. Record whether the planned verification and the repo's required checks were run and whether their actual outcomes are observable. Compare the PR description's testing claims against those results
- Diff quality: Pull the changed files and hunks from the branch diff. Record any unrelated changes, debugging artifacts, accidental files, commented out code, or other debris that is unnecessary for the intended fix
- Standards and comms: Pull the repo's PR template and contribution requirements from the repo facts or repository, and the candidate PR title and description. Record whether applicable template sections, issue references, contribution requirements, and disclosure asks are satisfied. Check factual claims against the diff and test evidence

If a check's evidence is genuinely absent from the package, record that explicitly rather than inferring an answer. An honestly reported test failure, unavailable check, or planned shortfall is not a failure by itself. Record it and apply the rubric's pass condition

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Grade checks in the order they appear in the rubric table
2. For each check, apply only the pass condition in the rubric row, using only the evidence gathered for that check. Do not reread the whole package for each check. Use the notes from the Evidence gathering stage
3. Grade each check pass, fail, or unclear. Use unclear only when the evidence needed to decide the check is genuinely missing or insufficient
4. Record a one line fact or quote that decided each grade before moving to the next check

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->

1. Apply the rubric's verdict rule: accept only if every required check passed
2. Treat any required check graded fail or unclear as a hold. This is a binary outcome with no partial verdict
3. If the verdict is reject, use the evidence line from the first failing or unclear required check in rubric order as the deciding evidence. Report any additional failing checks in their own evidence lines
4. If the verdict is accept, report the evidence supporting each passing check
5. Preferred checks, if any, never change the verdict. They are not present in this rubric, so this step does not currently apply
