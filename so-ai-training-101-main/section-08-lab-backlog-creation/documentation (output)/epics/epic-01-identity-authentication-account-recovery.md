---
title: "Identity, Authentication & Account Recovery (IAL2 + MFA + Biometric)"
summary: "Establish the patient and provider identity foundation for HealthConnect — IAL2 identity proofing, MFA with biometric and risk-based step-up, RBAC for staff, and PHI-safe account recovery — so every downstream capability inherits a compliant, equity-aware, anti-phishing trust anchor. Primary persona: all patient personas at registration; Dr. Alvarez and clinic staff for RBAC and shared-workstation flows."
owner: "Identity & Access Platform Team"
priority: "P0"
phase: "Phase 1 (Patient Foundation, Q3 2026 launch)"
personas:
  - "Linda R. — Chronic Condition Manager"
  - "Marcus T. — Busy Parent"
  - "Eleanor W. — Tech-Limited Senior (75+)"
  - "Dr. K. Alvarez — Primary Care Physician"
  - "Dr. R. Okonkwo — Specialist (Cardiology)"
okrs:
  objective: "Deliver a compliant, accessible, anti-phishing identity foundation that unblocks Phase 1 adoption and protects PHI across all personas."
  key_results:
    - description: "Patients completing first-time login successfully reach an authenticated session at IAL2"
      target: "≥ 95% completion rate across all age cohorts (including 75+)"
      timeframe: "First 90 days post-Phase-1 launch"
    - description: "MFA enrollment coverage of active patient accounts"
      target: "100% of active accounts enrolled in at least one non-SMS-link MFA factor"
      timeframe: "By Phase 1 GA"
    - description: "Account-recovery events completed without PHI-bearing helpdesk override"
      target: "100% (zero PHI override exceptions)"
      timeframe: "Ongoing from launch"
    - description: "Identity-related abandonment in registration / recovery flows for the 75+ cohort"
      target: "No negative variance vs. baseline cohorts (per `NF-072` equity guardrail)"
      timeframe: "First 6 months post-launch"
    - description: "Audit completeness for identity events (registration, MFA change, recovery, break-glass, privileged access)"
      target: "100% of events written to immutable audit store within 5 minutes (per `NF-032`)"
      timeframe: "From Phase 1 GA"
business_value: "Identity is the gating control for HIPAA compliance, anti-phishing trust, and adoption — without it, no Phase 1 capability can ship and `BO-1` (60% registered / 40% MAU) is unreachable."
success_metrics:
  - "First-time login success rate ≥ 95%, stratified by age / language / accessibility cohort (PRD §7.2, `NF-072`)"
  - "Zero HIPAA / OCR complaints attributable to identity / authentication (PRD §7.4)"
  - "Zero PHI exposures via helpdesk-driven account recovery (PRD §4.4 risk-driven req; `F-004`)"
  - "Identity-related helpdesk volume within tiered SLA (PRD §5.12, `NF-086`)"
  - "Adoption (registered + MAU) unblocked toward `BO-1` targets (PRD §2.1)"
regulatory_requirements:
  - "HIPAA — PHI access controls, audit, breach notification (PRD §6.5)"
  - "NIST 800-63-3 IAL2 patient identity proofing (PRD §5.3, `NF-030b`)"
  - "21st Century Cures Act / information-blocking — identity must not become a covert access barrier (PRD §5.9, `NF-074`)"
  - "DEA EPCS two-factor requirements for controlled-substance prescribers (PRD §6.5, `F-043` dependency)"
  - "State-privacy-law matrix for identity-data handling and notice (PRD §5.9, `NF-076`)"
