---
layout: article
title: "Secure by Default: The CISO's Guide to Safe Templating"
date: 2026-06-12
categories: [ security ]
tags: [ ciso, security, spel, office-stamper ]
author: Joseph
description: >
  Permissive templating turns "extensibility" into a vulnerability. office-stamper's restricted
  mode is the secure default, and here's why.
toc: true
---

I've seen too many systems where "extensibility" is a euphemism for "security
vulnerability." When document templates let users run arbitrary expressions,
that's a disaster waiting to happen.

## The problem with permissive templating

Templating engines often use expression languages like SpEL. Left in permissive
mode, an expression can reach into the JVM's classpath, instantiate objects, or
pull off an XXE attack through embedded SVG.

## The restricted baseline

In `office-stamper`, `SecurityMode.RESTRICTED` is the default for both SpEL and
SVG. That means:

1. No `T()` type access — you can't reach into the classpath.
2. No constructor access — you can't instantiate new objects.
3. A hardened SVG parser — DTDs and external entities are blocked.

## Governance in practice

The rule I recommend is simple: only allow `PERMISSIVE` mode for templates that
have been cryptographically signed or audited by a security team. "Governance as
code" is just that rule made explicit in the build, instead of left to whoever
writes the template next.
