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
| Environment recorded | The repro report's environment record, including relevant OS, runtime, dependency, and version information. | Pass if the environment records enough relevant setup and version information for another contributor to understand the conditions of the reproduction attempt. | required |
| Steps reproducible | The reproduction steps and commands in the repro report. | Pass if another contributor could follow the actions in order to attempt the same reproduction without guessing a necessary step. | required |
| Behavior matches issue | The observed output, error, logs, screenshots, or other artifacts read against the behavior described in the issue. | Pass if the evidence shows the behavior described by the issue, or clearly shows that the reported behavior could not be reproduced under the recorded conditions. | required |
| Outcome supported | The repro report's stated outcome read against its observed results and artifacts. | Pass if the stated conclusion is supported by the evidence, including an evidenced cannot-reproduce result; fail if the conclusion claims behavior that the evidence does not show. | required |
| Repo conventions | The claim comment and repro report read against the repository conventions and AI-use policy stated in the repo-facts block. | Pass if the comments follow all applicable repository requirements. If the repository requires AI-use disclosure, the submitted comments must include the required disclosure, including the tool and extent of assistance when the policy requires them. | required |

## Verdict rule

Accept if every required check passes. Treat unclear as fail and reject the package until the missing evidence is resolved.