security_considerations:
  - "MFA with biometric and risk-based step-up; **no CAPTCHA** in normal patient flows (PRD §5.3, `NF-030`)"
  - "RBAC with least privilege for providers/staff; workstation vs. personal-device session policy (PRD §5.3, `NF-030c`, `NF-030d`)"
  - "Service accounts use rotated credentials / workload identity (PRD §5.3, `NF-030e`)"
  - "Anti-phishing affordances; SMS never contains login links (PRD §5.4, `NF-034`; PRD §4.1, `F-072`)"
  - "Helpdesk-driven PHI account-recovery hardening — no override grants PHI-bearing access (PRD §4.4 risk-driven req; `F-004`)"
  - "Encryption in transit + at rest; centralized secrets management; KMS/HSM-backed keys (PRD §5.4, `NF-035`, `NF-036`, `NF-039e`)"
  - "Privileged-user access logging distinctly flagged in patient-visible audit (PRD §5.9, `NF-077`; PRD §4.1, `F-003`)"
  - "Pre-launch threat modeling on registration, recovery, proxy-link, and shared-workstation flows (PRD §8 R-SEC-01)"
dependencies:
  - "Identity-proofing vendor selection (PRD §10 decision 21; `A-033`)"
  - "OIDC + SMART on FHIR identity provider configured for third-party patient apps (PRD §6.3)"
  - "Epic MyChart linkage decision (PRD §10 decision 1) — affects credential federation model"
  - "Centralized secrets vault and KMS (PRD §5.4, `NF-036`, `NF-039e`)"
  - "Immutable audit store with ≥ 6yr retention (PRD §5.4, `NF-032`)"
  - "Helpdesk operating model + PHI-aware recovery process (PRD §10 decision 29; `A-034`)"
  - "Privacy Officer, CISO, Legal sign-off gates (PRD §5 Need-to-validate)"
  - "Accessibility audit vendor for identity flows (PRD §5.1, `NF-010`)"
  - "Multilingual onboarding content (PRD §5.12, `NF-087`; launch languages per `A-036`)"
  - "Legacy portal migration plan — first-time re-proofing flow (PRD §11.3)"
estimated_effort: "6-8 sprints (Phase 0 vendor selection + threat model, Phase 1 build through GA)"
monitoring_metrics:
  - "First-time login success rate, stratified by cohort (alert if any cohort < 90% over 7 days; per `NF-072`)"
  - "MFA enrollment coverage and factor mix (daily; alert on SMS-only > threshold)"
  - "Account-recovery completion rate and time-to-recovery (p50 / p90)"
  - "Identity-event audit-write latency (p95 ≤ 5 minutes per `NF-032`)"
  - "Privileged-user and break-glass event counts with anomaly detection (per `NF-079`)"
  - "Failed-login and suspected-credential-stuffing rate; risk-based step-up trigger rate (per `NF-030`)"
  - "Helpdesk identity-ticket volume vs. SLA tier (per `NF-086`)"
  - "Third-party SDK / tracking-tech inventory on identity pages = empty (per `NF-080b`, R-REG-01)"
acceptance_criteria:
  - "Patient registration completes with IAL2-equivalent proofing via at least two proofing paths (remote vendor + in-clinic); successful proofing yields an authenticated session and an audit entry (PRD §13.1 F-004; §5.3 `NF-030b`)"
  - "MFA is enrolled at first login using at least one non-SMS-link factor; biometric is offered on supported devices; risk-based step-up triggers on configured signals; CAPTCHA does not appear in normal patient flows (PRD §5.3 `NF-030`)"
  - "Account-recovery requests that cannot complete IAL2-equivalent verification do **not** receive PHI-bearing access; every recovery action is logged with method, evidence, and operator identity (PRD §13.1 F-004)"
  - "Provider/staff access is governed by RBAC with least privilege; workstation sessions use fast resume + auto-logout policy; personal-device sessions use the secure mobile chart view policy (PRD §5.2–5.3 `NF-022`, `NF-023`, `NF-030c`, `NF-030d`)"
  - "Every identity event (registration, MFA change, recovery, privileged access, break-glass) is written to the immutable audit store within 5 minutes and is visible to the patient via `F-003` where applicable (PRD §13.1 F-003, F-005; §5.4 `NF-032`)"
  - "All identity-flow SMS templates pass an automated CI check that rejects any template containing a login URL (PRD §13.8 F-072)"
  - "Identity surfaces (web + iOS + Android) meet WCAG 2.1 AA and pass independent accessibility audit; voice-call and in-clinic onboarding paths are available for the 75+ cohort (PRD §5.1 `NF-010`–`NF-017`; PRD §8 R-ORG-03)"
  - "Identity pages emit no third-party tracking SDK requests; telemetry follows the OCR-compliant baseline (PRD §5.10 `NF-080a`, `NF-080b`; PRD §8 R-REG-01)"
  - "Service accounts and integration credentials are rotated and managed via workload identity / centralized vault; no static long-lived secrets in code or config (PRD §5.3 `NF-030e`; §5.4 `NF-039e`)"
  - "Pre-launch threat model executed on registration, recovery, proxy-link, and shared-workstation flows with documented mitigations accepted by Security and Privacy (PRD §8 R-SEC-01)"
