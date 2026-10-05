# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->
1. Read the issue and its thread first. Note the stated bug, any maintainer confirmed facts, and the repo's contribution policy
2. Read the repro evidence next. Note the exact observed behavior, the steps that produced it, and the environment recorded
3. Read the candidate plan last, before grading any check. Note its diagnosis, scope/changes section, approach, test plan, and risks as you go
4. Read the candidate plan comment text


## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->
- Diagnosis matches evidence: pull the plan's stated cause and file. Record it alongside the repro evidence's observed behavior and steps
- Scope is bounded: pull the list of files the plan says it will change and any explicit statement of what it will not touch
- Test plan is observable: pull the plan's test plan section. Record whether it names a concrete command, assertion, or automated test, or only a vague instruction
- Targets root cause, not symptom: pull the plan's approach section. Record whether it names a fix to the cause from the diagnosis, or only a fix to the visible symptom
- Executable by a stranger: pull every command, script, or file path the plan's approach references. Record whether each one is shown in the plan or already exists in the repo, or whether it depends on something only on the plan author's machine
- Unknowns stated honestly: pull the plan's risks/unknowns section. Record whether it names real unknowns, or presents an assumption as settled
- Comment reflects the thread: pull the plan comment's stated facts. Record whether they match the issue thread's actual content
- Comment follows repo conventions: pull the repo's contribution policy from the repo facts block or CONTRIBUTING.md. Record whether it requires an AI disclosure statement, and whether the plan comment includes one if required

If a check's evidence is genuinely absent from the package, record that explicitly rather than inferring an answer.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->
1. Grade checks in the order they appear in the rubric table
2. For each check, apply only the pass condition in the rubric row, using only the evidence gathered for the check. Do not reread the whole package for each check, use the notes from the Evidence gathering stage
3. Grade each check pass, fail, or unclear. Use unclear only when the needed evidence is genuinely missing from the package, not when it is merely thin
4. Record a one line fact or quote that decided each grade before moving to the next check

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->
1. Apply the rubric's verdict rule: accept only if every required check passed
2. Treat any required check graded fail or unclear as a hold, this is a binary outcome, with no partial credit
3. In the output, quote the evidence line for whichever check decided the verdict
4. Preferred checks, if any, never change the verdict, they are not present in this rubric, so this step does not currently apply 