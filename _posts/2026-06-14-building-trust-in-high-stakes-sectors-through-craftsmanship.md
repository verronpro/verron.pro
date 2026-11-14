---
layout: article
title: "Building Trust in High-Stakes Sectors Through Craftsmanship"
date: 2026-06-14
categories: [ craftsmanship ]
tags: [ trust, security, java, office-stamper ]
author: Joseph
description: >
  Software quality is the foundation of trust in industries where an error has real-world
  consequences.
toc: true
---

In high-stakes industries, trust isn't built on promises. It's built on
verifiable evidence. Software should be held to the same standard.

## Verifiable quality

When I talk about craftsmanship, I mean the technical choices that make a system
resilient. For `office-stamper`:

- **Mutation testing (PIT)** — line coverage says which lines ran; mutation
  testing proves the tests actually catch bugs. It found code that, executed or
  not, had no effect on any test: either useless or untested, and I had cases of
  both. It also flagged an infinite loop that a particular condition could have
  triggered.
- **A strict API** — consolidating the surface in v3.1 and v3.2 reduced the room
  for misuse.
- **Continuous quality** — Qodana analysis on every commit keeps the bar from
  drifting.

## The real-world impact

When an automated system generates a compliance report for safety-critical
infrastructure, there's no room for error. Craftsmanship is what guarantees the
document says exactly what the data dictated, no more and no less.

That's the part a model can't give you. Correctness isn't a prompt; it's a
property of the system that produces the output.
