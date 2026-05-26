# Requirements Gap Analysis

**Date:** May 21, 2026
**Author:** M. Mettler
**Inputs:** [00-healthcare-portal-reference.md](../input/00-healthcare-portal-reference.md), all interview notes in [output/interview-notes/](interview-notes/), all requirements extracts in [output/requirements-extracts/](requirements-extracts/), conflict consolidation in [requirements-conflicts-and-resolutions.md](requirements-extracts/requirements-conflicts-and-resolutions.md)
**Status:** Draft — input for Phase 2 synthesis and the next round of stakeholder discovery

> Personas interviewed surfaced strong patient- and provider-facing requirements, but a number of operational, security, compliance, and lifecycle areas have not been covered. This document identifies those gaps and proposes candidate requirements to fill them. Each proposed requirement uses a `G-*` ID so it's traceable until it's promoted into the canonical PRD numbering.
>
> **Important:** these gaps are not new ideas — most are implied by the product brief, regulatory environment, or standard healthcare-IT practice. The interviews simply did not include the right stakeholders to cover them. Several of these gaps suggest **additional stakeholders we need to interview** before locking the PRD.

---

## How to read this document

For each gap area:
- **What's missing** — the gap relative to existing requirements
- **Why it matters** — risk / impact if unaddressed
- **Proposed requirements** — candidate `G-*` requirements to fill the gap
- **Stakeholders to engage** — who needs to be interviewed or consulted to validate

---

## 1. User Authentication & Authorization

### What's missing

Existing extracts touch on patient-side login friction (Eleanor: CAPTCHA, Linda: scam fears) and the broader auth conflict has a proposed resolution. But there is no comprehensive treatment of:
- Patient identity proofing at registration
- Account recovery flows (forgot password, lost device, lost phone number)
- Proxy/delegate access lifecycle (granting, modifying, revoking, expiring)
- Adolescent privacy state transitions (technical model, not just UX flow)
- Provider authentication and role-based access control (RBAC)
- Service / system account model for integrations
- Session management policies
- Break-glass / emergency access for clinicians

### Why it matters

- HIPAA Security Rule requires defined access controls, unique user IDs, and emergency-access procedures.
- Identity proofing failures lead to fraudulent account takeover and PHI breach.
- Account recovery is the most common point of social-engineering attack in healthcare portals.
- Adolescent-privacy and proxy lifecycles drive significant regulatory and legal exposure.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-AUTH-01 | Patient identity proofing at registration meets NIST 800-63-3 IAL2 minimum (e.g., in-clinic proofing, KBA, or remote-ID verification via approved vendor). | NF |
| G-AUTH-02 | MFA required for all PHI-bearing account access; biometric on registered devices counts as a factor. | NF |
| G-AUTH-03 | Account recovery flow requires identity re-verification at IAL2 equivalent; no helpdesk shortcut for resetting access to PHI-bearing accounts. | F + NF |
| G-AUTH-04 | RBAC model for providers and staff: roles defined for physician, MA, nurse, scheduler, billing, IT-admin, with least-privilege defaults. | NF |
| G-AUTH-05 | Proxy access lifecycle: grant with proof of relationship/guardianship, modify, revoke, time-bound expiration, auditable. Both parties notified on lifecycle events. | F |
| G-AUTH-06 | Adolescent privacy state transitions: defined access model per state of residence, with confirmed effective date, parent/teen notification, and graded data-element access. | F |
| G-AUTH-07 | Break-glass / emergency clinical access: documented justification required, auto-notification to compliance + patient, full audit trail. | F + NF |
| G-AUTH-08 | Session timeout policies: shorter for shared workstations and provider clinical surfaces, longer for patient personal devices, all within HIPAA-acceptable bounds. | NF |
| G-AUTH-09 | Service accounts / system integrations use rotated credentials or workload identity; no shared static secrets. | NF |
| G-AUTH-10 | Failed-login lockout, brute-force protection, and risk-based step-up (geo, device, behavior) on patient and provider auth surfaces. | NF |

### Stakeholders to engage

