---
pattern: a browser-automation script-injection timeout is not proof the page's content is broken — cross-check with an independent, non-script-injecting fetch before concluding you broke something
date: 2026-07-31
source: rrr: maru-oracle
concepts: [browser-automation, debugging, verification, artifacts, csp, cross-repo]
---

# Verify tooling failure before blaming content

When a headless-browser tool (screenshot, `get_page_text`, script injection) times out or errors against a page, that failure can mean one of two very different things:

1. The page's content is actually broken (infinite loop, crash, bad render).
2. The tool itself cannot operate in that page's security context — a sandboxed cross-origin iframe, a strict CSP blocking script injection, missing extension permissions on that origin.

These two failure modes look **identical** from the outside: both surface as "script injection timed out" or "still loading after N seconds." Jumping to conclusion (1) leads to wasted effort re-debugging content that was never wrong.

**The discriminating test**: fetch the same content through an independent path that doesn't rely on in-page script injection — an authenticated content fetch (e.g. a `WebFetch`-style tool), a plain HTTP request, or opening the same content via a different rendering path (a local file server instead of a sandboxed remote iframe). If that independent fetch returns full, correct content, and the console shows zero *origin-matched* errors (not just any console noise — cross-origin extension noise is common and irrelevant), the content is very likely fine and the failure is in the tool/environment boundary, not the page.

**Applies to**: any project using headless-browser verification (Puppeteer/Playwright/Chrome-extension automation) against pages that may run inside sandboxed iframes, strict CSPs, or third-party embed contexts — not specific to this Oracle's voxel-dog artifact pipeline. Also applies to Claude Artifacts specifically: `claude.ai/code/artifact/*` renders inside such a sandboxed iframe, so browser-extension automation against that URL form should expect this failure mode and not treat it as page-content evidence.

**How to apply**: when a screenshot/injection tool fails against a URL you suspect you just changed, do not start re-debugging the content. First re-fetch via an independent method and check for origin-matched console errors. Only escalate to content debugging if that independent check also shows a problem.

See also: [[2026-07-28_confirm-interpretation-before-building]] (a related discipline — verify assumptions before building on them, here applied to verifying tool failures before diagnosing on top of them).
