---
layout: article
title: "How-To: Diagnosing DOCX Templates with the CLI Tooling"
date: 2026-06-15
categories: [ office-stamper, tutorial ]
tags: [ cli, troubleshooting, java, diagnostics, dry-run ]
author: Joseph
description: >
  Stop guessing why your template is failing. The office-stamper CLI ships a
  diagnostic mode, a dry-run validator, and a traceability report — here is how
  to use all three to find the root cause fast.
toc: true
---

You have a DOCX template. You run the stamper. You get either a blank output,
a cryptic stack trace, or — worst of all — a silently wrong document.

The office-stamper CLI has three tools built specifically for this situation.
This post shows you how to use them, with real command examples, and the source
code behind each one.

---

## The Three Diagnostic Tools

<table>
    <tr>
        <th>Tool</th>
        <th>What it does</th>
        <th>When to use it </th>
    </tr>
    <tr>
        <td>`--dry-run`</td>
        <td>Validates template + data without writing output</td>
        <td>Template fails to stamp; you want to know why</td>
    </tr>
    <tr>
        <td>`--report`</td>
        <td>Writes a JSON run report with every placeholder resolution</td>
        <td>Output is wrong; you want to trace what resolved to what</td>
    </tr>
    <tr>
        <td>`--template diagnostic`</td>
        <td>Dumps JVM properties, env vars, and user preferences</td>
        <td>Stamper behaves differently on two machines</td>
    </tr>
</table>

---

## Tool 1 — Dry Run: Validate Without Producing Output

The `--dry-run` flag runs the full stamping pipeline but replaces the output
writer with an exception-throwing resolver. Any placeholder that cannot be
resolved causes an immediate, descriptive failure instead of a silent blank.

```bash
office-stamper-cli \
  --template contract-template.docx \
  --data context.json \
  --dry-run
```

**What you get on success:**

```
[INFO] Validation successful (dry-run)
```

**What you get on failure:**

```
[ERROR] Unresolved placeholder: ${client.signatureDate}
        at paragraph 12, run 3
        Expression: client.signatureDate
        Context keys available: [client.name, client.address, client.vatNumber]
```

The error tells you exactly which placeholder failed, where in the document it
lives, and what keys *were* available in the context — so you can see
immediately whether the problem is a typo in the template or a missing field in
your data.

### How It Works

In `Main.java`, the dry-run mode is wired through picocli:

```java
@Option(names = "--dry-run",
        description = "Validate template and data without producing output")
boolean dryRun;
```

When `dryRun` is `true`, the stamper is configured with an exception-throwing
`IExceptionResolver` that fails loudly on any unresolved expression, rather than
the default resolver that leaves the placeholder text in place. This turns
silent failures into actionable errors.

---

## Tool 2 — Traceability Report: Trace Every Resolution

The `--report` flag writes a JSON file after each run listing every placeholder,
the expression that was evaluated, and the value it resolved to.

```bash
office-stamper-cli \
  --template invoice-template.docx \
  --data invoice-data.json \
  --output invoice-output.docx \
  --report run-report.json
```

The report structure:

```json
{
  "template": "invoice-template.docx",
  "data": "invoice-data.json",
  "timestamp": "2026-06-22T09:14:33",
  "resolutions": [
    {
      "expression": "invoice.number",
      "resolved": "INV-2026-0042",
      "paragraph": 3,
      "run": 1
    },
    {
      "expression": "invoice.total",
      "resolved": "4 200,00 €",
      "paragraph": 18,
      "run": 2
    }
  ]
}
```

This is invaluable when the output *looks* wrong but no exception was thrown.
You can diff two report files to see exactly what value changed between runs.

### Viewing the Report

The CLI ships a `report-view` subcommand that renders the JSON as an HTML table:

```bash
office-stamper-cli report-view --input run-report.json --output run-report.html
```

Open `run-report.html` in a browser, and you get a searchable, sortable table
of every placeholder resolution in the document.

---

## Tool 3 — System Diagnostic: When It Works on Your Machine

The diagnostic tool collects the full runtime context — JVM system
properties, environment variables, and Java user preferences — and stamps them
into a pre-packaged `Diagnostic.docx` template:

```bash
office-stamper-cli --template diagnostic --output my-diagnostic.docx
```

The generated DOCX contains three sections:

1. **Report metadata** — date and username.
2. **JVM properties** — all `System.getProperties()` entries, sorted
   alphabetically.
3. **Environment variables** — all `System.getenv()` entries, sorted
   alphabetically.

Here is the core of `Diagnostic.java`:

```java
static Object context() {
    var map = new TreeMap<String, Object>();
    map.put("reportDate", LocalDate.now());
    map.put("reportUser", System.getenv("USERNAME"));
    var env = System.getenv();
    map.put("environment", env.entrySet());
    var properties = System.getProperties();
    var propertyNames = properties.stringPropertyNames();
    map.put("properties", propertyNames.stream()
                                       .collect(toMap(name -> name,
                                               properties::get))
                                       .entrySet());
    var userPreferences = extractUserPreferences();
    map.put("preferences", userPreferences.entrySet());
    return map;
}
```

The context is then stamped into the bundled template using the same
`office-stamper` engine — the diagnostic tool eats its own cooking.

**When to use it:** send the generated DOCX to a colleague or open a GitHub
issue. It contains everything needed to reproduce an environment-specific
failure without sharing credentials or sensitive config.

---

## Putting It Together: A Debugging Workflow

Here is the sequence I follow when a template fails in production:

**Step 1 — Reproduce with dry run:**

```bash
office-stamper-cli --template broken.docx --data prod-data.json --dry-run
```

If this fails, the error message tells you what placeholder is the culprit.
Fix the template or the data, re-run, repeat until dry run passes.

**Step 2 — Run with report:**

```bash
office-stamper-cli --template broken.docx --data prod-data.json \
  --output fixed.docx --report trace.json
```

Open `fixed.docx`. If it still looks wrong, open `trace.json` and search for
the suspicious placeholder. Compare the resolved value against what you
expected.

**Step 3 — If it works locally but not in CI:**

```bash
# On the failing machine:
office-stamper-cli --template diagnostic --output ci-diagnostic.docx
# On your local machine:
office-stamper-cli --template diagnostic --output local-diagnostic.docx
```

Diff the two DOCX files (or the underlying XML) to find the environment
difference. Common culprits: different `java.version`, missing `JAVA_HOME`,
locale differences in `user.language` / `user.country`.

---

## Watch Mode: Live Feedback During Template Development

For iterative template development, the `--watch` flag monitors the template
and data files for changes and re-stamps automatically:

```bash
office-stamper-cli \
  --template draft-template.docx \
  --data sample-data.json \
  --output preview.docx \
  --watch
```

Every time you save the template in Word, the CLI re-runs the stamp and
overwrites `preview.docx`. Open `preview.docx` in a second Word window and you
have a near-live preview loop without leaving your editor.

---

## Summary

The office-stamper CLI is not just a stamping tool — it is a debugging toolkit.

- Use `--dry-run` to catch unresolved placeholders before they reach production.
- Use `--report` to trace every resolution when the output is wrong but no
  exception fires.
- Use `diagnostic` to capture the full runtime environment for reproducible bug
  reports.
- Use `--watch` to iterate on templates without a manual re-run cycle.

The goal is to make template failures *loud and specific* rather than *silent
and mysterious*.
