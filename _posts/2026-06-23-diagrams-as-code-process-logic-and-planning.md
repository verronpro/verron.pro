---
layout: article
title: "Diagrams as Code: Process, Logic, and Planning"
date: 2026-06-23
categories: [ documentation-as-code ]
tags: [ plantuml, diagrams-as-code, state-diagram, activity-diagram, gantt, wbs ]
author: Joseph
description: >
  State and activity diagrams for logic, Gantt and WBS for planning — process diagrams that stay in
  version control.
toc: true
---

Structure diagrams show what a system is made of. Process diagrams show what it
does, in what order, and when. These are the ones I use most when the logic gets
hard to hold in my head.

## State diagrams

[State diagrams](https://plantuml.com/fr/state-diagram) model life cycles.

```plantuml
@startuml
[*] --> Uploaded
Uploaded --> Validating
Validating --> Error : Invalid Schema
Validating --> Ready : Valid
Ready --> Processing
Processing --> Completed
@enduml
```

They're the common language with business analysts. We walk through "what
happens if validation fails" before any code is written.

## Activity diagrams

For business processes or algorithm flow, the
[activity diagram](https://plantuml.com/fr/activity-diagram-beta) has a cleaner
syntax.

```plantuml
@startuml
start
:Read Template;
if (Is Valid?) then (yes)
  :Apply Variables;
  :Generate Output;
else (no)
  :Log Error;
  stop
endif
stop
@enduml
```

I trace the happy path and the error paths live, and by the end of the session
the diagram is most of the implementation plan.

## Work breakdown structure

Before a timeline, a [WBS](https://plantuml.com/fr/wbs-diagram) breaks the work
down.

```plantuml
@startwbs
* ImageIO Support
** EMF Plugin
*** Reader implementation
*** SPI Registration
** WMF Plugin
*** Integration tests
** SVG Support
*** Kroki integration
@endwbs
```

## Gantt charts

Once the tasks exist, a [Gantt](https://plantuml.com/fr/gantt-diagram) maps them
to time.

```plantuml
@startgantt
[Core Engine Update] lasts 10 days
[EMF Reader implementation] lasts 5 days
[EMF Reader implementation] starts at [Core Engine Update]'s end
[SPI Registration] lasts 2 days
[SPI Registration] starts at [EMF Reader implementation]'s end
@endgantt
```

Seeing dependencies mapped in the same repo as the code makes them a shared
constraint, not a manager telling people to hurry.
