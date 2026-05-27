---
title: "Patient enrolls biometric MFA at first login with risk-based step-up"
parent_epic: "documentation (output)/epics/epic-01-identity-authentication-account-recovery.md"
summary: "At first login after IAL2 proofing, the patient enrolls at least one non-SMS-link MFA factor (biometric on supported devices) and risk-based step-up is configured."
owner: "Identity & Access Platform Team"
priority: "P0"
sprint: "Identity Sprint 3"
story_points: 5
personas:
  - "All patient personas, with explicit attention to Marcus T. (mobile-first) and Eleanor W. (75+, low-friction)"
dependencies:
  - "IAL2 registration story complete (Story 01)"
  - "OIDC IdP MFA module configured (PRD §6.3)"
  - "Push-notification infrastructure available (PRD §5.2 `NF-025`)"
  - "Risk-signal source configured (device posture, geo, velocity)"
acceptance_criteria:
  - "At first login, user enrolls ≥ 1 non-SMS-link MFA factor; biometric is offered on supported devices (PRD §5.3 `NF-030`)"
  - "Risk-based step-up triggers on configured signals; no CAPTCHA in normal flow (PRD §5.3 `NF-030`)"
  - "All MFA enrollment / change events written to immutable audit store within 5 minutes (PRD §5.4 `NF-032`)"
  - "Enrollment UI ships at parity on web, iOS, Android in the same release (PRD §13.9 F-080)"
  - "Enrollment UI meets WCAG 2.1 AA (PRD §5.1 `NF-010`)"
tasks:
  - "Implement biometric enrollment for iOS (Face ID / Touch ID) and Android (BiometricPrompt)"
  - "Implement TOTP authenticator and FIDO2/WebAuthn enrollment for web"
  - "Wire risk-signal evaluator into the IdP step-up policy"
  - "Emit MFA enrollment + change events to audit"
  - "Add unit + integration tests for enrollment + step-up + fallback"
  - "axe-core in CI; accessibility audit on enrollment UI"
  - "Feature-flag enrollment by cohort wave"
links:
  - "context (ingestion)/prd.md"
  - "documentation (output)/epics/epic-01-identity-authentication-account-recovery.md"
---

> **Author reminder:** Every story MUST link to its parent epic via `parent_epic` and cite the originating PRD section (e.g., `(PRD §<section>)`) when establishing acceptance criteria, NFRs, and telemetry. Stories without epic linkage and PRD citations should not be accepted into a sprint.

## User Story

**Trigger scenario:** A patient has just completed IAL2 proofing and is logging in for the first time. They expect a low-friction, modern auth experience on their phone (Marcus) or tablet (Eleanor), and the platform must satisfy the Phase 1 MFA-with-biometric requirement before granting PHI access.

As a **newly-proofed patient**, I can **enroll a biometric or other non-SMS-link MFA factor at first login** so that **subsequent logins are fast and resistant to phishing, while step-up still protects me on unfamiliar devices**.

## Acceptance Criteria (Gherkin-style)

| # | Scenario | Given | When | Then | PRD Source |
|---|----------|-------|------|------|------------|
| 1 | Biometric enrollment on supported device | A first-login user on iOS/Android with a configured biometric | They tap "Use biometric" | Biometric is enrolled, persisted, and a non-SMS-link factor is recorded as active | (PRD §5.3 `NF-030`) |
| 2 | Non-biometric alternative | A user on web or an unsupported device | They proceed past the first-login MFA step | A TOTP / WebAuthn enrollment is offered and completed; SMS-link is never offered as primary | (PRD §5.3 `NF-030`; §13.8 F-072) |
| 3 | Risk-based step-up | An enrolled user signs in from a new device + new geo | They submit credentials | They are challenged with a step-up factor; no CAPTCHA appears | (PRD §5.3 `NF-030`) |
| 4 | Audit completeness | Any MFA enrollment, change, or step-up event | The event occurs | An audit record is written to the immutable store within 5 minutes | (PRD §5.4 `NF-032`) |
| 5 | Mobile + web parity | The release ships to GA | The build is published | Enrollment is available on web, iOS, and Android in the same release | (PRD §13.9 F-080) |

## Non-Functional / Compliance Notes

- Performance: enrollment screens ≤ 1.5s p95 on common actions; mobile cold start ≤ 3s (PRD §5.2 `NF-026`, `NF-028`).
- Security: no static long-lived secrets; risk-signal source via workload identity (PRD §5.3 `NF-030e`; §5.4 `NF-039e`).
- Privacy: biometric template never leaves the device; only an opaque assertion is sent (platform default).
- Regulatory: HIPAA access control + audit (PRD §6.5; §5.4 `NF-032`); IAL2 binding context (PRD §5.3 `NF-030b`).
- Accessibility: WCAG 2.1 AA; high-contrast and ≥44pt touch targets on enrollment UI (PRD §5.1 `NF-010`, `NF-013`).

## Telemetry and Reporting

- Events emitted: `mfa.enrollment.started`, `mfa.enrollment.completed`, `mfa.factor.added`, `mfa.stepup.triggered`, `mfa.challenge.failed`.
- Metrics tracked: MFA coverage %, factor-mix (biometric / WebAuthn / TOTP / other), step-up trigger rate, challenge-failure rate.
- Dashboards / alerts: daily MFA coverage with alert on regression or SMS-only share above threshold (PRD §5.3 `NF-030`); failed-login + suspected credential-stuffing alert.
- Audit logging: every enrollment / change / step-up event in immutable audit ≥ 6yr retention (PRD §5.4 `NF-032`).

## Dependencies

- Upstream services: OIDC IdP MFA module; risk-signal source; push notifications; immutable audit store.
- Data sources / documents: device-posture provider, geo / velocity signals.
- Teams / sign-offs: CISO, Privacy Officer, Accessibility audit.
- Blocking stories or epics: Story 01 (IAL2 registration); Identity epic (parent).

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| 75+ cohort abandons at biometric step (R-ORG-03) | Med | High | Offer simple TOTP/WebAuthn alternative; in-clinic onboarding assistance; stratified-cohort monitoring (`NF-072`) | Health Equity + Product |
| Risk-engine false positives over-step-up legitimate users | Med | Med | Tunable policy + monitoring; bypass for known device after cool-down | Identity Platform |
| SMS-link factor accidentally introduced as a "fallback" | Low | High | CI gate from sibling story (Story 04) catches login URLs in SMS templates | Identity Platform |

## Rollout / Validation Checklist

- [ ] Unit tests added and passing
- [ ] Integration tests cover acceptance criteria scenarios
- [ ] Manual QA spot-check against source documents completed
- [ ] Telemetry verified in staging dashboard
- [ ] Security / compliance review signed off
- [ ] Feature flag / rollout plan defined (cohort waves; biometric-supported devices first)
- [ ] Documentation updated (runbooks, user guides)
- [ ] Parent epic acceptance criteria still satisfied

## Source References

- Parent epic: [epic-01-identity-authentication-account-recovery.md](../epic-01-identity-authentication-account-recovery.md)
- Source PRD: [context (ingestion)/prd.md](../../../context%20(ingestion)/prd.md)
- PRD sections cited: §5.1, §5.2, §5.3, §5.4, §5.8, §6.5, §13.1 F-003 / F-004, §13.8 F-072, §13.9 F-080, §8 R-ORG-03.
- Design / architecture docs: PRD §6.2 (Identity & Auth service).

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Confirm `parent_epic` points to a real epic file before opening the story for review.
- Each acceptance criterion, NFR, and telemetry metric must reference its PRD section in the `PRD Source` column or inline citation.
