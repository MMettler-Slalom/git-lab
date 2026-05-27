---
title: "Identity events written to immutable audit and visible to patient within 5 minutes"
parent_epic: "documentation (output)/epics/epic-01-identity-authentication-account-recovery.md"
summary: "Every identity-related event (registration, MFA change, recovery, privileged access, break-glass primitives) is captured in the immutable audit store within 5 minutes and surfaced to the patient via the patient-visible audit log (`F-003`)."
owner: "Identity & Access Platform Team"
priority: "P0"
sprint: "Identity Sprint 5"
story_points: 5
personas:
  - "All patient personas (oversight via patient-visible audit log)"
  - "Eleanor W. — particularly values transparency on proxy / privileged access"
  - "Compliance / Privacy reviewers"
acceptance_criteria:
  - "All identity events captured to immutable audit store within 5 min, integrity-protected, ≥ 6yr retention (PRD §5.4 `NF-032`)"
  - "Patient-visible identity events surfaced via `F-003` patient-visible audit log within 5 min (PRD §13.1 F-003)"
  - "Privileged-user access events distinctly flagged (PRD §5.9 `NF-077`)"
  - "Anomaly detection enabled on privileged + break-glass event streams (PRD §5.9 `NF-079`)"
  - "Telemetry pipeline emits no third-party tracking requests and follows OCR-compliant baseline (PRD §5.10 `NF-080a`, `NF-080b`)"
tasks:
  - "Define identity-event schema (event type, actor, subject, method, evidence ref, correlation id, timestamp, privileged-flag)"
  - "Wire every identity surface (registration, MFA, recovery, RBAC, session) to emit events"
  - "Implement audit-write pipeline with end-to-end latency SLO ≤ 5 min p95"
  - "Expose the patient-visible subset to `F-003`"
  - "Configure anomaly detection on privileged + break-glass streams"
  - "Add CI test that asserts every identity code-path emits the expected audit event"
links:
  - "context (ingestion)/prd.md"
  - "documentation (output)/epics/epic-01-identity-authentication-account-recovery.md"
---

> **Author reminder:** Every story MUST link to its parent epic via `parent_epic` and cite the originating PRD section (e.g., `(PRD §<section>)`) when establishing acceptance criteria, NFRs, and telemetry. Stories without epic linkage and PRD citations should not be accepted into a sprint.

## User Story

**Trigger scenario:** Eleanor's granddaughter has proxy access. Eleanor wants to know, with confidence, every time her account is accessed, when MFA is changed, when recovery is attempted, and when a privileged operator touches her account. Compliance also needs this audit trail for HIPAA, OCR, and breach-investigation purposes. Today, none of the new identity surfaces emit events consistently.

As a **patient**, I can **see every identity-related event on my account in the patient-visible audit log within 5 minutes of it happening** so that **I have transparent, near-real-time oversight of who is touching my account and how**.

## Acceptance Criteria (Gherkin-style)

| # | Scenario | Given | When | Then | PRD Source |
|---|----------|-------|------|------|------------|
| 1 | Audit completeness | An identity event of any type occurs (registration, MFA change, recovery, privileged access, break-glass) | The event completes | A record is written to the immutable audit store within 5 min @ p95 | (PRD §5.4 `NF-032`) |
| 2 | Patient-visible surface | A patient with an account | They open the patient-visible audit log (`F-003`) | They see the identity events relevant to their account within 5 min of occurrence | (PRD §13.1 F-003; §5.4 `NF-032`) |
| 3 | Privileged-access flag | A privileged operator or break-glass action occurs | The audit event is written | The record carries a distinct privileged-access flag and triggers anomaly-detection evaluation | (PRD §5.9 `NF-077`, `NF-079`) |
| 4 | Immutability + retention | An identity audit record is written | Any attempt to modify or delete it occurs | The store rejects the modification; retention is ≥ 6 years | (PRD §5.4 `NF-032`) |
| 5 | Privacy-compliant telemetry | The audit pipeline is observed in production | Network traffic is captured | No third-party tracking SDK requests are emitted; telemetry follows OCR baseline | (PRD §5.10 `NF-080a`, `NF-080b`; §8 R-REG-01) |
| 6 | Code-path coverage | A new identity code-path is merged | CI runs | The audit-emission CI test fails if the path lacks an audit event | (PRD §15.1 testing strategy) |

