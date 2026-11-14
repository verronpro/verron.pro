---
layout: article
title: "Ember字: Redesigning to Canvas v4"
date: 2026-07-20
categories: [ emberzi ]
tags: [ emberzi, react-native, design-system, ui ]
author: Joseph
description: >
  Restyling the app against a new design version, one screen at a time.
---

The app ran on a design version that had drifted from the design tool. This pass
re-synced the authority and rebuilt the screens against it, one at a time: the
Home deck picker, Settings, Words browse and detail, Statistics, the Reader
lookup sheet, the study all-caught-up screen, and the onboarding flow.

Doing it screen by screen matters. A visual redesign applied all at once breaks
everything at once. Rebuilding one screen at a time, with a snapshot test on
each, keeps the app working while it changes.

The recurring gotcha was less the design and more React Native's deprecated
`shadow*` props: each screen had a slightly different idea of what a card looked
like. That's the point of a design version, in the end. One answer instead of
six.
