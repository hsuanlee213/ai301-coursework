# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

**Where it lives:** The plan's stated cause is the `Cause:` line under `## Candidate plan`. The behavior that cause must explain is in `## Repro evidence`: its numbered Steps, the Expected line, and the Actual line. Read `## Issue` for the reported symptom.

**What good looks like:** The stated cause explains the Actual behavior in the repro evidence, and the plan names a mechanism rather than restating the symptom. A diagnosis fails when the repro evidence shows something the cause cannot explain (for example, the repro points to one component but the cause blames another), or when the cause is asserted with nothing in the repro evidence behind it.

## Scope

**Where it lives:** Under `## Candidate plan`, the `Change:` line and its `In:` and `Out:` statements, plus any files or areas it names.

**What good looks like:** One bounded change that a reviewer could hold the final diff against: named files or areas, plus an explicit statement of what is left alone. Not bounded: "clean up the module", several unrelated changes bundled together, or files named that the stated cause does not require.

## Executability

**Where it lives:** Under `## Candidate plan`, the `Change:` line (which files or areas, what edit) and any order of work it gives.

**What good looks like:** A stranger could open the named file or area and make the first edit without asking the author. Not executable: "fix the bug", "refactor as needed", or steps that rely on knowledge the plan never states.

## Test plan

**Where it lives:** Under `## Candidate plan`, the `Test:` line, read against the Steps and Actual in `## Repro evidence`.

**What good looks like:** The test re-runs the repro steps and names an observable result that differs from the before state, so it would fail without the fix. Not decisive: "run the test suite", "verify it works", or an expected result that would also be true before the fix.

## Honesty

**Where it lives:** Claims anywhere in `## Candidate plan` and `## Candidate plan comment`, compared with what `## Repro evidence` actually establishes. Unknowns and risks, if the plan states any, appear in the plan text or the comment.

**What good looks like:** Anything the repro evidence does not establish is labeled as an assumption or unknown. A short plan that claims nothing beyond its evidence is honest. False confidence is a claim stated as fact that the evidence does not support, such as asserting a root cause the repro never showed or promising behavior the plan never tested. In live mode, a mid-build deviation belongs under `## Deviations` at the end of plan.md.

## Comms

**Where it lives:** `## Candidate plan comment`, read against `## Thread highlights` (what the maintainer and others already said, or "no comments") and `## Repo facts` (bug-report template, contribution policy, and any AI-use disclosure requirement).

**What good looks like:** The comment responds to what the thread actually asks and follows what the repo-facts block states: for example respecting a policy that outside PRs are reviewed selectively, or including a required AI disclosure. Fails when it repeats or contradicts a maintainer's comment, ignores a stated contribution rule, or reads as boilerplate that would fit any issue. With zero thread comments, check only the repo-facts conventions.
