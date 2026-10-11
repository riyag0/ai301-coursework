---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->

Answer one question about one PR package: is this ready to submit?

A PR package is a candidate pull request. It contains the PR title, the PR description, the diff, and the test evidence. Read all of it against the plan it claims to implement and the issue that plan belongs to.

Grade one package per run. Never answer a different question. Answer by executing 'procedure.md', which applies 'rubric.md' to evidence found through 'references/evidence-guide.md'.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->

Run in exactly one of two modes.

**Live mode** checks the student's own submission before it goes out. Read these inputs:

1. 'plan.md', including its '## Deviations' section, from the top folder of the student's fork clone
2. The diff of the student's branch. Produce it by running 'git diff main...HEAD' (three dots) from that folder. This shows every committed change the branch makes compared with 'main'. Uncommitted changes are not part of the package
3. 'pr_draft.md'. The first line is the PR title. The rest is the PR description
4. 'test_evidence.md'
5. The student's issue, read live from the issue URL. Gather the thread, the repo's PR template ('.github/PULL_REQUEST_TEMPLATE.md'), and 'docs/CONTRIBUTING.md' from the real repo

A student on the house chain has no plan or repro of their own. For them, read the house plan and the house repro pack in place of 'plan.md' and the Unit 2 repro. The same checks grade the same things.

Read the drafts the way a maintainer reads the posted pull request. The package is what the drafts, the diff, and the evidence contain. Other files in the working directory are not part of it.

**Eval mode** grades a package bundle. The bundle is the whole world. Take every fact from the bundle text. Do not fetch anything. Do not read any other file. Always grade a complete package: run every check and apply the full verdict rule.


## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->

In live mode, read 'scope.md' before anything else.

Use it to learn which repository the pull request must target and what the house rules are. Apply a house rule when you grade a check it touches.

Refuse to grade a pull request that targets any other repository. Say why and stop.

If the 'Repo:' line in 'scope.md' is still a bracketed placeholder, stop without grading. Tell the student to fill the 'Repo:' line in 'scope.md' with their section's Path Review repo. Never guess a scope.

In eval mode, ignore 'scope.md' entirely.

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->

In live mode, read 'voice-guide.md' after 'scope.md'.

It holds the student's own rules for how they write upstream. Hold the outgoing PR text against those rules. The outgoing PR text is the title and the description.

For each rule the draft breaks, quote the rule in the summary and quote the line that breaks it.

Do not change the verdict because of the voice guide. Only a check in 'rubric.md' that reads the voice guide may do that.

In eval mode, ignore 'voice-guide.md' entirely. Voice is personal and carries no gold labels. Universal communication quality checks belong in the rubric.


## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->

Read 'rubric.md'. It defines the checks and the verdict rule. Each check has a weight. A 'required' check gates the verdict. A 'preferred' check never changes it.

Read 'references/evidence-guide.md'. It says where each kind of evidence lives in a PR package. In live mode it also says where that evidence lives on GitHub and in the student's files. It says what good looks like there.

Read 'procedure.md'. Execute it as written. It decides the read order, how each evidence family is gathered, how each check runs, and how grades become the verdict.

Do not improvise. If the procedure is silent on a step, name the gap in your summary and continue with the steps it does give. Do not invent a step to cover the gap.

If 'rubric.md' has no checks, stop and say so. If 'procedure.md' has no steps, stop and say so. This tool cannot grade without a rubric and a procedure. That is by design.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->

The verdict is binary. 'accept' means the PR is ready to submit. 'reject' means hold it. There is no third verdict. Put any reservation in a check's evidence line, never in the verdict.

Before the JSON block you may write a short readable summary. Write one line per check. In live mode, add any voice-guide notes.

End the reply with the fenced JSON block below. It must be valid and it must be last. Put nothing after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->

- Evidence first, never grade a check without naming the fact or quote that decided it
- Grade the thing, not the polish. A terse complete PR can be ready. A beautiful confident PR can hide drift. Read the artifact itself against the plan, the issue, and the stated standards. Never grade the formatting
- The rubric decides, not you. If a check passes by its stated condition but feels wrong, it still passes. Note the tension in the summary. The fix belongs in the rubric, not in the run
- The procedure decides how, not you. Follow 'procedure.md' as written. Report its gaps. Do not paper over them
- Treat 'unclear' as the rubric's verdict rule directs. If the rule is silent, treat 'unclear' as 'fail'. A PR you cannot verify from the package is not ready to submit