- Information Security / IAM team
- Compliance / Privacy officer
- Legal (adolescent privacy state-by-state)
- Helpdesk / patient-access team (account-recovery operational model)

---

## 2. Data Privacy & Security

### What's missing

Extracts mention HIPAA at a high level and the brief lists compliance as a requirement, but there are no specific requirements around:
- Data classification scheme (PHI, PII, sensitive categories)
- Encryption standards (in transit, at rest, key management)
- Data residency / hosting location constraints
- De-identification and secondary-use policies
- Sensitive categories with elevated protection (mental health, substance use, HIV, reproductive health, genetic, adolescent)
- Third-party / vendor data handling and BAA scope
- Data subject rights workflows (HIPAA right of access, amendment, accounting of disclosures; state privacy laws)
- Breach notification procedures
- Patient consent management and granular sharing controls
- Photo/video/file attachment lifecycle (touched on by Marcus but not formalized)

### Why it matters

- A single PHI breach has severe financial, regulatory, and reputational consequences (the brief explicitly lists this as a top risk).
- 42 CFR Part 2 (substance use), state laws (e.g., CA CMIA, NY SHIELD), and category-specific federal protections require data-segmentation capabilities that must be designed in, not retrofitted.
- Patients increasingly exercise data-subject rights; manual fulfillment doesn't scale.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-SEC-01 | All PHI encrypted in transit (TLS 1.2+ minimum, TLS 1.3 preferred) and at rest (AES-256). | NF |
| G-SEC-02 | Key management via managed KMS / HSM-backed service; documented key rotation policy. | NF |
| G-SEC-03 | Data classification scheme defined (PHI, PII, sensitive subcategories) and applied across the data model; access control evaluated per classification. | NF |
| G-SEC-04 | Sensitive data categories (mental/behavioral health, substance use, HIV/STI, reproductive, genetic, adolescent) subject to elevated access controls and explicit consent for sharing. | F + NF |
| G-SEC-05 | Granular sharing controls: patient can restrict categories of data from specific providers or care relationships (operationalizes F-CCM-12). | F |
| G-SEC-06 | All vendors / sub-processors handling PHI under signed BAA; BAA scope, audit rights, breach notification SLAs documented. | NF |
| G-SEC-07 | Patient-facing data subject rights workflows: right-of-access (within 30 days), amendment request, accounting of disclosures, restriction request. | F |
| G-SEC-08 | Documented breach detection, classification, escalation, and notification procedures meeting HIPAA Breach Notification Rule and state law timelines. | NF |
| G-SEC-09 | Photo / video / file attachments encrypted; lifecycle policy (retention period, patient deletion right, provider deletion controls); media never stored outside PHI boundary. | F + NF |
| G-SEC-10 | Cloud hosting region(s) constrained to US (or as required by org policy); cross-border data flows prohibited unless explicitly approved. | NF |
| G-SEC-11 | Penetration testing, SAST, DAST, and dependency scanning integrated into CI/CD; remediation SLAs defined by severity. | NF |
| G-SEC-12 | Secrets management — no credentials in code or config; centralized secret store with rotation. | NF |
| G-SEC-13 | Consent records (data sharing, communication preferences, research opt-in) are versioned, time-stamped, and retrievable. | F + NF |

### Stakeholders to engage

- Chief Information Security Officer (CISO) / Information Security
- HIPAA Privacy Officer
- Legal (state privacy law)
- Cloud architecture / platform team
- Vendor management

---

## 3. Performance & Scalability

### What's missing

Dr. Alvarez gave provider-side performance numbers (chart open <2s, order screen <1s). No requirements yet cover:
- Patient-facing performance budgets (page load, mobile cold start, search latency)
- Concurrent user load model and peak-load assumptions
- Capacity planning for messaging, attachments, and telehealth video
- Performance under degraded network conditions (rural, mobile data)
- Caching, CDN, and offline behavior
- Background sync (e.g., device data ingestion)
- Performance SLOs and error budgets

### Why it matters

