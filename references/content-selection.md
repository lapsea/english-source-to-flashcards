# Content Selection and Card Writing

Use these rules after understanding the source and before editing the HTML template.

## Transcribe and interpret the source

- Treat visible subtitles, captions, headings, and body copy as source text. Preserve contractions, particles, punctuation, and conversational fragments when they affect meaning.
- For consecutive subtitle screenshots, reconstruct only the ordering that is visually supported. Do not invent missing dialogue.
- Correct an obvious OCR character error only when context makes the correction unambiguous. Otherwise note the uncertainty to the user before generating the deck.
- A supplied title or filename can identify the source, but it is not automatically a learning item.

## Choose worthwhile items

Select up to 12 items using these priorities:

1. Expressions that transfer naturally to other real situations.
2. Common collocations, phrasal verbs, and sentence frames whose meaning is not obvious word by word.
3. Frequent words with a useful contextual sense, confusing usage, or productive word family.
4. Dialogue expressions that reveal tone, stance, politeness, disagreement, hesitation, or emphasis.

Avoid proper names, transparent names of objects, accidental OCR fragments, duplicates, highly technical terms with no likely reuse, and words far below the inferred level unless their use in the source is unusual. Do not force equal counts across `word`, `phrase`, and `expression`.

For dialogue and TV subtitles, prefer chunks a learner could actually say. For formal articles, prefer transferable academic or workplace collocations rather than isolated rare words.

## Write each card

- `term`: use the smallest independently useful learning unit. Keep a necessary preposition or particle, such as `run into` or `be on the same page`.
- `label`: use a short learner-facing label such as `v.`, `n.`, `phr.`, `collocation`, or `spoken`.
- `meaning`: explain the meaning used in context first. Keep Chinese concise and natural; do not dump every dictionary sense.
- `pronunciation`: provide IPA only when confident and useful. It is normally empty for phrases and expressions.
- `example`: prefer a concise, natural sentence that makes the usage obvious. It may come from the source or be newly written.
- `exampleOrigin`: use `source` only for a sentence actually found in the supplied material. Use `supplemented` for rewritten, completed, or newly created examples.
- `translation`: translate the example naturally rather than mirroring English word order.
- `usageNote`: add only when it clarifies register, tone, grammar, collocation, or a likely misuse. Leave it empty when it would merely repeat the definition.

Keep examples short enough for a phone card. If a source sentence is too long, use a shorter generated example and mark it `supplemented`; do not silently edit it while labeling it as a source quotation.

## Assemble the deck

- `deckId` must be a stable lowercase ASCII slug so saved progress belongs only to this deck.
- `title` should name the learning theme, not merely say “English Flashcards”.
- `source` should be short, such as an article title, textbook unit, filename, or episode label. Use `User-provided English material` when no better label exists.
- Card IDs should be unique lowercase ASCII slugs. Add a numeric suffix when two items normalize to the same slug.
- Order cards from approachable to more nuanced, while spreading very similar items apart.

Before delivery, compare every `source` example against the supplied material and downgrade it to `supplemented` if it is not an exact match.
