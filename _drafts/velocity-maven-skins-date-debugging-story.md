---
layout: post
title: "Velocity, Maven Skins, and the Date That Wasn’t: A Debugging Story"
date: 2026-06-01
categories: [maven, velocity, debugging]
tags: [maven-skin, velocity, date, ai, documentation]
author: Joseph
description: "How I debugged a missing date in a custom Maven skin, why AI and old forums gave wrong answers, and the three lessons I learned about Velocity templating."
---

You ask an AI to generate a custom Maven skin. It looks great – except the current date in the footer isn’t rendered. Instead of `2026`, you see `$date` or a broken formatting call. You search online: forums suggest `$date.format('yyyy')`, `$date.getYear() + 1900`, or adding a `site-tools.xml` with a `DateTool`. Nothing works.

This is the story of how I fixed it, and why the real problem isn’t Velocity – it is the outdated advice that still haunts search engines and AI assistants.

## The real issue

Maven's site renderer uses Apache Velocity, a templating engine that was popular before React, Vue, or even Thymeleaf existed. Today, most developers have never touched it. The official documentation is sparse, forum answers date to 2008, and AI models blindly repeat those patterns.

In my case, I wanted to display the current year in the footer of a Maven-generated site. Simple, right?

## What I learned (the hard way)

### 1. Check what object you actually have

After two hours of trying `$date.format('yyyy')`, I added a debug line:

```velocity
<!-- date class: ${date.getClass().getName()} -->
```

The output?  
`org.apache.velocity.tools.generic.ComparisonDateTool`

That's not a plain `java.util.Date` (where `getYear()` would need `+1900`), nor a `LocalDate`, nor a `DateTool` with a `format()` method. It is a `ComparisonDateTool` – a specific Velocity Tools class that provides comparison methods but **no** `format()`. No wonder `$date.format()` failed silently.

**Lesson:** Always introspect the object before copying code from the internet.

### 2. Don’t assume you can easily add external tools

Many answers tell you to add `velocity-tools` as a dependency and a `site-tools.xml` file. That *should* work – but in practice, configuring the classpath between the Maven Site Plugin and your custom skin is a black hole. The documentation is missing, the community has moved on, and I never figured out how to make it work reliably.

I'm sure there's a way, but after hours of trial and error, I gave up. And that's fine – because I didn't need `DateTool` at all.

**Lesson:** Sometimes the simplest solution is to work with what's already there, not fight the toolchain.

### 3. The subtlety of `${var}`: outside directives, not inside

This one almost broke me. The common advice is to use `${var}` inside directives to avoid ambiguity. In my case, it was the opposite:

- **Inside** a `#set` or `#if`, `$date` worked fine.
- **Outside** – in plain HTML or inside HTML comments – `$date` was sometimes left as literal text. Wrapping it with `${date}` forced the parser to recognize it as a variable.

Example:
```velocity
<!-- This comment will NOT parse $date -->
#set( $year = $date.getYear() )   <!-- Works without ${} -->
```

The safe rule that worked for me: **use `${date}` in static text and comments; use `$date` inside Velocity directives**.

**Lesson:** Velocity's parsing rules are inconsistent. Test both syntaxes in different contexts.

## The final working code (no extra dependencies)

After all this, the solution was embarrassingly simple:

```velocity
#set( $currentYear = $date.getYear() )
```

Then in your footer:

```velocity
Copyright &copy; 2026–${currentYear}
```

That's it. No `velocity-tools`, no `site-tools.xml`, no complex formatting.

## Why this is a broader problem

- **AI assistants** confidently repeat outdated patterns. When I asked for a Maven skin with a dynamic date, it gave me `$date.format('yyyy')` and a `site-tools.xml` – completely unnecessary and broken.
- **Old forum answers** still rank high on Google. Many suggest `$date.getYear() + 1900` (pre-Java 8 behavior) or complex tool configurations that no longer apply.
- **Velocity is not dead, but it is forgotten** – so everyone reinvents the wheel with bad advice.

## Takeaway

Before adding libraries or copy-pasting code, **inspect the actual object** with `$something.getClass().getName()`. In Maven skins, the built-in `$date` is a `ComparisonDateTool` – simple and enough for getting the year.

Sometimes the old-school templating engine isn’t the enemy; the outdated documentation and AI hallucinations are.

---

*If you're building a Maven skin, test every variable with a debug comment. And if an AI gives you a `site-tools.xml` for a simple date, ask it to show you the class first.*
