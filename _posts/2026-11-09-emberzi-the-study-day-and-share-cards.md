---
layout: article
title: "Ember字: the Study Day and Share Cards"
date: 2026-11-09
categories: [ emberzi ]
tags: [ emberzi, srs, timezone, share ]
author: Joseph
description: >
  Defining when a study day starts, and adding outbound share cards.
---

Two unrelated things landed together.

The first is the day model. A spaced-repetition app has to decide when "today"
is, and midnight isn't always the right answer. ADR-0018 pins the study day to
04:00, so a learner who reviews at 01:30 is still on the previous day's
schedule, with a grace window for travel and a clamp so a clock change can't
push a streak backwards.

The second is share cards: three outbound share cards so a learner can tell
someone what they're studying. Small, but it's the kind of feature that has to
render correctly on device, and the day-model work had already forced the clock
handling to be honest, which the share feature inherited for free.
