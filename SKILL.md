---
name: english-source-to-flashcards
description: Turn user-provided English articles, passages, textbook pages, or subtitle screenshots into a curated set of vocabulary, phrases, and authentic expressions, then deliver them as a self-contained interactive HTML flashcard deck. Use when the user wants to learn English from supplied text or images; do not use for generic translation-only requests.
---

# English Source to Flashcards

Create one useful learning deck from the user's English material. Words, phrases, collocations, expressions, and a small number of useful supplemental items are allowed. Every card title must render on one line in the supplied template at a 360px-wide mobile viewport: do not wrap, truncate, or shrink it below the template's minimum title size. Reject a candidate that fails this visual gate, even if it is otherwise valuable.

## Demonstration content

When the user says exactly “演示内容” and does not provide learning material, return [assets/cet6-compact-terms-demo.html](assets/cet6-compact-terms-demo.html) as the demonstration case. It is a ready-to-use CET-6 deck with 20 compact titles; do not regenerate, edit, or supplement it. If the user asks for a file at a separate destination, copy this asset unchanged rather than building a new deck.

## Defaults

- Target Chinese-speaking adult learners around senior-high, university, or CET-4/6 level unless the user specifies otherwise.
- Produce at most 12 cards. Use fewer when the source does not support 12 worthwhile items; do not pad the deck.
- Mix useful words, phrases or collocations, and authentic expressions without enforcing a quota. Supplemental items are optional; retain their provenance in the data, but do not add a visible source-versus-supplemented label to the card.
- Keep short source attribution when it is known. Do not embed the full source text or source image in the deliverable.
- Do not add audio or pronunciation playback. IPA is optional for individual words and may be omitted when uncertain.
- Keep every card at one consistent, viewport-responsive fixed height. When content is longer than the available space, scroll it inside the card instead of changing the card height.
- Marking a card as known or as needing review must update its state without moving to another card.
- If no output location is specified, save the HTML in the current working directory. Use a concise topic-based filename ending in `-english-flashcards.html`, and do not overwrite an existing file without permission.

## Workflow

1. Inspect every supplied text block or image. Transcribe visible English faithfully and preserve the order of multiple screenshots. If essential text is illegible, identify the uncertainty instead of guessing.
2. Infer the source topic, register, and likely learning level. Preserve a supplied title, episode name, or article name as the short source label.
3. Read [references/content-selection.md](references/content-selection.md), then select the strongest learning items that pass the one-line title gate and write the card content.
4. Copy [assets/flashcards-template.html](assets/flashcards-template.html) to the output file. Replace the complete JSON value inside the `deck-data` script element; do not restructure the interface for ordinary requests.
5. Give each card a stable, unique `id`. Set `exampleOrigin` to `source` only when the example is actually present in the supplied material; otherwise use `supplemented`. This is a data-validation field and must not be rendered as card copy.
6. Keep the output fully self-contained: inline HTML, CSS, JavaScript, and data only. Do not introduce fonts, CDNs, APIs, remote images, or build steps.
7. Validate the result before handing it off. Confirm that the deck JSON parses, the template sample data is gone, all required card fields are present, the number of cards and progress maximum agree, and no content overflows at a 360px-wide mobile viewport. Specifically check every front-side title: it must be one line, fully visible, and at or above the template's minimum title size. When browser tools are available, open the local file and test card flip, next/previous navigation, both learning buttons, keyboard navigation, and saved progress.

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
      "label": "adj.",
      "term": "reluctant",
      "pronunciation": "/rɪˈlʌktənt/",
      "meaning": "不情愿的；勉强的",
      "example": "She was reluctant to change her mind.",
      "translation": "她不太愿意改变想法。",
      "usageNote": "常用结构：be reluctant to do something。",
      "exampleOrigin": "source"
    }
  ]
}
```

Allowed `kind` values are `word`, `phrase`, and `expression`. `term` may be a selected source item or an optional supplemental item, but it must pass the one-line title gate. Do not abbreviate, ellipsize, or alter a term merely to make it fit; choose a different item instead. Required string fields are `id`, `kind`, `label`, `term`, `meaning`, `example`, `translation`, and `exampleOrigin`. `pronunciation`, `usageNote`, and `source` may be empty strings. Allowed `exampleOrigin` values are `source` and `supplemented`.

When embedding user text in the JSON script element, serialize valid JSON and escape `<` as `\u003c` so source text cannot accidentally close the script element. The page renders content with `textContent`; keep that safety property.
