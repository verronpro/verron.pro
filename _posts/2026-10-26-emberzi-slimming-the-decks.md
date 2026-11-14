---
layout: article
title: "Ember字: Slimming the Decks"
date: 2026-10-26
categories: [ emberzi ]
tags: [ emberzi, content, srs, performance ]
author: Joseph
description: >
  ADR-0085 slims the decks: grammar points are taught by cards, not notes, and dead entries come
  out.
---

Decks had accumulated weight: grammar points carried notes as well as cards, and
some curated entries no longer pulled their weight.

ADR-0085 slims them. Grammar is taught by cards only, so the grammar packages
carry no notes. The deck headers that showed review-card counts were reworked to
match, and a batch of curated words was dropped and the decks regenerated.

The goal was mostly pruning and startup time. Download size mattered less. Every
entry a deck carries has to be resolved at startup and projected into the review
queue, so a note that teaches nothing is dead weight the learner loads on every
cold start. Prune it, and the launch gets faster and the queue gets cleaner.
