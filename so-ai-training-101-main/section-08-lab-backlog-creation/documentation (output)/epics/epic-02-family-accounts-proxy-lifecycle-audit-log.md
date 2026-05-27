---
title: "Family Accounts, Proxy Lifecycle & Patient-Visible Audit Log"
summary: "Deliver the family-account, delegated-proxy, and patient-visible audit-log foundation: a single account with linked dependents, a full proxy lifecycle (grant / modify / revoke / time-bound expiration), and a patient-facing audit log that exposes every PHI access — including proxy, privileged, and break-glass events. Primary personas: Marcus T. (family management), Eleanor W. (granddaughter caregiver, anti-scam audit visibility), and all patients who need transparent oversight of who is seeing their record."
owner: "Identity & Access Platform Team — Family & Proxy squad"
priority: "P0"
phase: "Phase 1 (Patient Foundation, Q3 2026 launch) — proxy MVP; scoped caregiver expansion → Phase 2"
personas:
  - "Marcus T. — Busy Parent"
  - "Eleanor W. — Tech-Limited Senior (75+)"
  - "Linda R. — Chronic Condition Manager (sensitive-category sharing context)"
  - "Dr. K. Alvarez — Primary Care Physician (provider-visible attribution)"
okrs:
  objective: "Make multi-account caregiving and oversight safe, auditable, and one-tap simple — without leaking sensitive-category data through proxy paths."
  key_results:
    - description: "Time from delegator grant to delegate having access (and both parties notified)"
      target: "≤ 5 minutes p95"
      timeframe: "From Phase 1 GA"
    - description: "Time from revocation to access removal"
      target: "≤ 60 seconds p95; both parties notified"
      timeframe: "From Phase 1 GA"
    - description: "Patient-visible audit-log completeness for PHI access (proxy, privileged, break-glass, integration)"
      target: "100% of PHI accesses logged within 5 minutes of the access event"
      timeframe: "From Phase 1 GA"
    - description: "Sensitive-category sharing violations through proxy paths"
      target: "0 (zero) confirmed violations"
      timeframe: "Ongoing from launch"
    - description: "Marcus-persona task — switching between own and dependent accounts to perform a Phase 1 task"
      target: "One tap/click; sub-3-tap to complete the downstream task"
      timeframe: "From Phase 1 GA"
business_value: "Family / proxy is the activation gate for the Marcus persona (BO-1 adoption) and the trust gate for the Eleanor persona (BO-6 equity). Patient-visible audit is the safety net that makes broader proxy expansion in Phase 2 organizationally and legally tenable."
success_metrics:
  - "Proxy grant / revoke / expiration SLAs met (PRD §13.1 F-002)"
  - "Patient-visible audit log shows every PHI access including proxy/privileged/break-glass within 5 minutes (PRD §13.1 F-003; §5.4 `NF-032`)"
  - "Zero sensitive-data sharing violations (PRD §7.4)"
  - "Family-account adoption supports `BO-1` (60% registered / 40% MAU) and `BO-6` equity targets (PRD §2.1)"
  - "Audit-review anomaly investigation rate = 100% within SLA (PRD §7.4; §5.9 `NF-079`)"
regulatory_requirements:
  - "HIPAA Privacy / Security — access controls, audit, sensitive-category protections (PRD §6.5; §5.4 `NF-038`)"
  - "21st Century Cures Act / information-blocking — proxy lifecycle must not become a covert access barrier (PRD §5.9 `NF-074`)"
  - "42 CFR Part 2 (if SUD in scope) — segmentation enforcement through proxy paths (PRD §5.9 `NF-075`)"
  - "State-privacy-law matrix for proxy / guardianship and minor / adolescent thresholds (PRD §5.9 `NF-076`; §4.1 `F-006`; §10 decisions 8, 16, 17)"
  - "Co-equal parent / split-custody policy (PRD §10 decision 16; `A-006`)"
  - "Immutable audit retention ≥ 6 years (PRD §5.4 `NF-032`; §5.6 `NF-052`)"
