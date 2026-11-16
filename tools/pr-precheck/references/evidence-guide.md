# Evidence guide: where evidence lives in a PR package

An eval bundle has these sections: `## Repo facts`, `## Issue`,
`## Thread highlights`, `## Plan context` (the accepted plan plus the
repro evidence it built on), and `## Candidate PR` with `### Title`,
`### Description`, `### Commits`, `### Diff`, and `### Test evidence`.
The `.json` twin holds the same content as fields. In live mode, the
same families come from the working copy and the scoped repo on
GitHub, as listed under each heading.

## Plan fidelity (harness category: silent-drift)

**Where it lives:**
- Eval: the plan's scope, steps, files, and "Not in scope" boundary
  are in `## Plan context` (usually a `Plan:` paragraph with `Files:`
  and `Not in scope:` statements); any deviation is stated there or in
  `### Description`. What actually changed is `### Diff` (file headers
  `--- a/` / `+++ b/` and each `@@` hunk). Fidelity claims are in
  `### Title` and `### Description`.
- Live: `plan.md` (scope, files, steps) and its `## Deviations`
  section; the branch diff from `git diff main...HEAD` run in the
  working copy; the draft title and description.

**What good looks like:** Every changed file and behavioral hunk maps
to a plan step or a deviation note, and every plan step maps to a
hunk or a deviation note. An honest deviation states what differs and
why, in the plan or the description, and re-ties the mismatch. Silent
drift runs both ways: more (a new flag, a refactor, a second bug fixed,
an out-of-scope file) or less (a planned guard, message, or doc change
missing) with no note. The description's claims belong here too: "as
planned", "no other changes", "also handles X" are fidelity claims, and
a claim the diff contradicts is silent drift, not a wording problem.

## Test evidence (harness category: not-tested)

**Where it lives:**
- Eval: `### Test evidence` (commands and their output, often with
  before/after), read against the `Test plan:` in `## Plan context`
  and the repro evidence's observed before output there. Test files
  the plan promised appear in `### Diff`. The repo's own suite or
  check commands are named in `## Repo facts` (the pull requests and
  contribution policy lines, e.g. `cargo test`, `yarn test`,
  pre-commit, clippy).
- Live: the captured terminal output the student provides or pastes
  into the draft description; `plan.md`'s test plan; test files in
  the branch diff; the repo's `CONTRIBUTING.md` and PR template for
  the named commands. Only output actually present counts; the tool
  does not run tests to fill a gap.

**What good looks like:** The plan's repro is re-run on the branch
with the actual command and its actual output shown, and that output
is the plan's expected-after, visibly different from the repro's
before. Every planned test (for example "add a regression test in
`tests/x`") is in the diff, or a note says why not. Where the repo
names a suite or check, its outcome is reported, or the PR says plainly
it was not run and why; a line naming the command with its result
("`go test ./...` passes (4108 tests)") is the normal report form for
the repo's suite, beside the decisive repro output. A repro transcript
counts as actual output when it shows the commands or input steps and
ties each to its observed result: verbatim lines, visible text such as
a toast quoted verbatim, or for an expected absence (error gone, file
not listed) an explicit after-note on that command. Not decisive:
"tests pass" or "all tests pass" with nothing named, "verified it
works" with no command shown, a screenshot described but not shown, a
control or unchanged path run in place of the failing repro, output
that would be the same without the fix, or a passing suite that never
exercises the changed behavior.

## Diff quality (harness category: unreviewable)

**Where it lives:**
- Eval: `### Diff` (every hunk, every file header) and `### Commits`
  (each message).
- Live: `git diff main...HEAD`, `git log --oneline main...HEAD`, and
  `git status --short` for files left out of or accidentally added to
  the branch.

**What good looks like:** A reviewer can find the fix in seconds: every
hunk serves the planned change, and commit messages describe that
change. Debris tells: debug prints or logging left in (`print(`,
`console.log`, `dbg!`, `eprintln!("DEBUG`), commented-out blocks, dead
code or unused helpers, whole-file reformatting or whitespace churn,
import reordering, renames unrelated to the fix, drive-by edits in
other functions, lockfile or generated-file churn, editor or OS files
(`.DS_Store`, `.vscode/`), and "wip"/"fix typo" commits carrying
unrelated work.

## Standards and comms (harness category: standards-wall)

**Where it lives:**
- Eval: `## Repo facts` — the `pull requests:` line (template
  sections, title convention, closing-link ask, required checklist
  items, CHANGELOG or docs entries, restrictions such as "not accepting
  new features") and the `contribution policy` line (CLA, stated rules,
  and the AI-use policy, or "no stated AI policy"). Maintainer
  direction is in `## Thread highlights`. Where the PR honors them:
  `### Title`, `### Description` (section headings and their content,
  closing link, disclosure), `### Commits` (message convention), and
  `### Diff` (CHANGELOG or docs files).
- Live: the repo's `.github/pull_request_template.md`,
  `CONTRIBUTING.md`, any `AI_POLICY.md` or "Use of AI" section, the
  issue thread, and `scope.md`'s Path Review house rules (fork branch
  named `fix/<issue-number>-<slug>`, one PR per issue, every template
  section filled including disclosure where it applies), held against
  the draft title, description, commits, and diff.

**What good looks like:** Each stated ask is met with content specific
to this change: every template section present and filled (not left as
the template's placeholder text), the required closing link present,
the title and commit convention followed, the required CHANGELOG or
docs entry in the diff, and explicit maintainer direction in the
thread followed or engaged. Where the repo requires AI-use disclosure,
the description discloses it with the detail the policy asks for (the
tool used and the extent of the assistance). Where the repo states no
AI policy, no disclosure is required. Ignored: an asked-for section
missing or boilerplate, a required disclosure absent, a convention
broken, a maintainer's stated direction contradicted. (Whether the
description's claims match the diff is plan fidelity, above.)
