---
name: english-source-to-flashcards
description: Turn user-provided English articles, passages, textbook pages, or subtitle screenshots into a curated set of vocabulary, phrases, and authentic expressions, then deliver them as a self-contained interactive HTML flashcard deck. Use when the user wants to learn English from supplied text or images; do not use for generic translation-only requests.
---

# English Source to Flashcards

Create one useful learning deck from the user's English material. Treat the material as a starting point: examples may be supplemented when that improves learning, but never present a generated example as a quotation from the source.

## Defaults

- Target Chinese-speaking adult learners around senior-high, university, or CET-4/6 level unless the user specifies otherwise.
- Produce at most 12 cards. Use fewer when the source does not support 12 worthwhile items; do not pad the deck.
- Mix useful words, phrases or collocations, and authentic expressions without enforcing a quota. Give conversational expressions more weight for dialogue or subtitle sources.
- Keep short source attribution when it is known. Do not embed the full source text or source image in the deliverable.
- Do not add audio or pronunciation playback. IPA is optional for individual words and may be omitted when uncertain.
- If no output location is specified, save the HTML in the current working directory. Use a concise topic-based filename ending in `-english-flashcards.html`, and do not overwrite an existing file without permission.

## Workflow

1. Inspect every supplied text block or image. Transcribe visible English faithfully and preserve the order of multiple screenshots. If essential text is illegible, identify the uncertainty instead of guessing.
2. Infer the source topic, register, and likely learning level. Preserve a supplied title, episode name, or article name as the short source label.
3. Read [references/content-selection.md](references/content-selection.md), then select the strongest learning items and write the card content.
4. Copy [assets/flashcards-template.html](assets/flashcards-template.html) to the output file. Replace the complete JSON value inside the `deck-data` script element; do not restructure the interface for ordinary requests.
5. Give each card a stable, unique `id`. Set `exampleOrigin` to `source` only when the example is actually present in the supplied material; otherwise use `supplemented`.
6. Keep the output fully self-contained: inline HTML, CSS, JavaScript, and data only. Do not introduce fonts, CDNs, APIs, remote images, or build steps.
7. Validate the result before handing it off. Confirm that the deck JSON parses, the template sample data is gone, all required card fields are present, the number of cards and progress maximum agree, and no content overflows at a narrow mobile width. When browser tools are available, open the local file and test card flip, next/previous navigation, both learning buttons, keyboard navigation, and saved progress.

## Output Contract

Return one `.html` file and briefly state the number and mix of cards created. Do not add a separate vocabulary report unless the user asks for one.

The embedded JSON must follow this shape:

```json
{
  "deckId": "stable-topic-slug",
  "title": "A short deck title",
  "source": "Short source label",
  "cards": [
    {
      "id": "stable-card-id",
      "kind": "word",
      "label": "v.",
      "term": "figure out",
      "pronunciation": "",
      "meaning": "弄清楚；想明白",
      "example": "We'll figure it out.",
      "translation": "我们会想出办法的。",
      "usageNote": "口语中常用来表示找到答案或解决办法。",
      "exampleOrigin": "source"
    }
  ]
}
```

Allowed `kind` values are `word`, `phrase`, and `expression`. Required string fields are `id`, `kind`, `label`, `term`, `meaning`, `example`, `translation`, and `exampleOrigin`. `pronunciation`, `usageNote`, and `source` may be empty strings. Allowed `exampleOrigin` values are `source` and `supplemented`.

When embedding user text in the JSON script element, serialize valid JSON and escape `<` as `\u003c` so source text cannot accidentally close the script element. The page renders content with `textContent`; keep that safety property.
