# Rubric: is this pull request ready to submit?

Every check reads the PR against the plan, the issue, and the repo's
stated standards. Locations named below are defined in
`references/evidence-guide.md`. "Covered by a deviation note" means
the plan's deviation notes (live: `plan.md`'s `## Deviations`; eval:
any deviation stated in the Plan context) or the PR description
itself states the difference from the plan and why.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diff stays inside plan | Every changed file and hunk in the diff (eval: Candidate PR → Diff; live: `git diff main...HEAD`), read against the plan's stated files, scope, and "not in scope" boundary, plus deviation notes | Every changed file and every behavioral hunk falls inside the plan's stated scope or is covered by a deviation note. Fail if the diff changes a file, behavior, or API the plan does not name or explicitly puts out of scope, with no deviation note (silent drift: more than the plan). | required |
| Planned change delivered | The plan's steps and named changes, each looked up in the diff | Every change the plan commits to appears in the diff, or its absence is covered by a deviation note. Fail if a planned step (a code change, a guard, an error message, a doc update the plan names) is missing with no note (silent drift: less than the plan). | required |
| Description matches diff | Each factual claim in the PR title and description (what changed, what was fixed, what was tested, "no other changes", "follows the plan"), looked up in the diff and the test evidence | Every claim about what the PR does or proved is observable in the diff or the test evidence. Fail if the description claims a change, test, fix, or fidelity the diff or evidence does not show, or omits a behavioral change the diff makes so the reader would be misled. Grade each claim on its substance: it is supported when the change, test, or behavior it asserts is observable. Loose counting or granularity is not a mismatch (a new helper called only by the touched function, described as "one function touched"; several cases asserted inside one test function, described as "tests for X, Y, and Z"). Scope and fidelity claims ("no other changes", "exactly as planned", "only touches X") are contradicted by any hunk that changes other existing code, behavior, config, or files. | required |
| Planned tests present and decisive | The plan's test plan, read against the diff's test files and the Test evidence section's commands and output | Every test the plan commits to (a regression test to add, a repro to re-run, a control, a suite run) appears in the diff or the evidence, or its absence is covered by a deviation note; a supporting item (a control, the added test's run, a suite run) is present when the evidence names it with a specific result. AND at least one piece of evidence re-runs the plan's failing repro (not a control or an unchanged path), shows the actual command or input steps, and shows the observed result tied to that command: verbatim output lines, or, where the expected-after is an absence (the error no longer printed, a file no longer listed, a prompt no longer opening), an explicit after-statement attached to that command, with any visible text (a toast, an error message) quoted verbatim. That result shows the expected-after behavior, which differs from the before behavior in the repro evidence. Fail if a planned test is silently missing, if the evidence is prose only with no command or steps shown ("tests pass", "tested locally, works now", "verified it works"), if the only re-run is a control or an unchanged path, or if the shown result would be the same without the fix. | required |
| Repo's own checks run | The repo's stated test or check commands (eval: Repo facts → pull requests / contribution policy lines; live: `CONTRIBUTING.md`, PR template, CI config named there), read against the Test evidence section | If the repo names a suite or check (for example `cargo test`, `yarn test`, `pre-commit`, clippy), the evidence names that command or check with its stated outcome (for example "`cargo test -p ignore` passes (214 tests)", "fmt and clippy clean"), or the PR states plainly that it was not run and why; in either case the decisive repro evidence above is shown. A named-command result line is the accepted report form for the repo's own suite and needs no pasted log; it never substitutes for the decisive repro output. Passes when the repo names no command and the decisive evidence is shown. Fail if a named suite or check is silently never mentioned, if the only report is generic with nothing named ("all tests pass", "tests pass"), or if the decisive repro evidence is not shown. | required |
| Change is reviewable | Every hunk in the diff and every entry in the commit list | Every hunk serves the planned change (or a deviation note). Fail on any of: debug leftovers (prints, `console.log`, `dbg!`, stray logging), commented-out code, dead code, unrelated formatting or whitespace churn, drive-by edits to unrelated code, stray or generated files (lockfiles, build output, editor files) the change does not need, or unrelated hunks that bury the fix. | required |
| Repo asks honored | The repo's stated asks (eval: Repo facts block's PR-template asks and contribution policy, including any AI-use policy, plus explicit maintainer direction in Thread highlights; live: the PR template, `CONTRIBUTING.md`, AI policy, the thread, and `scope.md` house rules), each looked up in the title, description, commits, and diff | Every stated ask is met with real content or explicitly addressed: each template section the repo asks for is present and filled with content specific to this change (not left as placeholder text); a required closing link (`Closes #N`, `fixes #N`) is present; a required title or commit convention is followed; a required artifact (CHANGELOG entry, docs, whatsnew entry) is in the diff or its omission is explained; a required AI-use disclosure is present with the detail the policy asks for (tool used, extent of assistance); explicit maintainer direction in the thread is followed or engaged. If the repo states no AI policy, a missing disclosure is not a fail. Fail if any stated ask is visibly ignored. | required |
| Reviewer can orient fast | The PR title and the first lines of the description | The title names the behavior change (not just "fix bug" or the issue number alone), and the description says what changed and why in terms a reviewer can hold the diff against, and references the issue. Fail if a reviewer could not tell from the title and opening what the PR does. | preferred |

## Verdict rule

- **accept** (ready to submit) only if every `required` check grades
  `pass`.
- **reject** (hold) if any `required` check grades `fail`.
- `unclear` on a `required` check counts as `fail`: evidence the
  package does not contain cannot pass a check. Unclear is never a
  pass.
- `preferred` checks are graded and reported but never change the
  verdict.
- Honest-outcome rule: a stated shortfall (a deviation note, a check
  not run with the reason given) is graded against the pass conditions
  above, which accept an explained gap. Do not reject a package only
  because it delivers less than everything; reject it when a gap is
  hidden, contradicted, or unproven.
