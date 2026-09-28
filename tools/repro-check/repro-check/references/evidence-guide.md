# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

Where it lives: In an eval bundle, the repro report's environment section or a repo facts block naming language,runtime, and OS versions.

What good looks like: The environment names specific versions such as language runtime, OS, package manager, and dependency versions that either match what the issue targets or any mismatch is explicitly named rather than silently ignored.


## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

Where it lives: In an eval bundle, the repro report's numbered steps. In live mode, the draft comment's step list, read against the issue body's own reproduction steps or its described trigger condition.

What good looks like: The steps begin from a clearly named starting state and proceed in an order a stranger could execute without guessing an omitted step, each step names an exact command, file, or action rather than a vague instruction like configure it.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

Where it lives: In an eval bundle, the report's evidence section such as a code block, log excerpt, or screenshot description. In live mode, the draft comment's pasted output, read directly against the behavior the issue describes.

What good looks like: The artifact shows the same specific behavior named in the issue rather than a different similar problem. A generic it broke without the actual output does not count as a shown behavior.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

Where it lives: The report's stated conclusion, read against its own evidence in the Steps and Behavior shown sections above.

What good looks like: The conclusion claims no more than the evidence supports. An honest "I followed these steps and did not observe the described behavior" is a pass when the steps and environment are genuinely reported.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

Where it lives: The claim comment and repro comment text, read against the issue's own content and the repo's contributing file or issue/PR templates.

What good looks like: The comment names specific facts about the actual issue and if the repo's contribution policy requires disclosing AI tool use, the comment states that disclosure plainly rather than omitting it.