# Alternative Output Files — Structuring Guide

The default output set is People, Organization, Systems, and
Opportunities, with templates in this folder. If the user requests an
additional output file (or replaces one of the defaults), follow this
guide to keep the new file consistent with the rest of the set.

## When an Alternative Output Makes Sense

Add a new file when the source material clearly contains a coherent
body of facts that doesn't fit cleanly into the four defaults. Common
candidates:

- **Processes.md** — repeated workflows, hand-offs, or operational
  procedures referenced often enough to warrant their own home.
- **Glossary.md** — domain-specific terms, acronyms, or product names
  whose meanings matter and recur.
- **Risks.md** — risks, compliance concerns, or known liabilities that
  cut across systems and people.
- **Decisions.md** — a log of decisions referenced in source (who
  decided, when, on what basis).
- **Timeline.md** — milestones, contract expirations, planned launches.
- **Metrics.md** — KPIs, baseline figures, targets pulled from source.
- **Customers.md / Segments.md** — when the project is customer-facing
  and the source has rich customer segmentation.

Do NOT add a file just because a topic was mentioned. Add one only
when:
1. The topic has enough material to fill at least a small table or two.
2. The material is awkward to host in one of the default files.
3. The user will plausibly come back to this file as a reference.

## Required Structural Elements

Every alternative output file must include, in this order:

1. **Title** — `# {File Topic} — {Project Name}`
2. **Intro paragraph** — one short paragraph stating what's in the
   file, with the standard `"unknown" indicates the information wasn't
   stated in source` note.
3. **Open Questions** *(conditional)* — include if the file has
   uncertainty. Use sub-headings if the list is long.
4. **Validation Recommended** *(conditional)* — table with columns
   `| Item | Field(s) to Validate | Why |`. Include if the file has
   inferences or single-source claims.
5. **Body** — one or more tables and/or narrative sections, grouped
   by a meaningful axis (theme, category, lifecycle stage).
6. **Conventions** — short closing section listing the conventions
   specific to this file (mirrors the templates).

## Choosing a Grouping Axis

Match the grouping axis to the file's content. Pick one primary axis:

| File Type | Typical Grouping Axis |
|---|---|
| Processes | Lifecycle stage or business function |
| Glossary | Alphabetical, OR by domain area if it's large |
| Risks | Risk category (technical, legal, operational, financial) |
| Decisions | Chronological, OR by decision area |
| Timeline | Chronological |
| Metrics | Metric category (acquisition, retention, ops, financial) |
| Customers | Segment, OR persona |

Avoid mixing two axes in one file — pick the primary and use Notes
columns for secondary attributes.

## Required Columns Pattern

When using tables, every row should answer: *what is this, what do we
know about it, what's the source confidence?* At minimum:

- **Name / Identifier** — the thing being recorded.
- **Description / Purpose** — one short phrase.
- **Owner or Source attribution** — who owns it OR who in source
  mentioned it.
- **Status / State / Stage** — if the entity has a lifecycle.
- **Notes** — for source quotes, ambiguity flags, cross-references.

Add columns specific to the file type (e.g., Risk Severity, Decision
Date, Metric Baseline → Target), but keep the column count manageable
(≤ 7).

## Cross-Linking

When an alternative file references entities documented in the
defaults, link to them rather than restating:

- People → link to `People.md`
- Systems → link to `Systems.md`
- Departments / teams → link to `Organization.md`
- Opportunities → link to `Opportunities.md`

This keeps each file the single source of truth for its entity type
and avoids divergence as files are refined.

## Updating `_progress.md`

When adding an alternative output file:

1. Add it to the `## Files` checklist in `_progress.md`.
2. Note in the initial check-in transcript / summary why it was added,
   so a future resume session understands the deviation from defaults.

## Anti-patterns

- **Creating a file with only 1–2 rows.** Merge into Notes columns of
  an existing file instead.
- **Restating entities from the default files.** Link, don't duplicate.
- **Skipping the Open Questions / Validation Recommended sections** in
  alternative files. The uncertainty discipline applies to every file
  in the set, not just the defaults.
- **Inventing new structural patterns.** When in doubt, mirror the
  closest default template's structure.
