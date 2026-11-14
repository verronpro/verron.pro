---
layout: article
title: "office-stamper: Placeholders That Respect Braces"
date: 2026-08-10
categories: [ office-stamper ]
tags: [ office-stamper, java, spel, parsing, bugfix ]
author: Joseph
description: >
  The placeholder scanner stopped at the first closing brace, so inline SpEL lists and maps broke.
  A brace-balancing scan fixes it.
toc: true
---

SpEL inline lists and maps look like `${ {1, 2, 3} }` and `${ {'a': 1, 'b': 2} }`.
The placeholder scanner, however, stopped at the first closing brace it saw.

The old implementation used a regular expression that forbade nested braces.
That was fine for `${user.name}` and broke the moment an expression legitimately
contained its own braces. An inline map would be truncated at its first `}`, and
the rest of the expression leaked out as literal text.

`PlaceholderHooker` now scans left-to-right for the opening delimiter, then
balances braces instead of stopping at the first close:

```java
int depth = 1;
// each '{' increments, each '}' decrements;
// the placeholder ends when depth reaches 0
```

A placeholder now ends at the brace that balances its opening brace:

```text
${ {1, 2, 3} }          -> expression " {1, 2, 3} "
${ {'a': 1, 'b': 2} }   -> expression " {'a': 1, 'b': 2} "
```

A placeholder whose opening brace is never balanced is captured verbatim and
handed to the configured exception resolver, so a broken template fails loudly
instead of silently emitting half an expression.

When a parser's job is to find the balanced end of a construct, a regex is
usually the wrong tool. Count the depth instead.

Related issue: [#796]({{site.ghos}}/issues/796).
