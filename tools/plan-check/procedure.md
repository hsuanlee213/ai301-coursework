# Procedure: how this skill grades a plan package

## Read order

1. Read the issue text first. Note the reported problem in one sentence and any maintainer request or constraint.
2. Read the Repro evidence section next, before the plan. Note the exact commands, the exact observed output, and what cause that output points to. Do this before reading the plan so the plan's claims can be judged against the evidence rather than shaping how you read it.
3. Read the plan: diagnosis, scope, files to touch, approach, test plan, risks and unknowns. Note the stated cause, the files named, and the expected result after the fix.
4. Read the thread highlights and the repo-facts block last. Note what the thread already says and any stated convention for plans, branches, or commits.
5. Read the plan comment. Note what it claims and whether it matches the plan.

## Evidence gathering

1. Cause matches repro: copy the plan's stated cause. Copy the one line of Repro evidence that supports it, or record "none" if no line does. Record what cause the repro output points to on its own.
2. Change is bounded: list every file and every change the plan says it will make, and every thing it says it will not change. Record whether each file is needed by the stated cause.
3. Stranger could start: record the first file the plan says to open and the first edit it says to make. Record any step that depends on knowledge the plan never states.
4. Test proves the fix: copy the test plan's commands and its expected result. Record whether they re-run the repro steps and whether the expected result differs from the observed before output.
5. Unknowns not dressed as facts: list claims in the plan that the Repro evidence does not establish. Record whether each is labeled as an assumption.
6. Comment fits thread and conventions: record any thread highlight the comment repeats, contradicts, or ignores. Record each stated convention in the repo-facts block and whether the comment follows it.
7. If a part named above is missing from the package, record "absent" for that item. Do not look elsewhere for a substitute.

## Check execution

1. Run the checks in the order they appear in the rubric table.
2. Grade each check using only the notes recorded in Evidence gathering for that check. Do not re-read the whole package for a check whose notes are complete.
3. Grade P if the pass condition is met, F if the fail condition is met. Write one line saying which recorded fact decided it.
4. If the evidence for a check is absent, or the pass condition cannot be applied to what was recorded, grade `?` and write one line saying what is missing. Do not guess.
5. Never give credit for something the plan does not say. If a step needs knowledge the plan does not state, that is a gap, not a pass.

## Verdict assembly

1. List every required check with its grade (P, F, or ?).
2. Apply the rubric's verdict rule. Any required F gives hold. Any required `?` counts as F and gives hold. Only if every required check is P is the verdict ready.
3. Preferred checks are graded and reported but never change the verdict.
4. In the output, quote the rubric check name and the one line of evidence that decided the verdict. For a hold, quote the first failing required check. For a ready, say that every required check passed.
