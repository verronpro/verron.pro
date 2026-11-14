---
layout: article
title: "Vermail: Decisions Before Code"
date: 2026-09-07
categories: [ vermail ]
tags: [ vermail, architecture, adr, governance, java ]
author: Joseph
description: >
  Vermail started with architecture decision records and build gates, before the first feature.
  The risky choices were made on paper while they were still cheap.
toc: true
---

Most projects start with a feature and grow a decision trail afterwards. Vermail
started the other way round. The first commits weren't a mail client; they were
a set of architecture decision records, and the build gates that would keep
them honest.

The ADR index now runs from identity, how you know a message is the same
message, to delivery topology, IMAP IDLE as the floor with push as a
notification accelerator, to the local store.

This isn't documentation for its own sake. Certain choices are cheap on paper
and expensive in code. "Is the local store a rebuildable projection or a second
source of truth?" is a five-minute argument as a document and a multi-week
rewrite as an architecture.

The build stood up the Enforcer and ArchUnit gates before the feature code, so
the first line of real code already had something checking its boundaries.

For a solo project this matters more, not less. I have no one to argue with, so
the ADR is the argument written down, the one I can have with my future self.
When I come back to the codebase weeks later, the why is already there.
