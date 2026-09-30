# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

hsuanlee213

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5904992137

Hi, I’d like to take this one. As I read it: the Quick Start in README.md says to add OPENROUTER_API_KEY to .env, but .env.example doesn’t list that variable and its LLM_PROVIDER comment offers only mock and openai, while core/config.py defines both keys. I’ll compare those three files on the current main and report back with my environment, steps, and what I observe.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5905164287

## Reproduction report

**Environment:** macOS 15.5; Git 2.55.0; fork revision f89c06f.

**Steps:**
1. Clone the repository and check out revision f89c06f.
2. Run `grep -n "OPENROUTER_API_KEY" README.md`.
3. Run `grep -nE "LLM_PROVIDER|OPENAI_API_KEY|OPENROUTER_API_KEY|OPENROUTER_MODEL" .env.example`.
4. Run `grep -nE "llm_provider|openai_api_key|openrouter_api_key|openrouter_model" core/config.py`.

**Observed:**
- `README.md:24` says to add `OPENROUTER_API_KEY` to `.env`.
- `.env.example` contains `LLM_PROVIDER=mock` and `OPENAI_API_KEY`, but does not list `OPENROUTER_API_KEY` or `OPENROUTER_MODEL`.
- `core/config.py` defines `llm_provider`, `openai_api_key`, `openrouter_api_key`, and `openrouter_model`.

**Expected:** `README.md`, `.env.example`, and `core/config.py` should describe the supported LLM configuration consistently.

**Actual:** The README instructs users to configure `OPENROUTER_API_KEY`, while `.env.example` does not document that variable or the OpenRouter model setting, even though `core/config.py` defines both.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

- Initial full run: 19/20 agreement.
- Targeted `--only pkg-20` run after revising the Repo conventions check: 1/1 agreement.
- Confirming full run: 20/20 agreement. Category results: clear-accept 8/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4.

**Package analysis**

I analyzed `pkg-20`. My initial rubric decided **accept**, while the gold label was **reject**. The package involved a repository with a strict AI-use disclosure requirement, but the candidate comment did not include the required disclosure. My original Repo conventions check was too general, so it did not reliably reject a package that violated a repository-specific AI disclosure policy. I revised the check to explicitly require the applicable disclosure, including the tool and extent of assistance when the repository policy requires them.

**Check rationale**

Current check from my `rubric.md`:

> `Repo conventions | The claim comment and repro report read against the repository conventions and AI-use policy stated in the repo-facts block. | Pass if the comments follow all applicable repository requirements. If the repository requires AI-use disclosure, the submitted comments must include the required disclosure, including the tool and extent of assistance when the policy requires them. | required`

I revised this check after the initial full evaluation scored 19/20 and disagreed with the gold label on `pkg-20`. The earlier version was not explicit enough about AI-use disclosure. I added the requirement that, when the repository has such a policy, the submitted comments must contain the required disclosure and include the tool and extent of assistance when required.

**Trade-offs**

Making the Repo conventions check stricter means that a package can be rejected for missing a repository-specific disclosure even when its technical reproduction evidence is otherwise strong. I accepted this trade-off because following the repository's contribution requirements is part of a valid submission. After the revision, I re-ran `pkg-20` with `--only` and it changed to the expected reject result (1/1 agreement). I then ran the complete evaluation again, and the confirming run reached 20/20 agreement with all category floors met.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
