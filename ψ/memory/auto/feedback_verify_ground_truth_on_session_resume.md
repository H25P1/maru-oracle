---
name: feedback-verify-ground-truth-on-session-resume
description: When resuming a session after any gap, check git log/status (or equivalent ground truth) before trusting memory of where things were left — even your own recent, clearly-stated prior output.
metadata:
  type: feedback
---

When a session resumes after any nontrivial gap (a few hours to several days), verify ground truth
— `git log`, `git status`, running-process state — before writing anything that depends on "what
state is this in right now." Applied and re-confirmed 4 times between 2026-07-30 and 2026-08-03 in
this project, always cleanly (no drift ever found, but only because it was actually checked each
time).

**Why**: a gap of any real length is exactly the window where external changes (a manual commit, a
push from another session, a revert) could happen without your knowledge. Having stated the state
correctly and recently is not evidence it's still correct now — confidence from recency is not the
same as verification.

**Companion rule**: when the gap turns out to be genuinely empty, say so plainly and briefly in any
status write-up — don't manufacture narrative content to fill out a template's expected sections.
Padding a quiet period to look substantive is the mirror image of inflating claims of progress; both
substitute a comfortable-looking report for an accurate one.

**How to apply**: before answering any question about current project/repo state, run the check
first, even if the last thing written (by you or anyone) already described that state clearly.
