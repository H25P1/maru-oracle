---
pattern: A literal translation of a user's request is not a confirmed shared understanding — for visual/creative asks, restate your interpretation or show the result before finalizing, especially when bundling it into a larger commit.
date: 2026-07-28
source: rrr: maru-oracle
concepts: [requirements-clarity, non-english-requests, visual-design, verification]
---

# Confirm interpretation before building, not just before shipping

## The pattern

When a user's request is a short phrase in their native language describing
a visual or creative outcome (e.g. Thai "นอนหมอบนิ่งๆ" — "lying prone,
quietly still"), a literal or best-effort translation gives you *a*
plausible interpretation, not *the* confirmed one. This is easy to miss
because the deliverable still "looks reasonable" once built — there's no
error, no crash, nothing that forces a second look.

In this case: an existing `lie` pose already existed. The new ask was
close enough in meaning that it was tempting to implement it as "a
variant of lie, just calmer" and move on — which is exactly what happened,
bundled into the same commit as two other new activities. That may well be
correct. But it was never checked against what the user actually pictured
(a legs-tucked crouch? a specific stillness quality?) before being folded
into a larger piece of work and committed.

## The fix

For requests like this:
1. If the deliverable is cheap to preview (a screenshot, a short
   description), show *that specific piece* before bundling it into a
   larger commit — not just the aggregate "3 things done, here's a
   summary."
2. If showing isn't practical in the moment, restate your interpretation
   in one plain sentence as part of the response ("built X as a stiller,
   less-tilted version of the existing Y — let me know if you pictured
   something more different") so silence-as-approval is a visible,
   acknowledged choice rather than a silent assumption.
3. Treat "the code works and looks plausible" as necessary but not
   sufficient evidence that the interpretation was right — plausibility is
   not confirmation.

**Takeaway**: the moment to double-check a fuzzy creative interpretation is
before it's built and bundled, not after a bug report. If checking before
isn't possible, at least make the interpretation explicit in the same
message as the result, so it's easy for the user to correct cheaply.

## Related

- [[voxel-mascots-desktop-overlay]] — same project, the sit/lie pivot
  mistake from earlier this session. That one was a *technical*
  verification gap (didn't test the geometry before committing to
  numbers); this one is an *interpretation* verification gap (didn't
  confirm meaning before committing to a build). Both are instances of the
  same broader habit: verify the specific thing that's actually uncertain,
  not just the things that are easy to check.
