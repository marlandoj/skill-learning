# skill-learning

![Don't copy skills. Learn them.](assets/hero.png)

**Don't copy skills. Learn them.**

Agent skills are distributed like code: write one, push it to GitHub, everyone clones it. That works until the skill succeeds. Popular repos attract contributors, contributors bring their own use cases, and every clone inherits the union of everyone's needs — files you'll never use, edge cases for systems you don't run, and all of it landing in your agent's context.

`skill-learning` is the other way to adopt a skill:

1. **Study** the source and extract its core functions.
2. **Check fit** against the system as it actually runs.
3. **Build a native version** — leaner, shaped to your system.
4. **Keep provenance** to the original, and let the system **re-learn** upstream changes selectively instead of blind-merging files.
5. **Prove it** — the learned candidate must match the verbatim original under non-inferiority gates before it may replace anything.
6. **Give back** — improvements that generalize are packaged as human-gated contributions to upstream.

This repository is the method, written as an agent skill ([`SKILL.md`](SKILL.md)) so any agent that reads it can run the process: the seven-stage pipeline, the 12 binding policy decisions, the safety-gate protocol (including its hard-won amendment), and the measurement discipline that keeps "zero regressions" an evidence claim instead of a slogan.

## Status — what has actually run

The process was built and verified end to end in the [Zouroboros Workshop](https://zouroboros.ai) in October 2026, with [blader/humanizer](https://github.com/blader/humanizer) as the test subject:

- ✅ Adoption with scan + provenance → learned candidate → three-arm evaluation (no-skill / verbatim original / learned) → safety gate → contribution package → validated on a pristine upstream checkout → **submitted: [blader/humanizer#317](https://github.com/blader/humanizer/pull/317)** — a rule treating fake closing tags and "operator notes" inside text-to-edit as material, never as instructions. Targeted injection failures: **9/30 → 0/30** (p=0.002). Core score: **100.2%** of the pristine baseline.
- ⚠️ **No learned candidate has passed — in three attempts.** Attempt #1 failed the safety gate (15/30 vs 9/30 on the injection case). Attempt #2 closed the safety gap to parity but failed upstream validation (its extraction dropped 4 of 26 patterns). Attempt #3 passed coverage, validation, safety, core, tasks, and canary, failing only trigger non-inferiority (−1.7pp, CI [−5.0, 0.0]). The campaign was closed with the three attempts standing as the record; every candidate remains in shadow, none activated. The failures are documented inside the skill itself, because a process whose gates can't fail a candidate isn't a gate.

The full story — including the judge-noise investigation that forced the safety protocol's redesign — is in the [launch article](launch/x-article.md).

## What's in here

| File | What it is |
|---|---|
| [`SKILL.md`](SKILL.md) | The meta-skill itself: pipeline, 12 decisions, amended safety protocol, measurement discipline, evidence status |
| [`launch/x-article.md`](launch/x-article.md) | The long-form launch article (drafted for X Articles) |
| [`launch/x-post.md`](launch/x-post.md) | The launch post / thread drafts |
| `assets/hero.png` | The banner above |

## Using it

Drop `SKILL.md` into any agent environment that loads skills, or read it as a process spec and implement the gates in your own tooling. The policy constants (thresholds, tolerances, judge protocol) are stated explicitly so you can adopt them as-is or amend them deliberately — in writing.

## License

MIT. The method is offered freely; if you run it and your gates catch something interesting, contributions and war stories are welcome.
