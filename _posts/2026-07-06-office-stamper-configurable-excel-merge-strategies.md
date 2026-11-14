---
layout: article
title: "office-stamper: Configurable Excel Merge Strategies"
date: 2026-07-06
categories: [ office-stamper ]
tags: [ office-stamper, java, cli, excel, tooling ]
author: Joseph
description: >
  When a template's Excel data source has more than one sheet, "merge" is not one operation. This
  commit makes MAP vs JOIN an explicit CLI choice.
---

Excel as a data source was already in office-stamper ([I wrote about it last
year]({% post_url 2025-03-01-monthly-commit-excel-as-data-source %})). What this
commit adds is that "merge the Excel data into the context" is not one
operation; it's a choice.

When your workbook has several sheets, you can treat them two ways:

- **MAP** — each sheet becomes a named entry in the context, keyed by sheet name.
  This is the default.
- **JOIN** — the sheets are related rows sharing a key, joined into one table
  before stamping.

`ExcelStrategy` turns that choice into a CLI flag group:

```text
officestamper -t template.docx -d data.xlsx \
    --excel-merge-strategy JOIN --excel-join-key ID
```

`--excel-join-key` defaults to `ID` and only matters for `JOIN`.

The previous behaviour assumed MAP, so anyone whose workbook looked like a
relational join had to pre-join it by hand. Making the strategy explicit moves
that knowledge into the tool.
