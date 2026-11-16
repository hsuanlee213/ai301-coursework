# Procedure: how this tool grades a PR package

## Read order

0. Live mode only, before anything else: read `scope.md` and apply
   SKILL.md's scope seam (placeholder → stop; out-of-scope repo →
   refuse). Then read `voice-guide.md` and set it aside until Verdict
   assembly. Eval mode skips this step and never opens either file.
1. Read the repo's stated standards first (eval: `## Repo facts`;
   live: the PR template, `CONTRIBUTING.md`, any AI policy, and
   `scope.md` house rules). Write down, as a numbered list, every
   stated ask: template sections, closing-link requirement, title or
   commit convention, required artifacts (CHANGELOG, docs), named test
   or check commands, and the AI-use disclosure requirement (or "no
   stated AI policy").
2. Read the issue and the thread (eval: `## Issue` and
   `## Thread highlights`; live: the issue page). Write down the
   reported behavior in one sentence and any explicit maintainer
   direction (quote it), or "none".
3. Read the plan before opening the PR (eval: `## Plan context`;
   live: `plan.md` and its `## Deviations`). Write down: the repro's
   observed before behavior (quote the output line), the plan's files,
   its numbered steps or changes, its "not in scope" boundary, its
   test plan items, and each deviation note. The plan goes first so
   the diff is held against what was promised, instead of the diff
   shaping how the plan is read.
4. Read the diff next (eval: `### Diff`; live: `git diff main...HEAD`)
   and the commit list (eval: `### Commits`; live:
   `git log --oneline main...HEAD`). Write down every changed file and
   one line per hunk saying what it does. Live: also note any file in
   `git status --short` that is uncommitted and therefore not in the PR.
5. Read the test evidence (eval: `### Test evidence`; live: the
   captured output the student provides or quotes). Write down each
   command shown and the output shown beside it, verbatim, and each
   result that is claimed in prose without output.
6. Read the title and description last (eval: `### Title` and
   `### Description`; live: the draft text). Write down each factual
   claim as its own line. They go last so every claim can be checked
   against the diff and evidence already recorded, not trusted ahead
   of them.

## Evidence gathering

Build these pairings from the notes above. Record facts, not
judgments; quote where possible.

1. Diff stays inside plan: for each changed file and hunk from step 4,
   mark it `planned` (name the plan item), `deviation` (name the note),
   or `unplanned`. Also mark any hunk that touches something the plan's
   boundary puts out of scope.
2. Planned change delivered: for each plan step from step 3, record the
   hunk that delivers it, or `missing`, and for each `missing` whether a
   deviation note or the description explains it.
3. Description matches diff: for each claim from step 6, record the
   hunk or evidence line that supports what it asserts in substance,
   or `unsupported` (a counting or granularity slip is not
   `unsupported`; a scope or fidelity claim contradicted by any
   unplanned hunk is). Separately
   record any behavioral hunk the description never mentions.
4. Planned tests present and decisive: for each test plan item from
   step 3, record where it appears (a test file hunk in the diff, a
   command in the evidence), or `missing` plus any deviation note.
   A supporting item (control, added-test run, suite run) named in the
   evidence with a specific result records as present. Then record the
   strongest piece of evidence: whether it is the plan's failing repro
   or a control, its command or input steps, its observed result
   (verbatim lines, or the explicit after-statement attached to that
   command when the expected-after is an absence), the plan's
   expected-after, and the repro's before output. Record whether the
   result differs from the before output. If the evidence shows no
   command or steps (prose only), record `no output shown`.
5. Repo's own checks run: for each test or check command listed in
   step 1, record its output or its named-command result line from the
   evidence (quote it), a stated reason it was not run, `unnamed claim`
   if only a generic "tests pass" covers it, or `not mentioned`. If
   step 1 lists none, record `none named`.
6. Change is reviewable: from step 4, record every hunk that is debug
   output, commented-out code, dead code, formatting or whitespace
   churn, an unrelated edit, or a stray or generated file. Record
   commit messages that describe unrelated work.
7. Repo asks honored: for each ask listed in step 1, and each
   maintainer direction from step 2, record where the PR meets it
   (quote the section heading or line, or name the file in the diff),
   `placeholder` if a section exists but holds template text only, or
   `absent`. For the AI policy, record the disclosure text verbatim or
   `absent`.
8. Reviewer can orient fast: record the title verbatim and the first
   sentence of the description, and whether the issue is referenced.
9. If a part of the package is missing (no test evidence section, no
   description, no plan test plan), record `absent` for every item
   that depends on it. Do not look elsewhere for a substitute, and do
   not reconstruct what it probably said.

## Check execution

1. Run the checks in rubric table order, one at a time.
2. Grade each check using only the record for it from Evidence
   gathering. Re-open the package only when that record is incomplete,
   and then only the part the record points to.
3. Grade `pass` when the pass condition holds on the recorded facts,
   and `fail` when any stated fail case is recorded (one `unplanned`
   hunk, one `missing` step without a note, one `unsupported` claim,
   one `absent` stated ask, one debris hunk is enough).
4. Grade `unclear` only when the record needed to apply the pass
   condition is `absent` or the package is genuinely ambiguous (for
   example, the plan names no files at all). Write what is missing.
   Do not guess in either direction.
5. A deviation note counts only if it states what changed from the
   plan; a note covers only what it names.
6. A claim in prose is never output. "All tests pass" with no command
   output records as `no output shown`, never as a passing run. The one
   exception is the rubric's: for Repo's own checks run, a result line
   naming the repo's command or check is that check's accepted report.
   It never stands in for the decisive repro output.
7. Write each check's evidence as one line: the deciding fact, quoting
   the file, hunk, claim, or output line that decided it.

## Verdict assembly

1. List every required check with its grade.
2. Apply the rubric's verdict rule: any required `fail` → `reject`;
   any required `unclear` counts as `fail` → `reject`; every required
   check `pass` → `accept`. Preferred checks never change the result.
3. The deciding check: for `reject`, the first required check in
   rubric table order whose grade is `fail` or `unclear`; quote its
   evidence line in the summary as the reason to hold. For `accept`,
   state that every required check passed and quote the decisive test
   evidence line.
4. Live mode only: after the verdict, list voice-guide rules the title
   or description breaks (rule name plus the offending phrase). These
   never change the verdict.
5. List any procedure gaps you hit.
6. End with the JSON block exactly as SKILL.md specifies: one entry per
   rubric check, in rubric order, with the same grades and evidence
   lines, and the verdict from step 2. Nothing after it.
