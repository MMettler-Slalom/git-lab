---
title: "Provider RBAC with shared-workstation fast resume and auto-logout"
parent_epic: "documentation (output)/epics/epic-01-identity-authentication-account-recovery.md"
summary: "Provider/staff identity uses least-privilege RBAC, with shared-workstation sessions supporting fast resume + auto-logout and personal-device sessions following the secure mobile chart view policy."
owner: "Identity & Access Platform Team"
priority: "P0"
sprint: "Identity Sprint 4"
story_points: 5
personas:
  - "Dr. K. Alvarez — Primary Care Physician (shared workstation between exam rooms)"
  - "Clinic staff (MA, nurse) — shared workstation"
  - "Dr. R. Okonkwo — Specialist on shared workstation and personal mobile"
dependencies:
  - "OIDC IdP with RBAC claims (PRD §6.3)"
  - "Workstation badge-tap / SSO integration (org infrastructure)"
  - "Immutable audit store (PRD §5.4 `NF-032`)"
  - "Provider mobile via Epic Haiku + thin patient-at-a-glance surface (PRD §13.9 F-081)"
acceptance_criteria:
  - "RBAC with least privilege enforced for providers/staff (PRD §5.3 `NF-030c`)"
  - "Workstation sessions support fast resume + auto-logout (PRD §5.2 `NF-022`)"
  - "Personal-device sessions follow the secure mobile chart view policy (PRD §5.2 `NF-023`; §5.3 `NF-030d`)"
  - "Chart open ≤ 2s, order screen ≤ 1s, message open ≤ 1s @ p95 not regressed by identity layer (PRD §5.2 `NF-020`)"
  - "Privileged-user access logged and distinctly flagged in audit (PRD §5.9 `NF-077`; §5.4 `NF-032`)"
tasks:
  - "Define RBAC roles and bind to OIDC claims (PCP, specialist, MA, nurse, helpdesk, admin)"
  - "Implement badge-tap / SSO fast-resume on shared workstations"
  - "Implement idle-based auto-logout policy with grace handling for active charts"
  - "Implement personal-device session policy (shorter TTL, biometric re-auth)"
  - "Emit privileged-access audit events with the distinct-flag attribute"
  - "Performance test chart-open / order-screen / message-open under the new session layer"
links:
  - "context (ingestion)/prd.md"
  - "documentation (output)/epics/epic-01-identity-authentication-account-recovery.md"
---

> **Author reminder:** Every story MUST link to its parent epic via `parent_epic` and cite the originating PRD section (e.g., `(PRD §<section>)`) when establishing acceptance criteria, NFRs, and telemetry. Stories without epic linkage and PRD citations should not be accepted into a sprint.

## User Story

**Trigger scenario:** Dr. Alvarez moves between exam rooms throughout the day, sharing a workstation with the MA and nurse. He needs to resume his session in seconds when he sits down, but the workstation must auto-logout to protect PHI when left unattended. On his personal phone after-hours, he needs a different (tighter) session policy.

As a **provider on a shared workstation**, I can **fast-resume my session via badge / SSO and have idle sessions auto-logout** so that **I stay productive between exam rooms while PHI stays protected on a shared device**.

## Acceptance Criteria (Gherkin-style)

| # | Scenario | Given | When | Then | PRD Source |
|---|----------|-------|------|------|------------|
| 1 | Fast resume on shared workstation | A provider with a valid badge at a shared workstation | They tap their badge / authenticate via SSO | Their previous session resumes; chart open completes ≤ 2s @ p95 | (PRD §5.2 `NF-022`, `NF-020`) |
| 2 | Auto-logout on idle | A provider session idle past the configured threshold | The idle timer elapses | The session is locked and requires re-auth; an audit event is written | (PRD §5.2 `NF-022`; §5.4 `NF-032`) |
| 3 | Personal-device session policy | A provider on a personal phone | They open the patient-at-a-glance surface | A shorter session TTL + biometric re-auth policy is enforced | (PRD §5.2 `NF-023`; §5.3 `NF-030d`) |
| 4 | RBAC least privilege | An MA, nurse, helpdesk, or admin user | They attempt to access a clinical surface outside their role | Access is denied; denial is logged | (PRD §5.3 `NF-030c`) |
| 5 | Privileged access logged distinctly | An admin / privileged action is performed | The action completes | An audit event with the privileged-access flag is written within 5 min | (PRD §5.9 `NF-077`; §5.4 `NF-032`) |

