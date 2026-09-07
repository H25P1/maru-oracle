---
name: feedback-verify-before-declaring-visual-work-done
description: A plausible-looking screenshot or render is not proof a value/animation/design is correct — verify against the specific ground truth that's actually uncertain before declaring visual/creative work done.
metadata:
  type: feedback
---

Recurring failure mode across this project (see [[project_undelivered_escalations_2026]] for the
frequency count): a new visual value, animation, or design ships because it "looks plausible" in a
single screenshot, when the actual uncertain thing was never independently checked. Four concrete
instances: a sit/lie rotation pivot picked by reasoning alone (produced a visibly "flopped over"
pose once actually rendered); bark's 4-value head-snap animation shipped without dump-dom
verification (its symmetric start/end value made a silently-dropped SMIL animation visually
indistinguishable from a working one — see the `keyTimes`/`values` mismatch bug this masked);
Jetaime's overlay `scale: 0.6` shipped without cross-checking the real geometry ratio to Maru
(caught only because `advisor()` was called before declaring done, not because it was verified
directly); BongChong's design built entirely from text with no reference-photo check (see
[[feedback_ask_for_reference_photo_before_designing]]).

**The generalizable rule**: a verification method that can't distinguish "broken" from "working"
for the specific case at hand isn't verification for that case. A single-frame screenshot of an
animation that starts and ends at the same value proves nothing about whether it ran. A comment
describing an invariant ("this scale matches what's tuned elsewhere") is not the same as the
invariant being enforced — check the actual numbers against each other.

**How to apply**: before calling new visual/config work done, identify what's actually uncertain
about it (does this animate at all? does this scale match the real ratio? does this pose match what
was asked?) and verify THAT specific thing via the strongest available method (DOM inspection via
`--dump-dom`, a direct geometry comparison, a reference photo, showing the actual render to H) —
not just whichever check is easiest or already passing.
