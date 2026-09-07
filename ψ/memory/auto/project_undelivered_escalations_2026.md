---
name: project-undelivered-escalations-2026
description: Two recurring-pattern self-audits were flagged for escalation to H but never actually reached H as of the retro record — surface them at the next standup.
metadata:
  type: project
---

The `/rrr` retrospective skill's "🔁 Recurring Pattern Detected" section fired three times between
2026-07-28 and 2026-08-07, each explicitly recommending "raise with H at the next standup" — but no
later retro or session record shows either one actually being surfaced to H. This mirrors a
documented failure mode in sibling Oracle Argon's own CLAUDE.md: escalations buried in a metrics/
retro file are never re-read at session start unless something forces the read.

1. **Browser-automation / headless-Chrome reliability** (flagged 2026-07-31, 3 of the prior 5
   sessions): `--virtual-time-budget` unreliable for rAF-driven animation testing, repeated
   mid-batch timeouts, and a script-injection timeout on a sandboxed CSP iframe once mistaken for a
   content bug. See [[feedback_environment_gotchas]], [[feedback_tool_failure_vs_content_bug]].
2. **Shipping a value/render/interpretation without verifying it against ground truth first**
   (flagged 2026-08-03 as 4 of 6 sessions, restated 2026-08-07 as 3 of 7 sessions with a new
   instance each time — the pattern was still recurring, not resolved): the sit/lie pivot picked
   without testing, `prone` bundled into a commit from a literal translation without confirming
   interpretation, bark's animation shipped without dump-dom verification, Jetaime's overlay scale
   shipped without checking the real geometry ratio, BongChong's design built from text alone
   without asking for a reference photo. See [[feedback_verify_before_declaring_visual_work_done]].

**How to apply**: if a future session's own retro flags a new recurring pattern with a
"raise with H" suggestion, actually raise it in the same session's response to H — don't rely on
it being read from a retro file later, since the record shows that doesn't reliably happen.