security_considerations:
  - "Proxy lifecycle requires explicit evidence of relationship/guardianship per configured policy (PRD §13.1 F-002)"
  - "Time-bound proxy expiration and explicit revoke — no permanent default grants (PRD §13.1 F-002; §8 R-SEC-01)"
  - "Sensitive-category access through proxy requires elevated controls / re-consent (PRD §5.4 `NF-038`; §4.1 `F-095`)"
  - "Pre-launch threat modeling on proxy grant, modify, revoke, and dependent-switching flows (PRD §8 R-SEC-01)"
  - "Audit log is append-only, immutable, integrity-protected, ≥ 6yr retention (PRD §5.4 `NF-032`)"
  - "Privileged-user and break-glass events distinctly flagged in patient-visible audit (PRD §5.9 `NF-077`; §13.1 F-003, F-005)"
  - "Vulnerable-population / shared-device safeguards in proxy flows (PRD §5.7 `NF-061`)"
  - "Anti-phishing affordances on grant / revoke notifications; SMS never contains login links (PRD §5.4 `NF-034`; §4.1 `F-072`)"
dependencies:
  - "Identity, Authentication & Account Recovery epic (IAL2 identity, MFA, session/RBAC claims)"
  - "Immutable audit store with ≥ 6yr retention (PRD §5.4 `NF-032`)"
  - "Privacy, Sharing & Consent epic — sensitive-category classifier and `F-095` controls"
  - "Notifications & Channel Preferences epic — proxy grant/revoke/expiration notifications (`F-070`, `F-072`)"
  - "All Phase 1 domain services (Messaging, Results, Medications, Appointments, Billing) must emit audit events and honor proxy/RBAC claims"
  - "Legacy migration plan — legacy proxy relationships are NOT auto-trusted; require re-validation (PRD §11.3, R-MIG-02)"
  - "State-privacy-law matrix + co-equal-parent / split-custody policy decisions (PRD §10 decisions 8, 16, 17)"
  - "Adolescent-privacy launch states for `F-006` (PRD §10 decision 17; `A-007`)"
  - "Helpdesk operating model — proxy disputes / re-establishment workflows (PRD §10 decision 29; `A-034`)"
  - "Privacy Officer, Legal, Health Equity sign-off gates"
estimated_effort: "6-8 sprints (Phase 1 single-account + linked dependents + proxy lifecycle MVP + patient-visible audit; scoped caregiver expansion deferred to Phase 2)"
monitoring_metrics:
  - "Proxy grant → access latency p95 ≤ 5 minutes; revoke → access removal p95 ≤ 60 seconds (PRD §13.1 F-002)"
  - "Audit-event write latency p95 ≤ 5 minutes; capture coverage = 100% (PRD §5.4 `NF-032`)"
  - "Sensitive-category access events through proxy — count + alert on any anomaly (PRD §5.9 `NF-079`; §5.4 `NF-038`)"
  - "Break-glass and privileged-access event counts with anomaly detection and review SLA = 100% (PRD §5.9 `NF-077`, `NF-079`; §13.1 F-005)"
  - "Proxy expiration auto-removal events logged 100% of the time"
  - "Account-switcher usage by Marcus-like users — adoption signal toward `BO-1` (PRD §2.1)"
  - "Patient-visible audit-log view rate by Eleanor-like (75+) cohort — equity signal (PRD §5.8 `NF-072`)"
  - "Proxy-related helpdesk ticket volume vs. SLA tier (PRD §5.12 `NF-086`)"
  - "Third-party tracking SDK requests on proxy / audit pages = 0 (PRD §5.10 `NF-080b`)"
