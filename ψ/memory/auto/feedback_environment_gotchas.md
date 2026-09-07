---
name: feedback-environment-gotchas
description: A grab-bag of this machine/environment's tooling traps that cost real time and aren't fixed by any code change — check for them proactively rather than rediscovering each one.
metadata:
  type: feedback
---

Concrete environment traps hit in this project, none derivable from reading the code itself:

- **zsh does not word-split unquoted variables like bash does** (`SH_WORD_SPLIT` off by default).
  A loop like `for combo in "a b" "c d"; do set -- $combo; x=$1; y=$2; done` silently produces
  malformed values (`$1` = whole string, `$2` = empty) instead of erroring. Use nested loops over
  separate variables when looping over multi-field data in a shell one-liner meant to be portable.
- **Headless Chrome's `--virtual-time-budget` does not reliably pump `requestAnimationFrame` or
  long `setTimeout` callbacks** — useless for validating rAF-driven animation loops dynamically;
  test against the real running app instead. Separately, headless Chrome batches also time out
  roughly 1 per 4-6 item batch as a baseline expectation, not an anomaly.
- **`/rrr`'s documented session-dir `sed` command (`s|^/|-|; s|[/.]|-|g'`) doesn't collapse
  underscores** — the real Claude Code project-dir encoding turns `h_wa` into `h-wa`, but the
  documented command doesn't, and returns "no matches found." Hardcode the path from the session's
  own system-reminder header instead.
- **Large generated files with embedded base64 binary blobs exceed the Read tool's token ceiling**
  (`oracle-family.html` hit ~199K tokens, one line at 72,886 chars). Once a rough size/line-count
  check suggests this, use `awk`/`grep -n` line-range previews instead of a whole-file Read —
  cheaper to check first than to hit the hard failure.
- **The `rm -f` safety hook blocks cleanup of session-scratchpad temp files**, even ones that are
  session-isolated and outside any repo. No workaround found; orphaned files may need to be left
  behind rather than cleaned up as instructed.
- **No `pypdf`/`PyPDF2` available in this Python environment** — for PDF page-count discovery, fall
  back to macOS's `mdls -name kMDItemNumberOfPages` rather than assuming a PDF library exists.
