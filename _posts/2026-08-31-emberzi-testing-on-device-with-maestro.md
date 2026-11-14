---
layout: article
title: "Ember字: Testing on the Device with Maestro"
date: 2026-08-31
categories: [ emberzi ]
tags: [ emberzi, testing, android, maestro, bdd ]
author: Joseph
description: >
  Adding an on-device Android test layer driven by Maestro, so the behaviour specs run against a
  real device instead of a mock.
---

The behaviour specs ran headless, against mocks. That catches logic errors and
misses everything that only shows up on a real device: the keyboard, the soft
input, the rendering, the navigation.

This adds an on-device Android layer driven by Maestro. The same behaviour specs
now run against a handset, with glue that drives the app the way a person does.
The pragmatic reason is speed: virtualisation without a dedicated processing
unit is slow, and a real device runs faster and gives a more compelling preview
of the UI than any virtual screen.

Two things took longer than expected. The first is text input: a Chinese pinyin
keyboard holds injected Latin keystrokes in its composition buffer and never
commits them, so an input that works headless silently does nothing on device.
The second is that text selectors in Maestro are full-match regular expressions,
so "Continue" never matches "Continue as Mara".

Both are the kind of thing you only learn by running against the real thing,
which is the point of the layer.