acceptance_criteria:
  - "Given a patient with at least one verified linked dependent, when they log in, then a UI affordance shows all accounts they can act on and switching is one tap/click (PRD §13.1 F-001)"
  - "Given a logged-in user acting on behalf of a dependent, when they perform any action that writes to the record, then the audit log records both the actor identity and the patient identity (PRD §13.1 F-001)"
  - "Given a patient (delegator), when they grant proxy access, then the system requires evidence of relationship/guardianship per the configured policy and both parties receive notification within 5 minutes (PRD §13.1 F-002)"
  - "Given an active proxy grant, when the delegator (or, in defined scenarios, the delegate) revokes it, then access is removed within 60 seconds and both parties are notified (PRD §13.1 F-002)"
  - "Given a proxy grant with a time-bound expiration, when the expiration time is reached, then access is automatically removed and the audit log records the expiration event (PRD §13.1 F-002)"
  - "Every grant, modification, revocation, and expiration event is queryable by the patient via `F-003` within 5 minutes (PRD §13.1 F-002)"
  - "Given a patient, when they open the audit log, then they see entries for every PHI-record access including proxy, privileged-user, and break-glass entries, with actor identity (or role), timestamp, action, and record category (PRD §13.1 F-003)"
  - "Privileged-user entries are distinctly flagged; audit-log entries are read-only from the patient surface (PRD §13.1 F-003)"
  - "Sensitive-category data is gated by `F-095` / `NF-038`; proxy access to sensitive categories requires elevated controls / re-consent (PRD §5.4 `NF-038`; §8 R-SEC-01)"
  - "Anti-phishing affordances applied to grant/revoke/expiration notifications; SMS templates contain no login URLs and fail CI if they do (PRD §13.8 F-072; §5.4 `NF-034`)"
  - "Family-account + proxy surfaces ship at parity on web, iOS, and Android in the same release; meet WCAG 2.1 AA (PRD §13.9 F-080; §5.1 `NF-010`–`NF-013`)"
  - "Pre-launch threat model executed on grant, modify, revoke, dependent-switching, and audit-view flows with documented mitigations accepted by Security and Privacy (PRD §8 R-SEC-01)"
  - "Audit pages and proxy surfaces emit zero third-party tracking-SDK requests (PRD §5.10 `NF-080a`, `NF-080b`; §8 R-REG-01)"
  - "Legacy proxy grants are NOT auto-trusted at migration; each existing relationship is re-validated through the new lifecycle (PRD §11.3, R-MIG-02)"
out_of_scope:
  - "IAL2 identity proofing, MFA enrollment, account recovery — owned by the Identity, Authentication & Account Recovery epic (`F-004`, `NF-030`–`NF-030b`)"
  - "Scoped caregiver-access expansion (`F-111`) — Phase 2"
  - "Adolescent-privacy state transitions (`F-006`) — phase placement pending `A-007`, owned in coordination with Privacy epic"
  - "Break-glass clinical access business rules (`F-005`) — owned by a separate Break-Glass & Privileged Access epic; this epic only consumes its audit events for the patient-visible log"
  - "Granular sharing UX and sensitive-category re-consent (`F-095`, `F-097`, `F-098`) — owned by the Privacy, Sharing & Consent epic; consumed here as gating policy"
  - "Parent audit-log feature for adolescent / dependent records (`F-206`) — nice-to-have, Phase 2–3"
  - "Co-equal-parent and split-custody policy authoring (`A-006`) — policy ownership sits with Legal/Compliance; this epic implements the resolved policy"
  - "Cross-org / TEFCA proxy or guardianship records ingestion (PRD §3.3 out-of-scope for Phase 1)"
stakeholders:
  - "Product Owner — Family & Proxy"
  - "Privacy Officer"
  - "Legal / Compliance (guardianship, split-custody, state matrix)"
  - "CISO / Security Engineering (proxy threat model)"
  - "Clinical Informatics (sensitive-category classifier inputs)"
  - "Clinical Operations (helpdesk proxy disputes)"
  - "Health Equity lead (Marcus + Eleanor cohort outcomes)"
  - "Accessibility lead / independent audit vendor"
  - "Engineering: Identity & Access Platform; Web; iOS; Android; SRE"
  - "Domain leads: Messaging, Results, Appointments, Medications, Billing, Notifications, Audit"
  - "QA / UAT"
links:
  - "context (ingestion)/prd.md"
---

> **Author reminder:** Cite the source PRD (`context (ingestion)/prd.md`) for every metric, target, regulatory requirement, and constraint referenced below. Use inline references like `(PRD §<section>)` so reviewers can trace each item to the originating requirement.

## Summary

This epic delivers the family-account, proxy-lifecycle, and patient-visible audit foundation that Phase 1 needs to be safely usable by parents and caregivers. It ships single-account-with-linked-dependents, a full proxy lifecycle (grant, modify, revoke, time-bound expiration), and a patient-visible audit log that surfaces every PHI access — including proxy, privileged-user, and break-glass entries. Primary personas: Marcus T. (parent managing three kids on mobile), Eleanor W. (senior whose granddaughter helps), with Linda R. and Dr. Alvarez as secondary contexts for sensitive-category sharing and provider-visible attribution (PRD §3.1, §13.1 F-001–F-003).

## OKRs

**Objective:** Make multi-account caregiving and oversight safe, auditable, and one-tap simple — without leaking sensitive-category data through proxy paths.

**Key Results** (3-5 measurable KRs):

