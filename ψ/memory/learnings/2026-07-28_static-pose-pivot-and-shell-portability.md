---
pattern: For a static rotated pose, anchor near the shape's visual bulk (not a "clean hinge" point far away) — and never assume bash word-splitting semantics under zsh.
date: 2026-07-28
source: rrr: maru-oracle
concepts: [svg-animation, smil, shell-scripting, zsh, headless-chrome, verification]
---

# Static-pose rotation pivots, and shell-portability traps

## The pattern

When building a discrete static pose (sit, lie, crouch — anything that's a
held rotation/offset rather than a loop) for a shape made of several
sub-parts, the pivot point matters more than the angle. A pivot far from
the shape's own bulk turns even a modest angle into a large visible arc,
because arc length scales with the lever-arm distance. Anchor the
rotation near where the shape's *weight* should visually stay planted
(e.g., for a sitting animal, near the hips/where the legs meet the
ground) rather than picking a pivot that tells a clean physical story
("hinge at the shoulder") but happens to be geometrically far from the
mass of the shape.

Concretely: rotating a ~40×80-unit box by 13° around a corner produced an
~19-unit arc at the far corner — proportionally huge against the box's own
40-unit height, and it read as the shape flopping over rather than
leaning back. The fix wasn't a smaller angle, it was moving the pivot to
the box's own bottom-center, which cut the effective lever arm by more
than half.

**Takeaway**: for any new static pose on an existing shape, render the
*worst case* (largest sub-part, pivot candidate) before finalizing numbers
across a whole preset table — don't reason through it purely on paper.

## The shell trap

`for combo in "a b" "c d"; do set -- $combo; x=$1; y=$2; done` relies on
bash's default unquoted word-splitting. zsh does not split unquoted
variables by default (`SH_WORD_SPLIT` is off), so `$combo` stays one
token, `$1` becomes the whole string, and `$2` is empty — silently
produces malformed downstream values (e.g. filenames with a stray space
and empty field) rather than an error. When looping over multi-field data
in a shell one-liner meant to be portable, use nested loops over separate
variables instead of relying on splitting a combined string.

## Related

- [[voxel-mascots-desktop-overlay]] retrospective — where this came up
  while building sit/lie/bark/happy activity poses for the Oracle desktop
  overlay's voxel-dog characters.
