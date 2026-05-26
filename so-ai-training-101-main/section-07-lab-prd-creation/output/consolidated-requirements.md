# Consolidated Requirements — HealthConnect Patient & Provider Portal

**Date:** May 22, 2026 (updated May 23, 2026 to fold in gap-analysis requirements)
**Author:** M. Mettler
**Inputs:**
- Source brief: [input/00-healthcare-portal-reference.md](input/00-healthcare-portal-reference.md)
- Per-persona requirements extracts in [output/requirements-extracts/](requirements-extracts/)
- Conflict resolutions in [requirements-extracts/requirements-conflicts-and-resolutions.md](requirements-extracts/requirements-conflicts-and-resolutions.md)
- Gap analysis in [requirements-gap-analysis.md](requirements-gap-analysis.md)

**Status:** Draft — input for Phase 2 PRD synthesis

> This document consolidates per-persona requirements **plus** the candidate requirements identified in the gap analysis into a single de-duplicated list. Where personas conflicted, the resolutions in the conflicts document are applied and noted. Where a gap-analysis requirement overlapped with an existing one, they are merged into a single broader requirement and both source IDs preserved. Where a gap-analysis requirement covers ground no persona raised, it is added as a new entry — explicitly marked **(gap-sourced)** since it has not yet been validated by stakeholder interview.
>
> **⚠️ Caveat:** gap-sourced requirements remain provisional until validated with the stakeholders listed in [requirements-gap-analysis.md § Summary](requirements-gap-analysis.md#summary--additional-stakeholders-to-interview). They are included here to give Phase 2 synthesis a single working list, not to imply they are confirmed.

---

## Conventions

- IDs: `F-###` functional, `NF-###` non-functional, `B-###` business, `D-###` dependency, `A-###` open question.
- Priority: **Must-Have / Should-Have / Nice-to-Have**.
- "Source" lists the originating per-persona requirement IDs (e.g., `F-CCM-01`, `F-PCP-07`) and/or gap-analysis IDs (e.g., `G-AUTH-01`).
- "Stakeholders" lists which personas raised it; **(gap-sourced)** marks requirements that came only from gap analysis and need stakeholder validation.
- 🔁 marks a requirement whose final form reflects a cross-persona reconciliation.
- ✚ marks a requirement that **merged** persona-sourced and gap-sourced inputs into a single broader entry.
- 🆕 marks a requirement that is **net-new from gap analysis** (no persona source).

---

## Table of Contents

- [Functional Requirements](#functional-requirements)
  - [Must-Have](#must-have)
  - [Should-Have](#should-have)
  - [Nice-to-Have](#nice-to-have)
- [Non-Functional Requirements](#non-functional-requirements)
  - [Must-Have (NF)](#must-have-nf)
  - [Should-Have (NF)](#should-have-nf)
- [Business Requirements](#business-requirements)
- [Constraints & Dependencies](#constraints--dependencies)
- [Ambiguities & Open Questions](#ambiguities--open-questions)
- [Traceability Index](#traceability-index)

---

## Functional Requirements

### Must-Have

#### Account, Identity, Access

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-001 🔁 | Single account per user with linked dependents; user can switch among self + family members from one login. Phase-1 "minimum viable family account" scope: view, message, schedule on behalf of dependents; co-guardian access for a second adult. | Busy Parent | F-BP-01, F-BP-02 | **Resolution applied (Conflict 7).** |
| F-002 ✚ | Proxy / delegated access with full lifecycle: grant (with proof of relationship/guardianship), modify, revoke, time-bound expiration. View + messaging rights configurable per delegate. Both parties notified on lifecycle events. Fully auditable. | Chronic Condition Manager, Tech-Limited Senior, Busy Parent | F-CCM-13, F-TLS-07, F-BP-18 (subset), G-AUTH-05 | Merged persona + gap. |
| F-003 ✚ | Patient-visible audit log of who accessed records (including proxy and privileged-user actions). | Chronic Condition Manager, Tech-Limited Senior | F-TLS-08, NF-CCM-03, G-AUTH-07 (patient notification subset), G-COMP-09 (patient view subset) | |
| F-004 🆕 | Account recovery flow requires identity re-verification at IAL2-equivalent assurance; no helpdesk shortcut for resetting access to PHI-bearing accounts. | (gap-sourced) | G-AUTH-03 | Validate with helpdesk / patient-access team. |
| F-005 🆕 | Break-glass / emergency clinical access workflow: documented justification required, auto-notification to compliance and patient, full audit trail. | (gap-sourced) | G-AUTH-07 | HIPAA Security Rule expectation. |
| F-006 ✚ | Adolescent-privacy state transitions: defined access model per state of residence, with confirmed effective date, parent/teen notification, graded data-element access. (Was: F-110 Should-Have — promoted to Must-Have for any state where Phase-1 rollout occurs.) | Busy Parent | F-BP-17, G-AUTH-06 | **Phase placement open** — see A-007. If Phase 1 only ships in states where no protected age occurs in scope, this may stay deferred. |

#### Messaging & Care-Team Communication

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-010 ✚ | Secure messaging between patient and care team with delivery + read confirmation visible to patient ("nurse Sarah viewed at 2pm"). Critical clinical workflows confirm success explicitly; ambiguous network failures retried with idempotency keys, not silently dropped. | Chronic Condition Manager, Tech-Limited Senior | F-CCM-02, F-TLS-02, G-ERR-02 (clinical-action subset) | |
| F-011 🔁 | Message routing rules: administrative, scheduling, billing, and form-request messages are routed to appropriate staff and **do not** reach the physician inbox. Routing protocols configurable per practice. | PCP, Specialist | F-PCP-01, G-OPS-02 | **Resolution applied (Conflict 2).** Merged with G-OPS-02 (configurable triage protocols). |
| F-012 🔁 | Tiered response SLAs by message type, surfaced in the patient compose UX (e.g., "a nurse typically replies within 4 hours"). | All patient personas, PCP | derived from Conflict 2 | |
| F-013 | Physician inbox triage view: sort/filter by urgency, type, patient. | PCP | F-PCP-02 | |
| F-014 | AI-assisted message drafting; physician reviews + signs every outbound clinical reply (no autosend). | PCP | F-PCP-03 | Aligns with AI-governance resolution (Conflict 4). |
| F-015 | AI-assisted message summarization (long patient messages) and classification (urgency / topic), with source content always visible. | PCP | F-PCP-04 | |
| F-016 | AI red-flag-symptom detection in patient messages with provider override. | PCP | F-PCP-05 | Requires clinical-safety validation. |
| F-017 | Provider-to-provider messaging in a separate queue from the patient inbox, with its own SLA, read receipts. | PCP, Specialist | F-PCP-06, F-SP-06 | |
| F-018 | "Off-scope redirect" one-click action so providers can route messages out of their scope to the appropriate provider/team. | Specialist | F-SP-20 | |
| F-019 🆕 | Message-acknowledgement SLA monitoring: if a message tagged urgent is not acknowledged within defined time, automatic escalation to backup / on-call coverage. | (gap-sourced) | G-ERR-03 | Patient-safety adjacent. |
| F-019b 🆕 | After-hours messaging UI clearly warns patients that messages are not monitored after hours, with explicit alternate paths (urgent care, nurse triage line, 911). | (gap-sourced) | G-ERR-04 | |

#### Lab Results & Health Information

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-020 🔁 | Lab results released to patients immediately on availability, **except** for clinically-defined carve-out categories that follow a short provider-review window. | Chronic Condition Manager, PCP, Tech-Limited Senior | F-CCM-03 | **Resolution applied (Conflict 1).** Carve-out list owned by clinical leadership. |
| F-021 | Lab results displayed with personal target ranges, trends over time, and a "what changed since last time" summary. | Chronic Condition Manager | F-CCM-04 | |
| F-022 ✚ | Plain-language explanation alongside clinical lab values; explanations are **curated content**, version-controlled, owned by clinical informatics — not free-form generated per request. | Chronic Condition Manager, Tech-Limited Senior | F-CCM-08, F-TLS-05, G-CMS-05 | Merged persona + gap content-governance. |
| F-023 | Result-available notification (both normal and abnormal) per patient's channel preferences. | Tech-Limited Senior | F-TLS-06 | Tied to notification model (F-070). |
| F-024 | Inline "message your care team" CTA on result views. | derived (Conflict 1) | Conflict 1 | |

#### Appointments & Scheduling

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-030 | Self-service appointment booking with real-time availability across providers in the same system. | Chronic Condition Manager, Busy Parent | F-CCM-06, F-BP-04 | |
| F-031 | Same-day / sick-visit booking with visibility across providers in a practice (not only primary). | Busy Parent | F-BP-05 | |
| F-032 | Single unified view of all upcoming appointments across patient + linked family members. | Chronic Condition Manager, Busy Parent | F-CCM-07 | |
| F-033 | Self-service reschedule / cancel without phone call. | Chronic Condition Manager | F-CCM-16 | |
| F-034 | Visit-prep info: directions, parking, what to bring, fasting requirements. | Tech-Limited Senior | F-TLS-09 | |
| F-035 | Voice-call appointment reminders supported (in addition to digital channels). | Tech-Limited Senior | F-TLS-03 | Part of multi-channel model (F-070). |

#### Medications & Prescriptions

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-040 | Prescription refill requests with proactive expiration / refill-auth alerts to both patient and provider. | Chronic Condition Manager | F-CCM-05 | |
| F-041 | Visibility into refill request status (including controlled substances, with DEA/EPCS constraints preserved). | Busy Parent | F-BP-06 | |
| F-042 | Refill workflow supports standing-order delegation to MA with physician daily batch sign-off. | PCP | F-PCP-09 | |
| F-043 | EPCS / controlled-substance e-prescribing supported. | PCP | F-PCP-11 | Regulatory mandate. |
| F-044 | Pharmacy fill-data integration showing whether patient is actually picking up prescriptions. | PCP | F-PCP-10 | Patient disclosure per Conflict 12. |
| F-045 | Immunization records accessible on demand, with quick-share / PDF export. | Busy Parent | F-BP-10 | |

#### Provider Workflow & Chart Review

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-050 🔁 | "Patient at a glance" summary view — **role- and specialty-configurable** layout. Default PCP view: problem list, active meds w/ recent changes flagged, last relevant vitals/labs, what-changed-since-last-visit, open orders, overdue care gaps. Specialty views (e.g., cardiology) configured to surface specialty-relevant data. | PCP, Specialist | F-PCP-07, F-SP-05 | **Resolution applied (Conflict 9):** single configurable framework. |
| F-051 | External / outside data source attribution and provenance visible in chart (e.g., wearable BP vs. validated cuff). | PCP | F-PCP-08 | |
| F-052 | Intelligent referral intake — required-info validation before referral hits specialist queue; auto-request missing pieces from referrer. | Specialist | F-SP-01 | |
| F-053 | Structured referral with specialty-configurable required fields (e.g., cards: reason for consult, recent ECG, recent echo, meds, prior workup). | Specialist | F-SP-02 | |
| F-054 | Referral triage queue with configurable urgency classification rules + escalation to physician for ambiguous cases. | Specialist | F-SP-03 | |
| F-055 | Consult-note loopback to referring provider with delivery confirmation; supports in-system AND outside (non-Epic) referrers. | Specialist | F-SP-04 | Outside-referrer scope depends on interop strategy (Conflict 16). |
| F-056 | Pre-op patient checklist (fasting, meds to hold, arrival time, what to bring) — patient confirms in portal; un-confirmed alert ≥ 24 hrs out. | Specialist | F-SP-07 | Patient-safety classification. |
| F-057 | Post-procedure messages route first to procedure-team nurse, not directly to the specialist. | Specialist | F-SP-08 | |
| F-058 🆕 | Portal-mediated clinical encounters automatically create a documentation stub in the EHR with structured fields. | (gap-sourced) | G-OPS-03 | Medical-legal completeness. |
| F-059 🆕 | Panel ownership view — providers see their assigned panel; reassignment requires defined approval workflow. | (gap-sourced) | G-OPS-05 | |

#### Telehealth

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-060 | Telehealth one-click join + ability for provider to text patient mid-visit (e.g., "turn on light"). | PCP | F-PCP-12 | |

#### Notifications, Errors & Channel Preferences

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-070 🔁 | Channel-by-event-type notification preferences. Each user configures per-event channel(s) from: push, email, SMS, voice call, in-app. Reasonable cohort-based defaults. | All patient personas | F-CCM-15, F-BP-08, F-TLS-03 | **Resolution applied (Conflict 3).** |
| F-071 🔁 | Hard separation between clinical and marketing/health-promotion notifications; marketing is opt-in on a distinct channel set. | Busy Parent | F-BP-08 | **Resolution applied (Conflict 3).** |
| F-072 | Clinical SMS, when used, must never include login links; only direct user to open the app. | Tech-Limited Senior | NF-TLS-08 | Anti-phishing. |
| F-073 | Proactive outage / degraded-performance alerting to providers **before** they encounter the failure (banner in EHR + Teams). | PCP | F-PCP-13, NF-PCP-06 | |
| F-074 🆕 | User-facing error messages explain what failed, what the user can do, and provide a human-channel fallback for clinical workflows (e.g., "Call the office at..."). | (gap-sourced) | G-ERR-01 | |
| F-075 🆕 | Dependency-failure degraded mode: each external dependency (Epic, Surescripts, telehealth vendor, payment processor) has defined behavior; user informed which capabilities are temporarily unavailable. | (gap-sourced) | G-ERR-05 | |
| F-076 🆕 | Information-blocking-compliant degraded mode: do not silently suppress patient access during partial outages; visible "loading / partial data" state, and audit-log the gap. | (gap-sourced) | G-ERR-09, G-COMP-04 | |

#### Mobile

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-080 🔁 | Patient-facing native mobile app (iOS + Android) with feature parity to web. | Busy Parent | F-BP-07 | **Resolution applied (Conflict 10).** |
| F-081 🔁 | Provider mobile access delivered via existing Epic Haiku integration in Phase 1, supplemented by a thin "patient at a glance" mobile surface and messaging notifications. No parallel provider native app in Phase 1. | PCP, Specialist | F-PCP-14, F-SP-09 | **Resolution applied (Conflict 10).** |

#### Dashboard / Home

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-090 🔁 | Personalized home dashboard with selectable layout variants (e.g., "Essentials," "Family," "Health Tracking"). All variants share the same underlying features; defaults are suggestions, not gates (no auto-applied "Essentials" based on age). | All patient personas | F-TLS-04, plus implicit from Linda + Marcus | **Resolution applied (Conflict 5).** |

#### Privacy, Consent & Data Rights

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-095 ✚ | Granular sharing controls — patient chooses which providers see which categories of data (operationalized as elevated controls for sensitive categories: mental/behavioral health, substance use, HIV/STI, reproductive, genetic, adolescent). | Chronic Condition Manager | F-CCM-12, G-SEC-05, G-SEC-04 (controls subset) | Promoted to Must-Have; was Should under F-122. **Was duplicated below — now consolidated here.** |
| F-096 🆕 | Patient-facing data-subject-rights workflows: right-of-access (within 30 days), amendment request, accounting of disclosures, restriction request. | (gap-sourced) | G-SEC-07 | HIPAA mandate; partial today. |
| F-097 🆕 | Consent records (data sharing, communication preferences, research opt-in) versioned, time-stamped, retrievable. | (gap-sourced) | G-SEC-13 | |
| F-098 🆕 | Legal copy (privacy notice, terms, consent) versioned with effective dates; patient re-acknowledgement triggered on material change. | (gap-sourced) | G-CMS-08 | |

---

### Should-Have

#### Communication & Triage

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-100 🔁 | Async nurse-triage chat for clinical questions (both adult and pediatric). Staffing model and SLA defined by clinical operations and funded before launch. | Busy Parent | F-BP-11 | **Resolution applied (Conflict 2).** |
| F-101 | Photo/video attachments in clinical messages, with secure storage, defined retention, and patient deletion right (see NF-050). | Busy Parent | F-BP-12 | |
| F-102 ✚ | Configurable message-triage routing per practice / MA staffing model. (Routing rules engine: G-OPS-02 absorbed.) | PCP | F-PCP-15, G-OPS-02 | Largely merged into F-011 Must; this remains for per-practice tuning UX. |
| F-103 ✚ | Coverage / handoff mode: covering provider receives scoped context (clinical only? inbox rules? auto-decline new initiations? — A-023). Coverage scope configurable (full inbox / urgent only / scheduled visits only). Coverage notifications visible to patients. | PCP | F-PCP-16, G-OPS-01, G-OPS-06 | Merged persona + gap. |
| F-104 | Auto-draft telehealth visit note from session. | PCP | F-PCP-17 | Coordinate with ambient-scribe initiative. |

#### Family & Caregiver Access

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-110 ✚ | (Was promoted partially to F-006 Must.) Should-Have residual: adolescent-privacy enhancements beyond the Phase-1 must-have — emergency parental-override workflow, graded data-element access tuning, multi-state matrix expansion. | Busy Parent | F-BP-17, G-AUTH-06 | See A-007, A-011. |
| F-111 | Temporary / scoped caregiver access (e.g., view-only immunization for grandparent). | Busy Parent | F-BP-18 | Phase 2 per Conflict 7. |
| F-112 | Quick "emergency info / allergies / current meds" shareable card (PDF or share-sheet). | Busy Parent | F-BP-19 | |
| F-113 | Insurance card image storage (photo capture). | Busy Parent | F-BP-20 | PHI-grade media handling (NF-050). |

#### Lab Results & Health Info

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-120 | Patient ability to annotate results / log context. | Chronic Condition Manager | F-CCM-09 | Provider visibility default = yes; confirm. |
| F-121 | Symptom triage tool (is-this-normal / call-doctor / ER). | Chronic Condition Manager | F-CCM-11 | Clinical + legal sign-off required (A-002). |
| F-123 | Trend visualizations for self-logged data (BP, weight, glucose) with provider-visibility toggle. | Chronic Condition Manager | F-CCM-14 | |

> Note: prior F-122 (granular sharing controls) was promoted to F-095 Must.

#### Scheduling & Reminders

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-130 | Stacked / family-batch appointment booking (e.g., 3 kids back-to-back). | Busy Parent | F-BP-13 | |
| F-131 | Day-of-morning appointment reminder (in addition to 24-hr). | Busy Parent | F-BP-15 | |
| F-132 | Telehealth offer surfaced when appropriate ("this visit can be done from home"). | Tech-Limited Senior | F-TLS-12 | Decision logic with provider. |

#### Medications

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-140 | Smart medication reminders that suppress if dose already logged. | Chronic Condition Manager | F-CCM-10 | |
| F-141 | Printable / downloadable medication list. | Tech-Limited Senior | F-TLS-10 | |
| F-142 | Self-service prescription refill simple enough for low-tech users (UX requirement). | Tech-Limited Senior | F-TLS-11 | |
| F-143 🔁 | **Medication Coordination capability** — single capability combining: (a) authoritative active med list (EHR + Surescripts fill data + patient-reported); (b) ownership / attribution per med with soft "primary owner" flag for high-risk classes; (c) change notification to owners and patient-visible change history. | Chronic Condition Manager, PCP, Specialist | F-CCM-04 (subset), F-PCP-10, F-SP-15 | **Resolution applied (Conflict 17).** |

#### Billing & Financial

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-150 ✚ | Family-wide consolidated bill view + pay. Statements consolidate across encounters and family members under a single guarantor account, with line-item detail. Multiple payment methods (card, ACH, Apple Pay, Google Pay). | Busy Parent | F-BP-14, G-BILL-04, G-BILL-08 | Merged. |
| F-151 🆕 | Insurance eligibility verification at appointment booking, with deductible / copay estimate where possible. | (gap-sourced) | G-BILL-02 | Subsumes Nice-to-Have F-203. |
| F-152 🆕 | Good Faith Estimates generated for self-pay patients per federal No Surprises Act requirements. | (gap-sourced) | G-BILL-03 | Regulatory. |
| F-153 🆕 | Refund and adjustment workflows visible to patient; no silent balance changes. | (gap-sourced) | G-BILL-07 | |

#### Telehealth

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-160 | Telehealth video visits, particularly for low-acuity pediatric and chronic-care follow-ups. | Busy Parent | F-BP-16 | |

#### Provider Workflow & Analytics

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-170 ✚ | Population-health dashboard: gaps in care, quality-metric performance, panel risk-stratification. Pop-health surface defined in coordination with quality / value-based-care team. | PCP | F-PCP-18, G-OBS-08 | |
| F-171 | Care-gap and quality alerts shown in a dedicated review surface, **not** as in-visit popups. | PCP | F-PCP-19 | |
| F-172 ✚ | Smart-phrase / dot-phrase parity with EHR (or integration so providers don't lose existing libraries). Shared library with governance, ability to favorite, auditability when shared phrases are used in clinical notes. | PCP | F-PCP-20, G-CMS-07 | |
| F-173 | Outside-records ingestion (imaging, prior op notes, outside labs) — replace CD-ROM / fax workflows. | Specialist | F-SP-11 | Phased per Conflict 16. |
| F-174 | Pre-authorization status visible in specialist patient view. | Specialist | F-SP-12 | Payer integration dependency. |
| F-175 ✚ | Auto-pushed condition-specific patient education on diagnosis. Patient education content follows a defined lifecycle: authoring, clinical review, approval, scheduled review (≤ 24 months), retirement, with audit trail. | Specialist | F-SP-13, G-CMS-01 | |
| F-176 | Structured consult-back template ("assessment + plan + what I changed + what PCP should do"). | Specialist | F-SP-14 | |
| F-177 | Specialty-specific patient check-in workflows (e.g., CHF daily-weight log w/ alert thresholds → nurse). | Specialist | F-SP-16 | |
| F-178 🔁 | **Shared care plan** — co-editable by PCP + specialist(s), patient-visible read-mostly with annotation and Q&A. PCP is default owner/coordinator; specialists own condition-specific sections w/ attribution. Versioned with full edit history; coordination alert on conflicting changes (no silent overwrites). Fallback ownership rules when no PCP is identified. | Chronic Condition Manager, PCP, Specialist | F-SP-17 + cross-persona | **Resolution applied (Conflict 14).** |
| F-179 | Specialty outcomes dashboards (cardiology MVP: 30/60/90-day readmits, post-PCI complication rates, AFib control, time-in-therapeutic-range). | Specialist | F-SP-18 | |
| F-180 | Trainee / fellow / resident supervised access mode. | Specialist | F-SP-19 | **Resolution applied (Conflict 15):** Phase 3 add-on. |
| F-181 🆕 | Asynchronous-care billing workflow integrated with revenue cycle; provider can mark a message exchange as billable with appropriate documentation. | (gap-sourced) | G-OPS-04 | Operationalizes B-010. |

#### Engagement & Onboarding

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-190 ✚ | Release / change-management UX: feature changes batched and previewed in advance; opt-in preview followed by mandatory adoption window. Communication via in-app, email, and (for 70+ cohort) printed materials at clinic check-in. | Tech-Limited Senior | F-TLS-13, G-TRN-06 | |
| F-191 | "Trusted clinic" branding in app — show clinic name, staff names (and optional photos) to combat scam-call confusion. | Tech-Limited Senior | F-TLS-14 | Anti-phishing UX. |
| F-192 🆕 | Patient onboarding flow with progressive disclosure, optional guided tour, completion measured; assisted-onboarding path for in-clinic registration. | (gap-sourced) | G-TRN-03 | |
| F-193 🆕 | In-app contextual help: every primary action has an accessible "What is this?" affordance; help content is part of the content lifecycle (F-175 framework). | (gap-sourced) | G-TRN-04 | |
| F-194 🆕 | Adoption-monitoring intervention triggers — e.g., provider portal usage drops below threshold → champion outreach. | (gap-sourced) | G-TRN-07 | |

#### Content, Language & Accessibility (functional aspects)

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-195 🆕 | Multi-language patient-facing content at launch in defined languages (proposed: English + top 2 by population; expand to top 5 by Phase 3). | (gap-sourced) | G-CMS-02 | |

#### Interoperability (functional aspects)

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-196 🆕 | DICOM imaging viewer or link-out for outside-sourced imaging; security review required for any embedded viewer. | (gap-sourced) | G-INT-04 | Supports F-173. |
| F-197 🆕 | Event / webhook capability for partner integrations (e.g., appointment-confirmed event); documented event schema. | (gap-sourced) | G-INT-07 | |

#### Observability (functional aspects)

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-198 🆕 | Analytics events for product success metrics (registration rate, MAU, self-scheduled appointments, message volume per provider, etc.) instrumented from launch. | (gap-sourced) | G-OBS-05 | Required to measure brief KPIs. |
| F-199 🆕 | Patient-facing transparency: patients can request which of their data has been used for which analytics purpose. | (gap-sourced) | G-OBS-09 | Intersects HIPAA accounting of disclosures. |

---

### Nice-to-Have

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| F-200 🔁 | Wearable / device data ingestion (Apple HealthKit, Google Health Connect, Dexcom CGM). **Phase 1:** patient-facing only (not pushed to provider chart). **Phase 2:** opt-in provider review with provenance, summary stats only, condition-specific alert thresholds, and a clearly documented review-expectation policy. | Chronic Condition Manager | F-CCM-17, F-CCM-18, F-PCP-21 | **Resolution applied (Conflict 8).** |
| F-201 | Correlation insights — surface relationships between med changes and tracked metrics. | Chronic Condition Manager | F-CCM-19 | Clinical validation required; AI-governance scope. |
| F-202 | "What changed since last time" summary on lab-results landing page. | Chronic Condition Manager | F-CCM-20 | Templated, not necessarily AI-generated. |
| ~~F-203~~ | (Subsumed by F-151 Should-Have — eligibility/cost estimate.) | — | F-CCM-21 | |
| F-204 | HSA-eligibility tagging on bills / receipts. | Busy Parent | F-BP-21 | |
| F-205 ✚ | Self-service payment plan setup with transparent fees. | Busy Parent | F-BP-22, G-BILL-05 | |
| F-206 | Audit / access-log visibility for parents (who saw kid's records). | Busy Parent | F-BP-23 | May be required by state law regardless. |
| F-207 | Audio readout / text-to-speech for results, messages, visit summaries. | Tech-Limited Senior | F-TLS-15 | OS-native TTS may cover MVP. |
| F-208 | Medication-identification aid — pill image alongside med name. | Tech-Limited Senior | F-TLS-16 | RxNorm + NLM RxImage dependency. |
| F-209 | "Easy mode" / "simple mode" toggle with larger touch targets, fewer options. | Tech-Limited Senior | F-TLS-17 | Realized via dashboard variants (F-090). |
| F-210 | In-clinic / in-person onboarding support (ambassador program, printed quick-start). | Tech-Limited Senior | F-TLS-18 | Service-design, not pure product. |
| F-211 | Wearable / device summary stats with provenance for providers (gated by patient consent + review-expectation policy). | PCP | F-PCP-21 | Subsumed by F-200 Phase 2 scope. |
| F-212 | Inbox volume dashboard for physicians to monitor own load. | PCP | F-PCP-22 | |
| F-213 | Patient-message templates for common responses. | PCP | F-PCP-23 | |
| F-214 | Templated post-procedure check-ins (day 1 / 3 / 7 / 14). | Specialist | F-SP-21 | |
| F-215 | Device-manufacturer integration for cardiac devices (pacemaker / ICD interrogation). | Specialist | F-SP-22 | Long-term; multi-vendor. |
| F-216 | Care-plan goal tracking (target BP, LDL, weight, EF) with progress visualization. | Specialist | F-SP-23 | Part of F-178 shared care plan. |
| F-217 🆕 | Financial assistance / charity care application initiated from the portal; status tracking. | (gap-sourced) | G-BILL-06 | |

---

## Non-Functional Requirements

### Must-Have (NF)

#### Accessibility & UX

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-010 ✚ | WCAG 2.1 AA conformance minimum; AAA-level contrast where feasible. Conformance verified by independent accessibility audit pre-launch and on a defined cadence; remediation SLAs by severity. | Tech-Limited Senior | NF-TLS-01, G-COMP-07 | |
| NF-011 | User-configurable text size scaling beyond OS default. | Tech-Limited Senior | NF-TLS-02 | |
| NF-012 | High-contrast color choices; never rely on color alone; no yellow-on-white combinations. | Tech-Limited Senior, Chronic Condition Manager | NF-TLS-03, NF-CCM-02 | |
| NF-013 | Touch targets ≥ 44pt (iOS) / 48dp (Android) for primary actions. | Tech-Limited Senior | NF-TLS-04 | |
| NF-014 🔁 | UI stability — minimize layout / navigation changes between releases; major UI updates ship with opt-in preview followed by mandatory adoption window; advance notice via in-app + email + (for 70+ cohort) printed materials. | Tech-Limited Senior | NF-TLS-05 | **Resolution applied (Conflict 13).** |
| NF-015 | Sub-3-tap completion of common patient tasks (refill, reschedule, view immunizations). | Busy Parent | NF-BP-01 | UX performance budget. |
| NF-016 | Native-quality mobile experience (no thin web-wrapper feel). | Busy Parent | NF-BP-02 | Architectural implication. |
| NF-017 🆕 | Plain-language reading-level target (e.g., 6th–8th grade) for patient-facing content, validated by tooling. | (gap-sourced) | G-CMS-09 | |

#### Performance & Reliability

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-020 | Provider chart open < 2 sec; order screen < 1 sec; message open < 1 sec (at 95th percentile). | PCP | NF-PCP-01 | Measured + enforced. |
| NF-021 | 99.9% uptime minimum; zero unplanned downtime during clinic hours for provider surfaces. | PCP, Specialist | NF-PCP-02, NF-SP-03 (brief) | |
| NF-022 | Fast session resume between procedures + auto-logout on inactivity for shared workstations. | Specialist | NF-SP-02 | |
| NF-023 | Mobile parity: secure view-only chart access from phone, biometric login, no PHI cached locally beyond session. | Specialist | NF-SP-04 | |
| NF-024 | Outage notification SLA: proactive alert to providers ≥ defined pre-notice window before scheduled or detected unavailability (window TBD). | PCP | NF-PCP-06 | |
| NF-025 | Push notification reliability — delivered promptly even when app is backgrounded (iOS + Android). | Busy Parent | NF-BP-06 | |
| NF-026 🆕 | Patient mobile app cold start ≤ 3s on mid-tier device + broadband; ≤ 5s on LTE. | (gap-sourced) | G-PERF-01 | |
| NF-027 🆕 | Patient web initial load (TTI) ≤ 3s on broadband; ≤ 5s on LTE. | (gap-sourced) | G-PERF-02 | |
| NF-028 🆕 | Common patient actions (open message thread, view appointment, view med list) ≤ 1.5s at 95th percentile. | (gap-sourced) | G-PERF-03 | |
| NF-029 🆕 | Concurrent user capacity sized for projected peak; baseline DAU, peak-to-average ratio, headroom multiplier documented. | (gap-sourced) | G-PERF-04 | |
| NF-029b 🆕 | Telehealth video sessions meet defined quality SLOs (jitter, packet loss, MOS); per-session quality monitoring with auto-escalation on degradation. | (gap-sourced) | G-PERF-05 | |
| NF-029c 🆕 | Graceful degradation under poor network conditions — async actions queue and retry; critical surfaces (med list, ID card, emergency info) available offline. | (gap-sourced) | G-PERF-06 | |
| NF-029d 🆕 | Defined SLOs with error budgets per capability (auth, messaging, scheduling, telehealth); public-facing status page surfaces current state. | (gap-sourced) | G-PERF-07 | |
| NF-029e 🆕 | Load testing against peak-day projections before each major release; results published. | (gap-sourced) | G-PERF-08 | |
| NF-029f 🆕 | CDN / caching strategy for static assets; cache-busting protocol on release. | (gap-sourced) | G-PERF-10 | |
| NF-029g 🆕 | Feature-flag / kill-switch capability for every major user-facing capability, enabling rapid disable without redeploy. | (gap-sourced) | G-ERR-06 | |
| NF-029h 🆕 | Documented incident-response runbooks, rollback procedures, and provider/patient communication templates; post-incident reviews with documented learnings. | (gap-sourced) | G-ERR-07, G-ERR-08 | |
| NF-029i 🆕 | Disaster recovery plan with documented RTO / RPO, tested at least annually. | (gap-sourced) | G-COMP-11 | |

#### Authentication, Identity & Access (NF)

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-030 🔁 ✚ | MFA required for all PHI-bearing account access; biometric on registered devices counts as a factor. Step-up authentication required for first use on a new device, sensitive-category access, and proxy-access changes. **No CAPTCHA in normal patient flows;** bot protection via device trust, rate limiting, risk-based signals. | Busy Parent, Tech-Limited Senior | NF-BP-04, NF-TLS-06, G-AUTH-02, G-AUTH-10 | **Resolution applied (Conflict 11).** |
| NF-030b 🆕 | Patient identity proofing at registration meets NIST 800-63-3 IAL2 minimum (in-clinic proofing, KBA, or approved remote-ID-verification vendor). | (gap-sourced) | G-AUTH-01 | |
| NF-030c 🆕 | RBAC model for providers and staff: roles for physician, MA, nurse, scheduler, billing, IT-admin, with least-privilege defaults. | (gap-sourced) | G-AUTH-04 | |
| NF-030d 🆕 | Session timeout policies: shorter for shared workstations and provider clinical surfaces, longer for patient personal devices, all within HIPAA-acceptable bounds. | (gap-sourced) | G-AUTH-08 | |
| NF-030e 🆕 | Service accounts / system integrations use rotated credentials or workload identity; no shared static secrets. | (gap-sourced) | G-AUTH-09 | |

#### Data Security & Privacy

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-031 | Message delivery + acknowledgement guarantees (no silent loss). | Chronic Condition Manager, Tech-Limited Senior | NF-CCM-04 | |
| NF-032 ✚ | Comprehensive audit logging: every PHI access (read, write, export, print) logged with user, timestamp, action, record identifier, source IP / device, justification where required. Logs immutable / append-only, retained ≥ 6 years, with integrity protection. | Chronic Condition Manager | NF-CCM-03, G-COMP-01, G-COMP-02 | Patient-facing view = F-003. |
| NF-033 | Hard separation of clinical vs. marketing notification channels — enforced technically. | Busy Parent | NF-BP-05 | **Resolution applied (Conflict 3).** |
| NF-034 🔁 | Anti-phishing affordances — clinic identity verification surface, no unexpected SMS login links, secure in-app inbox for sensitive comms. | Tech-Limited Senior | NF-TLS-08 | |
| NF-035 🆕 | All PHI encrypted in transit (TLS 1.2+ minimum, 1.3 preferred) and at rest (AES-256). | (gap-sourced) | G-SEC-01 | |
| NF-036 🆕 | Key management via managed KMS / HSM-backed service; documented key rotation policy. | (gap-sourced) | G-SEC-02 | |
| NF-037 🆕 | Data classification scheme defined (PHI, PII, sensitive subcategories) and applied across the data model; access control evaluated per classification. | (gap-sourced) | G-SEC-03 | |
| NF-038 🆕 | Sensitive data categories (mental/behavioral health, substance use, HIV/STI, reproductive, genetic, adolescent) subject to elevated access controls and explicit consent for sharing. | (gap-sourced) | G-SEC-04 | Pairs with F-095. |
| NF-039 🆕 | All vendors / sub-processors handling PHI under signed BAA; BAA scope, audit rights, and breach notification SLAs documented. | (gap-sourced) | G-SEC-06 | |
| NF-039b 🆕 | Documented breach detection, classification, escalation, and notification procedures meeting HIPAA Breach Notification Rule and state-law timelines. | (gap-sourced) | G-SEC-08 | |
| NF-039c 🆕 | Cloud hosting region(s) constrained to US (or per org policy); cross-border data flows prohibited unless explicitly approved. | (gap-sourced) | G-SEC-10 | |
| NF-039d 🆕 | Penetration testing, SAST, DAST, and dependency scanning integrated into CI/CD; remediation SLAs by severity. | (gap-sourced) | G-SEC-11 | |
| NF-039e 🆕 | Secrets management — no credentials in code or config; centralized secret store with rotation. | (gap-sourced) | G-SEC-12 | |

#### AI Governance

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-040 🔁 | AI never sends clinical content to patients without provider review + explicit signoff. (Limited exception: purely administrative templated autoresponses with no clinical content.) | PCP | NF-PCP-03 | **Resolution applied (Conflict 4).** |
| NF-041 | All AI-generated artifacts are labeled as AI-generated; source data + citations are one click away. | Chronic Condition Manager, PCP | NF-CCM-05, NF-PCP-04 | |
| NF-042 | No in-visit interrupting popups for non-emergency alerts. | PCP | NF-PCP-05 | |
| NF-043 🆕 | AI features tested for performance disparities across protected demographic groups before launch and on a defined cadence; mitigation triggered on threshold breach. | (gap-sourced) | G-ETH-01 | |
| NF-044 🆕 | AI features have a documented model card or equivalent describing intended use, training-data scope, known limitations, and out-of-scope use. | (gap-sourced) | G-ETH-05 | |
| NF-045 🆕 | Patient data used for model training only under explicit opt-in consent; governance includes IRB-equivalent review where applicable. | (gap-sourced) | G-ETH-03 | |

#### Media & Data Handling

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-050 ✚ | Secure storage + lifecycle for user-uploaded photos/videos: encryption at rest, defined retention, patient deletion right, never stored outside PHI boundary. | Busy Parent | NF-BP-03, G-SEC-09 | |
| NF-051 | Data export — patient ability to download own health data (HIPAA right of access). | Chronic Condition Manager | NF-CCM-06 | Aligns with F-096. |
| NF-052 🆕 | Records retention and disposition schedule defined per data class; automated disposition at end of retention period. | (gap-sourced) | G-COMP-08 | |

#### Patient Safety

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-060 | Patient-safety NFR: pre-op checklist alert if not confirmed by procedure − 24 hrs; clear escalation path. | Specialist | NF-SP-01 | |
| NF-061 🆕 | Vulnerable-population safeguards: defined handling for shared-device / household-abuse scenarios (e.g., quick-hide UI, separate notification channels for sensitive content). | (gap-sourced) | G-ETH-04 | |

#### Measurement Guardrails

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-070 🔁 | Engagement / success metrics for the 70+ cohort must **not** include reduction in phone-call volume; alternative metrics (satisfaction, completion of attempted digital tasks, absence of harm) defined. | Tech-Limited Senior | NF-TLS-07 | **Resolution applied (Conflict 6).** |
| NF-071 🔁 | Org-wide phone-call-reduction target (50%) scoped explicitly to call types the portal is designed to displace. | derived (Conflict 6) | brief target | |
| NF-072 🆕 | Portal adoption and engagement metrics stratified by demographic group; disparities trigger remediation planning. | (gap-sourced) | G-ETH-02 | |
| NF-073 🆕 | Provider performance dashboards include guardrails: ratio metrics (not absolute), peer-comparison ranges (not rankings), explicit policy that metrics are coaching tools, not evaluation. | (gap-sourced) | G-OBS-06 | |

#### Compliance & Audit

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-074 🆕 | Information-blocking compliance: no technical or procedural barriers preventing patient or authorized recipient access to ePHI; exceptions documented per the rule. | (gap-sourced) | G-COMP-04 | Pairs with F-076. |
| NF-075 🆕 | 42 CFR Part 2 — if substance-use disorder records are in scope, segmentation, consent, and re-disclosure controls implemented per rule. (Scope determination required first.) | (gap-sourced) | G-COMP-05 | |
| NF-076 🆕 | State privacy law compliance matrix maintained for each state where patients reside; technical requirements derived from the matrix. | (gap-sourced) | G-COMP-06 | |
| NF-077 🆕 | Privileged-user (admin, support, integration) access to PHI logged separately and reviewed at higher cadence. | (gap-sourced) | G-COMP-09 | |
| NF-078 🆕 | Annual HIPAA risk assessment covering the portal scope; remediation backlog tracked. | (gap-sourced) | G-COMP-10 | |
| NF-079 🆕 | Defined audit-review workflow: scheduled sampling, anomaly detection, alerting on suspicious patterns (VIP record access, mass export). | (gap-sourced) | G-COMP-03 | |

#### Observability

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-080a 🆕 | Defined telemetry baseline covering auth events, navigation, feature use, error events, performance traces, with PHI minimization. | (gap-sourced) | G-OBS-01 | |
| NF-080b 🆕 | All product analytics tools comply with current OCR guidance on tracking technologies; no third-party trackers on PHI-bearing pages without BAA and explicit consent. | (gap-sourced) | G-OBS-02 | |
| NF-080c 🆕 | Operational monitoring: latency, error rate, saturation, traffic per critical capability, with alerting tied to error budgets. | (gap-sourced) | G-OBS-03 | |
| NF-080d 🆕 | On-call rotation for portal services with documented escalation paths; clinical-impact incidents notified to clinical leadership in real time. | (gap-sourced) | G-OBS-04 | |
| NF-080e 🆕 | A/B testing framework restricted to non-clinical UX changes; clinical-workflow A/B tests require IRB / clinical-leadership approval. | (gap-sourced) | G-OBS-07 | |

#### Content Governance

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-081 🆕 | Translation governance: machine translation requires human qualified-translator review for clinical content; non-clinical content may use reviewed MT. | (gap-sourced) | G-CMS-03 | |
| NF-082 🆕 | Content versioning: every patient interaction with educational content, consent form, or notification template records the version shown; retrievable for audit. | (gap-sourced) | G-CMS-04 | |
| NF-083 🆕 | Notification templates (push, email, SMS, voice) follow an approval workflow; clinical-content templates require clinical review, marketing-content templates require communications review. | (gap-sourced) | G-CMS-06 | |

#### Training, Helpdesk, Change Mgmt

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-084 🆕 | Provider training program: role-based curriculum, required completion before go-live access, refresher cadence (annual + feature-driven). | (gap-sourced) | G-TRN-01 | |
| NF-085 🆕 | Champion / super-user program identified per practice or clinic, with defined responsibilities and recognition. | (gap-sourced) | G-TRN-02 | |
| NF-086 🆕 | Helpdesk model documented for patients and providers: tiered support, SLA per tier, escalation paths; staffing funded before launch. | (gap-sourced) | G-TRN-05 | |
| NF-087 🆕 | Multilingual onboarding materials and helpdesk support in supported languages (aligns with F-195). | (gap-sourced) | G-TRN-08 | |
| NF-088 🆕 | Accessibility-specific onboarding pathway and training materials for users with visual, motor, or cognitive impairments. | (gap-sourced) | G-TRN-09 | |

#### Interoperability

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-089 🆕 | FHIR R4 API conformant with US Core profiles for patient-data access; published API documentation. | (gap-sourced) | G-INT-01 | |
| NF-089b 🆕 | Patient-app authorization via SMART on FHIR / OAuth 2.0 per Cures Act standards. | (gap-sourced) | G-INT-02 | |
| NF-089c 🆕 | Reference terminologies enforced for structured data: LOINC (labs), SNOMED CT (problems), RxNorm (meds), CPT (procedures), ICD-10 (dx). | (gap-sourced) | G-INT-03 | |
| NF-089d 🆕 | API rate limits, authentication standards, deprecation policy (minimum 12-month deprecation window) published for third-party developers. | (gap-sourced) | G-INT-06 | |

#### Billing & PCI

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-089e 🆕 | Payment processing via a PCI-DSS-compliant processor; no card data stored within portal application boundary. | (gap-sourced) | G-BILL-01 | |

---

### Should-Have (NF)

| ID | Requirement | Stakeholders | Source | Notes |
|---|---|---|---|---|
| NF-090 | Liability-bounded scope on continuous device-data review — provider not assumed to be reviewing 24/7 streams; policy documented. | PCP | NF-PCP-07 | **Resolution applied (Conflict 8).** |
| NF-091 | Session persistence across short context switches between visits. | PCP | NF-PCP-08 | |
| NF-092 | Consult-note delivery confirmation tracked and surfaced. | Specialist | NF-SP-05 | |
| NF-093 | Trainee actions require attending sign-off where applicable; full audit trail. | Specialist | NF-SP-06 | Phase 3 alongside F-180. |
| NF-094 | App-to-OS integrations for sharing PDFs / storing insurance cards (Apple Wallet, Files, share sheet). | Busy Parent | NF-BP-07 | |
| NF-095 | Usability tested with low-vision and elderly participants explicitly (not just WCAG checklist). | researcher / Tech-Limited Senior | NF-TLS-09 | Process requirement. |
| NF-096 🆕 | TEFCA / Carequality / eHealth Exchange participation strategy decision recorded with timing. | (gap-sourced) | G-INT-05 | |
| NF-097 🆕 | Vendor evaluation framework covering security, HIPAA, performance, financial stability, support SLA, exit / data-portability. | (gap-sourced) | G-VEN-01 | |
| NF-098 🆕 | Vendor agreements require data export in defined standard formats on termination, within defined timelines. | (gap-sourced) | G-VEN-02 | |
| NF-099 🆕 | Open-source license inventory maintained; license compatibility reviewed before adoption. | (gap-sourced) | G-VEN-03 | |
| NF-099b 🆕 | Vendor performance reviewed against SLA quarterly; escalation paths defined. | (gap-sourced) | G-VEN-04 | |

---

## Business Requirements

| ID | Requirement | Stakeholders | Priority | Source | Notes |
|---|---|---|---|---|---|
| B-001 | Reduce administrative burden experienced by chronic-care patients acting as the messenger between providers. | Chronic Condition Manager | Should | B-CCM-01 | |
| B-002 | Improve portal adoption to meet brief targets (60% registration, 40% MAU) through reduced friction across cohorts. | Chronic Condition Manager, Busy Parent | Should | B-CCM-02 | |
| B-003 | Reduce family-care no-shows via reliable, channel-correct reminders. | Busy Parent | Should | B-BP-01 | Maps to brief's 10% no-show reduction. |
| B-004 | Reduce billing-call volume and improve collection cycle through consolidated billing experience. | Busy Parent | Should | B-BP-02 | |
| B-005 🔁 | Family-account capability is a Phase-1 differentiator with the MVP scope defined in F-001. | Busy Parent | Must | B-BP-03 | **Resolution applied (Conflict 7).** |
| B-006 🔁 | Avoid creating a digital divide — equitable access for elderly, low-tech, and accessibility-impacted patients is a launch requirement. | Tech-Limited Senior | Must | B-TLS-01 | |
| B-007 | Onboarding investment for 70+ cohort funded before launch (in-person help, printed guides, ambassador staffing). | Tech-Limited Senior | Should | B-TLS-02 | |
| B-008 🔁 | KPI framing: phone-call reduction is not a primary KPI for the 70+ cohort; alternative engagement metrics defined. | Tech-Limited Senior | Should | B-TLS-03 | **Resolution applied (Conflict 6).** |
| B-009 | Cap or measurably reduce physician message-handling time (target ties to brief's 30% admin-time reduction). | PCP | Must | B-PCP-01 | |
| B-010 🔁 | Asynchronous clinical messaging must have a defined billing / compensation model before nurse-triage and async-chat capabilities ship. | PCP, Busy Parent (implied) | Should | B-PCP-02 | **Resolution applied (Conflict 2).** |
| B-011 | Coordinate AI surfaces across the portal and the separate ambient-scribe initiative — single AI experience for physicians. | PCP | Should | B-PCP-03 | |
| B-012 | Establish ongoing provider advisory council for input throughout build and beyond. | PCP, researcher | Should | B-PCP-04 | |
| B-013 | Reduce referral-to-seen lag (current 6 weeks new, 5 days urgent) via intelligent intake + coordination. | Specialist | Should | B-SP-01 | |
| B-014 | Reduce redundant referrals and duplicate workups through better coordination. | Specialist | Should | B-SP-02 | |
| B-015 🔁 | Specialty-customizable portal experience delivered via a single configurable platform — not retrofit from PCP design and not separate apps. | Specialist | Must | B-SP-03 | **Resolution applied (Conflict 9).** |
| B-016 🔁 | Scope expansion: trainee / teaching workflow added as a Phase 3 deliverable; parallel discovery in Phase 1. | Specialist | Should | B-SP-04 | **Resolution applied (Conflict 15).** |
| B-017 🆕 | Post-launch operational ownership documented per capability; on-call rotation funded. | (gap-sourced) | Must | G-LCM-01 | |
| B-018 🆕 | Annual roadmap process with structured stakeholder input (provider advisory, patient advisory, ops). | (gap-sourced) | Should | G-LCM-02 | |
| B-019 🆕 | Feature sunset criteria: usage thresholds + value review trigger retirement consideration; sunset communicated per release-comms standards. | (gap-sourced) | Should | G-LCM-03 | |
| B-020 🆕 | Long-term cost model maintained; storage growth, vendor renewals, infrastructure scaling reviewed annually. | (gap-sourced) | Should | G-LCM-04 | |

---

## Constraints & Dependencies

### Regulatory / Legal

- **D-001** — HIPAA Privacy & Security Rules, HITECH, Breach Notification Rule.
- **D-002** — 21st Century Cures Act / information-blocking compliance (F-020, F-076, NF-074, NF-089b).
- **D-003** — Adolescent-privacy workflows (F-006, F-110) depend on state-by-state consent laws.
- **D-004** — Co-guardian verification (F-001) depends on identity-proofing process and legal-guardian documentation handling.
- **D-005** — 42 CFR Part 2 scope determination required; if in scope, segmentation controls apply (NF-075).
- **D-006** — State privacy laws compliance matrix (NF-076).
- **D-007** — EPCS / DEA requirements (F-043).
- **D-008** — NIST 800-63-3 IAL2 (NF-030b) — methods must be vetted by Security + Privacy.
- **D-009** — No Surprises Act / Good Faith Estimates (F-152).
- **D-009b** — OCR tracking-technologies guidance (NF-080b).

### EHR & Vendor

- **D-010** — Epic MyChart API availability — gates much of Phase 1.
- **D-011** — Surescripts integration scope + data-rights agreement (F-044, F-143).
- **D-012** — Apple HealthKit + Google Health Connect (F-200 Phase 1).
- **D-013** — Dexcom CGM (F-200 Phase 2).
- **D-014** — Device-manufacturer integration (F-215) — per-vendor agreements.
- **D-015** — Payer integration (F-174, F-151).
- **D-016** — Ambient-scribe initiative (B-011) — owner / governance unknown.
- **D-017** — Carequality / eHealth Exchange / TEFCA strategy (F-055, F-173, NF-096) — strategic decision required.
- **D-018** — Epic Haiku integration scope (F-081).
- **D-019** 🆕 — Payment processor selection + PCI scope decision (NF-089e, F-150).

### Organizational / Staffing

- **D-020** — Nurse-triage staffing model + FTE budget (F-100, F-012) — **gate** for shipping async chat.
- **D-021** — Async-messaging billing workflow (B-010, F-181) depends on revenue-cycle process design.
- **D-022** — In-person onboarding (F-210) depends on clinic staffing/budget.
- **D-023** — Procedure-team-nurse routing (F-057) depends on org staffing.
- **D-024** — Provider advisory council (B-012) — leadership endorsement.
- **D-025** — Phone-channel preservation policy (NF-070 / B-008) requires operations-leadership commitment.
- **D-026** 🆕 — Helpdesk staffing (NF-086) funded before launch.
- **D-027** 🆕 — Champion/super-user identification (NF-085) — clinical leadership endorsement.
- **D-028** 🆕 — Provider training program design + delivery (NF-084) — clinical education capacity.

### Technical / Architectural

- **D-030** — Specialty-configurable summary view (F-050) depends on flexible data-presentation framework.
- **D-031** — Granular sharing (F-095) depends on EHR / data-layer segmentation capability.
- **D-032** — Med-ownership flag (F-143) depends on Epic schema flexibility.
- **D-033** — Performance budgets (NF-020, NF-026, NF-028) depend on Epic API latency — partially outside our control.
- **D-034** — Symptom triage (F-121) depends on clinical-decision-support governance + medical-legal sign-off.
- **D-035** — Auto-pushed dx-triggered education (F-175) depends on maintained education content library + trigger governance.
- **D-036** — Apple Pay / Google Pay / ACH (F-150) depend on payment-processor integration + PCI scope.
- **D-037** — Apple Wallet integration (NF-094) depends on Apple developer program + pass design.
- **D-038** — Pill-image (F-208) depends on RxNorm / NLM RxImage coverage.
- **D-039** — Biometric / passwordless login (NF-030) depends on device capability + HIPAA-acceptable assurance.
- **D-040** 🆕 — Telehealth vendor selection drives NF-029b (video quality SLOs) feasibility.
- **D-041** 🆕 — Data warehouse / analytics pipeline (F-198, F-179, F-170) — platform team.
- **D-042** 🆕 — Feature-flag platform (NF-029g) — engineering platform choice.
- **D-043** 🆕 — CDN selection (NF-029f).
- **D-044** 🆕 — KMS / HSM availability for key management (NF-036).

### Process / Governance

- **D-050** 🆕 — Org AI-governance policy ownership and approval timeline (NF-040–NF-045).
- **D-051** 🆕 — Vendor management process (NF-097–NF-099b) — procurement engagement model.
- **D-052** 🆕 — IRB / research ethics involvement for AI training-data consent (NF-045).

---

## Ambiguities & Open Questions

| ID | Question | Source | Owner / Resolution Path |
|---|---|---|---|
| A-001 | Definitive list of lab-result carve-out categories for the provider-review window. | F-020 | Clinical leadership. |
| A-002 | Symptom triage (F-121): in-scope for v1, deferred, or excluded? | F-CCM-11 | Clinical + legal. |
| A-003 | Granular sharing UX complexity (F-095) vs. usefulness. | F-CCM-12 | UX design exploration. |
| A-004 | Provider visibility into patient-logged data: opt-in by patient, by provider, or both? | F-123, F-200 | Clinical policy. |
| A-005 | AI summary / interpretation features roadmap placement and labeling. | NF-040, NF-041 | AI-governance owner. |
| A-006 | Co-equal parent rights in divorced / split-custody scenarios. | F-001 | Legal. |
| A-007 | Adolescent-privacy default state at age threshold (lockout vs. graded access); Phase 1 placement of F-006. | F-006, F-110 | Legal + clinical. |
| A-008 | Temp caregiver access lifecycle (F-111). | F-BP-18 | Privacy + design. |
| A-009 | Photo / video retention duration and auto-deletion policy (NF-050). | F-BP-12 | Privacy + legal. |
| A-010 | Family bill model — separate financial responsibility per member vs. single guarantor (F-150). | F-BP-14 | Revenue cycle. |
| A-011 | Adolescent-privacy emergency parental override — definition of "emergency". | F-006, F-110 | Legal + clinical. |
| A-012 | Default home dashboard mode for users 70+ (F-090). | F-TLS-04 | UX + equity review. |
| A-013 | Tension between low-friction patient login (NF-030) and security review board posture. | NF-TLS-06 | Security review board. |
| A-014 | Audit-log notification to seniors re: proxy access. | F-003 | UX. |
| A-015 | TTS scope (F-207): v1 OS pass-through vs. v2 curated audio. | F-TLS-15 | Roadmap. |
| A-016 | Telehealth eligibility surfacing (F-132): rules engine vs. provider opt-in per visit type. | F-TLS-12 | Clinical informatics. |
| A-017 | Operational enforcement of phone-channel preservation if portal-adoption KPIs incentivize call deflection. | researcher | Operations leadership. |
| A-018 | AI draft vs. autoreply line (NF-040) — admin auto-acknowledgement definition. | NF-PCP-03 | AI governance. |
| A-019 | "Red-flag symptom" detection (F-016): conditions, thresholds, false-positive handling. | F-PCP-05 | Clinical informatics. |
| A-020 | Provider-to-provider messaging scope (F-017): same-system only vs. cross-system. | F-PCP-06 | Strategy. |
| A-021 | Wearable-data provider-review-expectation policy (F-200 Phase 2 / NF-090) ownership. | F-PCP-21 | Legal + clinical leadership. |
| A-022 | Outage-alert pre-notice window (NF-024). | F-PCP-13 | SRE / ops. |
| A-023 | Coverage / handoff scope (F-103). | F-PCP-16 | Clinical operations. |
| A-024 | Performance budget enforcement: who measures, who is accountable when missed? | NF-020 | SRE + product. |
| A-025 | Specialty-configurable summary view (F-050): how many specialties at launch? Configuration ownership? | F-SP-05 | Clinical informatics. |
| A-026 | Pre-op checklist non-confirmation alert routing (F-056, NF-060). | F-SP-07 | Clinical operations. |
| A-027 | Procedure-team-nurse routing (F-057): scope of specialties. | F-SP-08 | Clinical operations. |
| A-028 | Trainee access model (F-180, NF-093): supervision varies by stage. | F-SP-19 | Clinical education. |
| A-029 | Med-ownership conflict-resolution flow (F-143): override authority. | F-SP-15 | Clinical leadership. |
| A-030 | Outside-records ingestion normalization scope (F-173). | F-SP-11 | Integration team. |
| A-031 | Care-plan ownership when multiple specialists involved (F-178). | F-SP-17 | Clinical leadership. |
| A-032 | Cross-system interop scope and phasing (D-017). | F-CCM-01, F-SP-11 | Strategy. |
| **A-033 🆕** | Identity-proofing method selection (NF-030b) — in-clinic, KBA, remote vendor, or combination? | G-AUTH-01 | Security + Patient Access. |
| **A-034 🆕** | Helpdesk operating model and PHI-aware account-recovery process (F-004, NF-086). | G-AUTH-03, G-TRN-05 | Patient Access + IT. |
| **A-035 🆕** | 42 CFR Part 2 applicability — does the org provide / store SUD records (NF-075)? | G-COMP-05 | Compliance. |
| **A-036 🆕** | Languages supported at launch and Phase-3 expansion (F-195, NF-087). | G-CMS-02, G-TRN-08 | Health equity + Communications. |
| **A-037 🆕** | Telehealth vendor strategy (white-label vs. partner) and resulting NFR feasibility (NF-029b). | G-PERF-05 | Strategy + clinical operations. |
| **A-038 🆕** | TEFCA participation timing and which QHIN (NF-096, D-017). | G-INT-05 | Interop strategy. |
| **A-039 🆕** | A/B testing scope and IRB threshold for clinical-workflow tests (NF-080e). | G-OBS-07 | Research ethics + clinical leadership. |
| **A-040 🆕** | Demographic stratification scheme for adoption metrics (NF-072) — categories, consent model. | G-ETH-02 | Health equity + privacy. |
| **A-041 🆕** | Vulnerable-population safeguard scope (NF-061) — which scenarios trigger which protections. | G-ETH-04 | Patient advocacy + UX. |
| **A-042 🆕** | Disaster recovery RTO / RPO targets per capability (NF-029i). | G-COMP-11 | SRE + business continuity. |
| **A-043 🆕** | Sunset criteria thresholds (B-019) — usage cutoff, value-review cadence. | G-LCM-03 | Product operations. |

---

## Traceability Index

Quick map from consolidated IDs back to per-persona source IDs and gap-analysis IDs:

| Consolidated | Source IDs |
|---|---|
| F-001 | F-BP-01, F-BP-02 |
| F-002 | F-CCM-13, F-TLS-07, F-BP-18 (subset), G-AUTH-05 |
| F-003 | F-TLS-08, NF-CCM-03, G-AUTH-07 (subset), G-COMP-09 (subset) |
| F-004 | G-AUTH-03 |
| F-005 | G-AUTH-07 |
| F-006 | F-BP-17, G-AUTH-06 |
| F-010 | F-CCM-02, F-TLS-02, G-ERR-02 (subset) |
| F-011 | F-PCP-01, G-OPS-02 |
| F-012 | derived (Conflict 2) |
| F-013–F-018 | F-PCP-02–F-PCP-06, F-SP-06, F-SP-20 |
| F-019, F-019b | G-ERR-03, G-ERR-04 |
| F-020–F-024 | F-CCM-03, F-CCM-04, F-CCM-08, F-TLS-05, F-TLS-06, Conflict 1, G-CMS-05 |
| F-030–F-035 | F-CCM-06/07/16, F-BP-04/05, F-TLS-03/09 |
| F-040–F-045 | F-CCM-05, F-BP-06/10, F-PCP-09/10/11 |
| F-050–F-057 | F-PCP-07/08, F-SP-01/02/03/04/05/07/08 |
| F-058, F-059 | G-OPS-03, G-OPS-05 |
| F-060 | F-PCP-12 |
| F-070–F-073 | F-CCM-15, F-BP-08, F-TLS-03, NF-TLS-08, F-PCP-13 |
| F-074, F-075, F-076 | G-ERR-01, G-ERR-05, G-ERR-09 + G-COMP-04 |
| F-080–F-081 | F-BP-07, F-PCP-14, F-SP-09 |
| F-090 | F-TLS-04 (+ Conflict 5) |
| F-095 | F-CCM-12, G-SEC-05, G-SEC-04 (subset) |
| F-096, F-097, F-098 | G-SEC-07, G-SEC-13, G-CMS-08 |
| F-100–F-104 | F-BP-11/12, F-PCP-15/16/17, G-OPS-01, G-OPS-02, G-OPS-06 |
| F-110–F-113 | F-BP-17/18/19/20, G-AUTH-06 |
| F-120, F-121, F-123 | F-CCM-09/11/14 |
| F-130–F-132 | F-BP-13/15, F-TLS-12 |
| F-140–F-143 | F-CCM-10, F-TLS-10/11, F-CCM-04 + F-PCP-10 + F-SP-15 |
| F-150–F-153 | F-BP-14, G-BILL-02/03/04/07/08 |
| F-160 | F-BP-16 |
| F-170–F-180 | F-PCP-18/19/20, F-SP-11/12/13/14/16/17/18/19, G-CMS-01, G-CMS-07, G-OBS-08 |
| F-181 | G-OPS-04 |
| F-190–F-194 | F-TLS-13/14, G-TRN-03/04/06/07 |
| F-195 | G-CMS-02 |
| F-196, F-197 | G-INT-04, G-INT-07 |
| F-198, F-199 | G-OBS-05, G-OBS-09 |
| F-200–F-217 | F-CCM-17/18/19/20/21, F-BP-21/22/23, F-TLS-15/16/17/18, F-PCP-21/22/23, F-SP-21/22/23, G-BILL-05/06/08 |
| NF-010–NF-017 | NF-TLS-01/02/03/04/05, NF-BP-01/02, NF-CCM-02, G-COMP-07, G-CMS-09 |
| NF-020–NF-025 | NF-PCP-01/02/06, NF-SP-02/03/04, NF-BP-06 |
| NF-026–NF-029i | G-PERF-01–08, G-PERF-10, G-ERR-06–08, G-COMP-11 |
| NF-030–NF-030e | NF-BP-04, NF-TLS-06, G-AUTH-01/02/04/08/09/10 |
| NF-031–NF-039e | NF-CCM-03/04, NF-BP-05, NF-TLS-08, G-SEC-01/02/03/04/06/08/10/11/12, G-COMP-01/02 |
| NF-040–NF-045 | NF-PCP-03/04/05, NF-CCM-05, G-ETH-01/03/05 |
| NF-050–NF-052 | NF-BP-03, NF-CCM-06, G-SEC-09, G-COMP-08 |
| NF-060, NF-061 | NF-SP-01, G-ETH-04 |
| NF-070–NF-073 | NF-TLS-07 + Conflict 6, G-ETH-02, G-OBS-06 |
| NF-074–NF-079 | G-COMP-03/04/05/06/09/10 |
| NF-080a–NF-080e | G-OBS-01/02/03/04/07 |
| NF-081–NF-083 | G-CMS-03/04/06 |
| NF-084–NF-088 | G-TRN-01/02/05/08/09 |
| NF-089–NF-089e | G-INT-01/02/03/06, G-BILL-01 |
| NF-090–NF-099b | NF-PCP-07/08, NF-SP-05/06, NF-BP-07, NF-TLS-09, G-INT-05, G-VEN-01/02/03/04 |
| B-001–B-016 | persona-source B-* IDs |
| B-017–B-020 | G-LCM-01/02/03/04 |