- KR 1 — Description: "Grant → access + both-party notification" | Target: "≤ 5 minutes p95" | Timeframe: "From GA" | Source: "(PRD §13.1 F-002)"
- KR 2 — Description: "Revocation → access removal + both-party notification" | Target: "≤ 60 seconds p95" | Timeframe: "From GA" | Source: "(PRD §13.1 F-002)"
- KR 3 — Description: "Patient-visible audit completeness for PHI access (proxy, privileged, break-glass)" | Target: "100% within 5 minutes" | Timeframe: "From GA" | Source: "(PRD §13.1 F-003; §5.4 `NF-032`)"
- KR 4 — Description: "Sensitive-category sharing violations through proxy paths" | Target: "0 confirmed violations" | Timeframe: "Ongoing" | Source: "(PRD §7.4; §5.4 `NF-038`; §8 R-SEC-01)"
- KR 5 — Description: "Account-switch UX for Marcus persona to downstream task" | Target: "One tap to switch; sub-3-tap to complete task" | Timeframe: "From GA" | Source: "(PRD §13.1 F-001; §5.1 `NF-015`)"

## Objective and Business Value

Family / proxy is the activation gate for Marcus (drives `BO-1` adoption among households) and the trust gate for Eleanor (drives `BO-6` equity by giving caregivers a safe path and giving patients visible oversight). The patient-visible audit log is the safety net that makes broader caregiver expansion (`F-111` in Phase 2) organizationally, legally, and clinically defensible. Without proxy lifecycle and audit visibility, the program cannot expand beyond single-patient adults without unacceptable privacy risk (PRD §1; §2.1 BO-1, BO-6; §8 R-SEC-01).

## Personas Impacted

- Primary: **Marcus T.** — single login managing self + three kids; one-tap account switch; unified family appointment view + consolidated billing entry; mobile parity (PRD §3.1; F-001, F-032, F-150, F-080 dependencies).
- Primary: **Eleanor W.** — grants scoped, time-bound proxy to her granddaughter; sees every access her granddaughter makes; anti-scam audit signals visible on home (PRD §3.1; F-002, F-003, F-191).
- Primary (oversight): **All patients** — patient-visible audit log gives every patient transparent oversight of who is seeing their record (PRD §13.1 F-003).
- Secondary: **Linda R.** — sensitive-category sharing context; proxy access to behavioral-health or other sensitive records requires elevated controls / re-consent (PRD §3.1; UC-08; §5.4 `NF-038`).
- Secondary: **Dr. Alvarez / Dr. Okonkwo** — provider actions on behalf of a patient record produce attribution that appears in the patient-visible audit; privileged-user entries are flagged distinctly (PRD §13.1 F-003; §5.9 `NF-077`).

## Acceptance Criteria

- Given a patient with at least one verified linked dependent, when they log in, then a UI affordance shows all accounts they can act on and switching is one tap/click (PRD §13.1 F-001).
- Given a logged-in user acting on behalf of a dependent, when they perform any record-writing action, then audit captures both actor identity and patient identity (PRD §13.1 F-001).
- Proxy grant requires evidence of relationship/guardianship per configured policy; both parties notified within 5 minutes (PRD §13.1 F-002).
- Revocation removes access within 60 seconds and notifies both parties; defined scenarios allow delegate-initiated revoke (PRD §13.1 F-002).
- Time-bound expiration auto-removes access at the expiration moment and logs the expiration event (PRD §13.1 F-002).
- Every grant / modify / revoke / expiration event is queryable by the patient via `F-003` within 5 minutes (PRD §13.1 F-002).
- Patient-visible audit log surfaces all PHI accesses including proxy, privileged-user, and break-glass entries, with actor identity (or role), timestamp, action, and record category (PRD §13.1 F-003).
- Privileged-user entries are distinctly flagged; audit-log entries are read-only from the patient surface (PRD §13.1 F-003).
- Sensitive-category data is gated by `F-095` / `NF-038`; proxy access to sensitive categories requires elevated controls / re-consent (PRD §5.4 `NF-038`; §8 R-SEC-01).
- Grant / revoke / expiration notifications use anti-phishing-hardened templates; SMS contains no login URLs and fails CI if it does (PRD §13.8 F-072; §5.4 `NF-034`).
- Family-account + proxy + audit surfaces ship at parity on web, iOS, and Android in the same release and meet WCAG 2.1 AA (PRD §13.9 F-080; §5.1 `NF-010`–`NF-013`).
- Pre-launch threat model executed on grant, modify, revoke, dependent-switching, and audit-view flows; mitigations accepted by Security and Privacy (PRD §8 R-SEC-01).
- Proxy and audit pages emit zero third-party tracking-SDK requests (PRD §5.10 `NF-080a`, `NF-080b`; §8 R-REG-01).
- Legacy proxy grants are not auto-trusted at migration; each relationship is re-validated through the new lifecycle (PRD §11.3, R-MIG-02).

