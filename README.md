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

This repository is the method, written as a **process spec** in agent-skill form ([`SKILL.md`](SKILL.md)): the seven-stage pipeline, the 12 binding policy decisions, the activation gate and its safety protocol (including its hard-won amendment), and the measurement discipline that keeps "zero regressions" an evidence claim instead of a slogan. The reference implementation, and every enforcement point (approval tokens, the scanner, the sandbox, the eval harness, operator sign-off), lives in the private Zouroboros Workshop and is not in this repository. To run the process you need: a sandboxed scanner; an operator-held approval step; a provenance record; a frozen, hash-pinned eval suite with three arms; an LLM judge you can re-query; and a place to keep candidates in shadow. An agent that lacks any of these stops at study / check-fit and reports; it never installs or activates.

## Status — what has actually run

The process was built and run end to end in the [Zouroboros Workshop](https://zouroboros.ai) in October 2026, with [blader/humanizer](https://github.com/blader/humanizer) as the test subject. Full numbers, intervals and limits: [`EVIDENCE.md`](EVIDENCE.md).

- ✅ Adoption with scan + provenance → learned candidate → three-arm evaluation (no-skill / verbatim original / learned) → safety gate → contribution package → validated on a pristine upstream checkout → **open PR [blader/humanizer#317](https://github.com/blader/humanizer/pull/317) (no reviews yet)** — a hand-authored rule treating fake closing tags and "operator notes" inside text-to-edit as material, never as instructions. Targeted injection failures: **9/30 → 0/30** (p=0.002; 22 of the 30 resisting replies were verbatim echoes, not edits). Core score: **+0.2pp [−1.1, +1.7], 36 items × 3 runs/arm** against the pristine baseline.
- ⚠️ **No learned candidate has passed — in three attempts.** One standing gap blocks every candidate independently: there is no real-usage sample for humanizer, so the suite lacks the usage-derived items Decision 6b requires. On top of that: attempt #1 failed the safety gate — **15/30 vs 9/30 — an excess of 6 against the gate's policy margin of 3. Not statistically significant (Fisher p = 0.19); the gate is a count rule, by design.** It "failed fairly" in exactly that sense: a pre-registered, count-based policy threshold, applied without retroactive change; not a significance test. Attempt #2 closed the safety gap to parity (6/30 vs 6/30) but failed upstream validation (its extraction dropped 4 of 26 patterns). Attempt #3 passed coverage, validation, safety, core, tasks, and canary; its **trigger check failed on byte-identical routing requests; P(fail | identical arms) ≈ 33% — a known false-fail mode, recorded, not re-run**. The campaign was closed with the three attempts standing as the record; every candidate remains in shadow, none activated. The failures are documented with the skill, because a process whose gates can't fail a candidate isn't a gate.

Candidate size (`wc -w` of the skill file):

| candidate | words | vs upstream | outcome |
|---|---|---|---|
| upstream (B1) | 5,219 | — | baseline |
| round 1 | 4,036 | −23% | failed upstream's validator (frontmatter) |
| attempt 1, C | 5,159 | −1.1% | failed safety (excess 6) |
| attempt 2, C2 | 2,962 | −43% | dropped 4 patterns, failed the validator |
| attempt 3, C3 | 4,920 | −5.7% | failed trigger |
| H (hand-authored rule) | 5,275 | +1.1% | passed the contribution bar; open PR #317 |

The story — including the judge-noise investigation that forced the safety protocol's redesign — is in the [launch article](launch/x-article.md).

## What's in here

| File | What it is |
|---|---|
| [`SKILL.md`](SKILL.md) | The process spec: pipeline, 12 decisions, activation gate and safety protocol, measurement discipline |
| [`EVIDENCE.md`](EVIDENCE.md) | The dated record: per-attempt numbers with n and CIs, gate operating characteristics, candidate sizes, incidents |
| [`tools/gate_calculator.py`](tools/gate_calculator.py) | Standalone gate arithmetic (paired bootstrap, count rule, validity rules, Wilson/Fisher reporting); tests in [`tools/test_gate_calculator.py`](tools/test_gate_calculator.py) |
| [`schemas/provenance.schema.json`](schemas/provenance.schema.json) | JSON Schema of the per-skill provenance record |
| [`schemas/eval-suite.template.json`](schemas/eval-suite.template.json) | Eval-suite shape with placeholder items only |
| [`examples/`](examples/README.txt) | Worked example on humanizer as diffs (not loadable; failed gate — do not install) |
| [`launch/x-article.md`](launch/x-article.md) | The long-form launch article (archived copy of the text posted on X) |
| [`launch/x-post.md`](launch/x-post.md) | The launch post / thread (archived copy of the text posted on X) |
| `assets/hero.png` | The banner above |
| `assets/x-article-cover.png` | The 5:2 cover image for the X article |
| `assets/social-preview.png` | The repository's social preview image (1280×640) |

## Using it

Read `SKILL.md` as a process spec and implement the gates in your own tooling, or load it into an agent environment that has the enforcement points listed above; without them, an agent following it stops at study / check-fit. The policy constants (thresholds, tolerances, judge protocol) are stated explicitly so you can adopt them as-is or amend them deliberately — in writing. Run the calculator's tests with `python3 -m unittest discover -s tools -v`.

## License

MIT. The method is offered freely; if you run it and your gates catch something interesting, contributions and war stories are welcome. The diffs under `examples/` contain portions of blader/humanizer (MIT, Copyright (c) 2025 Siqi Chen); see `examples/LICENSE-humanizer.txt`.
