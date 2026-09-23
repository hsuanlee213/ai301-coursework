# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73)

**Verdict output**



**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73",
  "checks": [
    {"name": "Maintainer activity", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16 by Aburke225 (non-bot), 7 days before capture date 2026-09-23."},
    {"name": "Repository status", "grade": "pass", "evidence": "gh repo view reports \"isArchived\": false."},
    {"name": "Newcomer scope", "grade": "pass", "evidence": "\"Relevant files: README.md, .env.example ... Estimated effort: 1-2 hours\"; labels include good first issue, tier-1."},
    {"name": "Not already claimed", "grade": "pass", "evidence": "assignees: none; 0 comments; no cross-referenced PRs in the issue timeline."},
    {"name": "AI contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI clause and no AI_POLICY.md exists; silence passes."}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

- Smoke run 1: 2/3 agreement.

- Smoke run 2 after revising the Newcomer scope check: 2/3 agreement.

- Final full run: 17/20 agreement.

**Issue analysis**

issue-01 — My rubric decided `reject`, while the gold label was `accept`. The failed check was `Newcomer scope`. My rubric interpreted the issue as not sufficiently bounded for a newcomer because it included multiple proposed documentation changes and some details that were not fully settled. The eval result showed that this interpretation was stricter than the gold label.

**Check rationale**

"The issue describes a bounded, actionable task that a newcomer can work on without first resolving a major design decision. It may involve multiple related files or steps, but must not be an umbrella/tracking issue, a change explicitly requiring core internals, or a pure usage/support question."

I revised this check because my original wording required "one bounded piece of work," which could reject reasonable newcomer issues simply because they involved several related files or steps. The current version focuses instead on whether the work is actionable and whether a newcomer can begin without first resolving a major design decision.

**Trade-offs**

This broader wording can accept issues that involve several related changes, which reduces false rejections of manageable documentation tasks. However, it may also accept an issue whose individual steps together are larger than they initially appear. In the final eval, issue-01 and issue-19 were still rejected because of Newcomer scope, while issue-15 was accepted even though its gold label was reject.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. This issue fits my interests because it is a small, clearly scoped documentation/configuration issue, and the estimated 1–2 hour effort fits the time I have available.

2. The verdict correctly identified that the repository is active, the issue is bounded and newcomer-friendly, and nobody has already claimed it. Beyond the rubric, I also considered that the affected files and expected change are easy for me to understand quickly.

3. I expect claiming it to be relatively straightforward because the issue currently has no assignee, no comments, and no linked pull request.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
