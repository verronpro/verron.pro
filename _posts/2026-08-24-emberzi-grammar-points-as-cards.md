---
layout: article
title: "Ember字: Grammar Points as Cards"
date: 2026-08-24
categories: [ emberzi ]
tags: [ emberzi, grammar, srs, content ]
author: Joseph
description: >
  ADR-0024 turns grammar points from notes into cards, gated on viewing.
---

Grammar used to be taught by notes. ADR-0024 turns grammar points into cards,
which means they enter the same review queue as everything else instead of
sitting in a separate tab.

The stages built the data contract for highlight spans, rewrote the grammar
review, gated the review on having actually viewed the point, and added a
minimal intro screen. The highlight-span contract is the part that matters: the
card has to mark up which part of the sentence illustrates the grammar point,
and that markup has to survive the pipeline that produces the card.

Grammar is different from vocabulary. A word doesn't need much explanation, but
a grammar point does: it describes a sentence structure that doesn't exist in
the learner's own language. The card has to carry that explanation. Eventually
grammar should leave the card queue for dedicated activities — multiple choice,
fill-the-gap, understanding checks — but a scheduled card is enough to stop it
being read once and forgotten.
