---
layout: article
title: "Monthly Topic: The AsciiDoc Modernization Journey"
date: 2026-06-22
categories: [ asciidoc, office-stamper ]
tags: [ asciidoc, docx, docs-as-code, asciidoctor, eclipse-austen, ai ]
author: Joseph
description: >
  The real story behind office-stamper's AsciiDoc journey: from a developer
  debugging tool to a specialized, AI-assisted converter for DOCX-native
  features like headers, footnotes, and even SVG previews.
toc: true
---

The AsciiDoc features in `office-stamper` didn't start as a public-facing
module. They emerged from a practical, internal need: developer sanity.

When maintaining a library that manipulates complex OpenXML structures,
debugging means digging through endless hierarchies of `docx4j` objects. I
needed a way to see the results of my tests in a human-readable format without
launching Word every five minutes. AsciiDoc was the perfect tool for the job.

## From Debugging Tool to Codebase Cleanup

Once I had a basic converter that could turn AsciiDoc snippets into DOCX
fragments for testing, I realized I could use it for more than just debugging.

Our codebase was cluttered with binary `.docx` documents used as templates for
tests. These are a nightmare for version control and almost impossible to review
in a Pull Request. By moving these simple templates directly into AsciiDoc, I
could keep the logic, and the content in plain text, making the library much
easier to maintain.

## The Search for a Sustainable Pipeline

My first instinct was to integrate `AsciidoctorJ` directly into the pipeline. It
is the gold standard for AsciiDoc processing, but I quickly ran into a major
roadblock: performance. For the lightweight, fast-moving environment of
`office-stamper`, the JRuby-based engine's startup time and memory overhead were
simply more than I was willing to accept.

At the same time, I was keeping a close eye on the budding efforts of the
Eclipse Foundation to standardize the language
under [Project Austen](https://projects.eclipse.org/projects/asciidoc.austen)
and
the [AsciiDoc Language](https://projects.eclipse.org/projects/asciidoc.asciidoc-lang)
project. It is clear the ecosystem is moving towards more native and portable
implementations.

## A Specialized Path: AI and Custom Implementation

I decided to take a leap and experiment with AI to help me implement my own
specialized version of an AsciiDoc compiler.

By narrowing the scope strictly to what is relevant for DOCX generation, I could
create a highly optimized, native Java implementation. While it isn't (yet) a
general-purpose converter capable of a full round-trip for every AsciiDoc
and DOCX feature, it is pertinent at the things that matter most for office
documents.

Today, this custom engine handles features that are usually an afterthought in
general-purpose tools:

* **Headers and Footers**: Properly integrated into the Word document sections.
* **Endnotes and Footnotes**: With correct numbering and layout.
* **Comments and Annotations**: Allowing for collaborative-style documents.
* **Shapes and Images**: Native handling of vector formats.

## Visualizing the Documentation

One of the most exciting recent evolutions is the development of an
AsciiDoc-to-SVG converter.

Generating documentation for a document-generation library is ironic. To show
what `office-stamper` can do, you need visual examples. By converting AsciiDoc
snippets into SVGs that mimic the "look and feel" of a real DOCX editor, we can
generate high-quality, realistic previews directly within our documentation.

This allows us to keep our entire documentation base in AsciiDoc format while
providing the visual clarity of a GUI-based editor.

## The Journey Continues

The transition from a quick debugging hack to a specialized AI-assisted compiler
has been rewarding. It has allowed `office-stamper` to remain fast and
lightweight while offering deep integration with the most powerful features of
the Word format.

As the Eclipse Foundation projects mature, and our own implementation grows, the
goal remains the same: making document generation as seamless and
developer-friendly as writing code.