## Validation / QA Plan

- **Unit / service tests:** branch coverage ≥ 80% on family-link, proxy-lifecycle, sensitive-category gating, and audit-write modules (PRD §15.1 safety-critical target).
- **Contract tests:** consumer-driven contracts with every domain service that emits audit events or honors proxy/RBAC claims (Messaging, Results, Medications, Appointments, Billing, Notifications).
- **Integration tests:** end-to-end grant → notify → access → revoke → access-removed → expiration scenarios across web, iOS, Android; including delegator-initiated and delegate-initiated revoke paths.
- **Privacy data-flow tests:** sensitive-category access through proxy is blocked or requires explicit re-consent; no PHI to non-BAA destinations from proxy/audit telemetry (PRD §5.4 `NF-038`; §5.10 `NF-080a`, `NF-080b`).
- **Security:** SAST/DAST/dep-scan in CI; pre-launch pen test focused on proxy escalation, IDOR, and audit-tamper paths; pre-launch threat model accepted by Security + Privacy (PRD §5.4 `NF-039d`; §8 R-SEC-01).
- **Accessibility:** axe-core on every PR; independent WCAG 2.1 AA audit on proxy + audit surfaces; usability sessions with low-vision and elderly users for the audit-view experience (PRD §5.1 `NF-010`; §5.15 `NF-095`).
- **Performance:** grant/revoke latency, audit-write latency, audit-query latency validated against SLOs; load-tested per `NF-029e`.
- **Compliance gates:** Privacy Officer, Legal, and CISO sign-off before GA; tabletop on proxy-dispute / helpdesk-assisted re-establishment with Clinical Operations (PRD §10 decision 29; `A-034`).
- **UAT:** Marcus-like (parent + dependents) and Eleanor-like (delegator + delegate granddaughter) cohorts plus a sensitive-category scenario for Linda-like users.
- **Equity validation:** stratified adoption + audit-view usage reviewed before broader rollout (PRD §5.8 `NF-072`; §16 pilot framework).
- **Migration validation:** R-MIG-02 re-validation flow tested end-to-end with extended grace period and helpdesk-assisted recovery (PRD §11.3).

## Monitoring and Metrics

- Grant → access latency p95 ≤ 5 minutes; revoke → access-removed p95 ≤ 60 seconds; both-party notification delivery success ≥ 99% (PRD §13.1 F-002; §5.4 `NF-031`).
- Audit-event write latency p95 ≤ 5 minutes; capture coverage = 100% across all PHI-bearing domain services (PRD §5.4 `NF-032`).
- Sensitive-category proxy access events — count + anomaly alert on any unexpected pattern (PRD §5.9 `NF-079`; §5.4 `NF-038`).
- Break-glass and privileged-access event counts with anomaly detection; investigation-within-SLA = 100% (PRD §5.9 `NF-077`, `NF-079`; §7.4).
- Proxy expiration auto-removal events logged 100% of the time; alert on any missed expiration.
- Account-switcher usage by Marcus-like users — feature adoption indicator toward `BO-1` (PRD §2.1).
- Patient-visible audit-log view rate stratified by cohort, with focus on 75+ adoption indicator toward `BO-6` (PRD §5.8 `NF-072`).
- Proxy-related helpdesk ticket volume vs. SLA tier; alert on cutover-window surges (PRD §5.12 `NF-086`; §11.4).
- Third-party tracking-SDK requests on proxy / audit pages = 0 (PRD §5.10 `NF-080b`; §8 R-REG-01).
- Per-capability SLO error-budget consumption on proxy + audit endpoints (PRD §5.2 `NF-029d`).

## Out of Scope

