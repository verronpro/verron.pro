---
layout: article
title: "Ember字: Ordering the Review Queue by Note Type"
date: 2026-08-17
categories: [ emberzi ]
tags: [ emberzi, srs, review, spaced-repetition ]
author: Joseph
description: >
  The review queue used to interleave everything. ADR-0022 orders it by note type, in stages.
---

The review queue mixed every kind of card together. ADR-0022 orders it by note
type: the bucket derivation, then the drain, then the re-insertion of an `again`
card, then the persistence of a pending card across launches.

It landed in stages, one small piece per commit, each with its own test. The
staging matters because the queue is the part of a spaced-repetition app that a
learner actually feels. A wrong interleave is a subtle daily annoyance, not a
crash.

The `again` re-insertion was the one that took thought: a card you fail should
come back in the same sitting, but not immediately, and not at the expense of
the cards you haven't seen yet.
