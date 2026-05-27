---
title: "<fill me>" # Short, descriptive story title
parent_epic: "<fill me>" # Path or ID of the parent epic (e.g., documentation (output)/epics/updated-epic-template.md)
summary: "<fill me>" # One-line summary of the story
owner: "<fill me>" # Assignee or team
priority: "<fill me>" # e.g., P0 / P1
sprint: "<fill me>" # Sprint name or number
story_points: "<fill me>" # e.g., 3, 5, 8
personas:
  - "<fill me>" # primary persona impacted
dependencies:
  - "<fill me>"
acceptance_criteria:
  - "<fill me>" # atomic, testable criteria (mirror Gherkin table below)
tasks:
  - "<fill me>" # implementation tasks (dev, test, docs)
links:
  - "context (ingestion)/prd.md"
  - "<fill me>" # parent epic, design docs, tickets
---

> **Author reminder:** Every story MUST link to its parent epic via `parent_epic` and cite the originating PRD section (e.g., `(PRD §<section>)`) when establishing acceptance criteria, NFRs, and telemetry. Stories without epic linkage and PRD citations should not be accepted into a sprint.

## User Story

As a **<persona>**, I can **<action>** so that **<benefit>**.

## Acceptance Criteria (Gherkin-style)

| # | Scenario | Given | When | Then | PRD Source |
|---|----------|-------|------|------|------------|
| 1 | <fill me> | <fill me — precondition> | <fill me — action> | <fill me — observable outcome with measurable threshold> | (PRD §<fill me>) |
| 2 | <fill me> | <fill me> | <fill me> | <fill me> | (PRD §<fill me>) |
| 3 | <fill me> | <fill me> | <fill me> | <fill me> | (PRD §<fill me>) |

## Non-Functional / Compliance Notes

- Performance: <fill me — e.g., p90 latency, throughput. Cite PRD source.>
- Security: <fill me — e.g., RBAC, encryption in transit/at rest. Cite PRD source.>
- Privacy / Data handling: <fill me — e.g., no PHI, redaction rules. Cite PRD source.>
- Regulatory: <fill me — e.g., FDA / ISO / HIPAA controls, audit retention. Cite PRD source.>
- Accessibility / UX: <fill me>

## Telemetry and Reporting

- Events emitted: <fill me — event name, payload fields, trigger.>
- Metrics tracked: <fill me — e.g., success rate, latency p90, escalation rate.>
- Dashboards / alerts: <fill me — location and threshold.>
- Audit logging: <fill me — fields captured, retention window. Cite PRD source.>

## Dependencies

- Upstream services: <fill me>
- Data sources / documents: <fill me>
- Teams / sign-offs: <fill me>
- Blocking stories or epics: <fill me>

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| <fill me> | <Low/Med/High> | <Low/Med/High> | <fill me> | <fill me> |
| <fill me> | <Low/Med/High> | <Low/Med/High> | <fill me> | <fill me> |

## Rollout / Validation Checklist

- [ ] Unit tests added and passing
- [ ] Integration tests cover acceptance criteria scenarios
- [ ] Manual QA spot-check against source documents completed
- [ ] Telemetry verified in staging dashboard
- [ ] Security / compliance review signed off
- [ ] Feature flag / rollout plan defined (<fill me>)
- [ ] Documentation updated (runbooks, user guides)
- [ ] Parent epic acceptance criteria still satisfied

## Source References

- Parent epic: [<fill me>](<fill me>)
- Source PRD: [context (ingestion)/prd.md](../../context%20(ingestion)/prd.md)
- PRD sections cited: <fill me — list of §sections used above>
- Design / architecture docs: <fill me>
- Tickets / external references: <fill me>

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Confirm `parent_epic` points to a real epic file before opening the story for review.
- Each acceptance criterion, NFR, and telemetry metric must reference its PRD section in the `PRD Source` column or inline citation.
