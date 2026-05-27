---
title: "PHI-safe account recovery with no helpdesk PHI override"
parent_epic: "documentation (output)/epics/epic-01-identity-authentication-account-recovery.md"
summary: "Patient self-service and helpdesk-assisted account recovery flows that never grant PHI-bearing access without IAL2-equivalent verification, with every action logged."
owner: "Identity & Access Platform Team"
priority: "P0"
sprint: "Identity Sprint 4"
story_points: 8
personas:
  - "Eleanor W. (75+) — primary; also all patient personas who lose a factor or device"
dependencies:
  - "Story 01 (IAL2 proofing) and Story 02 (MFA enrollment) complete"
  - "Helpdesk operating model + PHI-aware recovery process approved (PRD §10 decision 29; `A-034`; §5.12 `NF-086`)"
  - "Immutable audit store available (PRD §5.4 `NF-032`)"
  - "Notification channels available, including voice-call (PRD §13.5 F-035)"
acceptance_criteria:
  - "Recovery requests that cannot complete IAL2-equivalent verification do NOT yield PHI-bearing access (PRD §13.1 F-004; §4.4 risk-driven req)"
  - "Helpdesk has no operator override that grants PHI access (PRD §4.4 risk-driven req)"
  - "Every recovery action logged with method, evidence, and operator identity (PRD §13.1 F-004; §5.4 `NF-032`)"
  - "Helpdesk SLA tiers met; voice-call path available for the 75+ cohort (PRD §5.12 `NF-086`; §13.5 F-035)"
  - "Anti-phishing affordances on recovery surfaces; trusted-clinic branding visible (PRD §5.4 `NF-034`; §13.10 F-191)"
tasks:
  - "Implement self-service recovery flow gated on IAL2-equivalent re-verification"
  - "Implement helpdesk-assisted recovery tool with strict capability boundary (no PHI access)"
  - "Add evidence-capture fields (method, operator id, ticket id) to audit event schema"
  - "Add patient notification on every recovery action (per channel preference)"
  - "Tabletop exercise of the helpdesk recovery process"
  - "Threat-model review of recovery flow signed off by Security + Privacy"
links:
  - "context (ingestion)/prd.md"
  - "documentation (output)/epics/epic-01-identity-authentication-account-recovery.md"
---

> **Author reminder:** Every story MUST link to its parent epic via `parent_epic` and cite the originating PRD section (e.g., `(PRD §<section>)`) when establishing acceptance criteria, NFRs, and telemetry. Stories without epic linkage and PRD citations should not be accepted into a sprint.

## User Story

**Trigger scenario:** Eleanor W. (75+) has a new tablet and can no longer access her account because her biometric is bound to the old device. She calls the clinic helpdesk for help. The risk PRD §4.4 calls out is that helpdesk-driven recovery becomes a phishing / social-engineering vector for PHI exposure — so recovery must be IAL2-strong and the helpdesk must never have a PHI override.

As a **patient**, I can **recover access to my account through a verified, PHI-safe channel** so that **I regain access without anyone — including a helpdesk operator — being able to bypass identity verification to see my health information**.

## Acceptance Criteria (Gherkin-style)

| # | Scenario | Given | When | Then | PRD Source |
|---|----------|-------|------|------|------------|
| 1 | Successful self-service recovery | A patient with a verifiable recovery factor (e.g., second MFA factor, in-clinic re-proofing) | They complete the recovery flow | Their session is restored at IAL2 and an audit record (method, evidence, timestamp) is written within 5 min | (PRD §13.1 F-004; §5.4 `NF-032`) |
| 2 | No PHI on failed verification | A patient who cannot complete IAL2-equivalent verification | They request recovery | They are NOT granted PHI-bearing access; they are directed to an in-clinic re-proofing path | (PRD §13.1 F-004; §4.4 risk-driven req) |
| 3 | No helpdesk PHI override | A helpdesk operator using the recovery tool | They attempt any action on a patient account | The tool exposes no PHI surfaces and offers no override that grants PHI access; the operator can only initiate verified recovery workflows | (PRD §4.4 risk-driven req; §5.3 `NF-030c`) |
| 4 | Audit completeness | Any recovery action (self-service or helpdesk-assisted) | The action occurs | An audit entry with method + evidence + operator identity is written to the immutable store within 5 min | (PRD §13.1 F-004; §5.4 `NF-032`) |
| 5 | Helpdesk SLA + accessible path | An Eleanor-class patient calls in for help | They request recovery via voice | They reach a helpdesk within the tiered SLA; voice-call confirmation is available | (PRD §5.12 `NF-086`; §13.5 F-035) |
| 6 | Anti-phishing affordances | A patient lands on the recovery page from any link | They view the page | Trusted-clinic branding and anti-phishing affordances are present; the recovery URL is canonical | (PRD §5.4 `NF-034`; §13.10 F-191) |

