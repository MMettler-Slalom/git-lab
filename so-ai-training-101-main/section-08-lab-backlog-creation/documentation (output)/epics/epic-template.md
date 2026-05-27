---
title: "<fill me>"
summary: "<fill me>" # 2-3 sentence human-readable summary
owner: "<fill me>" # Primary owner or team
priority: "<fill me>" # e.g., P0 / P1 / P2
phase: "<fill me>" # e.g., Phase 1 (Pilot)
personas:
  - "<fill me>"
okrs:
  objective: "<fill me>" # Short objective statement
  key_results:
    - description: "<fill me>"
      target: "<fill me>" # numeric or qualitative target
      timeframe: "<fill me>" # e.g., "12 weeks"
business_value: "<fill me>" # One-line description of business value
success_metrics:
  - "<fill me>" # cite PRD source
regulatory_requirements:
  - "<fill me>" # cite PRD source
security_considerations:
  - "<fill me>" # cite PRD source
dependencies:
  - "<fill me>" # external systems, docs, or teams
estimated_effort: "<fill me>" # e.g., 3-5 sprints
monitoring_metrics:
  - "<fill me>" # e.g., accuracy %, response time p90
acceptance_criteria:
  - "<fill me>"
out_of_scope:
  - "<fill me>"
stakeholders:
  - "<fill me>"
links:
  - "context (ingestion)/prd.md"
---

> **Author reminder:** Cite the source PRD (`context (ingestion)/prd.md`) for every metric, target, regulatory requirement, and constraint referenced below. Use inline references like `(PRD §<section>)` so reviewers can trace each item to the originating requirement.

## Summary

<fill me — 2-3 sentences describing the epic's intent, primary persona, and expected outcome.>

## OKRs

**Objective:** <fill me — single-sentence objective tied to PRD business value.>

**Key Results** (3-5 measurable KRs):

- KR 1 — Description: "<fill me>" | Target: "<fill me>" | Timeframe: "<fill me>" | Source: "(PRD §<fill me>)"
- KR 2 — Description: "<fill me>" | Target: "<fill me>" | Timeframe: "<fill me>" | Source: "(PRD §<fill me>)"
- KR 3 — Description: "<fill me>" | Target: "<fill me>" | Timeframe: "<fill me>" | Source: "(PRD §<fill me>)"
- KR 4 — Description: "<fill me>" | Target: "<fill me>" | Timeframe: "<fill me>" | Source: "(PRD §<fill me>)"
- KR 5 — Description: "<fill me>" | Target: "<fill me>" | Timeframe: "<fill me>" | Source: "(PRD §<fill me>)"

## Objective and Business Value

<fill me — describe how the epic advances PRD outcomes (e.g., pilot readiness, compliance, adoption). Cite PRD sections.>

## Personas Impacted

- Primary: <fill me — persona name and main benefit.>
- Secondary: <fill me — persona name and main benefit.>

## Acceptance Criteria

- <fill me — atomic, testable criterion with performance bounds, citation requirements, or failure-mode behavior. Cite PRD source.>
- <fill me>
- <fill me>

## Validation / QA Plan

<fill me — describe unit/integration tests, sample query sets with expected citations, manual spot-checks, regulatory/compliance review steps, and sign-off owners.>

## Monitoring and Metrics

- <fill me — dashboard or signal (e.g., response time p90, accuracy %, hallucination rate, escalation rate). Include aggregation window and alert threshold. Cite PRD source.>
- <fill me>

## Out of Scope

- <fill me — explicit exclusion (e.g., no PHI processing, no clinical advice, no replacement for human triage).>
- <fill me>

## Dependencies

- <fill me — upstream systems, teams, documents, or sign-offs required.>
- <fill me>

## Stakeholders / Reviewers

- Owner: <fill me>
- Product: <fill me>
- Engineering: <fill me>
- Compliance / Regulatory: <fill me>
- QA: <fill me>
- Other reviewers: <fill me>

## Notes and Links

- Source PRD: [context (ingestion)/prd.md](../../context%20(ingestion)/prd.md)
- Architecture diagrams: <fill me>
- Related epics / stories: <fill me>
- Additional references: <fill me>

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Every numeric target, regulatory requirement, and security control must cite the source PRD section it derives from.
- Keep the YAML frontmatter and narrative sections in sync — planning tools read the frontmatter; humans read the body.
