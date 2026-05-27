---
title: "Patient completes IAL2 remote identity proofing during first-time registration"
parent_epic: "documentation (output)/epics/epic-01-identity-authentication-account-recovery.md"
summary: "New patient self-registers and completes IAL2-equivalent identity proofing via the contracted remote vendor, yielding an authenticated session and an immutable audit entry."
owner: "Identity & Access Platform Team"
priority: "P0"
sprint: "Identity Sprint 2"
story_points: 8
personas:
  - "All patient personas (Linda R., Marcus T., Eleanor W.) at first-time registration"
dependencies:
  - "Identity-proofing vendor contracted and integrated (PRD §10 decision 21; `A-033`)"
  - "OIDC identity provider configured (PRD §6.3)"
  - "Immutable audit store available (PRD §5.4 `NF-032`)"
  - "Multilingual onboarding content for launch languages (PRD §5.12 `NF-087`)"
acceptance_criteria:
  - "Registration completes at IAL2-equivalent via the remote vendor and yields an authenticated session (PRD §13.1 F-004; §5.3 `NF-030b`)"
  - "Successful proofing writes an audit entry within 5 minutes (PRD §5.4 `NF-032`)"
  - "No CAPTCHA appears in the normal patient registration flow (PRD §5.3 `NF-030`)"
  - "Registration UI meets WCAG 2.1 AA and supports text scaling + ≥44pt touch targets (PRD §5.1 `NF-010`–`NF-013`)"
  - "Zero third-party tracking-SDK requests on registration pages (PRD §5.10 `NF-080b`)"
tasks:
  - "Integrate remote ID-proofing vendor SDK behind the registration BFF"
  - "Persist proofing result + evidence reference; issue OIDC session on success"
  - "Emit identity-event records to the immutable audit store"
  - "Wire feature flag / kill switch around the proofing flow"
  - "Add unit + integration tests, including failure paths"
  - "Run axe-core in CI; resolve any AA violations"
  - "Add CI check confirming zero third-party requests on registration page"
  - "Add stratified-cohort dashboard panels for completion rate"
links:
  - "context (ingestion)/prd.md"
  - "documentation (output)/epics/epic-01-identity-authentication-account-recovery.md"
---

> **Author reminder:** Every story MUST link to its parent epic via `parent_epic` and cite the originating PRD section (e.g., `(PRD §<section>)`) when establishing acceptance criteria, NFRs, and telemetry. Stories without epic linkage and PRD citations should not be accepted into a sprint.

## User Story

**Trigger scenario:** A new patient arrives at HealthConnect for the first time and needs to create an account before they can book an appointment, message their care team, or view results. The legacy portal's username/password flow is not acceptable — Phase 1 requires IAL2-equivalent proofing before PHI access (PRD §5.3 `NF-030b`).

As a **new patient**, I can **complete identity proofing through the remote ID-proofing vendor as part of registration** so that **I reach an authenticated, IAL2-verified session in a single sitting without having to visit a clinic**.

## Acceptance Criteria (Gherkin-style)

| # | Scenario | Given | When | Then | PRD Source |
|---|----------|-------|------|------|------------|
| 1 | Successful remote proofing | A new patient on the registration page with a valid government ID and a device camera | They complete the vendor proofing flow successfully | They reach an authenticated session at IAL2 and an identity audit entry is written within 5 minutes | (PRD §13.1 F-004; §5.3 `NF-030b`; §5.4 `NF-032`) |
| 2 | Failed proofing | A new patient who cannot complete IAL2-equivalent proofing | The vendor returns a failure | They are shown an in-clinic / alternative-path option and receive **no PHI-bearing access**; the attempt is logged | (PRD §13.1 F-004; §4.4 risk-driven req) |
| 3 | No CAPTCHA in normal flow | A new patient on the normal registration path | They submit registration | No CAPTCHA challenge is presented | (PRD §5.3 `NF-030`) |
| 4 | Accessibility | A low-vision patient using 200% text scale on iOS | They navigate registration with VoiceOver | All controls are labeled, focusable, meet ≥44pt touch targets, and pass WCAG 2.1 AA checks | (PRD §5.1 `NF-010`–`NF-013`) |
| 5 | No third-party tracking | The registration page is loaded in any supported browser | Network requests are captured | Zero third-party tracking-SDK requests are emitted | (PRD §5.10 `NF-080b`; §8 R-REG-01) |

