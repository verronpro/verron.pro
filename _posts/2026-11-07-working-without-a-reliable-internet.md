---
layout: article
title: "Working Without a Reliable Internet"
date: 2026-11-07
categories: [ governance ]
tags: [ china, network, portability, solo-maintainer, resilience ]
author: Joseph
description: >
  The VPNs that paper over the gap between China and Western services keep getting harder to use.
  That constraint has quietly changed how I build.
toc: true
---

A few years ago I wrote about the "No Network" rule: a build that requires a
steady connection is a broken build, because where I live the connection is
never guaranteed. I framed it as a preference back then. It's since become a
hard requirement.

The tools that paper over the gap between China and Western services, the VPNs,
keep getting harder to use. Servers vanish, protocols get throttled, and the
thing that worked last month quietly stops working this month.

Concretely: Google services don't work, most AI services don't work, and HTTPS
to GitHub is blocked or throttled at best. It cuts both ways. Even with a VPN
up, I can't reach the 163.com mail API or the chinesetest.com corpus from the
other side.

I won't pretend this is anything other than what it is: friction, imposed from
outside, on anyone doing ordinary remote work. But there's a difference between
a constraint you can change and one you can only design around. This one is the
second kind.

What it forces:

- Network-independent builds. Every dependency resolvable offline, every test
  suite runnable on a plane.
- Local-first tooling. The things I rely on daily are the things that work
  without a hop to a Western service.
- Commit, then sync. Write locally, commit locally, and treat the remote sync as
  a background task rather than a precondition for work.

None of this was meant to be good engineering, it just turns out that way. A
build that works offline in a Beijing coffee shop works the same in a clean CI
container. A project that doesn't depend on a particular VPN staying up is
easier for everyone else to build.

I'd rather not have the constraint. But it's there, so I build around it, and
the result is more portable software.
