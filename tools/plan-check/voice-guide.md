# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I am a student contributor who is still learning the repository and its contribution workflow. I am reproducing reported issues and documenting what I observe. Readers can expect me to distinguish what I verified from what I have not yet confirmed.

## Rules I write by

### Rule: Say only what I verified

I separate observed results from assumptions and do not claim that I reproduced something unless my evidence supports it.

- Wrong: "I confirmed this bug and know what is causing it."
- Right: "I reproduced the reported behavior in my environment; I have not identified the cause."

### Rule: Be specific about what I will do

When claiming an issue, I describe the investigation I plan to perform without promising a fix or outcome.

- Wrong: "I'll fix this issue by tomorrow."
- Right: "I'd like to reproduce this issue and report back with my environment, steps, and observed results."

### Rule: State uncertainty clearly

If I cannot reproduce something or do not know the cause, I say so instead of guessing.

- Wrong: "This is probably caused by the dependency update."
- Right: "I could not reproduce the reported behavior under the environment described below, so I cannot confirm the cause."

### Rule: Keep comments focused on evidence

I include information that helps maintainers understand the reproduction attempt and avoid unnecessary speculation.

- Wrong: "Everything looks broken, so I think there may be several other problems too."
- Right: "Using these steps, I observed the reported error after the final command."

## Things I never post

- Promises that I will fix an issue or finish by a specific date when I cannot guarantee it.
- Claims that I reproduced an issue without supporting evidence.
- Guesses about the cause presented as facts.
- Boilerplate comments that do not refer specifically to the issue.
- Disrespectful, demanding, or overly confident language.
