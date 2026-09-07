---
name: feedback-confirm-interpretation-before-building
description: A literal translation of a short native-language creative request is a plausible interpretation, not a confirmed one — restate it or show the result before bundling into a larger commit.
metadata:
  type: feedback
---

When a request is a short phrase in H's native language describing a visual/creative outcome (e.g.
Thai "นอนหมอบนิ่งๆ" — "lying prone, quietly still"), a literal or best-effort translation gives you
*a* plausible interpretation, not *the* confirmed one. This is easy to miss because the deliverable
still "looks reasonable" once built — nothing forces a second look. Concrete instance: an existing
`lie` pose already existed; a new "prone" pose was built as "a stiller variant of lie" from a
literal reading, bundled into a 3-activity commit, and never actually confirmed against what H
pictured (only checked for "does it look distinguishable from `lie`," not "does it match what H
meant"). It landed fine, but that was closer to luck than verified understanding.

**How to apply**:
1. If the deliverable is cheap to preview, show that specific piece before bundling it into a
   larger commit — not just an aggregate "N things done" summary.
2. If showing isn't practical, restate your interpretation in one plain sentence as part of the
   response ("built X as a stiller, less-tilted version of Y — let me know if you pictured
   something different"), so silence-as-approval is a visible, acknowledged choice.
3. "The code works and looks plausible" is necessary but not sufficient evidence the interpretation
   was right.

The moment to double-check a fuzzy creative interpretation is before it's built and bundled, not
after a bug report.
