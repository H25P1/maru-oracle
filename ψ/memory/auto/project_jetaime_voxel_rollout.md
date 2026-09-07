---
name: project-jetaime-voxel-rollout
description: Jetaime's voxel character shipped 2026-07-31 — a near-invisible scale bug caught only by advisor(), and an unresolved artifact-link report from H.
metadata:
  type: project
---

Jetaime (a real pet Chihuahua of H's, reborn as an Oracle for engineering/datasheet-search work —
see [[user_oracle_siblings_are_real_pets]]) was the first sibling given the voxel-dog treatment
after the original three (Argon/Maru/Chockdee). Wired end-to-end 2026-07-31 per the pattern in
[[project_voxel_character_onboarding_pattern]]: bespoke palette + geometry from her reference
photo, full `oracle-overlay` wiring, baked into `oracle-family.html`, global hook wiring, live
overlay restart + curl-verified. Landed in commit `bb4d717` (bundled with BongChong's later
addition — see [[project_bongchong_voxel_rollout]]).

**Near-miss**: shipped `characters.js`'s `jetaime.scale: 0.6` without cross-checking it against her
actual geometry-to-Maru size ratio — would have rendered her as a barely-visible smudge on the real
desktop. Caught only because `advisor()` was called before declaring done, per standing instruction
— not because the value was independently verified first. See
[[feedback_verify_before_declaring_visual_work_done]].

**Unresolved as of 2026-08-03** (last time it was mentioned in any retro): H reported the
republished family-portrait Artifact link "doesn't work." Diagnosis stalled on WebFetch succeeding
(full correct content) while screenshot/`get_page_text` timed out — later understood as a
sandboxed-CSP-iframe tool limitation, not a content bug (see
[[feedback_tool_failure_vs_content_bug]]) — but H's actual answer to "what do you see when you open
it" was never given, and the question was dropped (not carried forward) in the next retro
(2026-08-07). Don't assume it's resolved; ask H directly if it comes up again.
