---
layout: article
title: "Ember字: the Startup Snapshot"
date: 2026-10-12
categories: [ emberzi ]
tags: [ emberzi, performance, react-native, caching ]
author: Joseph
description: >
  Startup was 7.6 seconds, and a content snapshot that was supposed to fix it silently never
  landed. The cause took several days to find, and it was my own sideloaded deck.
---

A cold launch took 7.6 seconds: sources, dictionary, projection, then first
paint. The fix was meant to be a content snapshot written on first launch and
read on the next, which should have cut that to about a second and a half.

It didn't. Every launch reported a cache miss, and for a whole release nobody
noticed, because the snapshot code caught and discarded every error. An absent
cache and an unreadable one looked identical.

The root cause took several days. The cache seemed to work, debug sessions
showed nothing, and the bug only appeared on my own device. Then it clicked: I
was the only person who had sideloaded every deck to try them, and one of them
sat flagged as non-compliant on a screen that wouldn't let me remove it. I
started on a small hygiene feature to let me delete a blocked deck, and realised
that stale package was poisoning the snapshot.

A stale sideloaded package produced a `rejected` read on every launch, and the
snapshot logic declined to write whenever the read recorded any failure. So no
cache was ever written, silently.

Two fixes. The failure now travels in the snapshot payload, so a hydrating
launch can say what it's missing. And only a failure that might still resolve
blocks the write: `unreadable` blocks, `rejected` and `corrupt` don't.

With the faulty package removed, the next launch hit the cache: 7.6 seconds
down to about 1.1, with the read at 299 ms and the decode at 323 ms. The lesson
isn't about caching; it's that a cache that can fail silently is worse than no
cache at all.
