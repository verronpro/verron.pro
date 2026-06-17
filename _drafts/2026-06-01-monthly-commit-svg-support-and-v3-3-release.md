---
layout: article
title: "Monthly Commit: SVG Support and v3.3 Release"
date: 2026-06-01
categories: [ office-stamper ]
tags: [ office-stamper, svg, release, java ]
author: Joseph
description: Announcing office-stamper v3.3.0 with native SVG support, smart tag validation, and a leaner engine.
toc: true
---

June starts with a major milestone for `office-stamper`: the release of **v3.3.0**. The headline feature is something many of you have asked for: **Native SVG Support**.

### High-Fidelity Vector Graphics
Until now, inserting images usually meant dealing with raster formats. With v3.3.0, the `Image` class now automatically detects SVG content. Under the hood, we've implemented `WmlFactory.newSVGDrawing` to handle the complex handshake between SVG and OpenXML. This means your charts, icons, and diagrams stay crisp at any zoom level.

### Smarter Templates with Tag Validation
We've also introduced `WmlUtils.hasTagAttribute`. This might sound like a low-level utility, but it's a game-changer for template debugging. It allows the engine to validate the existence and value of attributes within DOCX smart tags before processing, catching typos early.

### Leaner and Meaner
As part of our ongoing "Caring Coder" mission to keep the codebase maintainable, we've stripped out legacy utilities like `ByteUtils` and `DocxRenderer` from the core module. 

**Questions for the next round:**
- Joseph, how much should we emphasize the "vector vs raster" benefit? Is there a specific high-stakes use case (like technical blueprints) where SVG was a blocker for you?
- Do you want to mention the specific SVG library used, or keep it focused on the end-user experience?

---
### June 1st 2026 – Commit Summary
- **Feature**: Native SVG insertion.
- **Tooling**: Smart tag attribute validation.
- **Cleanup**: Deprecated utility removal.
