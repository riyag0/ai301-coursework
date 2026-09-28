# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | Environment section per reference/evidence-guide.md | Specific versions and any mismatch with the issue's stated target is explicitly called out rather than left unmentioned | required |
| Steps are complete and easy to follow  | Steps section per references/evidence-guide.md | Steps begin from a clearly named starting state and proceed in order without a gap a another person would need to guess | required |
| Behavior matches the issue | Behavior shown section per references/evidence-guide.md | If the report claims reproduction succeeded, the pasted output shows the same specific behavior the issue names. If the report honestly states it could not reproduce the behavior, this check passes regardless of what the output shows | required |
| Outcome stated honestly | Honesty section per references/evidence-guide.md | The stated conclusion claims no more than the Steps and Behavior shown sections actually support | required |
| Words respect the repo's conventions | Comms section per references/evidence-guide.md | The comment names specific facts about the actual issues rather than generic boilerplate. This check only requires a disclosure statement when the policy explictly asks the contributor to state that AI was used | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept if every required check passes. A single required check fail or unclear rejects the package. Unclear is treated as fail for all checks.