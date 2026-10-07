# Plan for #73: .env.example does not document OpenRouter settings

## Diagnosis

`.env.example` does not list the OpenRouter settings that `core/config.py` defines and that the README tells users to set.

Repro evidence I rely on (revision f89c06f, from my repro comment on #73):
- `README.md:24` says to add `OPENROUTER_API_KEY` to `.env`.
- `.env.example` has `LLM_PROVIDER=mock` and `OPENAI_API_KEY`, and does not list `OPENROUTER_API_KEY` or `OPENROUTER_MODEL`.
- `core/config.py` defines `llm_provider`, `openai_api_key`, `openrouter_api_key`, and `openrouter_model`.

Cause: a user who follows the README and copies `.env.example` to `.env` finds no OpenRouter variables to fill in. The fix belongs in the template, not in the code or the README.

## Scope

In: add `OPENROUTER_API_KEY` and `OPENROUTER_MODEL` to `.env.example`, with one comment line above them pointing to the README Quick Start.

Out: no change to `core/config.py`, no change to the README, no change to the existing `# Options:` comment or `LLM_PROVIDER` line, and no other variables in `.env.example`.

## Files I will touch

- `.env.example` (only this file)

## Approach

1. Open `.env.example` and find the `# LLM provider` block (it holds `LLM_PROVIDER=mock` and `OPENAI_API_KEY=sk-your-key-here`).
2. Leave the `# Options: "mock" (default, no API key needed), "openai"` line unchanged. I checked at f89c06f (not part of my repro) that `llm_provider` appears only at `core/config.py:18`, so no code reads it and I cannot confirm `openrouter` is a supported value. Adding it to that line would advertise something I have not verified.
3. Directly below the line `OPENAI_API_KEY=sk-your-key-here`, add these three lines, exactly as written here:

       # OpenRouter (see README Quick Start)
       OPENROUTER_API_KEY=your-openrouter-key-here
       OPENROUTER_MODEL=google/gemma-3-27b-it:free

   The model value is the default in `core/config.py` line 22.
4. Run the test plan below and compare with the before output.

## Test plan

Re-run the repro steps against the change:
1. `grep -nE "LLM_PROVIDER|OPENAI_API_KEY|OPENROUTER_API_KEY|OPENROUTER_MODEL" .env.example`
   - Before: only `LLM_PROVIDER=mock` and `OPENAI_API_KEY=...`.
   - Expected after: also `OPENROUTER_API_KEY=your-openrouter-key-here` and `OPENROUTER_MODEL=google/gemma-3-27b-it:free`.
2. `grep -n "OPENROUTER_API_KEY" README.md .env.example`
   - Before: a match in `README.md` only.
   - Expected after: matches in both files.
3. `grep -n "Options:" .env.example`
   - Expected after: unchanged, still `# Options: "mock" (default, no API key needed), "openai"`.
4. `git diff --stat` shows only `.env.example` changed.

## Risks and unknowns

- Checked by me at f89c06f, not part of my repro: `llm_provider` appears only at `core/config.py:18`, so no code reads it. `docs/SETUP.md:47` also mentions the OpenRouter key, and it needs no change. Because of this I only add template lines and do not claim OpenRouter works end to end.
- Risk: the default model `google/gemma-3-27b-it:free` may change later. I copy it from `core/config.py`, so the two files can drift.
- Unknown: whether the maintainer wants the Options comment or README changed too. I am leaving both alone.

## Deviations

Nothing changed between the plan I posted and the build. The diff touches only `.env.example` and adds the three lines exactly as written in Approach step 3. I did not touch `core/config.py`, the README, or the `# Options:` line. The test greps gave the expected after output.
