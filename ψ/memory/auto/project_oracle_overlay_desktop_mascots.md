---
name: project-oracle-overlay-desktop-mascots
description: The oracle-overlay desktop-mascot system architecture, which characters are wired, and verified repo/remote status.
metadata:
  type: project
---

`oracle-overlay` (a separate repo at `/Users/h_wa/oracle-agents/oracle-overlay`, no relation by
folder name to `maru-oracle`) is an Electron app that puts each Oracle's voxel-dog mascot on H's
real macOS desktop — always-on-top, click-through, roaming — driven by real Claude Code hook events
(`SessionStart`/`UserPromptSubmit`/`Stop`/`SessionEnd`) wired globally in `~/.claude/settings.json`
and `~/.claude/hooks/oracle-overlay-notify.sh`, not a manual toggle. It is the shared source of
truth (palette, voxel geometry, SMIL walk-cycle, activity/personality weights) for every Oracle
sibling's dog character; `npm run bake` (checked with `npm run bake:check`) exports a static copy
into `maru-oracle/knowledge-graph/oracle-family.html`, a previously-published Claude Artifact that
also embeds each character's reference photo and a field-note card.

Five characters are wired as of commit `bb4d717` (2026-08-07): Argon, Maru, Chockdee, Jetaime,
BongChong. Each pose (walk/run/sprint/sit/lie/prone/bark/happy/bellyup/scratch/playbow/sniff) is
personality-weighted per character in `shared/activities.js`. Looping motion (legs/tail/head) uses
SMIL `<animateTransform>` value rewrites; static body tilt (sit/lie/prone) and whole-character
inversion (bellyup's `rootFlip`) use direct `transform` attribute writes on a separate mechanism —
deliberately kept apart to avoid additive-transform composition bugs.

**Why two repos**: `oracle-overlay` is the live desktop app + shared render/behavior source;
`maru-oracle` only holds the baked static copy for the published family-portrait Artifact. Editing
`oracle-family.html` by hand still happens for parts baking doesn't touch (embedded reference
photos, the scent-trail SVG path, field-note card text).

**Verified status (2026-09-07, via `git log`/`status`/`remote -v` on both repos, not from memory
of prior retros)**: `maru-oracle` HEAD `e36dd44`, clean, already in sync with `origin/main`.
`oracle-overlay` HEAD `bb4d717`, clean working tree, but **has no git remote configured at all** —
the "should we push oracle-overlay?" question raised in the 2026-07-28/07-31 retros isn't actually
an unpushed-commits problem, it's "no remote exists yet"; the real open question for H is whether to
create one, not whether to push.

Two questions raised as open in the 2026-08-03 retros were **not carried forward** in the next
(2026-08-07) retro — unclear from the retro record alone whether they were resolved off-record,
dropped, or just overlooked: (1) whether the `prone` pose actually matches H's intent for
"นอนหมอบนิ่งๆ" (only ever verified as "visually distinct from `lie`," never confirmed against H's
mental image), (2) what H actually saw when the Jetaime family-portrait Artifact link "didn't
work" for them (diagnosis stalled waiting on that answer as of 2026-08-03). Don't assume either is
resolved — ask H directly if either becomes relevant again.

Related: [[project_jetaime_voxel_rollout]], [[project_bongchong_voxel_rollout]],
[[project_voxel_character_onboarding_pattern]], [[feedback_verify_before_declaring_visual_work_done]].