## Non-Functional / Compliance Notes

- Performance: recovery actions ≤ 1.5s p95 (PRD §5.2 `NF-028`).
- Security: helpdesk tool runs under least-privilege RBAC; no static credentials; privileged-user access distinctly flagged in audit (PRD §5.3 `NF-030c`, `NF-030e`; §5.9 `NF-077`).
- Privacy: recovery evidence stored per the IAL2 policy; PHI never displayed in helpdesk tool; OCR-compliant telemetry (PRD §5.10 `NF-080a`, `NF-080b`).
- Regulatory: HIPAA access-control + audit (PRD §6.5; §5.4 `NF-032`); state-privacy notice for identity-data handling (PRD §5.9 `NF-076`).
- Accessibility: voice-call path for the 75+ cohort (PRD §13.5 F-035; §5.1 `NF-014`); WCAG 2.1 AA on web/mobile recovery surfaces.

## Telemetry and Reporting

- Events emitted: `identity.recovery.requested`, `identity.recovery.completed`, `identity.recovery.failed`, `identity.recovery.helpdesk_action`, with non-PHI correlation IDs.
- Metrics tracked: recovery completion rate, time-to-recovery (p50 / p90), PHI-override-attempt count (target: 0), helpdesk ticket SLA attainment by tier.
- Dashboards / alerts: alert on any non-zero PHI-override-attempt; alert on time-to-recovery p90 regression; alert on helpdesk SLA misses.
- Audit logging: every recovery action in immutable audit with method, evidence reference, operator identity, ≥ 6yr retention (PRD §5.4 `NF-032`).

## Dependencies

- Upstream services: OIDC IdP, immutable audit store, helpdesk ticketing system, notifications (voice + email + push), trusted-clinic branding service.
- Data sources / documents: helpdesk runbook; PHI-aware recovery SOP from Clinical Operations (`A-034`).
- Teams / sign-offs: Privacy Officer, CISO, Clinical Operations, Legal.
- Blocking stories or epics: Story 01, Story 02; Family Accounts & Proxy epic (consumer of audit primitives).

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| Social-engineering attack on helpdesk for PHI access (R-SEC-01, PRD §4.4 risk) | Med | High | Capability-bounded helpdesk tool with no PHI surfaces; tabletop exercises; pre-launch threat model sign-off | Security + Clinical Ops |
| Recovery flow becomes a covert access barrier for 75+ (R-ORG-03 + `NF-074` info-blocking) | Med | High | Voice-call + in-clinic re-proofing paths; stratified-cohort dashboard; equity gate before broader rollout | Health Equity + Product |
| Audit gap on helpdesk-initiated action | Low | High | Helpdesk tool emits audit events synchronously; CI test verifies event for every action path | Identity Platform + SRE |

## Rollout / Validation Checklist

- [ ] Unit tests added and passing
- [ ] Integration tests cover acceptance criteria scenarios
- [ ] Manual QA spot-check against source documents completed
- [ ] Telemetry verified in staging dashboard
- [ ] Security / compliance review signed off (incl. pre-launch threat model — PRD §8 R-SEC-01)
- [ ] Feature flag / rollout plan defined (helpdesk pilot before broad enablement)
- [ ] Documentation updated (helpdesk runbook, patient-facing recovery help articles)
- [ ] Parent epic acceptance criteria still satisfied

## Source References

- Parent epic: [epic-01-identity-authentication-account-recovery.md](../epic-01-identity-authentication-account-recovery.md)
- Source PRD: [context (ingestion)/prd.md](../../../context%20(ingestion)/prd.md)
- PRD sections cited: §4.4 risk-driven req, §5.1 `NF-014`, §5.2 `NF-028`, §5.3 `NF-030c`/`NF-030e`, §5.4 `NF-032`/`NF-034`, §5.9 `NF-076`/`NF-077`, §5.10 `NF-080a`/`NF-080b`, §5.12 `NF-086`, §6.5, §8 R-SEC-01 / R-ORG-03, §13.1 F-003 / F-004, §13.5 F-035, §13.10 F-191.
- Design / architecture docs: PRD §6.2 (Identity & Auth service).

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Confirm `parent_epic` points to a real epic file before opening the story for review.
- Each acceptance criterion, NFR, and telemetry metric must reference its PRD section in the `PRD Source` column or inline citation.