out_of_scope:
  - "Proxy / delegated-access lifecycle and family-account linkage — owned by the Family Accounts & Proxy Lifecycle epic (`F-001`, `F-002`, `F-003`)"
  - "Adolescent-privacy state transitions (`F-006`) — phase placement pending `A-007`"
  - "Break-glass workflow business rules beyond audit/notification primitives — owned by a separate Break-Glass & Privileged Access epic (`F-005`)"
  - "EPCS prescriber two-factor enrollment workflow — dependency of the Medications epic (`F-043`)"
  - "Granular sharing controls and sensitive-category re-consent — owned by the Privacy, Sharing & Consent epic (`F-095`, `NF-038`)"
  - "Migration of legacy passwords (explicitly destroyed; users re-enroll) — covered by the Legacy Migration epic (PRD §11.3)"
  - "Patient-facing autonomous AI symptom triage and any AI-driven identity decisioning (PRD §3.3 out-of-scope)"
stakeholders:
  - "Product Owner — Identity & Access"
  - "CISO / Security Engineering"
  - "Privacy Officer"
  - "Compliance / Legal"
  - "Clinical Informatics (provider RBAC + shared-workstation policy)"
  - "Clinical Operations (helpdesk model + cutover staffing)"
  - "Health Equity lead (cohort guardrails)"
  - "Accessibility lead / independent audit vendor"
  - "SRE (identity SLOs, audit-write latency)"
  - "Vendor mgmt (ID-proofing vendor, IdP)"
  - "QA / UAT"
links:
  - "context (ingestion)/prd.md"
---

> **Author reminder:** Cite the source PRD (`context (ingestion)/prd.md`) for every metric, target, regulatory requirement, and constraint referenced below. Use inline references like `(PRD §<section>)` so reviewers can trace each item to the originating requirement.

## Summary

HealthConnect needs a single, compliant identity foundation before any patient or provider capability can ship. This epic delivers IAL2 patient identity proofing, MFA with biometric and risk-based step-up, RBAC for providers and staff, anti-phishing-hardened account recovery, and immutable identity-event auditing — wired into the experience APIs so every downstream domain inherits a consistent trust anchor. Primary personas: all patient personas at registration and recovery; Dr. Alvarez and clinic staff for RBAC, shared-workstation, and privileged-access flows.

## OKRs

**Objective:** Deliver a compliant, accessible, anti-phishing identity foundation that unblocks Phase 1 adoption and protects PHI across all personas.

**Key Results** (3-5 measurable KRs):

