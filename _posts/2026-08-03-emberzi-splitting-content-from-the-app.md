---
layout: article
title: "Ember字: Splitting Content from the App"
date: 2026-08-03
categories: [ emberzi ]
tags: [ emberzi, content, corpus, srs ]
author: Joseph
description: >
  Moving content out of the app bundle into packages that can ship separately, and adding an
  in-house gloss corpus as a fourth content source.
---

The app shipped with its content baked in. The main problem was licensing: the
content's licences were tangled up with the app's, so the corpus couldn't ship
or change on its own terms. Release cadence came a close second, because every
corpus edit also meant a full app release.

This work split content out: bundled packages, runtime delivery from a CDN, and
a consent-gated dictionary. On top of that, ADR-0012 added a fourth content
source, an in-house level-appropriate gloss corpus, authored by us, so a note
that has no dictionary gloss still shows a sensible default instead of nothing.

The runtime resolver falls back in a fixed order across the sources, and the
glosses union across the packages the learner has started. A word that isn't in
the installed deck still gets a gloss when one of the in-house sources has one.

The part that bit me: the resolver's fallback order is the whole feature. Get
one priority backwards and the learner silently sees a worse gloss.
