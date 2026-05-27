---
title: "Patient-visible audit log surfaces every PHI access including proxy, privileged, and break-glass"
parent_epic: "documentation (output)/epics/epic-02-family-accounts-proxy-lifecycle-audit-log.md"
summary: "Patient-facing audit-log surface that lists every PHI-record access — proxy, privileged-user, break-glass, and integration — with actor identity (or role), timestamp, action, and record category, read-only and within 5 minutes of the access event."
owner: "Identity & Access Platform Team — Family & Proxy squad"
priority: "P0"
sprint: "Family/Proxy Sprint 4"
story_points: 8
personas:
  - "Eleanor W. — Tech-Limited Senior (75+) — primary, anti-scam oversight"
  - "All patients — universal oversight"
  - "Linda R. — sensitive-category oversight context"
acceptance_criteria:
  - "Patient sees every PHI access entry (proxy, privileged, break-glass, integration) with actor/role, timestamp, action, record category within 5 min (PRD §13.1 F-003; §5.4 `NF-032`)"
  - "Privileged-user entries are distinctly flagged (PRD §5.9 `NF-077`; §13.1 F-003)"
  - "Audit-log entries are read-only from the patient surface (PRD §13.1 F-003)"
  - "Audit surface ships at web + iOS + Android parity, WCAG 2.1 AA (PRD §13.9 F-080; §5.1 `NF-010`–`NF-013`)"
  - "Zero third-party tracking SDK requests on audit pages (PRD §5.10 `NF-080b`; §8 R-REG-01)"
  - "Audit-query response ≤ 1.5s p95 for the default time window (PRD §5.2 `NF-028`)"
dependencies:
  - "Identity epic Story 05 (immutable audit event emission)"
  - "Every Phase 1 domain service emitting audit events (Messaging, Results, Meds, Appointments, Billing)"
  - "Break-Glass & Privileged Access epic (event producer)"
  - "Notifications channel preferences for audit-anomaly alerts"
tasks:
  - "Design patient-facing audit-log UI with filter / search / pagination"
  - "Implement audit-query API with role-based redaction (no operator PII beyond role+identifier per policy)"
  - "Render privileged + break-glass entries with distinct visual treatment"
  - "Add 'report concern' affordance routing to helpdesk + Privacy"
  - "axe-core in CI; accessibility audit; usability test with Eleanor-class users"
  - "CI gate for zero third-party requests on audit pages"
links:
  - "context (ingestion)/prd.md"
  - "documentation (output)/epics/epic-02-family-accounts-proxy-lifecycle-audit-log.md"
---

> **Author reminder:** Every story MUST link to its parent epic via `parent_epic` and cite the originating PRD section (e.g., `(PRD §<section>)`) when establishing acceptance criteria, NFRs, and telemetry. Stories without epic linkage and PRD citations should not be accepted into a sprint.

## User Story

**Trigger scenario:** Eleanor has a granddaughter with proxy access (Stories 02 + 03) and wants to confirm, with her own eyes, every time someone — including her granddaughter, a clinic staff member, or a system integration — has touched her record. She is alert to scams and the audit log is part of her trust calculus. Linda also uses it to verify that behavioral-health notes have not been viewed by the primary-care team (PRD §3.1 Eleanor, Linda; UC-06, UC-08).

As a **patient**, I can **see a complete, read-only audit log of every PHI access to my record — including proxy, privileged-user, and break-glass entries — within 5 minutes of the access** so that **I have transparent oversight of who is seeing my health information**.

## Acceptance Criteria (Gherkin-style)

| # | Scenario | Given | When | Then | PRD Source |
|---|----------|-------|------|------|------------|
| 1 | Audit completeness | A patient with various access events on their record | They open the patient-visible audit log | They see every PHI-access entry (proxy, privileged, break-glass, integration) with actor (or role), timestamp, action, record category | (PRD §13.1 F-003) |
| 2 | 5-minute freshness | An access event occurs | The patient opens the audit log within 5 min | The new entry is visible | (PRD §13.1 F-003; §5.4 `NF-032`) |
| 3 | Privileged-flag rendering | A privileged-user or break-glass event entry | The patient views the log | The entry is distinctly flagged (color + label + icon, not color-alone) | (PRD §5.9 `NF-077`; §13.1 F-003, F-005; §5.1 `NF-012`) |
| 4 | Read-only patient surface | A patient on the audit log | They attempt any modification action | The surface offers no edit/delete control; modifications are rejected server-side | (PRD §13.1 F-003) |
| 5 | Mobile + web parity & accessibility | The release ships to GA | All three platforms publish | The audit log is functionally identical and meets WCAG 2.1 AA with text scaling and ≥44pt touch targets | (PRD §13.9 F-080; §5.1 `NF-010`–`NF-013`) |
| 6 | No third-party tracking | The audit page is loaded | Network traffic is captured | Zero third-party tracking-SDK requests are emitted | (PRD §5.10 `NF-080a`, `NF-080b`; §8 R-REG-01) |
| 7 | Query performance | A patient opens the audit log with default time window | The query runs | Response ≤ 1.5s p95 on broadband; meaningful loading state on slower networks | (PRD §5.2 `NF-027`, `NF-028`, `NF-029c`) |

