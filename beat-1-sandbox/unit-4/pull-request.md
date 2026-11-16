# Unit 4 — Test and Submit

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/254

**Branch**

fix/73-env-example-openrouter

## Eval iterations

**Run history**

- Full run 1: 17/20 agreement. Three clear-accept packages (pkg-05, pkg-08, pkg-11) were incorrectly rejected.
- Partial run: 7/7 agreement. Re-tested pkg-05, pkg-08, and pkg-11, plus regression canaries pkg-03, pkg-07, pkg-14, and pkg-17.
- Full run 2: 20/20 agreement (PASS). All five categories met the category floor. This is the final saved run in eval-run.txt.

**Package analysis**

I analyzed pkg-08 (clear-accept).

Gold label: accept.
Initial rubric verdict: reject.
Revised rubric verdict: accept.

The initial rubric rejected this package because "Planned tests present and decisive" and "Repo's own checks run" were graded as failures.

The package provides evidence for a terminal UI change, including interaction steps and observed text. My initial rubric was too strict about the required evidence format and did not consistently recognize specific reported results for supporting tests.

I revised the evidence rules to recognize actual input steps tied to observed behavior and to accept named repository checks with specific results. The decisive reproduction still needs concrete evidence. After these changes, pkg-08 was correctly accepted in the partial and final evaluations.

**Check rationale**

The following check is quoted exactly from my current rubric.md:

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Reviewer can orient fast | The PR title and the first lines of the description | The title names the behavior change (not just "fix bug" or the issue number alone), and the description says what changed and why in terms a reviewer can hold the diff against, and references the issue. Fail if a reviewer could not tell from the title and opening what the PR does. | preferred |

I kept this check as preferred because a clear title and summary make review easier, but a minor writing-quality issue should not independently reject an otherwise verifiable PR. Required checks instead focus on plan fidelity, evidence, reviewability, and repository standards.

**Trade-offs**

I loosened the evidence requirements to accept named repository-check results and observable terminal UI behavior without requiring a complete raw log for every supporting check. The trade-off is that a concise reported result provides less detail than a full transcript.

To reduce false accepts, I retained the requirement for decisive reproduction evidence and re-tested pkg-03, pkg-07, pkg-14, and pkg-17 as canaries. All four remained correctly rejected. The subsequent full evaluation achieved 20/20 agreement across all five categories.
