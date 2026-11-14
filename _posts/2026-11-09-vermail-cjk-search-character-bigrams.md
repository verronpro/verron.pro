---
layout: article
title: "Vermail: CJK Search with Character Bigrams"
date: 2026-11-09
categories: [ vermail ]
tags: [ vermail, search, sqlite, fts, cjk, java ]
author: Joseph
description: >
  Full-text search assumes words, but Chinese has no spaces. I measured four tokenisation strategies
  against graded truth; character bigrams won.
toc: true
---

Full-text search assumes words. Chinese, Japanese and Thai don't separate them.
The default SQLite tokeniser, `unicode61`, splits on word boundaries, and a
run of unspaced Chinese has none. A Chinese message tokenises into one enormous
term, and recall collapses to 35%.

The easy answer is a word segmenter. I measured four strategies instead of
picking one.

Twenty thousand synthetic messages, four strategies, scored against graded truth:

| strategy | index MiB | build s | msgs/s | recall | precision | median ms |
|---|---|---|---|---|---|---|
| unicode61 (baseline) | 26.6 | 2.2 | 9,285 | 35.0% | 100% | 0.08 |
| trigram | 52.6 | 6.0 | 3,313 | 35.7% | 100% | 0.03 |
| split (unicode61 + trigram) | 78.1 | 7.7 | 2,595 | 50.0% | 100% | 0.04 |
| bigrams | 39.7 | 3.4 | 5,886 | 100% | 100% | 0.09 |

Character bigrams, every overlapping two-character pair, reach full recall at
half the index size of trigrams and build twice as fast. The strategy is simple:

```java
// CjkTokens — index every overlapping 2-char pair of an unspaced run,
// keep space-delimited text as ordinary words, expand queries the same way.
```

Korean is excluded on purpose: it's written in visible syllables, so the
ordinary tokeniser already handles it.

Then the ranking. SQLite FTS returns rows in `rowid` order unless you ask for
`bm25`. Measured as NDCG@10:

| strategy | bm25 | rowid |
|---|---|---|
| bigrams | 0.870 | 0.535 |

Ranked beats unordered by a wide margin, and every candidate is verified against
the stored envelope text before it's shown.

The shipped store stays linear: 100,000 messages is 40.9 MiB, built at about
10,000 messages per second, with query times from single digits to around 30 ms.
The numbers are recorded in the ADR, not retrofitted to it.