## Non-Functional / Compliance Notes

- Performance: registration page TTI ≤ 3s on broadband; common actions ≤ 1.5s p95 (PRD §5.2 `NF-027`, `NF-028`).
- Security: encryption in transit + at rest; secrets via centralized vault; no static credentials in code (PRD §5.4 `NF-035`, `NF-039e`).
- Privacy / Data handling: proofing evidence stored only as required by the IAL2 policy; OCR-compliant telemetry baseline; no PHI to non-BAA destinations (PRD §5.10 `NF-080a`, `NF-080b`; §5.4 `NF-039`).
- Regulatory: NIST 800-63-3 IAL2 (PRD §5.3 `NF-030b`); HIPAA access-control and audit (PRD §6.5; §5.4 `NF-032`).
- Accessibility / UX: WCAG 2.1 AA; text scaling, high-contrast, no color-alone, ≥44pt touch targets (PRD §5.1 `NF-010`–`NF-013`).

## Telemetry and Reporting

- Events emitted: `identity.registration.started`, `identity.proofing.completed`, `identity.proofing.failed`, `identity.session.issued` with non-PHI correlation IDs only.
- Metrics tracked: registration completion rate (stratified by age / language / accessibility cohort), proofing latency p50/p95, vendor error rate.
- Dashboards / alerts: stratified completion-rate dashboard with alert if any cohort < 90% over 7 days (PRD §5.8 `NF-072`); p95 latency alert > 20% week over week.
- Audit logging: every proofing attempt + result + session issuance written to the immutable audit store within 5 minutes; ≥ 6yr retention (PRD §5.4 `NF-032`).

## Dependencies

- Upstream services: ID-proofing vendor, OIDC identity provider, immutable audit store, Notifications (for confirmation email).
- Data sources / documents: launch-language content pack; trusted-clinic branding assets (`F-191`).
- Teams / sign-offs: Privacy Officer, CISO, Health Equity, Accessibility audit vendor.
- Blocking stories or epics: Identity, Authentication & Account Recovery epic (parent); Helpdesk model story (for failed-proofing escalation path); In-clinic onboarding story (alternative path).

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| Vendor false-reject rate disproportionately affects the 75+ cohort (R-ORG-03) | Med | High | Stratified-cohort monitoring on completion rate; in-clinic + voice-supported alternative path; equity gate before broader rollout | Health Equity + Product |
| Vendor SDK introduces a third-party tracking request (R-REG-01) | Low | High | Automated third-party-request scan in CI gates the build; Privacy Officer sign-off before GA | Privacy + Engineering |
| Vendor outage blocks registration | Med | Med | Feature flag / kill switch + degraded-mode messaging directing user to in-clinic path (PRD §5.2 `NF-029g`; §4.1 `F-074`, `F-075`) | SRE |

## Rollout / Validation Checklist

- [ ] Unit tests added and passing
- [ ] Integration tests cover acceptance criteria scenarios
- [ ] Manual QA spot-check against source documents completed
- [ ] Telemetry verified in staging dashboard
- [ ] Security / compliance review signed off
- [ ] Feature flag / rollout plan defined (pilot clinic → cohort waves)
- [ ] Documentation updated (runbooks, user guides)
- [ ] Parent epic acceptance criteria still satisfied

## Source References

- Parent epic: [epic-01-identity-authentication-account-recovery.md](../epic-01-identity-authentication-account-recovery.md)
- Source PRD: [context (ingestion)/prd.md](../../../context%20(ingestion)/prd.md)
- PRD sections cited: §2.1 BO-1 / BO-6, §3.1 personas, §4.4 risk-driven reqs, §5.1, §5.2, §5.3, §5.4, §5.8, §5.10, §5.12, §6.5, §8 R-ORG-03 / R-REG-01, §13.1 F-004.
- Design / architecture docs: PRD §6.2 (Identity & Auth service).
- Tickets / external references: ID-proofing vendor RFP outcome (PRD §10 decision 21; `A-033`).

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Confirm `parent_epic` points to a real epic file before opening the story for review.
- Each acceptance criterion, NFR, and telemetry metric must reference its PRD section in the `PRD Source` column or inline citation.