- IAL2 identity proofing, MFA, account recovery — owned by the Identity, Authentication & Account Recovery epic (`F-004`, `NF-030`–`NF-030b`).
- Scoped caregiver-access expansion (`F-111`) — Phase 2.
- Adolescent-privacy state transitions (`F-006`) — pending `A-007`; jointly owned with Privacy & Consent epic.
- Break-glass clinical access business rules (`F-005`) — owned separately; this epic consumes its audit events for the patient-visible log only.
- Granular sharing UX and sensitive-category re-consent (`F-095`, `F-097`, `F-098`) — owned by the Privacy, Sharing & Consent epic; consumed here as gating policy.
- Parent audit-log for adolescent / dependent records (`F-206`) — nice-to-have, Phase 2–3.
- Co-equal-parent and split-custody policy authoring (`A-006`) — Legal/Compliance own the policy; this epic implements it once resolved.
- Cross-org / TEFCA proxy or guardianship ingestion (PRD §3.3 out-of-scope).

## Dependencies

- Identity, Authentication & Account Recovery epic (IAL2 identity, MFA, session, RBAC).
- Immutable audit store with ≥ 6yr retention (PRD §5.4 `NF-032`).
- Privacy, Sharing & Consent epic — sensitive-category classifier + `F-095` gating.
- Notifications & Channel Preferences epic — grant/revoke/expiration notifications honoring `F-070`, `F-072`.
- All Phase 1 domain services emitting audit events and honoring proxy/RBAC claims.
- Legacy migration plan — R-MIG-02 re-validation flow (PRD §11.3).
- State-privacy-law matrix + co-equal-parent / split-custody policy decisions (PRD §10 decisions 8, 16, 17).
- Adolescent-privacy launch-states decision for `F-006` (PRD §10 decision 17; `A-007`).
- Helpdesk operating model for proxy disputes (PRD §10 decision 29; `A-034`).
- Privacy Officer, Legal, CISO, and Health Equity sign-off gates.

## Stakeholders / Reviewers

- Owner: Family & Proxy product owner
- Product: HealthConnect Product lead
- Engineering: Identity & Access Platform; Web; iOS; Android; SRE; Audit / Logging platform
- Compliance / Regulatory: Privacy Officer; Legal; Compliance
- QA: QA lead; independent accessibility audit vendor; external pen-test partner
- Other reviewers: CISO; Clinical Informatics; Clinical Operations (helpdesk); Health Equity lead; Design/UX; Domain leads for Messaging / Results / Appointments / Medications / Billing / Notifications

## Notes and Links

- Source PRD: [context (ingestion)/prd.md](../../context%20(ingestion)/prd.md)
- Key PRD sections: §2.1 (BO-1, BO-6), §3.1 personas (Marcus, Eleanor), §3.2 use cases UC-03, UC-06, UC-08, §3.3 out-of-scope, §4.1 Identity & Access (F-001–F-003), §4.1 Privacy (F-095, F-097), §5.1 Accessibility, §5.4 Data Security & Privacy (`NF-031`, `NF-032`, `NF-034`, `NF-038`), §5.7 Patient Safety (`NF-061`), §5.8 Equity (`NF-072`), §5.9 Compliance (`NF-074`–`NF-077`, `NF-079`), §5.10 Observability (`NF-080a`, `NF-080b`), §5.12 Helpdesk (`NF-086`), §6.2 logical architecture (Proxy / Family + Audit / Logging services), §8 risks R-SEC-01 / R-REG-01 / R-ORG-03, §10 decisions 8 / 16 / 17 / 29, §11 migration §11.3 + R-MIG-02, §13.1 Acceptance Criteria F-001–F-003.
- Architecture diagrams: PRD §6.2 — Identity & Auth + Proxy/Family + Consent/Sharing + Audit/Logging services.
- Related epics / stories:
  - Identity, Authentication & Account Recovery (upstream)
  - Privacy, Sharing & Consent (sensitive-category gating, `F-095`)
  - Break-Glass & Privileged Access (audit-event producer consumed here)
  - Notifications, Channel Preferences & Anti-Phishing Safeguards (grant/revoke notifications)
  - Unified Patient Dashboard (account switcher + audit entry point on the home)
  - Consolidated Billing, Self-Service Scheduling, Secure Messaging, Lab Results, Prescription Management (all emit audit events and honor proxy claims)
  - Legacy Portal Migration & Phased Cutover (R-MIG-02 re-validation)
- Additional references: HIPAA Privacy/Security Rule, 21st Century Cures Act / information-blocking, 42 CFR Part 2 (if applicable), state-by-state guardianship and minor/adolescent thresholds.

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Every numeric target, regulatory requirement, and security control must cite the source PRD section it derives from.
- Keep the YAML frontmatter and narrative sections in sync — planning tools read the frontmatter; humans read the body.
