---
layout: article
title: "Ember字: Migrating to a Monorepo"
date: 2026-07-13
categories: [ emberzi ]
tags: [ emberzi, monorepo, pnpm, turborepo, typescript ]
author: Joseph
description: >
  Moving the app into a pnpm + Turborepo workspace, with the review engine and content pipeline
  split into packages instead of living inside the mobile app.
---

The app started as one Expo project. As it grew, review logic, content, and UI
all lived in the same tree, and the boundaries started to blur. In July I split
it into a pnpm + Turborepo workspace: `apps/` for the mobile app and the corpus
tooling, `packages/` for the UI components, design tokens, the spaced-repetition
core, and the content pipeline.

The point is dependency direction. The review engine (`srs-core`) doesn't import
the app, and the content pipeline doesn't import either. Once that's enforced, a
change to one package can't silently leak into another, and each package gets a
test suite it actually owns.

The cost is tooling. Metro has to resolve `@ember/*` imports out of `packages/`,
and pnpm on Windows has its own sharp edges with native dependencies. But the
alternative, one folder where everything touches everything, was already
starting to hurt more than the tooling does.
