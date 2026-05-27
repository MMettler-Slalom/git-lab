---
title: "Patient grants time-bound proxy access with evidence and both-party notification"
parent_epic: "documentation (output)/epics/epic-02-family-accounts-proxy-lifecycle-audit-log.md"
summary: "A patient (delegator) grants scoped, time-bound proxy access to a chosen delegate, providing relationship/guardianship evidence per policy; both parties are notified within 5 minutes and the event is in the patient-visible audit."
owner: "Identity & Access Platform Team — Family & Proxy squad"
priority: "P0"
sprint: "Family/Proxy Sprint 2"
story_points: 8
personas:
  - "Eleanor W. — Tech-Limited Senior (75+) — delegator"
  - "Eleanor's granddaughter — delegate (represented as a non-PRD secondary caregiver)"
acceptance_criteria:
  - "Grant requires evidence of relationship/guardianship per configured policy (PRD §13.1 F-002)"
  - "Both parties notified within 5 min p95 via their channel preferences (PRD §13.1 F-002; §4.7 F-070)"
  - "Time-bound expiration is mandatory on every grant (PRD §13.1 F-002; §8 R-SEC-01)"
  - "Grant event appears in the patient-visible audit log within 5 min (PRD §13.1 F-002, F-003; §5.4 `NF-032`)"
  - "Notification templates pass the SMS anti-phishing CI check (no login URLs) (PRD §13.8 F-072; §5.4 `NF-034`)"
dependencies:
  - "Story 01 (linked dependents + switcher)"
  - "Identity epic (IAL2 + MFA)"
  - "Notifications service with channel preferences"
  - "Immutable audit store (PRD §5.4 `NF-032`)"
  - "Policy decisions on co-equal parent / split custody (PRD §10 decision 16; `A-006`)"
tasks:
  - "Implement grant wizard with evidence-capture step (per configured policy)"
  - "Add mandatory expiration field with sensible defaults and max upper bound"
  - "Wire both-party notifications honoring channel preferences (`F-070`)"
  - "Emit grant event with evidence reference to immutable audit"
  - "Surface grant entry in patient-visible audit log (`F-003`)"
  - "Anti-phishing review of notification templates; add to SMS CI gate"
  - "Threat-model review of grant flow (R-SEC-01)"
links:
  - "context (ingestion)/prd.md"
  - "documentation (output)/epics/epic-02-family-accounts-proxy-lifecycle-audit-log.md"
---

> **Author reminder:** Every story MUST link to its parent epic via `parent_epic` and cite the originating PRD section (e.g., `(PRD §<section>)`) when establishing acceptance criteria, NFRs, and telemetry. Stories without epic linkage and PRD citations should not be accepted into a sprint.

## User Story

**Trigger scenario:** Eleanor wants her granddaughter to help her review lab results and book appointments for the next six months while she recovers from a procedure. The legacy portal only offered a permanent "share my password" anti-pattern. She needs to grant scoped, time-bound proxy access through an audit-able flow that the clinic recognizes as official, and she wants to see proof in her own record that she granted it (PRD §3.1 Eleanor; UC-06).

As a **patient (delegator)**, I can **grant scoped, time-bound proxy access to a chosen delegate after providing relationship evidence** so that **my caregiver can help me without compromising my account security or my visibility into what they are doing**.

## Acceptance Criteria (Gherkin-style)

| # | Scenario | Given | When | Then | PRD Source |
|---|----------|-------|------|------|------------|
| 1 | Grant requires evidence | A patient initiates a proxy grant | They submit the grant wizard | The system requires and records relationship/guardianship evidence per the configured policy before the grant becomes active | (PRD §13.1 F-002) |
| 2 | Both parties notified | A grant is approved | The grant becomes active | Delegator AND delegate receive notification within 5 min p95 via their channel preferences | (PRD §13.1 F-002; §4.7 F-070; §5.4 `NF-031`) |
| 3 | Time-bound expiration mandatory | A user fills the grant wizard | They attempt to submit without an expiration | The wizard blocks submission and requires an expiration ≤ configured max | (PRD §13.1 F-002; §8 R-SEC-01) |
| 4 | Audit visibility | A grant has just been created | The delegator opens the patient-visible audit log | The grant event (with delegate identity, scope, expiration) is visible within 5 min | (PRD §13.1 F-002, F-003; §5.4 `NF-032`) |
| 5 | Anti-phishing in notifications | A grant notification is rendered for SMS | CI runs the template-scan test | The template contains no login URL; build fails if one is added | (PRD §13.8 F-072; §5.4 `NF-034`) |
| 6 | Accessibility | An Eleanor-class user on a tablet with 200% text scale | They walk through the grant wizard | All steps meet WCAG 2.1 AA and ≥44pt touch targets; voice-call helpdesk path is offered as alternative | (PRD §5.1 `NF-010`–`NF-013`; §13.5 F-035) |

