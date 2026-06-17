---
layout: article
title: "How-To: Diagnosing DOCX Templates with the New CLI Tooling"
date: 2026-06-10
categories: [ office-stamper, tutorial ]
tags: [ cli, troubleshooting, java ]
author: Joseph
description: Stop guessing why your template is failing. Use the new v3.3 diagnostic CLI tools to find the root cause.
toc: true
---

We've all been there: you run the stamper, and nothing happens—or worse, the document comes out mangled. With the v3.3.0 update, we've beefed up the **CLI Diagnostic** capabilities to help you debug templates faster.

### The `Diagnostic` Command
The new `pro.verron.officestamper.Diagnostic` utility (accessible via the CLI) can now perform a "dry run" of your template. It scans for:
- **Malformed Smart Tags**: Tags that aren't closed or have invalid syntax.
- **Unresolvable Placeholders**: Fields in your template that don't match your data model.
- **SVG Compatibility**: Checking if the embedded SVG assets meet the required XML standards.

### Integration with JavaFX
For those using the GUI-based CLI, we've updated to **JavaFX 27-ea+10**. This brings better rendering for the template preview and more responsive error reporting.

**Questions for the next round:**
- Joseph, should we provide a 'Troubleshooting Checklist' as a downloadable PDF for the CLI?
- Do you want to highlight any specific error messages that are now 'more human-readable'?

---
### June 10th 2026 – CLI Update
- **Feature**: Enhanced diagnostic commands.
- **UI**: JavaFX 27-ea integration for the CLI tool.
