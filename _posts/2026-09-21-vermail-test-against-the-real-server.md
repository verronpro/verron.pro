---
layout: article
title: "Vermail: Test Against the Real Server"
date: 2026-09-21
categories: [ vermail ]
tags: [ vermail, imap, smtp, testing, java ]
author: Joseph
description: >
  Unit tests don't tell you a mailbox is reachable or that credentials work. For that you talk to a
  real server.
toc: true
---

Unit tests tell you the code does what you told it to. They don't tell you a
mailbox is reachable, that the credentials are accepted, or that the server
behaves the way its name implies. For that you need to talk to a real server.

The connection test is a port, a `ConnectionTester` with a connection outcome
model, so "does this account actually work?" is a first-class question rather
than a side effect of a sync.

The outcome is modelled, not thrown. A failed connection is a value with a cause,
so the settings screen can say why it failed instead of painting a red border and
shrugging.

The first client increment wired it to a real account: from the settings screen
you can test an account against a live IMAP/SMTP server before trusting it to
sync.

The same pass recorded the first real provider observations: IDLE confirmed off
one provider, labels confirmed on another. Those became ADR amendments, because
delivery topology is measured per provider, never inferred from its name.

For anything that speaks a network protocol, the earliest test worth writing is
the one against the real thing.
