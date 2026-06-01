---
layout: page
title: Projects
permalink: /projects.html
description: A living list of ongoing work and projects I’m actively building — from Office automation to document testing, vector rendering, and Maven-based publishing.
aside:
  toc: true
---

This page tracks current projects and initiatives I’m actively building, along
with a focused backlog of work in progress. Office-stamper is the origin project:
what started as a Java template engine for Office documents is now expanding
into a broader ecosystem around document automation, testing, rendering,
publishing, and project presentation.

If you want to collaborate on any of these, or if a topic would help your team,
reach out via LinkedIn (see About) or GitHub issues.

## Office‑stamper

**A Java template engine for dynamic DOCX generation — secure by default, crafted with care.**

Office‑stamper lets you design a Word template in your favourite processor and stamp it at runtime with any Java object as context.
It uses Spring Expression Language (SpEL) for powerful, type-safe expressions and preserves all formatting from the original template.

**Why it exists:** generating `.docx` files programmatically and compliant to company graphic guidelines is harder than it looks.
Office‑stamper handles the edge cases — nested repeats, conditional sections, table rows, image insertion, and more — so you don't have to.

### Key links

|                       |                                                                                    |
|-----------------------|------------------------------------------------------------------------------------|
| 📦 **Source**         | [github.com/verronpro/office-stamper](https://github.com/verronpro/office-stamper) |
| 📖 **Docs**           | [office-stamper.verron.pro](https://office-stamper.verron.pro/engine)              |
| 🚀 **Latest release** | v3.3 — SVG support, smart tag validation, hardened SpEL security                   |
| 🪪 **License**        | MIT                                                                                |

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
void main(){
  var stamper = OfficeStampers.docxStamper();
  try (var template = Files.newInputStream(templatePath);
       var output  = Files.newOutputStream(outputPath)) {
      stamper.stamp(template, context, output);
  }
}
```

### Stories behind the code

- [The Expression Pivot — Harnessing Spring SpEL]({% post_url 2026-03-01-monthly-topic-the-expression-pivot-harnessing-spring-spel %})
- [Predicting the Unpredictable — the v3 Overhaul]({% post_url 2025-12-15-monthly-topic-predicting-the-unpredictable-v3-overhaul %})
- [Office-stamper 3.1 — Stabilizing the Surface]({% post_url 2026-01-01-monthly-commit-office-stamper-3-1-stabilizing-the-surface %})
- [Feedback Loops, and the AsciiDoc Pivot]({% post_url 2026-02-01-monthly-commit-feedback-loops-and-the-asciidoc-pivot %})
- [Engine Refactoring — the Road to v3]({% post_url 2025-11-01-monthly-commit-engine-refactoring-the-road-to-v3 %})
- TODO post 2026-05-17-monthly-topic-expression-safety-patterns-with-spel [Expression Safety Patterns with SpEL]()

### Current status

- **Shipped:** v3.3 — SVG support, smart tag attribute validation, hardened XML parser for XXE/DTD mitigation.
- **In progress:** ecosystem consolidation around vector-image support, textual document testing, and Maven-based publishing.
- **Used in:** energy sector document automation in China, where strict schema compliance and security are non-negotiable.

---

## Office-stamper ecosystem

Office-stamper remains the origin project, but the work around it has become
larger than a single template engine. The surrounding projects address recurring
needs that appear when document automation becomes a real product concern:
rendering fidelity, testability, documentation, and coherent presentation.

### Vector-image format support

Office documents often need diagrams, logos, and technical illustrations to
remain sharp and editable across export pipelines. This work focuses on ImageIO
plugins and related tooling for vector-image formats, with the goal of improving
support for formats commonly encountered in Office automation workflows.

The ambition is to make vector assets easier to load, test, convert, and embed
when producing Word or PowerPoint documents programmatically.

### Textual Word-document representation

Testing generated Word documents is difficult when the only artifact is a binary
`.docx` file. The AsciiDoc-oriented tooling explores a more reviewable approach:
representing relevant document structures in a textual form so they can be
tested, compared, documented, and discussed like source code.

This supports the broader Office-stamper goal: make document generation not only
powerful, but observable and maintainable.

### Maven-based visual identity

The Maven skin work helps give related Maven-generated sites a consistent visual
identity. It supports the product side of the ecosystem: documentation should not
only exist, it should feel coherent across projects.

The goal is to make project sites easier to recognize, navigate, and maintain,
while keeping the publishing workflow close to standard Maven practices.

---

## Other ongoing projects

- Le cloud familial — https://cloud.verron.pro/
- L'espace de Pascal — https://pascal.verron.pro/
- Les recettes d'Yvette — https://yvette.verron.pro/
- use Documentero as inspiration and office-stamper as technical base for my own word processing SaaS
- Isabelle Muñoz, Ennoblisseur textile à l'habit en roses — https://habit-en-roses.fr/
- Hugues Malbreil, Sculpteur — https://malbreil.fr/
- Docs‑as‑Code pipelines for diagrams

# Next ideas / backlog

- Anki inspired app for Chinese learners
  - Description: Partnering with a local enthusiast in China to develop a dedicated app for Chinese learners that integrates and streamlines the learning process. (Replacing the previous idea of sharing a static HSK deck).
  - Output: Functional app and write-up on the development journey.

- Mock screenshot generator for Office apps (Word/PowerPoint)
  - Description: generate images that mimic editor chrome, and a sample document layout from a simple text input.
  - Status: **Prototype phase**. Using JavaFX as the graphical engine and the Office-stamper AsciiDoc module to compile formatted text to a JavaFX Scene. Rendering is functional but still needs refinement for clean, usable outputs.

- Le coin des fantasmes — http://fantas.me
- Best emails — http://isda.best and http://isze.best
- Diagram‑as‑Code cookbook — seeded from Practices & Tools
  - Description: practical snippets for PlantUML, Mermaid, and Graphviz (themes, layout tricks, and export recipes) with copy‑paste ready examples.
  - Output: post series, or a dedicated repo linked from the blog.

- Presentations‑as‑Code starter
  - Description: a thin starter showing Reveal.js or Marp with syntax‑highlighting presets and CI export to PDF.
  - Output: repo and short guide; link from the blog's Practices & Tools.

## How I prioritize

I pick tasks that:

- unblock current users or reduce maintenance toil,
- can be shipped in small, verifiable increments,
- produce reusable checklists, scripts, or examples others can adopt.

If you depend on any of these, tell me — real users trump curiosity.
