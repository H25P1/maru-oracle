---
pattern: When a spec leaves visual specifics ambiguous, ask whether a reference photo/asset exists before designing from text alone — a mid-build redesign costs more than the question would have.
date: 2026-08-07
source: "rrr: maru-oracle"
concepts: [design-process, scope-confirmation, reference-material, voxel-character]
---

# Ask for the reference photo before inventing the design

Built BongChong Oracle's voxel-dog character end-to-end from a birth-brief text
description alone (chihuahua, male, white-black, heart-shaped marking) — invented
coat length, ear shape, tail carriage, marking color and placement to make a
coherent, deliberately-differentiated design. H then supplied the actual reference
photo, which contradicted nearly every invented specific: long coat vs assumed
short, winged ears vs assumed hood, curled plume tail vs assumed upright stick,
and the "heart" turned out to be a black fur patch on the flank, not a red symbol
on the chest. A full redesign followed.

The rework was cheap here only because the rendering pipeline's geometry lived in
one function (`voxel-render.js`) separate from the skeleton/pivot definitions —
had the pivots needed to move too, the redesign would have touched three files
instead of one.

**How to apply:** Before investing effort in a from-scratch visual/design task
built from a text spec, ask directly whether a reference photo, mockup, or asset
already exists — especially when the spec is specific enough that a real
reference is plausible (e.g., every sibling in this family already had a
reference photo on file). One question is cheaper than a redesign, and it isn't
knowable in advance whether the pipeline will make a later fix cheap or
expensive.
