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

Where it lives: In eval mode, look at the repro report's environment record and the issue context. In live mode, look at the student's draft repro comment and the issue's stated environment or version requirements.

What good looks like: The report identifies the relevant OS, runtime, dependency, or version information needed to understand the reproduction attempt. The recorded environment should match the issue's target environment, or any relevant difference should be clearly stated.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

Where it lives: In eval mode, look at the reproduction steps and commands in the repro report. In live mode, look at the student's draft repro comment.

What good looks like: The steps describe the setup and actions from the starting state through the trigger of the reported behavior. Another contributor should be able to attempt the reproduction without guessing a necessary action.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

Where it lives: In eval mode, look at output excerpts, logs, screenshots, or other artifacts in the repro report and compare them with the issue context. In live mode, compare the student's evidence with the behavior described in the GitHub issue.

What good looks like: The evidence demonstrates the specific behavior described by the issue rather than a different or adjacent problem. A cannot-reproduce result is acceptable when the evidence clearly shows what was attempted and observed.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

Where it lives: Compare the repro report's stated outcome with its observed results, artifacts, and the issue description.

What good looks like: The conclusion says only what the evidence supports. A supported cannot-reproduce result is valid, while a claim of successful reproduction must be backed by evidence showing the issue's described behavior.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

Where it lives: In eval mode, look at the claim comment, repro report, repo-facts block, and applicable repository contribution or AI-use policies. In live mode, check the issue thread, repository documentation, and the student's draft comment.

What good looks like: The comments are specific to the issue and follow the repository's applicable contribution conventions and disclosure requirements. They should accurately describe what the student plans to do or actually observed without unsupported claims.
