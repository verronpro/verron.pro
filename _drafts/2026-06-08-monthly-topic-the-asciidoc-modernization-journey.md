---
layout: article
title: "Monthly Topic: The AsciiDoc Modernization Journey"
date: 2026-06-08
categories: [ office-stamper ]
tags: [ asciidoc, docx, docs-as-code ]
author: Joseph
description: Deep dive into the AsciiDoc module overhaul—nested tables, hyperlinks, and why we're betting on docs-as-code.
toc: true
---

The `office-stamper-asciidoc` module just went through a major growth spurt. If you're building "Docs-as-Code" pipelines, this update is for you.

### Breaking the Table Barrier
One of the biggest technical hurdles we faced was **nested tables**. Mapping the recursive structure of AsciiDoc tables to the flat-ish world of OpenXML (DOCX) is notoriously tricky. The v3.2/v3.3 updates finally solve this, allowing complex data structures to render faithfully.

### Interactive Documents
We've also landed support for **hyperlinks, headers, and footers** within AsciiDoc snippets. This makes the generated DOCX feel less like a "snapshot" and more like a professionally authored document.

### Why AsciiDoc?
In high-stakes environments, we need formats that are version-control friendly and readable by both humans and machines. AsciiDoc remains the gold standard for this, and our goal is to make the Java transition to DOCX as seamless as possible.

**Questions for the next round:**
- Joseph, should we include a side-by-side comparison of AsciiDoc source vs. the generated DOCX?
- Are there specific 'Docs-as-Code' patterns (like automated release notes) that you're personally using this for?

---
### June 8th 2026 – AsciiDoc Focus
- **Tech**: Nested table support and hyperlink rendering.
- **Vision**: Strengthening the Docs-as-Code bridge.
