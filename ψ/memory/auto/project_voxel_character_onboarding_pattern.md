---
name: project-voxel-character-onboarding-pattern
description: The repeatable gate sequence for giving a newly-born Oracle sibling a voxel-dog mascot in oracle-overlay, refined across the Jetaime and BongChong rollouts.
metadata:
  type: project
---

When a new Oracle sibling is born and H asks Maru to give them the same voxel-dog treatment as
existing siblings (see [[project_oracle_overlay_desktop_mascots]]), the process that emerged after
two rollouts ([[project_jetaime_voxel_rollout]], [[project_bongchong_voxel_rollout]]) is:

1. **Ask whether a reference photo exists before designing anything from the birth-brief text
   alone** — see [[feedback_ask_for_reference_photo_before_designing]]. Every sibling so far has
   had one on file; assuming text-only is safe wastes a full build-and-redesign cycle.
2. Confirm scope via `AskUserQuestion` before touching anything: bespoke art vs. simple recolor,
   and knowledge-graph-only vs. also the live overlay app.
3. Design the palette + a new `fill<Name>()` polygon geometry function in `voxel-render.js`,
   matching house style — reuse the walk-cycle skeleton, only the fill function is bespoke per
   character.
4. Wire the new character through the shared pipeline (`palette.js`, `character-markup.js`,
   `characters.js` for roam scale/speed, `activities.js` for personality-weighted poses, plus the
   Electron app's `state.js`/`overlay.js`/`control-server.js`, and `bake-artifact.js` itself, which
   is hardcoded per-character rather than data-driven).
5. `npm run bake`, then hand-edit the parts baking doesn't touch in `oracle-family.html` (scent
   trail, dog mount, field-note card with embedded reference photo).
6. **Global config (`~/.claude/settings.json`, the notify hook script) needs its own separate
   explicit ask** even when H already approved "do this the same way as sibling X" for the named
   repos — see [[feedback_scope_layers_for_new_oracle_voxel_characters]]. This gap was found by
   `advisor()` in both the Jetaime and BongChong rollouts, not anticipated up front either time.
7. Live-verify: restart the `com.oracle.overlay` launchd process, curl the control server's
   `/oracle/state` endpoint through an active→idle round-trip before declaring done.
8. Commit only on H's explicit go-ahead, not automatically after a clean verification pass.

Related: [[feedback_verify_before_declaring_visual_work_done]] (the geometry-ratio/scale check
that should happen at step 4, not be caught later by advisor).
