# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis matches evidence | Plan's diagnosis, read against the repro evidence's steps and observed output | The diagnosis names a cause tied to a specific file or component, and that cause accounts for everything the repro evidence actually showed. It does not contradict or ignore a result the evidence reported. | required |
| Scope is bounded | Plan's scope/changes section | The plan names specific files or components it will change and explicitly states what it will not touch. Exact function names may be deferred if the plan says why and names where they will be found. It does not expand into unrelated fixes or files beyond what the diagnosis requires. | required |
| Test plan is observable | Plan's test plan section | The plan gives clear, concrete steps or commands to verify the fix, ideally an automated test. | required |
| Targets root cause, not symptom | Plan's approach, read against the diagnosis | The approach addresses the cause the diagnosis names. It does not patch only the visible symptom while leaving the named cause unaddressed. | required |
| Executable by a stranger | Plan's approach, file list and any commands or scripts it references | A stranger could run every referenced command from a fresh clone of the repo, with nothing that only exists on the plan author's machine. A command that calls a script, fixture, or file not shown in the plan or already in the repo fails this check, even if the command itself looks specific. | required |
| Unknowns stated honestly | Plan's risks and unknowns section | Genuine unknowns or risks are named as such. The plan does not present an untested assumption as a certainty. | required |
| Comment reflects the thread | Plan comment text, read against the issue thread | The comment's stated facts match what the thread actually says. It does not contradict or ignore something a maintainer or prior commenter already established. | required |
| Comment follows repo conventions | Plan comment text, read against the repo's contribution policy | The comment follows any stated repo convention, including AI disclosure requirements where the policy explicitly asks for one. | required |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." --> 
Accept if every required check passes. A single required check fail or unclear rejects the package. Unclear is treated as fail for all checks.