- KR 1 — Description: "First-time login success at IAL2 across all cohorts" | Target: "≥ 95%" | Timeframe: "First 90 days post-Phase-1" | Source: "(PRD §7.2, `NF-072`; §5.3 `NF-030b`)"
- KR 2 — Description: "MFA enrollment coverage with a non-SMS-link factor" | Target: "100% of active accounts" | Timeframe: "By Phase 1 GA" | Source: "(PRD §5.3 `NF-030`)"
- KR 3 — Description: "Account-recovery events completed without PHI-bearing helpdesk override" | Target: "100%" | Timeframe: "Ongoing from launch" | Source: "(PRD §4.4 risk-driven req; §13.1 F-004)"
- KR 4 — Description: "75+ cohort identity-flow abandonment vs. baseline cohorts" | Target: "No negative variance" | Timeframe: "First 6 months" | Source: "(PRD §5.8 `NF-072`; §8 R-ORG-03)"
- KR 5 — Description: "Identity-event audit write latency" | Target: "p95 ≤ 5 minutes; 100% events captured" | Timeframe: "From GA" | Source: "(PRD §5.4 `NF-032`)"

## Objective and Business Value

Identity gates HIPAA compliance (PRD §6.5), unblocks the `BO-1` adoption target of 60% registered / 40% MAU (PRD §2.1), and is the anti-phishing trust anchor Eleanor W. and similar vulnerable cohorts depend on (PRD §3.1, §8 R-ORG-03). It is also the precondition for messaging, results release, prescriptions, billing, and proxy — without it, no Phase 1 capability can ship safely (PRD §1, §9.1). Equity-stratified success ensures the 75+ and accessibility-impaired cohorts are not silently excluded (PRD §2.1 BO-6; §5.8 `NF-072`).

## Personas Impacted

- Primary: **All patient personas** at registration, MFA enrollment, and account recovery — IAL2 proofing protects PHI; biometric + risk-based step-up minimizes friction (PRD §3.1).
- Primary: **Eleanor W. (75+)** — accessible identity flows + anti-phishing affordances + voice/in-clinic onboarding paths are launch requirements (PRD §3.1; §5.1 `NF-014`; §8 R-ORG-03).
- Primary: **Dr. K. Alvarez and clinic staff** — RBAC with least privilege, shared-workstation fast resume + auto-logout, and privileged-access auditing (PRD §3.1; §5.2–5.3 `NF-022`, `NF-030c`).
- Secondary: **Marcus T. and Linda R.** — biometric on registered devices minimizes login friction so high-frequency mobile use is viable (PRD §3.1; §5.3 `NF-030`).
- Secondary: **Dr. Okonkwo** — provider RBAC and EPCS prescriber two-factor are prerequisites for downstream specialist workflows (PRD §3.1; §6.5).

## Acceptance Criteria

- Patient registration completes with IAL2-equivalent proofing via at least two proofing paths (remote vendor + in-clinic); successful proofing yields an authenticated session and an audit entry (PRD §13.1 F-004; §5.3 `NF-030b`).
- MFA is enrolled at first login with at least one non-SMS-link factor; biometric is offered on supported devices; risk-based step-up triggers on configured signals; **no CAPTCHA** in normal patient flows (PRD §5.3 `NF-030`).
- Account-recovery requests that cannot complete IAL2-equivalent verification do not receive PHI-bearing access; the helpdesk has no override that grants PHI access; every recovery action is logged with method, evidence, and operator identity (PRD §13.1 F-004; §4.4 risk-driven req).
- Provider/staff access is governed by RBAC with least privilege; workstation sessions use fast resume + auto-logout; personal-device sessions use the secure mobile chart-view policy (PRD §5.2–5.3 `NF-022`, `NF-023`, `NF-030c`, `NF-030d`).
- All identity events (registration, MFA change, recovery, privileged access, break-glass primitives) are written to the immutable audit store within 5 minutes and surfaced to the patient via `F-003` where applicable (PRD §13.1 F-003, F-005; §5.4 `NF-032`).
- All identity-flow SMS templates pass an automated CI check that rejects any template containing a login URL (PRD §13.8 F-072).
- Identity surfaces (web, iOS, Android) meet WCAG 2.1 AA, pass independent accessibility audit, and provide voice-call and in-clinic onboarding paths for the 75+ cohort (PRD §5.1 `NF-010`–`NF-017`; §8 R-ORG-03).
- Identity pages emit no third-party tracking-SDK requests; telemetry follows the OCR-compliant baseline (PRD §5.10 `NF-080a`, `NF-080b`; §8 R-REG-01).
- Service accounts and integration credentials are rotated and managed via workload identity / centralized vault; no static long-lived secrets in code or config (PRD §5.3 `NF-030e`; §5.4 `NF-039e`).
- Pre-launch threat model executed on registration, recovery, proxy-link, and shared-workstation flows with documented mitigations accepted by Security and Privacy (PRD §8 R-SEC-01).

