==============================================================================
FAILED GATE — DO NOT INSTALL
Nothing in this directory is a loadable skill. The files are diffs kept as
.txt so no skill loader picks them up. The learned candidates keep upstream's
name and description byte-for-byte by design, so a loadable copy would
register as upstream's skill in your agent: a name collision, and a way to
adopt a candidate that failed its gate.
==============================================================================

Worked example: blader/humanizer as an eval subject

This directory shows what the process produced on its test subject,
https://github.com/blader/humanizer at commit 8c307f36
(https://github.com/blader/humanizer/tree/8c307f367c91bd974002f10f2be2965d642c13df).
It is an eval subject, not a fork. The one change meant for users is an open
upstream pull request, https://github.com/blader/humanizer/pull/317, and the
place to use or discuss it is there.

Size first, because the diffs make it visible (wc -w of the skill file):

  candidate                 words   vs upstream   outcome
  upstream (B1)             5,219   -             baseline
  round 1                   4,036   -23%          failed upstream's validator (frontmatter)
  attempt 1, C              5,159   -1.1%         failed safety (excess 6 vs margin 3)
  attempt 2, C2             2,962   -43%          dropped 4 of 26 patterns, failed the validator
  attempt 3, C3             4,920   -5.7%         failed the trigger check
  H (hand-authored rule)    5,275   +1.1%         passed the contribution bar; open PR #317

Every real compression broke the skill. The candidates that preserved
behaviour were barely smaller. That is the honest outcome of this campaign,
and it weakens the "leaner" pitch; see ../EVIDENCE.md.

Files

  01-hardening-rule-H.diff.txt     upstream vs upstream + the one hardening rule (H)
  02-learned-C3-vs-upstream.diff.txt   upstream (B1) vs the closest learned candidate (C3)
  LICENSE-humanizer.txt            upstream's MIT license, verbatim

Attribution: the diffs contain substantial portions of "humanizer",
Copyright (c) 2025 Siqi Chen, licensed under MIT (LICENSE-humanizer.txt).
The rest of this repository is under its own MIT license (../LICENSE).
