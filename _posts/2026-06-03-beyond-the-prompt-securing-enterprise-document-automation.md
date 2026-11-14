---
layout: article
title: "Beyond the Prompt: Securing Enterprise Document Automation"
date: 2026-06-03
categories: [ security ]
tags: [ ai, security, ciso, governance, office-stamper ]
author: Joseph
description: >
  LLMs are great at writing text and bad at producing compliant documents. The pattern that works
  is AI for content, deterministic Java for structure and security.
toc: true
---

Can an LLM generate a perfect `.docx`? Not yet, and not in a way that satisfies a
CISO in a high-stakes sector like energy or finance. AI is good at synthesizing
text. The structure and compliance requirements of enterprise documents are
unforgiving.

## The compliance gap

Prompt an AI to "write a contract" and you get a wall of text. An enterprise
contract needs specific styles, metadata, and a structure that won't break when
opened in Word. More than that, it needs governance: someone has to vouch that
the document says what it should, and nothing else.

## Bridging the gap: AI plus deterministic stamping

The pattern I keep coming back to has two steps:

1. **AI synthesis** — the LLM produces structured data (JSON), not the final
   document.
2. **Deterministic stamping** — that JSON goes into `office-stamper` against a
   pre-validated, secure template.

The content is intelligent; the format and the security are guaranteed by code
you control. The LLM never touches the document structure, so there's nothing for
it to hallucinate into the wrong shape.

That separation is the whole point: let the model do what it's good at, and keep
the parts that must be deterministic out of its hands.
