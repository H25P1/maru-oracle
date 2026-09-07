---
pattern: When resuming a session after any nontrivial gap, verify ground truth (git log, git status, running state) before trusting your own memory of where things were left — a gap is exactly the window where memory and reality can silently diverge.
date: 2026-07-30
source: rrr: maru-oracle
concepts: [session-continuity, verification, retrospectives]
---

# Verify ground truth on session resume, don't trust memory of the gap

## The situation

A session picked back up after a two-day gap with no messages or commits
in between. The prior retro (written 2026-07-28) had already stated
exactly which commits were the latest in both repos involved. It would
have been easy to just assume that state still held and write the next
retro from memory alone.

## The rule

Don't. Check `git log` / `git status` (or the equivalent ground truth for
whatever the project is) before writing anything that depends on "what
state is this in right now" — even, or especially, when your own prior
output already described that state clearly and recently. A gap of any
real length is exactly the window in which external changes (a manual
commit, a push from another session, a revert, a dependency update) could
have happened without your knowledge. Confidence from having stated
something correctly before is not evidence it's still correct now.

## The companion rule

A retrospective (or any status report) covering a genuinely empty segment
should say so plainly and briefly, not manufacture narrative content to
look substantive. Padding a quiet period to satisfy a template's expected
sections is a mirror image of the more commonly-flagged failure (inflating
claims of progress) — both substitute a comfortable-looking write-up for
an accurate one. Say "nothing happened, here's how I confirmed that" and
stop.

## Related

- [[unrewritten-attributes-are-hidden-dependencies]] — same underlying
  discipline from a few days earlier in the same project: verify the
  specific thing that's actually uncertain (there, DOM state; here,
  repo/session state) rather than trusting an assumption because it's
  convenient or was true recently.