## Non-Functional / Compliance Notes

- Performance: audit-query p95 ≤ 1.5s for default window; pagination for longer ranges; graceful degraded mode on backend slow-path (PRD §5.2 `NF-028`, `NF-029c`).
- Security: read-only API; server-side enforcement; role-based redaction so operator PII is not over-exposed beyond policy (PRD §5.3 `NF-030c`).
- Privacy / Data handling: OCR-compliant telemetry; no PHI in client-side analytics (PRD §5.10 `NF-080a`, `NF-080b`).
- Regulatory: HIPAA right of access + audit; ≥ 6yr retention; information-blocking — audit cannot be a covert denial path (PRD §6.5; §5.4 `NF-032`; §5.9 `NF-074`).
- Accessibility / UX: WCAG 2.1 AA; high-contrast and no-color-alone for privileged-entry flag; usability testing with low-vision + elderly users (PRD §5.1 `NF-010`–`NF-013`; §5.15 `NF-095`).

## Telemetry and Reporting

- Events emitted: `audit.viewed`, `audit.entry.expanded`, `audit.concern.reported`, with non-PHI correlation IDs.
- Metrics tracked: audit-page view rate stratified by cohort (75+ focus for `BO-6`), audit-query latency p95, concern-report rate, audit-completeness coverage % (target 100%).
- Dashboards / alerts: alert on coverage < 100%; alert on view-rate disparities for 75+ cohort (PRD §5.8 `NF-072`); anomaly detection on concern-report spikes.
- Audit logging: this story IS a primary consumer of the audit pipeline; ≥ 6yr retention (PRD §5.4 `NF-032`).

## Dependencies

- Upstream services: immutable audit store + query API, every domain service emitting events, Break-Glass producer, Notifications.
- Data sources / documents: redaction policy (operator identity vs. role).
- Teams / sign-offs: Privacy Officer, Legal, CISO, Accessibility audit, Clinical Operations (concern-report routing).
- Blocking stories or epics: Identity epic Story 05 (audit-event foundation); Story 02 + 03 (proxy events).

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| Missing event from a domain service (R-SEC-01) | Med | High | CI contract test asserts emit on every PHI-bearing endpoint; coverage dashboard | Audit Platform + Domain teams |
| Over-exposure of operator identity | Low | High | Role-based redaction reviewed by Privacy + Legal; redaction policy as code | Privacy + Identity Platform |
| 75+ cohort under-uses audit, defeating oversight value (R-ORG-03) | Med | Med | Anti-scam-aligned onboarding content; voice-call helpdesk walkthrough; in-clinic onboarding option | Product + Health Equity |
| Audit page leaks PHI to analytics (R-REG-01) | Low | High | Build-time third-party-request scan + Privacy data-flow review | Privacy + Engineering |

## Rollout / Validation Checklist

- [ ] Unit tests added and passing
- [ ] Integration tests cover acceptance criteria scenarios
- [ ] Manual QA spot-check against source documents completed
- [ ] Telemetry verified in staging dashboard
- [ ] Security / compliance review signed off
- [ ] Feature flag / rollout plan defined (cohort waves; in-clinic onboarding for 75+ first)
- [ ] Documentation updated (runbooks, patient-facing help, helpdesk script)
- [ ] Parent epic acceptance criteria still satisfied

## Source References

- Parent epic: [epic-02-family-accounts-proxy-lifecycle-audit-log.md](../epic-02-family-accounts-proxy-lifecycle-audit-log.md)
- Source PRD: [context (ingestion)/prd.md](../../../context%20(ingestion)/prd.md)
- PRD sections cited: §2.1 BO-6, §3.1 Eleanor/Linda, §3.2 UC-06/UC-08, §5.1 `NF-010`–`NF-013`, §5.2 `NF-027`/`NF-028`/`NF-029c`, §5.3 `NF-030c`, §5.4 `NF-032`, §5.8 `NF-072`, §5.9 `NF-074`/`NF-077`, §5.10 `NF-080a`/`NF-080b`, §5.15 `NF-095`, §6.5, §8 R-SEC-01/R-REG-01/R-ORG-03, §13.1 F-003/F-005, §13.9 F-080.
- Design / architecture docs: PRD §6.2 (Audit / Logging service).

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Confirm `parent_epic` points to a real epic file before opening the story for review.
- Each acceptance criterion, NFR, and telemetry metric must reference its PRD section in the `PRD Source` column or inline citation.
