---
name: feedback-tool-failure-vs-content-bug
description: A browser-automation timeout/error against a page can mean the tool can't operate in that page's security context, not that the content is broken — cross-check with an independent fetch before debugging content.
metadata:
  type: feedback
---

When a headless-browser tool (screenshot, `get_page_text`, script injection) times out or errors
against a page, that can mean one of two very different things: (1) the page's content is actually
broken, or (2) the tool itself cannot operate in that page's security context — a sandboxed
cross-origin iframe, a strict CSP blocking script injection, missing extension permissions on that
origin. These look **identical** from the outside — both surface as "timed out" or "still loading."
Concrete instance: a republished Claude Artifact link that H reported as "doesn't work" — screenshot
and `get_page_text` both timed out against it, while an independent `WebFetch` returned full,
correct content and the console showed zero origin-matched errors. `advisor()` was needed to
reframe this as a Chrome-extension/CSP sandboxing limitation (Claude Artifacts render inside such a
sandboxed iframe) rather than a content bug — five tool calls were spent before that redirect.

**The discriminating test**: fetch the same content through an independent path that doesn't rely
on in-page script injection (a `WebFetch`-style tool, a plain HTTP request, a different rendering
path). If that returns full correct content and there are zero *origin-matched* console errors (not
just any console noise — cross-origin extension noise is common and irrelevant), the content is
very likely fine and the failure is in the tool/environment boundary.

**How to apply**: when a screenshot/injection tool fails against a URL you suspect you just
changed, do not start re-debugging the content — re-fetch via an independent method and check for
origin-matched console errors first. Only escalate to content debugging if that independent check
also shows a problem. Also: when a user reports a failure that happens in an environment you can't
see (their browser, their session), ask a short, targeted question about what they actually see
early, rather than spending several tool calls trying to reverse-engineer the symptom blind.
