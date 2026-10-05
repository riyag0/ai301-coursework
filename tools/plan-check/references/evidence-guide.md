# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->
Where it lives: in an eval bundle, the "Cause:" line under Candidate plan, read against the "Repro evidence" section's Steps and Expected/Actual lines. In live mode, the plan's diagnosis read against the student's own posted repro comment

What good looks like: the stated cause accounts for every step the repro evidence observed, not just the headline symptom. In calib-01, the cause of "that view's model is not refreshed... until the view is rebuilt on reentry", explains both the failure at step 3 and the fix on reentry at step 4. A cause that contradicts a step, or explains only part of what was observed, does not ground


## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->
Where it lives: the "Change:" line under Candidate plan, specifically its "In:" and "Out:" sub parts. In live mode, the plan's own scope or changes section

What good looks like: the plan names the specific files or areas it will touch and explicitly states what it will not touch. calib-01's Change line names 'pkg/gui/controllers/sync_controller.go' and the push callback as In, and excludes "any change to how push status is computed, or to other views refresh behavior" as Out. A plan with files named but no Out statement or whose described change drifts into unrelated areas, is not bounded

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->
Where it lives: the "Change:" line's described approach, read against the "Cause:" line it should address, plus every file, function, or command named anywhere in the Candidate plan

What good looks like: First, the change targets the mechanism named in Cause, not just the symptom. Second, every referenced file or command either already exists in the repo or is fully specified in the plan, with nothing that depends on something only on the plan author's own machine. 
## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->
Where it lives: the "Test:" line under Candidate plan, read against the Repro evidence's Steps

What good looks like: a concrete check with a stated pass condition, built from the repro steps rather than invented separately. calib-01's Test line reuses the repro steps, states exactly what must be observed and extends the check to the two related surfaces sharing the same callback

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->
Where it lives: any explicit risks or unknowns named in the Candidate plan, live. Also, the ## Deviations section of a built plan

What good looks like: real uncertainty is named as uncertainty, not asserted as settled fact. calib-01 has no seperate risks line, but it treats the shared callback case as something to verify rather than assume, by folding it into the test
plan instead of skipping it. A plan that states an untested assumption as if confirmed is false confidence 

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->
Where it lives: the Candidate plan comment, read against the Issue, Thread highlights, and the "contribution policy" line under Repo facts

What good looks like: every fact the comment states matches the issue and thread and the comment follows any convention the policy states, including AI disclosure where required. calib-01's comment matches its own plan and the repro evidence, and the repo's policy states no AI disclosure requirement, so silence on AI use passes here 