## Validation / QA Plan

- **Unit / service tests:** branch-coverage ≥ 80% on identity, MFA, recovery, RBAC modules per the safety-critical target (PRD §15.1).
- **Contract tests:** consumer-driven contracts with downstream services (Messaging, Results, Meds, Proxy) confirming session/RBAC claims propagation.
- **Integration tests:** end-to-end registration → MFA enroll → first login → recovery flows on web + iOS + Android, with mocked ID-proofing vendor and IdP.
- **FHIR / SMART conformance:** SMART on FHIR + OAuth 2.0 flow conformance for third-party patient apps (PRD §5.13 `NF-089b`).
- **Accessibility:** axe-core in CI on every PR; independent WCAG 2.1 AA audit pre-launch with remediation SLAs (PRD §5.1 `NF-010`; §15.1).
- **Performance:** identity surfaces meet `NF-026`–`NF-028` (cold start ≤ 3s mid-tier, common actions ≤ 1.5s p95); load-tested per `NF-029e`.
- **Security:** SAST/DAST/dep-scan in CI; pre-launch penetration test focused on auth, session, and recovery; secrets-scan gate (PRD §5.4 `NF-039d`; §15.1).
- **Privacy data-flow tests:** verify no PHI leaks to non-BAA destinations; verify no tracking SDK on identity pages (PRD §15.1; §5.10 `NF-080b`).
- **UAT:** representative patient cohorts including 75+ and low-vision users (per `NF-095`); provider + staff cohorts for RBAC and shared-workstation flows.
- **Compliance gate:** Privacy Officer, CISO, and Legal sign-off before GA; helpdesk PHI-recovery process tabletop exercise (PRD §10 decision 29; `A-034`).
- **Equity validation:** stratified pilot metrics reviewed before broader rollout (PRD §16 pilot framework; §5.8 `NF-072`).

## Monitoring and Metrics

- First-time login success rate, stratified by age / language / accessibility cohort — alert if any cohort < 90% over a rolling 7-day window (PRD §5.8 `NF-072`).
- MFA enrollment coverage and factor mix — daily snapshot; alert on regression or SMS-only share above threshold (PRD §5.3 `NF-030`).
- Account-recovery completion rate, time-to-recovery (p50 / p90), and PHI-override-attempt count (target: 0) (PRD §13.1 F-004).
- Identity-event audit-write latency p95 ≤ 5 minutes; 100% capture coverage (PRD §5.4 `NF-032`).
- Privileged-user and break-glass event counts with anomaly detection (PRD §5.9 `NF-077`, `NF-079`).
- Failed-login rate and risk-based step-up trigger rate; suspected credential-stuffing detection (PRD §5.3 `NF-030`).
- Helpdesk identity-ticket volume vs. SLA tier (PRD §5.12 `NF-086`).
- Automated third-party-request inventory on identity pages = empty (PRD §5.10 `NF-080b`; §8 R-REG-01).
- Per-capability SLO dashboards tied to error budgets and surfaced on the status page (PRD §5.2 `NF-029d`).

## Out of Scope

