# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/122


**Branch**

fix/63-readme-word-count


## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

20/20

**Package analysis**

pkg-03 was the one my rubric decided reject and the gold label was also reject.

The Plan fidelity check rejected this package because the accepted plan described "one bounded change" in `src/modules/directory.rs` with one module test, but the candidate PR contained additional substantive changes outside that plan. In addition to the planned fallback for `contract_repo_path`, the diff refactored the `truncate` helper and added a new `resolve_symlinks` configuration option. The candidate description claimed, "Implements the posted plan exactly" and "No other behavior changes," even though those extra changes appeared in the diff. This is silent drift because the implementation went beyond the plan without recording those changes as deviations.

**Check rationale**

I wrote this Plan fidelity check "Pass if every substantive change in the diff is covered by the plan or an honestly recorded deviation, and the PR description accurately represents what the diff implements. An honestly disclosed planned shortfall may still pass. Fail when the diff silently adds, omits, or contradicts planned work or the description materially misrepresents the implementation" to require the actual PR changes to match the accepted plan rather than only checking whether the main issue was fixed. This matters because a PR can include extra changes that were never part of the plan, even if the intended fix itself is correct. I wanted the check to accept changes that follow the plan or are honestly recorded as deviations, and reject changes that silently add, omit, or contradict planned work.

**Trade-offs**

I made every current check required and made an unclear required check result in rejection. This gives up some tolerance for incomplete evidence, but a PR should not be marked ready when a required result cannot be verified. At the same time, the Test evidence check does not automatically reject an honestly recorded failing or unavailable check. It rejects silently omitted verification or unsupported claims instead. I kept this balance because the goal is reviewable, truthful evidence rather than making every local command appear successful. No rubric changes were needed after the scored evaluation: the first completed full run produced 20/20, with clear-accept 7/7, not-tested 4/4, silent-drift 4/4, standards-wall 2/2, and unreviewable 3/3.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
