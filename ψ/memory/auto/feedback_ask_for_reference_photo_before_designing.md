---
name: feedback-ask-for-reference-photo-before-designing
description: Before designing a from-scratch visual/character from a text spec, ask whether a reference photo already exists — a mid-build redesign costs more than the question would have.
metadata:
  type: feedback
---

When a spec leaves visual specifics ambiguous (coat length, marking color/placement, ear shape,
etc.) and describes something specific enough that a real reference is plausible, ask directly
whether a reference photo, mockup, or asset already exists before investing effort in an
invented design. Confirmed twice in this project: BongChong's first-pass design (built from
birth-brief text alone) was wrong on nearly every visual specific once H's real photo arrived —
coat length, ear shape, tail carriage, marking color and placement (see
[[project_bongchong_voxel_rollout]]). Every prior sibling in this family already had a reference
photo on file, which in hindsight made the check especially cheap to have asked for upfront.

**Why**: it isn't knowable in advance whether the rendering pipeline will make a later fix cheap
(here: geometry lived in one function separate from skeleton/pivots, so the redesign only touched
one file) or expensive (a redesign needing different pivots would have touched three). One question
is cheaper than a redesign regardless of which case it turns out to be.

**How to apply**: before starting any from-scratch visual/design task built from a text
description, ask "do you have a reference photo/asset for this?" as a first step, not an
afterthought triggered by the result looking wrong.
