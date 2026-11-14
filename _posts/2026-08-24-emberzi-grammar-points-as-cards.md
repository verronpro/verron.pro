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

Teaching grammar by card rather than note means the learner reviews it like
vocabulary, on a schedule, instead of reading it once.
