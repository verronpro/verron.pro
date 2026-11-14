---
layout: article
title: "Ember字: Scoping Study to the Active Level"
date: 2026-07-27
categories: [ emberzi ]
tags: [ emberzi, srs, product, study-session ]
author: Joseph
description: >
  Making the active HSK level a hard wall for study sessions, so the deck picker and the session
  draw from one level instead of drifting.
---

The learner picks a level, but for a while the study session didn't take that
pick seriously. You'd declare yourself at HSK 3 and the review kept handing you
words from the lowest level, the ones you hadn't revised yet. The picker and the
session could quietly draw from different pools. It felt like the app had
ignored your choice.

This change makes the active HSK level a hard wall. The deck picker is
data-driven off the level list instead of a hand-maintained window, and the
session scopes to the level the learner actually chose.

It's the kind of fix that looks trivial on the surface and isn't. The word
"level" appears in a dozen places: the picker, the session, the review queue,
the statistics. Until the scoping is a single source of truth, each one can
quietly disagree with the others, and the learner gets a session that doesn't
match the deck they picked.