## Non-Functional / Compliance Notes

- Performance: chart open ≤ 2s, order screen ≤ 1s, message open ≤ 1s @ p95 (PRD §5.2 `NF-020`); identity layer must not regress these.
- Security: RBAC + workstation policy + service-account workload identity (PRD §5.3 `NF-030c`, `NF-030d`, `NF-030e`).
- Privacy: shared-device safeguards per `NF-061`; no PHI cached past session lock.
- Regulatory: HIPAA access control + audit logging + privileged-user flagging (PRD §6.5; §5.4 `NF-032`; §5.9 `NF-077`).
- Accessibility: workstation lock screen meets WCAG 2.1 AA (PRD §5.1 `NF-010`).

## Telemetry and Reporting

- Events emitted: `provider.session.resumed`, `provider.session.locked`, `provider.session.logout`, `rbac.denied`, `privileged.access.event`.
- Metrics tracked: fast-resume latency p95, idle-logout count, RBAC-denial count by role, chart-open p95.
- Dashboards / alerts: alert on chart-open p95 regression; alert on anomalous privileged-access volume (PRD §5.9 `NF-079`).
- Audit logging: every session event + privileged action in immutable audit ≥ 6yr retention (PRD §5.4 `NF-032`).

## Dependencies

- Upstream services: OIDC IdP, badge/SSO infrastructure, immutable audit store, Epic Haiku integration surface.
- Data sources / documents: RBAC role catalog from Clinical Informatics.
- Teams / sign-offs: CISO, Clinical Informatics, Clinical Operations.
- Blocking stories or epics: Identity epic (parent); audit-emission story (sibling).

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| Auto-logout disrupts active documentation | Med | Med | Active-chart-aware grace + warning toast before lock; configurable per role | Clinical Informatics + Product |
| RBAC misconfiguration grants over-broad access | Low | High | Role catalog reviewed by Clinical Informatics + Compliance; CI test asserts deny-by-default | Identity Platform |
| Personal-device policy frustrates after-hours use | Med | Med | Biometric re-auth keeps friction low; documented in provider onboarding (`NF-084`) | Product |

## Rollout / Validation Checklist

- [ ] Unit tests added and passing
- [ ] Integration tests cover acceptance criteria scenarios
- [ ] Manual QA spot-check against source documents completed
- [ ] Telemetry verified in staging dashboard
- [ ] Security / compliance review signed off
- [ ] Feature flag / rollout plan defined (pilot clinic first)
- [ ] Documentation updated (provider runbook, training materials)
- [ ] Parent epic acceptance criteria still satisfied

## Source References

- Parent epic: [epic-01-identity-authentication-account-recovery.md](../epic-01-identity-authentication-account-recovery.md)
- Source PRD: [context (ingestion)/prd.md](../../../context%20(ingestion)/prd.md)
- PRD sections cited: §5.1 `NF-010`, §5.2 `NF-020`/`NF-022`/`NF-023`, §5.3 `NF-030c`/`NF-030d`/`NF-030e`, §5.4 `NF-032`, §5.7 `NF-061`, §5.9 `NF-077`/`NF-079`, §5.12 `NF-084`, §6.5, §13.9 F-081.
- Design / architecture docs: PRD §6.2 (Identity & Auth service).

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Confirm `parent_epic` points to a real epic file before opening the story for review.
- Each acceptance criterion, NFR, and telemetry metric must reference its PRD section in the `PRD Source` column or inline citation.