- Proxy / delegated-access lifecycle, family-account linkage, and patient-visible audit UX — owned by the Family Accounts & Proxy Lifecycle epic (`F-001`, `F-002`, `F-003`).
- Adolescent-privacy state transitions (`F-006`) — phase placement pending `A-007`.
- Break-glass clinical access business rules beyond audit/notification primitives — owned by a separate Break-Glass & Privileged Access epic (`F-005`).
- EPCS prescriber two-factor enrollment workflow — dependency of the Medications epic (`F-043`).
- Granular sharing controls and sensitive-category re-consent — owned by the Privacy, Sharing & Consent epic (`F-095`, `NF-038`).
- Legacy password migration — passwords are not migrated; users re-enroll at first login (PRD §11.3).
- Any patient-facing autonomous AI identity decisioning (PRD §3.3 out-of-scope).

## Dependencies

- Identity-proofing vendor selected and contracted (PRD §10 decision 21; `A-033`).
- OIDC + SMART on FHIR identity provider configured (PRD §6.3; §5.13 `NF-089b`).
- Epic MyChart linkage decision resolved to clarify credential federation model (PRD §10 decision 1).
- Centralized secrets vault and KMS/HSM available (PRD §5.4 `NF-036`, `NF-039e`).
- Immutable audit store with ≥ 6yr retention provisioned (PRD §5.4 `NF-032`).
- Helpdesk operating model + PHI-aware recovery process approved (PRD §10 decision 29; `A-034`; §5.12 `NF-086`).
- Independent accessibility audit vendor engaged (PRD §5.1 `NF-010`).
- Multilingual onboarding content for launch languages (PRD §5.12 `NF-087`; `A-036`).
- Legacy migration plan for first-time re-proofing (PRD §11.3).
- Privacy Officer, CISO, Legal sign-off gates established (PRD §5 Need-to-validate).

## Stakeholders / Reviewers

- Owner: Identity & Access Platform Team product owner
- Product: HealthConnect Product lead
- Engineering: Identity & Access Platform Team; Mobile (iOS, Android); Web; SRE
- Compliance / Regulatory: Privacy Officer; Compliance; Legal
- QA: QA lead; independent accessibility audit vendor; external pen-test partner
- Other reviewers: CISO; Clinical Informatics; Clinical Operations (helpdesk); Health Equity lead; Vendor management

## Notes and Links

- Source PRD: [context (ingestion)/prd.md](../../context%20(ingestion)/prd.md)
- Key PRD sections: §2.1 BO-1 / BO-6, §3.1 personas, §4.1 Identity & Access (F-001–F-006), §4.4 risk-driven reqs, §5.1 Accessibility, §5.2 Performance, §5.3 Authentication, §5.4 Data Security, §5.8 Measurement Guardrails, §5.9 Compliance, §5.10 Observability, §5.12 Training/Helpdesk, §5.13 Interop, §6.3 Architecture, §8 risks R-SEC-01 / R-REG-01 / R-ORG-03, §11.3 Migration, §13.1 Acceptance Criteria for F-001–F-006, §15 Testing Strategy.
- Architecture diagrams: see PRD §6.2 logical architecture (Identity & Auth service).
- Related epics / stories:
  - Family Accounts, Proxy Lifecycle & Patient-Visible Audit Log (consumes session + audit primitives)
  - Break-Glass & Privileged Access (extends auditing surface)
  - Legacy Portal Migration & Phased Cutover (first-time re-proofing flow)
  - Privacy, Sharing & Consent (consumes identity claims for sensitive-category controls)
  - All Phase 1 domain epics (Messaging, Results, Appointments, Medications, Billing) depend on this epic for session + RBAC claims.
- Additional references: NIST 800-63-3 IAL2, SMART on FHIR, ONC HTI-1/HTI-2, OCR online-tracking guidance.

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Every numeric target, regulatory requirement, and security control must cite the source PRD section it derives from.
- Keep the YAML frontmatter and narrative sections in sync — planning tools read the frontmatter; humans read the body.
