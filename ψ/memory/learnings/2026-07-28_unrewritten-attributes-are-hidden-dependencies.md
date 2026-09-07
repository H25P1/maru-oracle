---
pattern: A function that only rewrites some of an element's attributes implicitly depends on whatever was baked into the ones it doesn't touch — and a verification method that can't distinguish "broken" from "working" for a symmetric case isn't verification for that case.
date: 2026-07-28
source: rrr: maru-oracle
concepts: [svg-animation, smil, hidden-state, verification, dom-inspection]
---

# Unrewritten attributes are hidden dependencies

## The bug

`character-markup.js` bakes `keyTimes="0;0.5;1"` into every animated
part's `<animateTransform>` at author time, matching the original
3-keyframe walk cycle. The runtime pose-switching code only ever rewrote
`values`/`dur`/`repeatCount`/`fill` — never `keyTimes`. As long as every
new pose's `values` list also happened to have 3 entries, this was
invisible. The moment a pose needed a different-length values list (a
5-keyframe head sweep, a 5-keyframe leg flick), the mismatched
`keyTimes`/`values` counts caused the browser to silently drop the
animation entirely — no error, just a part frozen at its identity
transform despite the correct values being set.

**The generalizable rule**: when a function's job is "rewrite this
element's dynamic properties," explicitly enumerate every attribute the
element actually carries — not just the ones your own code sets. Anything
left untouched is an implicit dependency on whatever was baked in at
authoring time, and that dependency is invisible until a case comes along
that violates the assumption the original baked-in value encoded.

## The verification gap

A second, compounding issue: the bug shipped in an earlier pose (a 4-value
head-snap "bark" animation) two commits before anyone noticed, because
that particular animation started and ended at the same value (0). A
single-frame screenshot cannot distinguish "this animation is silently
broken" from "this animation is working and currently at a 0-crossing" —
both render identically. The bug only surfaced when a later pose's
values list was asymmetric enough that a broken vs. working render looked
visibly different.

**The generalizable rule**: before trusting a screenshot/render-based
check as sufficient verification, ask whether the specific case could look
identical whether the underlying mechanism worked or not. If yes (e.g. an
animation that returns to its starting value, a toggle whose "off" state
matches uninitialized state), that check isn't proof for that case — reach
for inspecting the actual underlying state (DOM attributes via
`--dump-dom`, a debugger, a log of the actual value) instead of the
rendered output.

## Related

- [[static-pose-pivot-and-shell-portability]] and [[confirm-interpretation-before-building]]
  — earlier lessons from the same project. All three are instances of the
  same broader habit: identify what's actually uncertain about a given
  change, and verify THAT specific thing, rather than defaulting to
  whichever check is easiest to run.
