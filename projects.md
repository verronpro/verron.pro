---
layout: page
title: Projects
permalink: /projects.html
description: A living list of ongoing work and projects I’m actively building — from docs-as-code tooling to Office automation experiments.
aside:
  toc: true
---

This page tracks current projects and initiatives I’m actively building, along with a focused backlog of work in progress. If you want to collaborate on any of these, or if a topic would help your team, reach out via LinkedIn (see About) or GitHub issues.

## Office‑stamper

**A Java template engine for dynamic DOCX generation — secure by default, crafted with care.**

Office‑stamper lets you design a Word template in your favourite processor and stamp it at runtime with any Java object as context.
It uses Spring Expression Language (SpEL) for powerful, type-safe expressions and preserves all formatting from the original template.

**Why it exists:** generating `.docx` files programmatically and compliant to company graphic guidelines is harder than it looks.
Office‑stamper handles the edge cases — nested repeats, conditional sections, table rows, image insertion, and more — so you don't have to.

### Key links

| | |
|---|---|
| 📦 **Source** | [github.com/verronpro/office-stamper](https://github.com/verronpro/office-stamper) |
| 📖 **Docs** | [office-stamper.verron.pro](https://office-stamper.verron.pro/engine) |
| 🚀 **Latest release** | v3.3 — SVG support, smart tag validation, hardened SpEL security |
| 🪪 **License** | MIT |

### Quick start

```xml
<dependency>
  <groupId>pro.verron.office-stamper</groupId>
  <artifactId>engine</artifactId>
  <version>3.3</version>
</dependency>
<!-- also include your version of docx4j -->
```

```java
var stamper = OfficeStampers.docxStamper();
try (var template = Files.newInputStream(templatePath);
     var output  = Files.newOutputStream(outputPath)) {
    stamper.stamp(template, context, output);
}
```

### Stories behind the code

- [The Expression Pivot — Harnessing Spring SpEL](/2026/03/01/monthly-topic-the-expression-pivot-harnessing-spring-spel.html)
- [Predicting the Unpredictable — the v3 Overhaul](/2025/12/15/monthly-topic-predicting-the-unpredictable-v3-overhaul.html)
- [Office-stamper 3.1 — Stabilizing the Surface](/2026/01/01/monthly-commit-office-stamper-3-1-stabilizing-the-surface.html)
- [Feedback Loops and the AsciiDoc Pivot](/2026/02/01/monthly-commit-feedback-loops-and-the-asciidoc-pivot.html)
- [Engine Refactoring — the Road to v3](/2025/11/01/monthly-commit-engine-refactoring-the-road-to-v3.html)
- [Expression Safety Patterns with SpEL](/2026/05/17/monthly-topic-expression-safety-patterns-with-spel.html)

### Current status

- **Shipped:** v3.3 — SVG support, smart tag attribute validation, hardened XML parser for XXE/DTD mitigation.
- **In progress:** imageio unification and vector format support (EMF, WMF, SVG).
- **Used in:** energy sector document automation in China, where strict schema compliance and security are non-negotiable.

---

## Other ongoing projects

- Docs‑as‑Code pipelines for diagrams — seeded from Resources.
  - Scope: standardize PlantUML/Mermaid/Graphviz flows via Kroki; ensure diagrams build in CI alongside docs.
  - Status: ongoing; looking to publish a minimal starter and a checklist.

- Site hygiene and authoring ergonomics — seeded from Resources
  - Scope: small fixes to navigation, structured data, and print styles; keep content and assets tidy.
  - Status: ongoing; incremental.

# Next ideas / backlog

- Anki inspired app for Chinese learners
  - Description: Partnering with a local enthusiast in China to develop a dedicated app for Chinese learners that integrates and streamlines the learning process. (Replacing the previous idea of sharing a static HSK deck).
  - Output: Functional app and write-up on the development journey.

- Mock screenshot generator for Office apps (Word/PowerPoint)
  - Description: generate images that mimic editor chrome, and a sample document layout from a simple text input.
  - Status: **Prototype phase**. Using JavaFX as the graphical engine and the Office-stamper AsciiDoc module to compile formatted text to a JavaFX Scene. Rendering is functional but still needs refinement for clean, usable outputs.

- Link checker CI for this site — seeded from Resources
  - Description: lightweight GitHub Action to validate internal and external links on PRs.
  - Output: `ruby/setup-ruby` + `htmlproofer` pipeline with a short allowlist for known false positives.

- Diagram‑as‑Code cookbook — seeded from Resources
  - Description: practical snippets for PlantUML, Mermaid, and Graphviz (themes, layout tricks, and export recipes) with copy‑paste ready examples.
  - Output: post series, or a dedicated repo linked from the blog.

- Presentations‑as‑Code starter
  - Description: a thin starter showing Reveal.js or Marp with syntax‑highlighting presets and CI export to PDF.
  - Output: repo and short guide; link from the blog's Resources.

## How I prioritize

I pick tasks that:

- unblock current users or reduce maintenance toil,
- can be shipped in small, verifiable increments,
- produce reusable checklists, scripts, or examples others can adopt.

If you depend on any of these, tell me — real users trump curiosity.
