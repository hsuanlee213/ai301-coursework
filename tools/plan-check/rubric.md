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

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Cause matches repro | The plan's stated cause, read against what the Repro evidence section actually shows | The cause the plan names is something the repro evidence directly shows (a quoted output, line, or error), and the plan targets that cause rather than restating the symptom. Fail if the repro points to a different cause, if the evidence does not support the stated cause, or if the plan quotes no repro evidence for it. | required |
| Change is bounded | The plan's scope statement (what it changes and what it will not), read against its files-to-touch | The plan describes one bounded change a reviewer could hold the final diff against. Fail if the scope is open-ended, includes unrelated cleanup, or the files it touches go beyond what the stated cause requires. | required |
| Stranger could start | The plan's approach and files-to-touch | Someone who has never seen the repo could tell which files to open and what to change first, without asking the author. Fail if key steps depend on unstated knowledge or say only "fix the bug". | required |
| Test proves the fix | The plan's test plan, read against the repro evidence's steps | The test re-runs the repro and states an observable result that differs from the before state, so it would fail without the fix. Fail if it would pass either way (e.g. "run the test suite") or states no expected result. | required |
| Unknowns not dressed as facts | The plan's risks and unknowns, read against the claims elsewhere in the plan | Anything the repro evidence does not establish is labeled as an assumption or unknown, not stated as fact. A short plan that claims nothing beyond its evidence passes. Fail if a claim goes beyond the evidence with no hedge. | preferred |
| Comment fits thread and conventions | The plan comment, read against the thread highlights and the repo-facts block | The comment does not repeat or contradict what the thread already says, and follows any convention the repo-facts block states for plans, branches, or commits. Fail if it ignores a maintainer request in the thread or breaks a stated convention. | required |

## Verdict rule

- **ready** only if every required check is P.
- **hold** if any required check is F.
- A `?` on a required check counts as F. Unclear is never a pass.
- Preferred checks never change the verdict.
