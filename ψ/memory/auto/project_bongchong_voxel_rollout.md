---
name: project-bongchong-voxel-rollout
description: BongChong's voxel character shipped 2026-08-07 — first-pass design built from text alone was wrong on nearly every visual specific once H's reference photo arrived.
metadata:
  type: project
---

BongChong (ยามเฝ้าประตู — Gatekeeper, born 2026-08-06) was the second sibling given the voxel-dog
treatment. First pass was designed purely from his birth-brief text (chihuahua, male, white-black,
"heart" marking) without asking whether a reference photo existed: short coat, black hood ears, red
chest heart — deliberately differentiated from Jetaime's design. H then sent the real reference
photo, which contradicted nearly every invented detail: long coat, winged butterfly ears, white
forehead blaze with black eye-masks, a plume tail curled over the back, and the "heart" turned out
to be a black fur patch on the flank, not a red chest symbol. Full redesign followed, confirmed by
H simply re-sending the same photo when asked to pick a heart color.

This is the concrete incident behind [[feedback_ask_for_reference_photo_before_designing]]. The
redesign itself was cheap only because geometry lives in one `fill<Name>()` function separate from
skeleton/pivot definitions — a redesign needing different pivots would have touched three files
instead of one.

Also the second instance (after Jetaime) of `advisor()` catching that global config
(`~/.claude/settings.json`, the notify hook script) needed its own separate approval beyond what H
had approved for the two named repos — see [[feedback_scope_layers_for_new_oracle_voxel_characters]].

Committed 2026-08-07: `oracle-overlay` `bb4d717` (also folds in Jetaime's previously-uncommitted
work), `maru-oracle` `e7c0d6f`. Both repos verified clean and current as of 2026-09-07 — see
[[project_oracle_overlay_desktop_mascots]].