- Patient adoption goals (40% MAU) cannot be hit if mobile cold start is slow or the app feels sluggish.
- Telehealth video sessions have hard latency/quality requirements; reimbursement can depend on session quality.
- Phased rollouts will see traffic bursts (e.g., immunization-record requests around school-year start).

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-PERF-01 | Patient mobile app cold start to first interactive screen ≤ 3 seconds on a mid-tier device with typical broadband; ≤ 5 seconds on LTE. | NF |
| G-PERF-02 | Patient web initial page load (TTI) ≤ 3 seconds on broadband; ≤ 5 seconds on LTE. | NF |
| G-PERF-03 | Common patient actions (open message thread, view appointment, view med list) ≤ 1.5 seconds at the 95th percentile. | NF |
| G-PERF-04 | Concurrent user capacity sized for projected peak: define baseline DAU, peak-to-average ratio, and headroom multiplier. Document assumptions. | NF |
| G-PERF-05 | Telehealth video sessions meet defined quality SLOs (e.g., jitter, packet loss, MOS). Quality monitoring per session, with auto-escalation on degradation. | NF |
| G-PERF-06 | Graceful degradation under poor network conditions — async actions queue and retry, critical surfaces (med list, ID card, emergency info) available offline. | F + NF |
| G-PERF-07 | Defined SLOs with error budgets per capability (auth, messaging, scheduling, telehealth). Public-facing status page surfaces current state. | NF |
| G-PERF-08 | Load testing performed against peak-day projections before each major release; results published. | NF |
| G-PERF-09 | Background sync for device data and attachments respects battery and metered-network preferences. | NF |
| G-PERF-10 | CDN / caching strategy for static assets; cache-busting protocol on release. | NF |

### Stakeholders to engage

- Platform / SRE team
- Telehealth vendor (if partnered)
- Network operations (rural site performance)

---

## 4. Error Handling, Resilience & Escalation

### What's missing

Dr. Alvarez asked for proactive outage notification; otherwise this area is unaddressed. Missing:
- User-facing error message standards
- Failure modes for critical clinical actions (e.g., refill request fails silently?)
- Retry / idempotency for safety-critical operations
- Escalation paths for messages that aren't acknowledged within SLA
- Workflow for after-hours messages classified as urgent
- Dependency-failure handling (Epic API down, Surescripts down, telehealth vendor down)
- Incident response and rollback procedures
- "Big red button" disabling of features that misbehave

### Why it matters