## Non-Functional / Compliance Notes

- Performance: audit-write latency p95 ≤ 5 min; pipeline backpressure handled without event loss (PRD §5.4 `NF-032`).
- Security: integrity-protected, append-only store; KMS / HSM-backed keys for signing (PRD §5.4 `NF-032`, `NF-036`).
- Privacy: only non-PHI correlation IDs in transport; OCR-compliant telemetry posture (PRD §5.10 `NF-080a`, `NF-080b`).
- Regulatory: HIPAA audit + breach-investigation support (PRD §6.5; §5.4 `NF-039b`); 6yr retention.
- Accessibility: patient-visible audit log meets WCAG 2.1 AA (PRD §5.1 `NF-010`).

## Telemetry and Reporting

- Events emitted: all `identity.*` event types defined in the schema task.
- Metrics tracked: audit-write latency p50 / p95, event-capture coverage % (target 100%), privileged-event count, anomaly-detection alert count, dropped-event count (target 0).
- Dashboards / alerts: alert if audit-write p95 > 5 min; alert on any dropped event; alert on anomaly-detection signals.
- Audit logging: this story IS the audit-logging foundation; ≥ 6yr retention (PRD §5.4 `NF-032`).

## Dependencies

- Upstream services: immutable audit store, KMS/HSM, anomaly-detection service, patient-visible audit UI (`F-003`).
- Data sources / documents: identity-event schema.
- Teams / sign-offs: CISO, Privacy Officer, SRE, Family Accounts & Proxy epic team (consumer of `F-003`).
- Blocking stories or epics: depends on Stories 01–04 emitting events; consumed by Family Accounts & Proxy Lifecycle epic.

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| Event loss under load | Med | High | Backpressure + durable buffer; dropped-event alert at 0 threshold; pre-launch load test (`NF-029e`) | SRE |
| Telemetry pipeline leaks PHI or adds tracking SDK (R-REG-01) | Low | High | CI gate on third-party requests; data-flow review by Privacy Officer | Privacy + Engineering |
| Missing event on a new identity code-path | Med | Med | CI test that fails when an identity code-path lacks an emit; code-review checklist | Identity Platform |

## Rollout / Validation Checklist

- [ ] Unit tests added and passing
- [ ] Integration tests cover acceptance criteria scenarios
- [ ] Manual QA spot-check against source documents completed
- [ ] Telemetry verified in staging dashboard
- [ ] Security / compliance review signed off
- [ ] Feature flag / rollout plan defined
- [ ] Documentation updated (audit schema, runbook for SRE / Privacy)
- [ ] Parent epic acceptance criteria still satisfied

## Source References

- Parent epic: [epic-01-identity-authentication-account-recovery.md](../epic-01-identity-authentication-account-recovery.md)
- Source PRD: [context (ingestion)/prd.md](../../../context%20(ingestion)/prd.md)
- PRD sections cited: §5.1 `NF-010`, §5.2 `NF-029e`, §5.4 `NF-032`/`NF-036`/`NF-039b`, §5.9 `NF-077`/`NF-079`, §5.10 `NF-080a`/`NF-080b`, §6.5, §8 R-REG-01, §13.1 F-003 / F-005, §15.1 testing strategy.
- Design / architecture docs: PRD §6.2 (Identity & Auth service); audit-store reference architecture.

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Confirm `parent_epic` points to a real epic file before opening the story for review.
- Each acceptance criterion, NFR, and telemetry metric must reference its PRD section in the `PRD Source` column or inline citation.
