---
layout: article
title: "Secure by Default: The CISO's Guide to Safe Templating"
date: 2026-06-12
categories: [ security ]
tags: [ ciso, security, spel, office-stamper ]
author: Joseph
description: A look at why office-stamper's "Restricted" mode is the industry standard for secure document generation.
toc: true
---

As a CISO, I've seen too many systems where "extensibility" is just a euphemism for "security vulnerability." When it comes to document templates, letting users execute arbitrary code via expressions is a recipe for disaster.

### The Problem with Permissive Templating
Modern templating engines often use expression languages like SpEL (Spring Expression Language). If left in "Permissive" mode, an attacker can use these expressions to access system properties, run shell commands, or perform XXE attacks via embedded XML formats like SVG.

### The "Restricted" Baseline
In `office-stamper`, we've made `SecurityMode.RESTRICTED` the mandatory default for both SpEL and SVG. This means:
1. **No T() Type Access**: You can't reach into the JVM's classpath.
2. **No Constructor Access**: You can't instantiate new objects.
3. **Hardened SVG Parser**: DTDs and external entities are blocked.

### Governance in Practice
I recommend a "Governance-as-Code" approach: only allow `PERMISSIVE` mode for templates that have been cryptographically signed or audited by a security team.

**Questions for the next round:**
- Joseph, should we include a 'Security Checklist' for developers embedding office-stamper?
- How much do you want to lean into the 'Governance-as-Code' terminology?

---
### June 12th 2026 – Security Deep Dive
- **Policy**: Restricted mode defaults.
- **Threat Model**: Expression injection and XXE mitigation.
