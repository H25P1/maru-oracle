---
name: reference-oracle-overlay-repo-location
description: Where the oracle-overlay repo and its live desktop app actually live, since it's outside maru-oracle's own folder and not discoverable from this repo alone.
metadata:
  type: reference
---

`oracle-overlay` — the Electron desktop-mascot app and shared render/behavior source of truth
described in [[project_oracle_overlay_desktop_mascots]] — lives at
`/Users/h_wa/oracle-agents/oracle-overlay`, a sibling repo to `maru-oracle`, not nested inside it.
Its live running instance is a launchd service (`com.oracle.overlay`) exposing a local control
server with an `/oracle/state` endpoint (used for curl-based active→idle verification after
restarts). Key scripts: `npm run bake` (exports the shared render source into
`maru-oracle/knowledge-graph/oracle-family.html`) and `npm run bake:check` (verifies no drift
between the two before committing either repo).
