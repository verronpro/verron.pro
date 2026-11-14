---
layout: article
title: "Diagrams as Code: Data, Sketches, and Prototypes"
date: 2026-06-21
categories: [ documentation-as-code ]
tags: [ plantuml, diagrams-as-code, json, yaml, regex, salt, mindmap, ux ]
author: Joseph
description: >
  Quick text-driven visualizations: JSON and YAML trees, regex state machines, Salt GUI mockups,
  and MindMaps for brainstorming.
toc: true
---

Not every diagram models architecture. Some of the most useful ones are quick
sketches: the shape of a data structure, a regex, a GUI mockup, or a
brainstorming tree. PlantUML covers these too, and they stay in plain text.

## JSON and YAML

PlantUML's [JSON](https://plantuml.com/fr/json) and
[YAML](https://plantuml.com/fr/yaml) support turns raw data into a readable
tree.

```plantuml
@startjson
{
  "project": "office-stamper",
  "version": "2.4.0",
  "features": ["docx", "xlsx", "pptx"],
  "security": {
    "sanitization": true,
    "allowed_macros": false
  }
}
@endjson
```

Because it's trivial to make software print PlantUML-format text, I add debug
endpoints that return JSON or YAML this way. Instead of parsing a thousand log
lines, a developer hits an endpoint and sees the current configuration as an
image.

## Regular expressions

PlantUML can
[visualize regular expressions](https://plantuml.com/fr/regex), turning a
cryptic string into a state machine.

```plantuml
@startregex
^([a-zA-Z0-9_\-\.]+)@([a-zA-Z0-9_\-\.]+)\.([a-zA-Z]{2,5})$
@endregex
```

From a security standpoint, visualizing schemas and validation logic means the
developer and the auditor see the same thing.

## Salt for GUI mockups

[Salt](https://plantuml.com/fr/salt) is PlantUML's wireframing language. It's
about function and flow, not pixel-perfect design.

```plantuml
@startsalt
{
  Login    | "MyUsername   "
  Password | "****         "
  [Cancel] | [  OK   ]
}
@endsalt
```

I use it with business analysts. When they describe a feature, I type a Salt
mockup instead of writing a spec. If they want the OK button on the left, I move
it in two seconds.

## MindMaps

When I start a new module, I map requirements and edge cases with a
[MindMap](https://plantuml.com/fr/mindmap-diagram).

```plantuml
@startmindmap
* Office Stamper
** Template Engine
*** Variables
*** Loops
*** Conditionals
** Image Processing
*** EMF
*** WMF
*** SVG
@endmindmap
```

The text form means the ideas can be copied straight into task descriptions.
