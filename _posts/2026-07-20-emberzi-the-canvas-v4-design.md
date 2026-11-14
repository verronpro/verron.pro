---
layout: article
title: "Ember字: The Canvas v4 Design"
date: 2026-07-20
categories: [ emberzi ]
tags: [ emberzi, react-native, design-system, ui ]
author: Joseph
description: >
  Canvas v4 was the app's first shipped UI, iterated with AI tooling and rebuilt screen by
  screen. Efficient, but too flat.
---

Canvas v4 was the fourth design my partner produced, iterating back and forth
with his AI tooling. It became the app's first shipped UI. Rebuilding the
screens against it was a screen-by-screen job: the Home deck picker, Settings,
Words browse and detail, Statistics, the Reader lookup sheet, the study
all-caught-up screen, and the onboarding flow.

Doing it screen by screen matters. A visual redesign applied all at once breaks
everything at once. Rebuilding one screen at a time, with a snapshot test on
each, keeps the app working while it changes.

Canvas v4 was efficient, but too flat and impersonal. In October we moved to a
v2 that added what v4 lacked: a Wada palette, ink and paper surfaces, a subtle
grain, and card-reveal animations. It shipped as release 1.2.0.