- Silent failures in clinical workflows (lost refill, lost message) cause patient harm. The interviews already document this (Linda's lost-message story).
- Healthcare downstream systems fail regularly; graceful degradation is the difference between "annoying" and "dangerous."
- Information-blocking rules limit how much we can hold back during partial outages.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-ERR-01 | User-facing error messages explain what failed, what the user can do, and provide a human-channel fallback for clinical workflows (e.g., "Call the office at ..."). | F + NF |
| G-ERR-02 | Critical clinical workflows (refill, appointment booking, messaging) confirm success explicitly; ambiguous network failures retried with idempotency keys, not silently dropped. | F + NF |
| G-ERR-03 | Message-acknowledgement SLA monitoring: if a message tagged urgent is not acknowledged within defined time, automatic escalation to backup pool / on-call coverage. | F |
| G-ERR-04 | After-hours urgent messaging: clear in-app warning that messages are not monitored after hours, with explicit alternate paths (urgent care, nurse triage line, 911). | F + NF |
| G-ERR-05 | Dependency-failure handling: each external dependency (Epic, Surescripts, telehealth vendor, payment processor) has defined degraded-mode behavior; user is informed which capabilities are temporarily unavailable. | F + NF |
| G-ERR-06 | Feature-flag / kill-switch capability for every major user-facing capability, enabling rapid disable without redeploy. | NF |
| G-ERR-07 | Documented incident-response runbooks, rollback procedures, and provider/patient communication templates. | NF |
| G-ERR-08 | Post-incident review process with documented learnings; high-severity incidents reviewed by clinical leadership. | NF |
| G-ERR-09 | Information-blocking compliant degraded-mode: do not silently suppress patient access to results during partial outages; provide visible "loading / partial data" state and audit-log the gap. | F + NF |

### Stakeholders to engage

- SRE / platform reliability team
- Clinical operations (on-call coverage model)
- Patient experience (error-message tone and content)

---

## 5. Content Management & Updates

### What's missing

Dr. Okonkwo asked for condition-triggered patient education; no other content management requirements exist. Missing:
- Patient education content authoring, governance, and review cycles
- Plain-language translation governance (lab explanations, summaries)
- Multi-language support and translation workflow
- Content versioning and provenance (which version was shown to a patient?)
- Provider-facing content (smart phrases, templates, order sets) lifecycle
- Notification content templates and approval workflow
- Legal/compliance copy (privacy notices, consent forms) versioning

### Why it matters

- Outdated clinical education content is a safety issue. Governance is required.
- The brief raises "equitable access for non-English speakers" as an open question — translation is not a feature, it's an entire workstream.
- Showing the wrong version of a consent form has legal consequences.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-CMS-01 | Patient education content lifecycle: authoring, clinical review, approval, scheduled review (≤ 24 months), retirement, with audit trail. | F + NF |
| G-CMS-02 | Multi-language support for patient-facing content at launch in defined languages (proposed: English + top 2 by population; expand to top 5 by Phase 3). | F |
| G-CMS-03 | Translation governance: machine translation requires human qualified-translator review for clinical content; non-clinical content may use reviewed MT. | NF |
| G-CMS-04 | Content versioning: every patient interaction with educational content, consent form, or notification template records the version shown; retrievable for audit. | NF |
| G-CMS-05 | Plain-language lab-result explanations are curated content, version-controlled, owned by clinical informatics — not free-form generated per request. | F + NF |
| G-CMS-06 | Notification templates (push, email, SMS, voice) follow an approval workflow; clinical-content templates require clinical review, marketing-content templates require communications review. | NF |
| G-CMS-07 | Smart phrases / templates for providers: shared library with governance, ability to favorite, with auditability when shared phrases are used in clinical notes. | F |
| G-CMS-08 | Legal copy (privacy notice, terms, consent) versioned with effective dates; patient re-acknowledgement triggered on material change. | F + NF |
| G-CMS-09 | Plain-language reading-level target (e.g., 6th–8th grade) for patient-facing content, validated by tooling. | NF |

### Stakeholders to engage

- Clinical informatics
- Patient education team
- Health-equity / language-access program
- Legal / compliance
- Communications / marketing

---

## 6. Monitoring, Analytics & Observability

### What's missing

The brief references success metrics. Interviews don't touch on:
- Telemetry strategy and what gets instrumented
- Analytics for product/UX decisions vs. operational monitoring
- Patient-facing analytics privacy (HIPAA + state law on tracking)
- Provider performance dashboards (and the policy guardrails on them)
- Population-health analytics (Dr. Alvarez mentioned briefly)
- Alerting thresholds and on-call rotation
- Data warehouse / analytics pipeline
- A/B testing framework and ethics

### Why it matters

- Without telemetry, success metrics cannot be measured.
- Healthcare tracking analytics is a regulatory minefield (recent OCR guidance on third-party trackers, pixel-tracking enforcement actions).
- Provider performance dashboards can drive perverse incentives if not designed carefully.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-OBS-01 | Defined telemetry baseline covering: auth events, navigation, feature use, error events, performance traces, with PHI minimization. | NF |
| G-OBS-02 | All product analytics tools comply with current OCR guidance on tracking technologies; no third-party trackers on PHI-bearing pages without BAA and explicit consent. | NF |
| G-OBS-03 | Operational monitoring: latency, error rate, saturation, traffic per critical capability, with alerting tied to error budgets. | NF |
| G-OBS-04 | On-call rotation for portal services with documented escalation paths; clinical-impact incidents notified to clinical leadership in real time. | NF |
| G-OBS-05 | Analytics events for product success metrics (registration rate, MAU, self-scheduled appointments, message volume per provider) instrumented from launch. | F + NF |
| G-OBS-06 | Provider performance dashboards include guardrails: ratio metrics (not absolute), peer-comparison ranges (not rankings), and explicit policy that metrics are coaching tools, not evaluation. | F + NF |
| G-OBS-07 | A/B testing framework restricted to non-clinical UX changes; clinical-workflow A/B tests require IRB / clinical-leadership approval. | NF |
| G-OBS-08 | Population-health analytics surface defined in coordination with quality / value-based care team; not a portal-only artifact. | F |
| G-OBS-09 | Patient-facing transparency: patients can request which of their data has been used for which analytics purpose (HIPAA accounting of disclosures intersection). | F |

### Stakeholders to engage

- Data analytics / data engineering team
- Privacy / compliance (tracking technology guidance)
- Quality / population-health team
- SRE / observability platform team

---

## 7. Training, Change Management & Adoption Support

### What's missing

Eleanor flagged onboarding and the human-channel preservation issue. The brief mentions provider training. There are no detailed requirements for:
- Provider training program (initial + ongoing)
- Patient onboarding (digital + assisted)
- Super-user / champion program
- In-app help, guided tours, contextual help
- Helpdesk model — patient-facing and provider-facing
- Adoption metrics and intervention triggers (e.g., when a provider's usage drops)
- Communication plan for releases and feature additions

### Why it matters

- The brief lists provider adoption as a top risk; training is the primary mitigation.
- Patient adoption goals depend on assisted onboarding for less-tech-savvy cohorts (Eleanor).
- Without an explicit helpdesk model, the operational burden defaults to clinic staff and quickly degrades the experience.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-TRN-01 | Provider training program: role-based curriculum, required completion before go-live access, refresher cadence (annual + feature-driven). | NF |
| G-TRN-02 | Champion / super-user program identified per practice or clinic, with defined responsibilities and recognition. | NF |
| G-TRN-03 | Patient onboarding flow: progressive disclosure, optional guided tour, completion measured; assisted-onboarding path for in-clinic registration. | F |
| G-TRN-04 | In-app contextual help: every primary action has an accessible "What is this?" affordance; help content is part of the content lifecycle (G-CMS-01). | F |
| G-TRN-05 | Helpdesk model documented for both patient and provider: tiered support, SLA per tier, escalation to clinical/IT/security as appropriate; staffing funded before launch. | NF |
| G-TRN-06 | Release communication plan executed for every patient-visible UI change ≥ defined threshold: in-app announcement, email summary, printed materials for in-clinic for 70+ cohort. | NF |
| G-TRN-07 | Adoption monitoring with defined intervention triggers (e.g., provider sees <50% of inbox in portal vs. EHR → outreach by champion). | F + NF |
| G-TRN-08 | Multilingual onboarding materials and helpdesk support in supported languages. | NF |
| G-TRN-09 | Accessibility-specific onboarding pathway and training materials for users with visual, motor, or cognitive impairments. | NF |

### Stakeholders to engage

- Clinical education / provider training
- Patient experience / patient education
- Helpdesk / IT support leadership
- Change-management lead
- Health-equity / language-access program

---

## 8. Compliance & Audit

### What's missing

The brief lists HIPAA, HITECH, and state laws at a high level. Specifics not yet captured:
- Comprehensive audit logging (what gets logged, retention, immutability)
- Audit review workflows (who reviews, how often, what triggers alerts)
- 21st Century Cures Act / information-blocking compliance
- 42 CFR Part 2 (substance use disorder records) compliance, where applicable
- State-by-state privacy laws (CA CMIA, NY SHIELD, CO CPA, etc.)
- Accessibility compliance auditing (WCAG 2.1 AA per brief)
- Section 508 (if any federal nexus)
- Records retention and disposition
- ePHI access logging by privileged users (admins, support)
- Regulatory reporting obligations

### Why it matters

- Audit log gaps are the #1 finding in OCR investigations.
- Information-blocking enforcement (with significant fines) is active as of 2024.
- 42 CFR Part 2 segmentation is technically demanding and must be designed in.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-COMP-01 | Comprehensive audit logging: every PHI access (read, write, export, print) logged with user, timestamp, action, record identifier, source IP / device, justification (where required). | NF |
| G-COMP-02 | Audit logs are immutable / append-only, retained ≥ 6 years (HIPAA minimum; longer per state law), with integrity protection. | NF |
| G-COMP-03 | Defined audit review workflow: scheduled sampling, anomaly detection, alerting on suspicious patterns (e.g., VIP record access, mass export). | NF |
| G-COMP-04 | Information-blocking compliance: no technical or procedural barriers preventing patient or authorized recipient access to ePHI; exceptions documented per the rule. | NF |
| G-COMP-05 | 42 CFR Part 2 — if substance use disorder records are in scope, segmentation, consent, and re-disclosure controls implemented per rule. (Confirm scope first.) | NF |
| G-COMP-06 | State privacy law compliance matrix maintained for each state where patients reside; technical requirements derived from the matrix. | NF |
| G-COMP-07 | WCAG 2.1 AA conformance verified by independent accessibility audit pre-launch and on a defined cadence; remediation SLAs by severity. | NF |
| G-COMP-08 | Records retention and disposition schedule defined per data class; automated disposition at end of retention period. | NF |
| G-COMP-09 | Privileged-user (admin, support, integration) access to PHI logged separately and reviewed at higher cadence. | NF |
| G-COMP-10 | Annual HIPAA risk assessment covering the portal scope; remediation backlog tracked. | NF |
| G-COMP-11 | Disaster recovery plan with documented RTO / RPO, tested at least annually. | NF |

### Stakeholders to engage

- HIPAA Privacy Officer
- Compliance / Regulatory affairs
- Internal Audit
- Legal (state law + 42 CFR Part 2 scope)
- Accessibility lead / external accessibility auditor

---

## 9. Interoperability & Data Standards

### What's missing

Brief references HL7 FHIR and Epic integration; interviews surfaced cross-system pain (Linda, Dr. Okonkwo). Specific requirements gaps:
- FHIR API conformance levels (R4 vs. R5; US Core profiles)
- API for third-party patient apps (per Cures Act)
- Data normalization (LOINC, SNOMED, RxNorm, CPT, ICD-10)
- Photo/document interop (DICOM for imaging)
- Carequality / eHealth Exchange / TEFCA participation
- API rate limits, authentication, deprecation policy
- Webhook / event-stream support

### Why it matters

- Cures Act requires patient access via standardized APIs.
- Without normalization, "outside records" arrive as PDFs that can't be queried, defeating the purpose.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-INT-01 | FHIR R4 API conformant with US Core profiles for patient-data access; published API documentation. | NF |
| G-INT-02 | Patient-app authorization via SMART on FHIR / OAuth 2.0 per Cures Act standards. | NF |
| G-INT-03 | Reference terminologies enforced for structured data: LOINC (labs), SNOMED CT (problems), RxNorm (meds), CPT (procedures), ICD-10 (dx). | NF |
| G-INT-04 | Imaging viewer or link-out for DICOM content from outside sources; security review for embedded viewer. | F |
| G-INT-05 | Participation strategy defined for Carequality / eHealth Exchange / TEFCA QHIN — decision recorded with timing. | NF |
| G-INT-06 | API rate limits, authentication standards, deprecation policy (minimum 12-month deprecation window) published for third-party developers. | NF |
| G-INT-07 | Event / webhook capability for partner integrations (e.g., appointment-confirmed event); documented event schema. | F |

### Stakeholders to engage

- Integration / interoperability team
- EHR (Epic) integration lead
- Health information exchange (HIE) participation lead

---

## 10. Billing, Payment & Financial Workflows

### What's missing

Marcus mentioned consolidated billing and payment plans; otherwise unaddressed. Gaps:
- Payment processing and PCI-DSS scope
- Insurance eligibility checking
- Cost estimation pre-service
- Statement generation and delivery
- Refund and adjustment workflows
- Financial assistance / charity care application
- Collections and bad-debt workflows
- HSA/FSA receipt handling

### Why it matters

- Billing is the #1 source of patient complaints in many systems.
- PCI-DSS scope expansion if card data flows through portal infrastructure.
- Cost estimation is increasingly required by federal price-transparency rules.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-BILL-01 | Payment processing via a PCI-DSS-compliant processor; no card data stored within portal application boundary. | NF |
| G-BILL-02 | Eligibility verification at appointment booking, with deductible / copay estimate where possible. | F |
| G-BILL-03 | Good Faith Estimates generated for self-pay patients per federal No Surprises Act requirements. | F + NF |
| G-BILL-04 | Statement consolidation across encounters and family members under a single guarantor account, with line-item detail available. | F |
| G-BILL-05 | Payment plans self-service setup with transparent fee disclosure. | F |
| G-BILL-06 | Financial assistance application initiated from the portal; status tracking. | F |
| G-BILL-07 | Refund and adjustment workflows visible to patient; no silent balance changes. | F |
| G-BILL-08 | Apple Pay / Google Pay / ACH support in addition to card. | F |

### Stakeholders to engage

- Revenue cycle / billing leadership
- Patient financial services
- Payment processor / treasury

---

## 11. Provider Workflow & Clinical Operations

### What's missing

PCP and specialist interviews surfaced operational issues without translating them into requirements:
- Coverage / call-pool model (vacation, after-hours, weekend)
- Patient panel ownership and reassignment
- Triage protocols and decision rules (who handles what)
- Documentation expectations for portal-mediated care
- Medical-legal record completeness when care happens via portal
- Telephone / portal-message billing workflow

### Why it matters

- Without clear coverage and triage rules, the inbox-volume crisis Dr. Alvarez described will not be solved by product features alone.
- Documentation gaps create medical-legal exposure.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-OPS-01 | Coverage / on-call configuration: providers can designate coverage for absences with defined scope (full inbox, urgent only, scheduled visits only); coverage notifications visible to patients. | F |
| G-OPS-02 | Triage protocols configurable per practice; defined rules for routing message types to MA, nurse, physician, scheduler, billing. | F |
| G-OPS-03 | Portal-mediated clinical encounters automatically create a documentation stub in the EHR with structured fields. | F |
| G-OPS-04 | Asynchronous-care billing workflow integrated with revenue cycle; provider can mark a message exchange as billable with appropriate documentation. | F |
| G-OPS-05 | Panel ownership view: providers see their assigned panel; reassignment requires defined approval. | F |
| G-OPS-06 | "Hand-off" mode for transitioning a patient or message thread to another provider with context preserved. | F |

### Stakeholders to engage

- Clinical operations leadership
- Revenue cycle (async billing)
- Medical staff leadership

---

## 12. Vendor, Procurement & Lifecycle Management

### What's missing

The brief lists key vendors implicitly (Epic, telehealth, etc.); nothing on vendor lifecycle:
- Vendor evaluation criteria for new integrations
- Exit / data-portability requirements
- Source-code escrow / business-continuity arrangements
- License compliance (open-source)
- Vendor performance monitoring

### Why it matters

- Telehealth vendor and other partner choices have multi-year implications.
- Exit strategies are often the missing piece that traps an organization in a bad vendor relationship.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-VEN-01 | Vendor evaluation framework covering security, HIPAA, performance, financial stability, support SLA, exit/data-portability. | NF |
| G-VEN-02 | Data portability — vendor agreements require data export in defined standard formats on termination, within defined timelines. | NF |
| G-VEN-03 | Open-source license inventory maintained; license compatibility reviewed before adoption. | NF |
| G-VEN-04 | Vendor performance reviewed against SLA quarterly; escalation paths defined. | NF |

### Stakeholders to engage

- Vendor management / procurement
- Legal (contracts)
- Open-source program office (if exists)

---

## 13. Ethics, Equity & Responsible AI

### What's missing

AI-governance basics are in the conflict doc (Conflict 4). Broader ethics gaps:
- Algorithmic bias testing for AI features
- Equitable outcomes monitoring across demographic groups
- Disparities in adoption and access tracked
- Vulnerable-population safeguards (mental health, domestic violence, immigration status concerns)
- Use of patient data for model training — consent and governance

### Why it matters

- Healthcare AI has documented bias issues; deploying without monitoring perpetuates harm.
- Adoption disparities undermine the value case and the equity question raised in the brief.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-ETH-01 | AI features tested for performance disparities across protected demographic groups before launch and on a defined cadence; mitigation triggered on threshold breach. | NF |
| G-ETH-02 | Portal adoption and engagement metrics stratified by demographic group; disparities trigger remediation planning. | F + NF |
| G-ETH-03 | Patient data used for model training only under explicit opt-in consent; governance includes IRB-equivalent review where applicable. | NF |
| G-ETH-04 | Vulnerable-population safeguards: defined handling for shared-device / household-abuse scenarios (e.g., quick-hide UI, separate notification channels for sensitive content). | F + NF |
| G-ETH-05 | AI features have a documented "model card" or equivalent describing intended use, training data scope, known limitations, and out-of-scope use. | NF |

### Stakeholders to engage

- AI governance / responsible AI lead
- Health equity program
- Patient advocacy
- IRB / research ethics

---

## 14. Sustainability & Operational Lifecycle

### What's missing

Brief touches on first-year operational costs; longer-term gaps:
- Operational runbook ownership post-launch
- Long-term cost modeling (storage growth, support, vendor renewals)
- Sunset criteria for features that don't earn their keep
- Roadmap-process commitment (annual planning, stakeholder input loop)

### Why it matters

- Many portal initiatives launch successfully and then degrade over years due to lack of ownership.
- Without sunset criteria, dead features accumulate complexity and confuse users.

### Proposed requirements

| ID | Requirement | Type |
|---|---|---|
| G-LCM-01 | Post-launch operational ownership documented per capability; on-call rotation funded. | NF |
| G-LCM-02 | Annual roadmap process with structured stakeholder input (provider advisory, patient advisory, ops). | NF |
| G-LCM-03 | Feature sunset criteria: usage thresholds + value review trigger retirement consideration; sunset communicated per release-communication standards. | NF |
| G-LCM-04 | Long-term cost model maintained; storage growth, vendor renewals, infrastructure scaling reviewed annually. | NF |

### Stakeholders to engage

- Product operations leadership
- Finance / IT budgeting
- Service-management / ITIL function

---

## Summary — additional stakeholders to interview

Several gap areas above can only be properly scoped with input from stakeholders not yet interviewed:

1. **CISO / Information Security** — Sections 1, 2, 6, 8
2. **HIPAA Privacy Officer / Compliance** — Sections 1, 2, 6, 8, 13
3. **Legal counsel** — Sections 1, 2, 5, 8, 13
4. **Revenue cycle / billing leadership** — Sections 2, 6, 10, 11
5. **SRE / platform reliability** — Sections 3, 4, 6
6. **Clinical informatics** — Sections 5, 9, 11
7. **Clinical operations** — Sections 4, 11
8. **Patient experience / advocacy** — Sections 4, 7, 13
9. **Health equity / language access** — Sections 5, 7, 13
10. **Integration / EHR team (Epic)** — Sections 3, 4, 9, 12
11. **Vendor management / procurement** — Sections 2, 12
12. **Accessibility specialist** — Sections 7, 8
13. **Responsible AI / governance** — Sections 6, 13
14. **Telehealth program owner** — Sections 3, 4, 12

These interviews should be scheduled before Phase 2 synthesis is finalized so the resulting PRD is grounded rather than aspirational.

---

## Recommended next steps

1. Review this gap document with the product owner and prioritize which gaps must be closed before Phase 2 synthesis vs. which can be deferred.
2. Schedule discovery sessions with the stakeholder list above.
3. Promote validated `G-*` requirements into the canonical PRD numbering during Phase 2 synthesis.
4. Update the conflict-and-resolution document if new gap-driven requirements introduce new cross-persona tensions.
