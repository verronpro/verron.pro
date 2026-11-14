---
layout: article
title: "office-stamper 3.8: Shared Headers, Once"
date: 2026-11-13
categories: [ office-stamper ]
tags: [ office-stamper, java, release, docx, packaging ]
author: Joseph
description: >
  office-stamper 3.8: a fix for shared headers and footers being processed twice, the asciidoc 3.10
  bump, and a portable Windows EXE. No breaking changes.
---

This is a maintenance release with one headline fix and a packaging improvement.

## Headline — shared headers and footers, once (#805)

A header or footer that is shared by several sections was being visited more
than once. The smart-tags postprocessor then found a tag it had already
unwrapped, and threw an `IndexOutOfBoundsException: Index: -1`.

The fix is small and lives in one place — a deduplication set plus an index
guard:

```java
// HookRemover — process each header/footer part exactly once
private final Set<CTSmartTagRun> seen =
        Collections.newSetFromMap(new IdentityHashMap<>());

// A tag may have been unwrapped by a previous pass when the same
// part was visited more than once (a header shared by several sections).
if (index < 0) continue;
```

Document visitors now process each header/footer part exactly once, and a
regression test (`HeaderInheritanceTest`) pins the inherited-header case.

## Dependency — asciidoc 3.10

The AsciiDoc module moves to v3.10, which brings the standalone `[section]`
marker for ending a document section explicitly.

## Packaging — a portable Windows EXE

There is now an `officestamper.exe` you can run without an installer: a fat jar
wrapped in a 7-Zip self-extracting executable, built from the `windows-portable`
profile. The installer profile (`windows-exe`) remains for a proper jpackage
build.

```text
mvn -pl :cli -am -P windows-portable -DskipTests package
mvn -pl :cli -am -P windows-exe      -DskipTests package
```

## Breaking changes

None. No migration notes are required; the change is invisible unless you were
tripping over shared headers.

Related issues: [#805]({{site.ghos}}/issues/805).

---
### 3.8 — Release Summary
- **Fix**: shared header/footer parts are visited once (#805).
- **Deps**: asciidoc 3.10.
- **Packaging**: portable Windows EXE (fat jar + 7-Zip SFX).
- **Breaking**: none.
