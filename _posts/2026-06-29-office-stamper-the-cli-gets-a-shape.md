---
layout: article
title: "office-stamper: The CLI Gets a Shape"
date: 2026-06-29
categories: [ office-stamper ]
tags: [ office-stamper, java, cli, picocli, tooling ]
author: Joseph
description: >
  The CLI grew organically into a Main class that did too much. This commit split it into a
  contextualizer, an emitter, and a stamp command with watch mode.
---

office-stamper started as a library you embed. The CLI grew on top of it
organically, and by June 2026 it had accreted into a `Main` class that did too
much. Reading five hundred lines to see a workflow I already knew was the pain.
A `main` method should read like the workflow it drives. This commit gives it
that shape.

Two responsibilities were tangled: turning a data file into a SpEL context, and
reporting what happened. They're now two seams.

`Contextualizer` parses a data file, JSON, YAML, properties, CSV, XLSX, XML or
HTML, into the context SpEL evaluates against, and it can stamp a directory of
templates in one pass.

`Emitter` is a single-method interface with two implementations, `JsonEmitter`
and `LogEmitter`:

```java
public interface Emitter {
    void emit(String level, String message, @Nullable Map<String, ?> fields);
}
```

One is for humans, the other for machines. The stamping logic doesn't care which.

The command surface is now a `stamp` command:

```text
officestamper -t template.docx -d data.json -o output.docx
officestamper -t template.docx -d data.json --watch
```

`--watch` re-runs stamping when the template or data files change, which turns
the CLI from a one-shot tool into the front half of a development loop.

The internals moved into a few small types: `TemplateKind`, the `RunResult` and
`Item` records, and `PathUtils` for the file plumbing. The `Main` entry point is
now mostly wiring.
