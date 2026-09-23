# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer activity | "last 5 default-branch commits" under Repo facts | At least one non-bot maintainer commit occurred within 30 days of the capture date. | required |
| Repository status | "archived:" on the repo line under Repo facts | The repository is not archived. | required |
| Newcomer scope | Issue body and comment thread | The issue describes a bounded, actionable task that a newcomer can work on without first resolving a major design decision. It may involve multiple related files or steps, but must not be an umbrella/tracking issue, a change explicitly requiring core internals, or a pure usage/support question. | required |
| Not already claimed | "this issue: assignees:" and "linked PRs:" under Repo facts, plus the Comments section | The issue has no current assignee, no open linked PR, and no comment indicating that someone is actively working on it. | required |
| AI contribution policy | "contribution policy" under Repo facts | The repository does not explicitly ban AI-generated or AI-assisted contributions. Conditional AI-use policies and no stated AI policy both pass. | required |

## Verdict rule

Accept an issue only if every required check passes. If a required check fails or is unclear, reject the issue.

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