## Non-Functional / Compliance Notes

- Performance: grant submission + notification dispatch ≤ 5 min p95 (PRD §13.1 F-002); wizard interactions ≤ 1.5s p95 (PRD §5.2 `NF-028`).
- Security: evidence-reference stored, never the raw document body unless required by policy; least-privilege RBAC on grant tool (PRD §5.3 `NF-030c`); pre-launch threat model on grant flow (PRD §8 R-SEC-01).
- Privacy / Data handling: only non-PHI correlation IDs in telemetry; vulnerable-population safeguards on shared devices (PRD §5.7 `NF-061`; §5.10 `NF-080a`).
- Regulatory: HIPAA Privacy + state guardianship matrix (PRD §6.5; §5.9 `NF-076`); information-blocking — grant flow cannot be used as a covert barrier (PRD §5.9 `NF-074`).
- Accessibility / UX: WCAG 2.1 AA; voice-call alternative for the 75+ cohort (PRD §13.5 F-035; §5.1 `NF-014`).

## Telemetry and Reporting

- Events emitted: `proxy.grant.started`, `proxy.grant.evidence_submitted`, `proxy.grant.completed`, `proxy.notification.sent`, with non-PHI correlation IDs.
- Metrics tracked: grant completion rate, grant → both-party-notified latency p95, abandonment by step, helpdesk-assisted grant volume.
- Dashboards / alerts: alert if notification delivery success < 99%; alert on grant-step abandonment regression for 75+ cohort (PRD §5.8 `NF-072`).
- Audit logging: grant event with delegate identity, scope, expiration, evidence reference, written within 5 min; ≥ 6yr retention (PRD §5.4 `NF-032`).

## Dependencies

- Upstream services: OIDC IdP, immutable audit store, Notifications, helpdesk tool (for assisted grants).
- Data sources / documents: relationship/guardianship policy spec; state-privacy matrix (`A-006`, decisions 8/16/17).
- Teams / sign-offs: Privacy Officer, Legal, CISO, Health Equity, Accessibility audit.
- Blocking stories or epics: Story 01 (switcher); Identity epic; SMS anti-phishing CI gate (cross-epic).

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| Social-engineered grant (R-SEC-01) | Med | High | Mandatory evidence + both-party notification + threat-model review + delegator-initiated revoke story (Story 03) | Security + Privacy |
| Permanent / over-long grant defaults | Med | High | Mandatory expiration + max-duration policy enforced server-side | Identity Platform |
| 75+ delegator abandons grant wizard | Med | Med | Voice-call helpdesk alternative; stratified-cohort completion dashboard | Product + Health Equity |

## Rollout / Validation Checklist

- [ ] Unit tests added and passing
- [ ] Integration tests cover acceptance criteria scenarios
- [ ] Manual QA spot-check against source documents completed
- [ ] Telemetry verified in staging dashboard
- [ ] Security / compliance review signed off (incl. threat model — PRD §8 R-SEC-01)
- [ ] Feature flag / rollout plan defined (helpdesk pilot before broad enablement)
- [ ] Documentation updated (helpdesk runbook, patient-facing help articles)
- [ ] Parent epic acceptance criteria still satisfied

## Source References

- Parent epic: [epic-02-family-accounts-proxy-lifecycle-audit-log.md](../epic-02-family-accounts-proxy-lifecycle-audit-log.md)
- Source PRD: [context (ingestion)/prd.md](../../../context%20(ingestion)/prd.md)
- PRD sections cited: §3.1 Eleanor, §3.2 UC-06, §4.7 F-070, §5.1 `NF-010`–`NF-014`, §5.2 `NF-028`/`NF-031`, §5.3 `NF-030c`, §5.4 `NF-032`/`NF-034`, §5.7 `NF-061`, §5.8 `NF-072`, §5.9 `NF-074`/`NF-076`, §5.10 `NF-080a`, §6.5, §8 R-SEC-01, §10 decisions 8/16/17, §13.1 F-002/F-003, §13.5 F-035, §13.8 F-072.
- Design / architecture docs: PRD §6.2 (Proxy / Family + Audit / Logging services).

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Confirm `parent_epic` points to a real epic file before opening the story for review.
- Each acceptance criterion, NFR, and telemetry metric must reference its PRD section in the `PRD Source` column or inline citation.
