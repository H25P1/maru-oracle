---
name: feedback-scope-layers-for-new-oracle-voxel-characters
description: An approval to touch named repos the way a prior sibling's rollout did does not cover global machine-wide config — that needs its own explicit ask, surfaced as soon as the gap is found.
metadata:
  type: feedback
---

When H approves "do this for the new sibling the same way you did it for [prior sibling]," that
approval covers exactly the repos named (e.g. `oracle-overlay` and `maru-oracle`) — it does not
extend to global, machine-wide configuration: `~/.claude/settings.json`, hook scripts under
`~/.claude/hooks/`, launchd/systemd configs, shell profiles. `advisor()` caught this gap
independently in both the Jetaime and BongChong voxel-character rollouts (see
[[project_jetaime_voxel_rollout]], [[project_bongchong_voxel_rollout]]) — in both cases the overlay
app's recognition of the new character required editing global hook wiring that hadn't been part of
the original ask, and it was surfaced as a separate `AskUserQuestion` before touching it, not
bundled retroactively into the earlier repo-scoped approval.

**Why**: global config affects every other Oracle's session, not just the one repo being worked in
— a materially different blast radius than the named repos, even when the change itself is small
(e.g. adding one new character key to an existing hook block).

**How to apply**: when a task's plan surfaces a need to touch anything outside the explicitly-named
repos — especially shared/global machine config — stop and ask for that specific scope separately,
as soon as the gap is discovered, rather than assuming a broader "do it like last time" covers it.
