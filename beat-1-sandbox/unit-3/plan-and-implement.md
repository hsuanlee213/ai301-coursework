# Unit 3 — Plan and Build

## Posted upstream

**GitHub username**

hsuanlee213

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-6032286857

Following up on my reproduction above (https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5905164287).

**Cause:** `README.md:24` tells users to add `OPENROUTER_API_KEY` to `.env`, and `core/config.py` defines `openrouter_api_key` and `openrouter_model`, but `.env.example` lists neither.

**Plan:** one change, in `.env.example` only. Below `OPENAI_API_KEY` I'll add the comment line `# OpenRouter (see README Quick Start)`, then `OPENROUTER_API_KEY=your-openrouter-key-here` and `OPENROUTER_MODEL=google/gemma-3-27b-it:free` (the default from `core/config.py`). I'm leaving the `# Options:` line alone, because at f89c06f I found no code that reads `llm_provider`, so I can't confirm `openrouter` is a supported value. I won't touch `core/config.py` or the README.

**Test:** re-run the grep from my repro on `.env.example`. Before, it shows only `LLM_PROVIDER` and `OPENAI_API_KEY`. After, it should also show both OpenRouter variables, and `grep -n "Options:"` should be unchanged.

**Open question:** at f89c06f I found no code that reads `llm_provider`, so I'm only adding template lines and not claiming OpenRouter works end to end. Happy to adjust if you'd prefer the Options comment or README changed too.

---

## Your branch

**Branch**

docs/73-env-example-openrouter

**Evidence**

Before the change (branch `main`, revision f89c06f):

```
$ grep -nE "LLM_PROVIDER|OPENAI_API_KEY|OPENROUTER_API_KEY|OPENROUTER_MODEL" .env.example
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here

$ grep -n "OPENROUTER_API_KEY" README.md .env.example
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)

$ grep -n "Options:" .env.example
17:# Options: "mock" (default, no API key needed), "openai"
```

After the change (branch `docs/73-env-example-openrouter`, commit 1900e04):

```
$ grep -nE "LLM_PROVIDER|OPENAI_API_KEY|OPENROUTER_API_KEY|OPENROUTER_MODEL" .env.example
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
21:OPENROUTER_API_KEY=your-openrouter-key-here
22:OPENROUTER_MODEL=google/gemma-3-27b-it:free

$ grep -n "OPENROUTER_API_KEY" README.md .env.example
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
.env.example:21:OPENROUTER_API_KEY=your-openrouter-key-here

$ grep -n "Options:" .env.example
17:# Options: "mock" (default, no API key needed), "openai"

$ git diff --stat
 .env.example | 3 +++
 1 file changed, 3 insertions(+)
```

## Eval iterations

**Run history**

Run 1: agreement: 19/20 scored items (bar: 18/20: PASS). This is the only full run, and it matches the agreement line in the committed `eval-run.txt`.

**Package analysis**

pkg-14 (zellij-org/zellij#5174, category clear-accept). The gold label is accept. My rubric decided reject, so this is the one package I disagreed on. The run reported: "failed: Cause matches repro, Stranger could start, Unknowns not dressed as facts".

The first two are required checks, so they decided the verdict. The third is preferred and did not.

My rubric's `Cause matches repro` check wants the cause to be "something the repro evidence directly shows (a quoted output, line, or error)". pkg-14's diagnosis says "the reattach path wires the client's stdin to the session before the query responses have been consumed". The repro evidence only shows symptoms: raw `rgb:1c1c/1c1c/1c1c` strings after re-attach, a 0.44.1 control run that is clean, and a cache control. It never shows the stdin wiring order, so my check read the mechanism as inferred rather than shown. `Stranger could start` failed because the plan says the exact functions are "to be pinned in the PR after tracing the query issuance with debug logs", so I read the first edit as not yet knowable.

The gold label accepts it because the diagnosis is a reasonable hypothesis grounded in a clean regression window and the cache control, the scope is bounded, and the risk and the Windows limitation are stated honestly. My checks were stricter than that: they demanded direct evidence for the mechanism and a named edit site. They did not distinguish "a grounded hypothesis the plan labels as something to confirm by tracing" from "an unsupported claim".

**Check rationale**

From `tools/plan-check/rubric.md`, exactly as it reads now:

| Cause matches repro | The plan's stated cause, read against what the Repro evidence section actually shows | The cause the plan names is something the repro evidence directly shows (a quoted output, line, or error), and the plan targets that cause rather than restating the symptom. Fail if the repro points to a different cause, if the evidence does not support the stated cause, or if the plan quotes no repro evidence for it. | required |

It reads this way because my first draft was shaped like a write-up check ("names the specific files... AND states at least one thing it will not change"), and the rubric template says pass conditions must judge the outcome, not the shape. So I rewrote this one to judge whether the stated cause is supported by what the repro shows, and added "rather than restating the symptom" to cover the case where a plan only repeats the bug. I kept it `required` because the lecture's first failure family is a diagnosis that ignores or contradicts the reproduced evidence.

**Trade-offs**

This check gives up pkg-14: it fails a plan whose mechanism is plausible but inferred, which is why that package flipped to reject against a gold accept. I did not loosen it, and I did not re-run anything with `--only`. Nothing else changed after the run because the full run already agreed on 19 of 20 and every category on the `categories:` line had a match (clear-accept 6/7, scope-creep 4/4, thread-convention 2/2, unbuildable 3/3, wrong-cause 4/4). Loosening the check to admit hypotheses could flip the four wrong-cause packages that agree now, and I had no canary run to show it would not. The cost I accept is that a short, honest plan with an unconfirmed mechanism can be held.
