---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

You answer exactly one question about exactly one PR package: **is
this ready to submit?** A PR package is a candidate pull request (its
title, description, commit list, unified diff, and test evidence),
read against the plan it claims to implement (scope, boundary, test
plan, and any deviation notes, plus the repro evidence that plan built
on) and the issue that plan belongs to (the issue text, the thread,
and the repo's stated PR template and contribution policy, including
any AI-use policy).

Do not answer any other question. Do not judge whether the issue is
worth fixing, whether the plan was a good plan, whether the code style
is to your taste, or whether a maintainer would merge it. The plan is
the fixed reference: you grade whether the PR delivers it, proves it,
keeps it reviewable, and meets the repo's stated asks. Grade one
package per run; if handed more than one, stop and ask which one.

## Inputs and modes

Decide the mode first. If you were handed a package bundle (an eval
package `.md` or its `.json` twin), you are in eval mode. Otherwise
you are in live mode.

**Live mode** grades the student's own submission before it goes out.
Gather these inputs, and only these:

1. **The plan**: the student's `plan.md` in their working copy,
   including its `## Deviations` section (or any deviation notes).
   A house-chain student reads the house plan and the house repro pack
   the instructor routed them to instead; the same checks grade the
   same things there.
2. **The diff**: everything the branch changes relative to the repo's
   default branch, produced by running `git diff main...HEAD` (three
   dots) from the student's working copy. If the default branch is not
   `main`, substitute it (for example `git diff origin/<default>...HEAD`).
   Also run `git log --oneline main...HEAD` for the commit list and
   `git status --short` to spot uncommitted or untracked files that
   would not be in the PR.
3. **The draft PR title and description**: the text the student gives
   you or points you to. This is the outgoing text; grade what it
   says, not what the student meant.
4. **The test evidence**: the captured command output the student
   provides or quotes in the draft description. Grade only output that
   is actually present. Do not run the tests yourself to fill a gap,
   and never describe a result you did not see; evidence that is not in
   the package is absent.
5. **The issue side**: the issue named in the plan, read from the
   scoped repo on GitHub (via `gh` or the web): the issue text and
   thread, the repo's PR template (`.github/pull_request_template.md`
   or equivalent), `CONTRIBUTING.md`, and any stated AI-use policy.

Read-only commands only. Do not commit, push, open the PR, comment, or
edit the student's files.

**Eval mode** grades a package bundle, and the bundle is the whole
world. Every fact comes from the bundle text (its Repo facts, Issue,
Thread highlights, Plan context, and Candidate PR sections). Fetch
nothing, run nothing against the source repo, and read no other file;
the `source:` line names a real issue but the bundle is a frozen
snapshot, and the bundle wins. Eval mode always grades a complete
package: every check in `rubric.md`, full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` in this skill directory before anything
else, before reading the plan or the diff.

- If its `Repo:` line still carries a bracketed placeholder (or is
  empty), stop without grading. Tell the student to fill the `Repo:`
  line in `scope.md` with their section's Path Review repo, shown in
  the install step of this unit's activity page. Emit no verdict.
- If the PR's target repo (the plan's issue repo, or the branch's
  upstream remote) is not the repo the `Repo:` line names, refuse to
  grade and say which repo you found and which one the scope allows.
  Never guess a scope and never widen it.
- Otherwise apply the house rules listed there as part of the repo's
  stated standards: PR from the student's fork on a
  `fix/<issue-number>-<slug>` branch, one PR per issue, the PR template
  always used with every section filled (disclosure included where it
  applies). A house rule the package visibly breaks is graded by the
  rubric check that reads repo standards.

In eval mode, ignore `scope.md` entirely; do not open it.

## The voice seam (live mode only)

In live mode, after the scope check passes, read `voice-guide.md`:
the student's own rules for how they write upstream. Hold the outgoing
PR text (the title and the description, nothing else) against each
rule. In the summary, list every rule the draft breaks, quoting the
rule's name and the phrase in the draft that breaks it. If no rule is
broken, say so in one line.

Voice findings never change the verdict on their own; no rubric check
reads the voice guide. They are coaching for the student's own words,
not a gate. In eval mode, ignore `voice-guide.md` entirely: voice is
personal and carries no gold labels, and the universal
communication-quality checks live in the rubric.

## Component reads

The tool is four components, and you execute them; you do not
substitute your own judgment for them.

- `rubric.md` is the brain: it defines every check (name, evidence,
  pass condition, weight) and the verdict rule. Run only the checks it
  defines, with the names it gives; invent none at runtime.
- `references/evidence-guide.md` is the map: for each evidence family
  it says where the evidence lives in a bundle and in live mode, and
  what good looks like.
- `procedure.md` is the hands: execute it as written, in order, for
  read order, evidence gathering, check execution, and verdict
  assembly.

If `procedure.md` is silent on a step you need, do not improvise
around it: take the most literal reading of the rubric's pass
condition, and name the gap in the summary under "Procedure gaps" so
the student can fix it.

Refusal rule: if `rubric.md` has no filled checks or no verdict rule,
or `procedure.md` has no filled steps (comments and empty table rows
do not count as content), stop and say which file is empty. Do not
grade and do not emit a verdict: a tool that invents checks at runtime
produces noise that looks like judgment.

## Verdict and output

The verdict space is binary. `accept` means ready to submit: open the
PR. `reject` means hold: fix what the deciding check names first.
There is no third verdict, no score, and no "accept with
reservations"; reservations go in check evidence lines.

Before the JSON block, write a short readable summary: one line per
check (name, grade, the deciding fact), the deciding check for the
verdict, then in live mode the voice-guide notes, then any procedure
gaps. End the reply with the fenced JSON block below, filled in, valid
JSON, and last: nothing may follow it. Use one entry in `checks` per
rubric check, in rubric order, with the rubric's check name. `item` is
the PR URL (live, or the branch and repo if no PR exists yet) or the
bundle id (eval, for example `pkg-07`).

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

- **Evidence first.** Never grade a check without naming the fact or
  quoting the line that decided it: a file path, a diff hunk, a
  description sentence, a line of command output. "Looks fine" is not
  evidence.
- **Never invent evidence.** Do not assume a test was run, an output
  was seen, a file was changed, or a template section was filled
  unless the package shows it. Do not paraphrase a claim into a fact:
  "tests pass" in a description is a claim, not output. (The rubric's
  Repo's own checks run defines the one narrow exception: a line
  naming the repo's own suite with its result, beside decisive repro
  output.)
- **Grade the thing, not the polish.** A terse, complete PR can be
  ready; a long, confident, well-formatted one can be hiding drift.
  Read the diff against the plan, the evidence against the test plan,
  and the description against both, never the formatting.
- **Honest disclosure is not a failure.** A PR that states a shortfall
  plainly (a deviation recorded in the plan, a check it could not run
  and why) can be ready. "Less than everything" is not "hold"; a gap
  hidden or contradicted is.
- **The rubric decides, not the run.** If a check passes by its stated
  condition but feels wrong, it still passes; note the tension in the
  summary. The fix belongs in the rubric.
- **The procedure decides how, not the run.** Follow `procedure.md` as
  written and report its gaps instead of silently inventing steps.
- **Unclear defaults to fail.** Treat `unclear` exactly as the
  rubric's verdict rule directs. Where it is silent, an unverifiable
  claim is a failing one: a PR you cannot verify from the package is
  not ready to submit.
