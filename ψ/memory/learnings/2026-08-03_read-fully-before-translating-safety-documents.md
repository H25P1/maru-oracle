---
pattern: For long safety-critical translations, read the entire source document first (even across multiple tool-call chunks) before writing any translated output, and keep proper nouns/units/model numbers untranslated with an explicit "original governs" disclaimer
date: 2026-08-03
source: rrr: maru-oracle
concepts: [translation, technical-documentation, safety, terminology-consistency]
---

# Read fully before translating safety-critical documents

## The situation

Asked to translate a 69-page electrical installation manual (SolarEdge inverter) into Thai, with an
explicit request to translate the whole thing, not a summary. The source PDF had to be fetched in
5 separate chunks due to a per-call page limit.

## The rule

Read the entire source document before writing any of the translation, even when tool limits force
you to fetch it piecemeal. Chunk-by-chunk translate-as-you-go creates a real risk: the same source
term (a product name, a safety term, a technical concept) can get rendered two different ways in
different chunks if you commit to a phrasing before seeing how the term is used elsewhere in the
document. Reading everything first lets you fix one consistent glossary before any output is
written, rather than doing find-and-replace cleanup afterward (which is easy to miss instances of).

## The companion rule

When the content being translated carries real-world safety, legal, or contractual weight — electrical
installation steps, dosage instructions, compliance thresholds, contract terms — keep the source
language's proper nouns, product/model names, units, and technical identifiers untranslated in the
output, and add an explicit, prominent disclaimer stating that the original document governs in case
of any conflict or ambiguity. This isn't just a spoken caveat in the conversation — it needs to live
inside the delivered file itself, since the file is what persists and gets used later, detached from
the conversation that produced it. A translation is a convenience layer for reading comprehension, not
a new authoritative source — the document should say so plainly, on its own.

## Related

- [[2026-07-28_confirm-interpretation-before-building]] — same underlying discipline: confirm scope
  and calibrate before committing effort, applied there to a build task, here to a translation task.
