---
layout: article
title: "When a DOCX Round Trip Stops Converging"
date: 2026-11-23
categories: [ documentation-as-code ]
tags: [ asciidoc, docx, testing, docs-as-code ]
author: Joseph
description: >
  A DOCX section carries page setup, headers, footers, and inheritance rules. Making those survive
  AsciiDoc conversion meant treating round-trips as fixed points, not as one successful conversion.
toc: true
---

A DOCX file is more than paragraphs. It can have several sections, each with its own page size, margins, columns, headers and footers, and break type. Word keeps most of that in `sectPr` elements.

AsciiDoc has no native equivalent. When I convert DOCX to AsciiDoc and back, the easy mistake is to preserve the words and lose the layout.

This is the work behind [v4.0.0](https://github.com/verronpro/asciidoc/releases/tag/v4.0.0), released on 14 November. It made section round-trips converge.

## The test is the second conversion

One round-trip is not enough evidence. I want two assertions:

```java
var rendered = toText(toDocx(source), false);
assertEquals(source.stripTrailing(), rendered.stripTrailing());

var stabilized = toText(toDocx(rendered), false);
assertEquals(rendered.stripTrailing(), stabilized.stripTrailing());
```

The first says the converter can rebuild the source. The second says the rebuilt output does not drift when converted again. A converter that adds a block on each pass is still changing the document.

## A section is a span, not only a marker

Version 3.10 added a standalone `[section]` marker. In AsciiDoc, it ends the current section. When writing DOCX, the converter moves the body-level `sectPr` onto the last paragraph of the ended section, which is how Word represents that break, and installs a fresh body-level `sectPr` for the next section.

Headers and footers show the ownership rules:

- a section with no `[header]` or `[footer]` block inherits the previous section's part for that reference kind;
- a section with its own block gets its own part;
- an empty block refers to a distinct empty part and breaks inheritance.

```text
[footer]
--
Section one footer
--

First section content

[section]

[footer]
--
--

Second section content
```

The DOCX reader now emits each section's own header and footer blocks at the start of that section's span, immediately after its `[section]` marker. The previous approach collected all headers at the top and all footers at the end. On re-conversion, they could bind to the wrong section.

## The `titlePg` trap

`titlePg=true` asks for a different first-page header or footer. With no explicit references, docx4j can create empty first-page parts. If the reader treats those parts as authored content, it emits stray `[header]` or `[footer]` blocks. On the next conversion, those blocks can become default parts. The document grows on every cycle.

The fix is to decide ownership from the section's actual `headerReference` and `footerReference` elements. No reference means no emitted block. First-page and even-page parts keep their roles as `[header-first]`, `[footer-even]`, and the other explicit variants.

An explicitly empty part still survives, because it breaks inheritance. An automatically created part with no reference does not, because there was no instruction to preserve.

## Page setup as data

The old converter emitted section layout as a dead `// section {...}` comment. That was readable by a person and useless to the next conversion.

The new `[section-properties]` block carries the layout as data:

```text
[section-properties]
--
pgSz={w=16838, h=11906, orient=landscape}
--

First section content

[section]

Second section content
```

Values accept nested brace maps or dotted paths, and the two forms can be mixed. Rendering is canonical: nested maps and alphabetically sorted keys. DOCX may add defaults the source omitted, so the first rendering can contain `code=9` beside the landscape page size. The canonical rendering, not necessarily the original bytes, becomes the fixed point.

The covered vocabulary includes page size and margins, columns with per-column widths, document grid, break type, `titlePg`, page borders, and right-to-left layout. That is a real section model, not a claim that arbitrary OOXML survives unchanged.

## Metadata is not content

Adding `[section-properties]` exposed a second problem: comment anchors moved when the emission option changed.

The anchors had been captured as a running block weight while walking the document. A newly emitted properties block consumed a position even though it described page setup rather than content. Turn the option on, and a comment's coordinates changed.

The fix separates the two channels. `BlockRecorder.add` registers content; `addMetadata` appends emission metadata without advancing comment coordinates. `SectionBreak` itself has zero size. `CommentRecorder.attach` now resolves a pending anchor when its containing content block is registered.

The tests pin the same anchor across a range spanning two sections, with properties enabled and disabled, and again after a DOCX → AsciiDoc → DOCX → AsciiDoc round-trip:

```text
comment::0[start="0,0", end="1,0", value="commented text"]
```

An output option can change presentation. It should not change where a comment points.

## The edges I left visible

Some page-border details are deliberately not round-trippable: theme-based colors and the `shadow` and `frame` flags. docx4j's `CTBorder` cannot distinguish an unset flag from a set one, so preserving them would mean inventing intent. Unknown top-level section-property keys are ignored with a warning.

That boundary is worth documenting. "Lossless" is only meaningful inside a declared vocabulary.

## Why this became 4.0.0

The breaking change is the output contract. The dead section comments are gone, and `[section-properties]` is emitted by default. Consumers with test pins containing the old comments have to migrate. Callers that only want content can suppress the new blocks with `toAsciidoc(pkg, skipComments, false)`.

The Java API did not need to break for the release to be major. The generated document changed.

The checked-in test run from 14 November records 11 section tests, 2 comment-anchor tests, and 4 header/footer tests, all green. The tests now run the second conversion as part of the contract.
