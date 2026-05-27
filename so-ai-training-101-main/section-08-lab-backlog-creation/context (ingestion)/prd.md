# Product Requirements Document — HealthConnect Patient & Provider Portal

**Version:** 0.1 (Draft for stakeholder review)
**Date:** May 26, 2026
**Author:** M. Mettler
**Status:** Draft — pre-stakeholder review. Sections include explicit "Have / Need to validate" callouts so reviewers can see what is grounded vs. what is provisional.

**Source artifacts (in this repo):**
- Product brief: [input/00-healthcare-portal-reference.md](../input/00-healthcare-portal-reference.md)
- Per-persona requirements: [output/requirements-extracts/](requirements-extracts/)
- Conflicts & resolutions: [output/requirements-extracts/requirements-conflicts-and-resolutions.md](requirements-extracts/requirements-conflicts-and-resolutions.md)
- Gap analysis: [output/requirements-gap-analysis.md](requirements-gap-analysis.md)
- Consolidated requirements: [output/consolidated-requirements.md](consolidated-requirements.md)
- Market analysis: [output/market-analysis.md](market-analysis.md)
- Risk analysis: [output/risk-analysis.md](risk-analysis.md)

> **How to read this PRD.** Each section ends with a **"Have / Need to validate"** callout. The body of the section is the proposed PRD content; the callout is the discovery-honest view of what's been validated with stakeholders vs. what is still inferred or gap-sourced. Items marked "Need to validate" are not yet committed.

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Business Objectives](#2-business-objectives)
3. [User Personas and Use Cases](#3-user-personas-and-use-cases)
4. [Functional Requirements](#4-functional-requirements)
5. [Non-Functional Requirements](#5-non-functional-requirements)
6. [Technical Architecture](#6-technical-architecture)
7. [Success Metrics](#7-success-metrics)
8. [Risks and Mitigation](#8-risks-and-mitigation)
9. [Timeline and Milestones](#9-timeline-and-milestones)
10. [Open Questions & Decisions Needed](#10-open-questions--decisions-needed)
11. [Appendix A — Legacy Portal Migration & Cutover Plan](#11-appendix-a--legacy-portal-migration--cutover-plan)
12. [Appendix B — Cost Breakdown (Stakeholder Input Required)](#12-appendix-b--cost-breakdown-stakeholder-input-required)
13. [Appendix C — Acceptance Criteria for Phase 1 Must-Have Requirements](#13-appendix-c--acceptance-criteria-for-phase-1-must-have-requirements)
14. [Appendix D — Data Model & Key Sequence Diagrams](#14-appendix-d--data-model--key-sequence-diagrams)
15. [Appendix E — Testing Strategy](#15-appendix-e--testing-strategy)
16. [Appendix F — Pilot Plan (Framework + Stakeholder Input Required)](#16-appendix-f--pilot-plan-framework--stakeholder-input-required)
17. [Appendix G — Adolescent-Privacy State Matrix (Stakeholder Input Required)](#17-appendix-g--adolescent-privacy-state-matrix-stakeholder-input-required)
18. [Appendix H — Sensitive-Category Data Segmentation Plan](#18-appendix-h--sensitive-category-data-segmentation-plan)
19. [Appendix I — Nurse-Triage & Async-Messaging Staffing (Stakeholder Input Required)](#19-appendix-i--nurse-triage--async-messaging-staffing-stakeholder-input-required)

---

## 1. Executive Summary

HealthConnect Portal is a unified patient + provider digital platform that replaces the organization's 2012 legacy portal, addressing low patient adoption (22% registered / 12% MAU), fragmented patient experience across appointments, results, billing, and messaging, and rising provider administrative burden. The program ships in three phases over twelve months from a planned Q3 2026 Phase 1 launch, on a $7M total development + first-year operating budget.

**Phase 1** ships the patient foundation — unified dashboard, self-service scheduling, secure messaging, lab results with plain-language explanation, prescription management, and native iOS + Android mobile apps with web-feature parity — plus the provider workflow primitives needed to support it (inbox triage, AI-drafted replies with mandatory provider sign-off, "patient at a glance" view, Epic Haiku-mediated provider mobile).

**Phase 2** layers in family/proxy account expansion, telehealth video visits, consolidated bill pay, health tracking, medication reminders, opt-in wearable data ingestion with provider review, and the operational scaffolding for asynchronous nurse-triage messaging.

**Phase 3** completes provider tools and care coordination — referral management, shared care plans, population-health surfaces, specialty-configurable workflows, and trainee/teaching access.

Five product principles cut across all phases: **(1)** safety and HIPAA compliance are gates, not goals; **(2)** AI augments providers — it never substitutes clinical judgment; **(3)** equity is a launch requirement, not a future state — the 75+ cohort, accessibility-impaired users, and non-English speakers ship with the product; **(4)** Epic is the system of record, HealthConnect is the experience layer — we don't duplicate EHR functionality; **(5)** the phone channel is preserved as a guardrail against digital exclusion, regardless of call-deflection KPIs.

The proposal targets $8M annual revenue impact and $6.5M annual cost savings, with material patient-satisfaction and provider-burnout improvements as strategic value drivers.

**Have:**
- Brief, vision, problem statement, phased rollout, budget, timeline.
- Discovery-driven 5-persona requirement set with conflict resolutions, gap analysis, market validation, and risk register.

**Need to validate:**
- Whether the executive sponsor agrees with the five product principles (especially #3 equity-as-launch-requirement and #5 phone-channel preservation, which have organizational cost).
- Whether the $7M budget envelope reflects the full scope after gap analysis (see §9 risks).
- Whether Epic MyChart is the underlying build platform vs. custom (Open Question in the brief).

---

## 2. Business Objectives

### 2.1 Primary Objectives

| # | Objective | Rationale | Source |
|---|---|---|---|
| BO-1 | Increase patient portal adoption from 22% registered / 12% MAU to **60% registered / 40% MAU** within 18 months of Phase 1 launch. | Adoption is prerequisite to every downstream benefit. | Brief §"Success Metrics" |
| BO-2 | Lift CAHPS patient-experience score from 62nd to **85th percentile**; achieve **NPS ≥ 50** for the portal experience. | Patient experience is the strategic differentiator. | Brief |
| BO-3 | Shift appointment booking from 55% to **75% self-service** and reduce administrative phone-call volume by **50%** — **scoped explicitly to call types the portal is designed to displace, not phone-channel atrophy overall**. | Operational efficiency without harm to equity-vulnerable cohorts. | Brief + Conflict 6 resolution |
| BO-4 | Reduce provider time spent on inbox + administrative work by **30%**; achieve **90% provider satisfaction** with portal tools. | Provider burnout is both an ethical issue and a retention risk. | Brief |
| BO-5 | Improve **medication adherence by 15%** for chronic conditions and reduce **no-show rate by 10%**. | Adherence and attendance are the clinical-outcome levers the portal can directly influence. | Brief |
| BO-6 | Avoid creating a digital divide. Adoption, satisfaction, and clinical-outcome gains for patients 75+, accessibility-impaired patients, and non-English-speakers must be measurable and **not negative**. | Equity is a precondition to all other metrics. | Conflict 6 + consolidated B-006 |

### 2.2 Financial Targets

- **Revenue:** +$8M annual (improved retention, telehealth revenue, word-of-mouth-driven acquisition).
- **Cost savings:** +$6.5M annual (call-center reduction, no-show reduction, readmission reduction).
- **Total budget:** $7M (development + first-year operating).
- **Strategic value:** foundation for value-based care, provider retention, competitive position.

### 2.3 Strategic Outcomes

- Foundation for value-based care contracts (population-health surfaces in Phase 3).
- Provider satisfaction and retention.
- Patient retention and referral-driven acquisition.
- Demonstrated digital-experience competitive position vs. peer IDNs.

**Have:**
- All quantitative targets from the brief.
- Refined target framing post-Conflict 6 (call-reduction scoped to displaceable call types, not seniors).
- Discovery-derived caveats on revenue / cost assumptions (mature messaging programs *increase* clinical-staff cost — see risk `R-ORG-01`).

**Need to validate:**
- Whether the $8M / $6.5M financial targets reflect updated assumptions post-gap-analysis (nurse-triage staffing, helpdesk staffing, ambient-scribe coordination cost are all upward pressures).
- Whether adoption targets are stratified by cohort (currently single number; equity tracking requires stratification — see `NF-072`).
- Sensitivity analysis on the no-show and adherence targets (these are the most assumption-dependent).

---

## 3. User Personas and Use Cases

### 3.1 Patient Personas

#### Linda R. — Chronic Condition Manager (45–65)
- T2 diabetes + hypertension; on metformin + lisinopril; sees PCP + endocrinology + cardiology.
- **Key needs:** track medications and lab trends, log self-measured BP / glucose, coordinate across specialists, see "what changed" between visits.
- **Top requirements:** F-021 (trend visualization), F-022 (plain-language lab explanations), F-095 (granular sharing), F-123 (self-logged trend with provider visibility), F-143 (medication coordination), F-178 (shared care plan).

#### Marcus T. — Busy Parent (30–45)
- Three kids; FSA-funded household; lives on mobile.
- **Key needs:** family-account management, single bill, family appointment view, mobile-native experience, sick-visit booking.
- **Top requirements:** F-001 (family account), F-002 (proxy lifecycle), F-031 (same-day booking), F-080 (mobile parity), F-101 (photo attachments), F-150 (consolidated billing).

#### Eleanor W. — Tech-Limited Senior (75+)
- Macular degeneration; tablet-only user; has a granddaughter who helps.
- **Key needs:** large text, simple navigation, voice-call appointment reminders, audit-trail visibility for proxy access, anti-scam trust signals.
- **Top requirements:** F-035 (voice reminders), F-090 (dashboard variants without auto-applying), F-191 (trusted clinic branding), NF-010–017 (accessibility), F-002 + F-003 (proxy access + patient-visible audit).

#### Dr. K. Alvarez — Primary Care Physician
- Outpatient PCP, panel ~2,200; pajama-time after kids' bedtime.
- **Key needs:** triaged inbox without admin/billing/scheduling noise, AI message draft with sign-off, "what changed since last visit," coverage handoffs, EHR-grade smart-phrase parity.
- **Top requirements:** F-011 (admin/billing/scheduling routed away), F-013 (triage view), F-014 (AI draft with sign-off), F-050 (patient at a glance), F-103 (coverage), F-172 (smart-phrase parity), NF-020 (chart open < 2s).

#### Dr. R. Okonkwo — Specialist (Interventional Cardiology)
- High-volume referrals; mix of clinic + procedure days; works with PCPs and other specialists.
- **Key needs:** intelligent referral intake, specialty-configurable summary view, consult-back loopback, pre-op patient checklist, shared care plan with PCP, specialty outcomes dashboards.
- **Top requirements:** F-050 (specialty-configurable), F-052–F-055 (referral workflow), F-056 (pre-op), F-057 (procedure-team-nurse routing), F-176 (consult-back), F-178 (shared care plan), F-179 (outcomes dashboard).

### 3.2 Core Use Cases (illustrative, not exhaustive)

| ID | Use Case | Persona(s) | Phase | Linked Reqs |
|---|---|---|---|---|
| UC-01 | Patient registers account with IAL2 identity proofing, MFA, and biometric on registered device. | All patient | 1 | NF-030, NF-030b |
| UC-02 | Patient receives lab result on phone, reads plain-language explanation, messages care team from inline CTA. | Linda, Marcus, Eleanor | 1 | F-020, F-022, F-023, F-024 |
| UC-03 | Parent switches between own account and child's account; books same-day sick visit; messages pediatrician with photo of rash. | Marcus | 1 | F-001, F-031, F-101 |
| UC-04 | PCP opens inbox, sees triaged view with AI-drafted reply for clinical messages; edits + signs; admin and scheduling messages routed away. | Dr. Alvarez | 1 | F-011–F-015 |
| UC-05 | Patient with chronic condition logs BP daily; provider sees trend with provenance attribution at next visit. | Linda | 2 | F-123, F-051, F-200 (Ph 2) |
| UC-06 | Senior patient's granddaughter is granted scoped, time-bound proxy; patient sees audit entry when granddaughter views records. | Eleanor | 1 (proxy MVP) → 2 (scoped expansion) | F-002, F-003, F-111 |
| UC-07 | Specialist receives structured cardiology referral with required ECG / echo / meds; intake validates completeness; consult-back returns to PCP with delivery confirmation. | Dr. Okonkwo, Dr. Alvarez | 3 | F-052, F-053, F-055, F-176 |
| UC-08 | Patient with mental-health diagnosis sets sharing controls so behavioral-health notes are not visible to primary-care team without explicit re-consent. | Linda (hypothetical extension), all patients | 1 | F-095, NF-038 |
| UC-09 | Outage in Epic API: portal shows visible "partial-data" state, audit-logs the gap, does not silently suppress patient access. | All | 1 | F-075, F-076, NF-074 |
| UC-10 | Specialist + PCP co-edit shared care plan; conflicting changes trigger coordination alert (no silent overwrite). | Dr. Alvarez, Dr. Okonkwo | 3 | F-178 |

### 3.3 Out-of-Scope (Phase 1–3)

- Patient-facing autonomous AI symptom triage with disposition (deferred pending clinical + legal sign-off — `A-002`).
- Autonomous AI message reply to patients without provider sign-off (`NF-040` explicitly prohibits).
- Standalone provider-facing native app distinct from Epic Haiku (Conflict 10 resolution).
- Specialty-specific separate apps (Conflict 9 — single configurable platform).
- Cross-system / non-Epic outside-records ingestion beyond TEFCA/Carequality scope determined for Phase 1 (`A-032`).

**Have:**
- Five fully-developed personas with mock interviews and per-persona requirements extracts.
- Defined use cases derived from cross-persona analysis.

**Need to validate:**
- Whether the chosen pseudonymous personas match the org's actual patient mix (esp. demographic / language distribution).
- Whether additional personas are needed: pediatric patient transitioning to adult portal, non-English-speaking caregiver, palliative-care surrogate, behavioral-health-specific patient.
- Whether the five personas adequately represent specialty diversity (only one specialty modeled — Cardiology). Phase 1 launch specialties → see `A-025`.

---

## 4. Functional Requirements

> The complete, ID-stable, traceable list is maintained in [consolidated-requirements.md](consolidated-requirements.md). This section summarizes by capability domain and points to that document for exhaustive detail. **All IDs below match the consolidated document.**

### 4.1 Capability Domains — Must-Have (Phase 1 emphasis)

| Domain | Capability summary | Key IDs |
|---|---|---|
| **Identity & Access** | Single account with linked dependents (`F-001`); proxy lifecycle (`F-002`); patient-visible audit log (`F-003`); IAL2 account recovery (`F-004`); break-glass clinical access (`F-005`); adolescent-privacy state transitions where in-scope (`F-006`). | F-001–F-006 |
| **Messaging & Care-Team Communication** | Secure messaging with delivery / read confirmation (`F-010`); admin/billing/scheduling routed away from physician inbox (`F-011`); tiered response SLAs surfaced in compose UX (`F-012`); inbox triage view (`F-013`); AI-drafted reply with mandatory provider sign-off (`F-014`); summarization + classification (`F-015`); red-flag detection with override (`F-016`); provider-to-provider messaging (`F-017`); off-scope redirect (`F-018`); urgent-message escalation SLA (`F-019`); after-hours messaging warnings (`F-019b`). | F-010–F-019b |
| **Lab Results** | Immediate release with narrow clinically-defined carve-outs (`F-020`); personal target ranges + trends + "what changed" (`F-021`); curated plain-language explanations (`F-022`); result-available notifications per channel preference (`F-023`); inline CTA to message care team (`F-024`). | F-020–F-024 |
| **Appointments** | Self-service booking with real-time availability (`F-030`); same-day / sick visit booking across practice (`F-031`); unified family appointment view (`F-032`); self-service reschedule/cancel (`F-033`); visit-prep info (`F-034`); voice-call reminders (`F-035`). | F-030–F-035 |
| **Medications** | Refill requests with proactive alerts (`F-040`); refill status visibility (`F-041`); MA delegation w/ daily physician sign-off (`F-042`); EPCS (`F-043`); pharmacy fill data with patient disclosure (`F-044`); immunization quick-share (`F-045`). | F-040–F-045 |
| **Provider Workflow & Chart Review** | Role- and specialty-configurable "patient at a glance" (`F-050`); outside-data provenance (`F-051`); referral intake validation (`F-052`); structured specialty-configurable referrals (`F-053`); referral triage queue (`F-054`); consult-note loopback (`F-055`); pre-op patient checklist (`F-056`); procedure-team-nurse routing (`F-057`); EHR documentation-stub creation (`F-058`); panel ownership view (`F-059`). | F-050–F-059 |
| **Telehealth** | One-click join + provider mid-visit text (`F-060`). | F-060 |
| **Notifications, Errors & Channels** | Per-event channel preferences (`F-070`); hard separation of clinical vs. marketing (`F-071`); SMS never includes login links (`F-072`); proactive provider outage alerts (`F-073`); user-friendly error messages with human fallback (`F-074`); dependency-failure degraded modes (`F-075`); info-blocking-compliant degraded mode (`F-076`). | F-070–F-076 |
| **Mobile** | Patient-facing native iOS + Android with web parity (`F-080`); provider mobile via Epic Haiku + thin "patient at a glance" surface (`F-081`). | F-080, F-081 |
| **Dashboard** | Personalized dashboard with selectable variants (`F-090`). | F-090 |
| **Privacy & Consent** | Granular sharing with elevated controls for sensitive categories (`F-095`); patient-facing data-subject-rights workflows (`F-096`); versioned consent records (`F-097`); versioned legal copy with re-acknowledgement (`F-098`). | F-095–F-098 |

### 4.2 Should-Have (Phase 2 emphasis)

Async nurse-triage chat (`F-100`), photo/video attachments (`F-101`), configurable per-practice routing (`F-102`), coverage / handoff (`F-103`), auto-draft telehealth note (`F-104`), adolescent-privacy enhancements (`F-110`), scoped caregiver access (`F-111`), emergency-info shareable card (`F-112`), insurance card image (`F-113`), patient-annotated results (`F-120`), symptom triage (`F-121` — pending clinical sign-off), self-logged trends (`F-123`), batch family scheduling (`F-130`), day-of reminders (`F-131`), telehealth eligibility surfacing (`F-132`), medication reminders (`F-140`), printable med list (`F-141`), simple-UX refills (`F-142`), unified medication coordination (`F-143`), consolidated bill + multi-payment (`F-150`), eligibility/cost estimate (`F-151`), Good Faith Estimates (`F-152`), refund/adjustment visibility (`F-153`), telehealth visits (`F-160`), pop-health dashboard (`F-170`), care-gap review surface (`F-171`), smart-phrase parity (`F-172`), outside-records ingestion (`F-173`), pre-auth status (`F-174`), patient education content lifecycle (`F-175`), structured consult-back (`F-176`), specialty check-in workflows (`F-177`), shared care plan (`F-178`), specialty outcomes dashboards (`F-179`), trainee mode (`F-180` — Phase 3), async-billing workflow (`F-181`), release/change mgmt UX (`F-190`), trusted-clinic branding (`F-191`), onboarding flow (`F-192`), contextual help (`F-193`), adoption-monitoring (`F-194`), multi-language content (`F-195`), DICOM viewer/link-out (`F-196`), event/webhook capability (`F-197`), analytics events (`F-198`), patient transparency (`F-199`).

### 4.3 Nice-to-Have (Phase 2–3, opportunistic)

Wearable ingestion (`F-200` — patient Phase 1, provider Phase 2), correlation insights (`F-201`), "what changed since last time" (`F-202`), HSA tagging (`F-204`), payment plans (`F-205`), parent audit log (`F-206`), TTS readout (`F-207`), pill image (`F-208`), simple-mode toggle (`F-209`), in-clinic onboarding (`F-210`), provider wearable summary (`F-211`), inbox-volume dashboard (`F-212`), patient message templates (`F-213`), templated post-procedure check-ins (`F-214`), cardiac-device integration (`F-215`), care-plan goal tracking (`F-216`), charity-care application (`F-217`).

### 4.4 Functional Requirements Identified by Risk Analysis (Phase 1 if validated)

Per [risk-analysis.md §8](risk-analysis.md#8-risk--requirement-coverage-gaps), the following candidate requirements emerged from risk review and should be folded in pending stakeholder approval:

- Patient disclosure of AI use in clinical communication (CA AB 3030 and similar) — extend `NF-041`.
- Prompt-injection / adversarial-input protection for patient-input AI features — new NF under AI Governance.
- Dev/non-prod environments prohibited from sending PHI to LLM providers — new NF.
- Vendor BAA / sub-processor / license central registry with renewal SLAs — strengthens `NF-097`–`NF-099b`.
- Helpdesk-driven PHI account-recovery hardening — extends `F-004`.

**Have:**
- Complete consolidated functional requirement list (~120 IDs across Must / Should / Nice).
- Conflict resolutions documented with rationale.
- Traceability index mapping every ID back to persona-source or gap-source IDs.
- Cross-persona conflict map with proposed resolutions (17 conflicts).

**Need to validate:**
- All `🆕` gap-sourced requirements have not been confirmed with stakeholders — the gap-analysis caveat applies.
- Phase placement of `F-006` (adolescent privacy) depends on Phase 1 launch states (`A-007`).
- Whether `F-016` red-flag detection and `F-121` symptom triage are in-scope for any phase — requires clinical + legal + AI-governance review.
- Whether F-181 (async-messaging billing workflow) is in scope for Phase 1, 2, or 3 (`D-021`).
- Risk-driven new requirements above need explicit add/defer decision.

---

## 5. Non-Functional Requirements

### 5.1 Accessibility & UX

WCAG 2.1 AA with independent audit + remediation SLAs (`NF-010`); user-configurable text scaling (`NF-011`); high-contrast / no color-alone (`NF-012`); ≥44pt / 48dp touch targets (`NF-013`); UI stability with opt-in preview + advance notice + printed materials for 70+ (`NF-014`); sub-3-tap common tasks (`NF-015`); native-quality mobile (`NF-016`); plain-language reading-level target (`NF-017`).

### 5.2 Performance & Reliability

Provider chart open < 2s, order screen < 1s, message open < 1s @ p95 (`NF-020`); 99.9% uptime / zero unplanned downtime during clinic hours (`NF-021`); shared-workstation fast resume + auto-logout (`NF-022`); secure mobile chart view (`NF-023`); proactive outage notification SLA (`NF-024`); push notification reliability (`NF-025`); cold start ≤ 3s mid-tier + broadband (`NF-026`); web TTI ≤ 3s broadband (`NF-027`); common actions ≤ 1.5s p95 (`NF-028`); concurrent-user sizing for peak (`NF-029`); telehealth video quality SLOs (`NF-029b`); graceful network degradation + offline-critical surfaces (`NF-029c`); per-capability SLOs + status page (`NF-029d`); pre-release load testing (`NF-029e`); CDN strategy (`NF-029f`); feature-flag / kill-switch capability (`NF-029g`); incident-response runbooks + post-incident reviews (`NF-029h`); disaster recovery with tested RTO/RPO (`NF-029i`).

### 5.3 Authentication, Identity & Access

MFA with biometric, risk-based step-up, **no CAPTCHA** in normal patient flows (`NF-030`); IAL2 patient identity proofing (`NF-030b`); RBAC for providers/staff with least privilege (`NF-030c`); workstation vs. personal-device session policy (`NF-030d`); service accounts use rotated credentials / workload identity (`NF-030e`).

### 5.4 Data Security & Privacy

Message delivery + ack guarantees (`NF-031`); comprehensive audit logging w/ ≥6yr retention, immutable, integrity-protected (`NF-032`); hard separation of clinical vs. marketing channels (`NF-033`); anti-phishing affordances (`NF-034`); encryption in transit + at rest (`NF-035`); KMS / HSM-backed key management (`NF-036`); data classification scheme (`NF-037`); elevated controls for sensitive categories (`NF-038`); BAA-covered vendors only (`NF-039`); breach detection / classification / notification per Breach Notification Rule (`NF-039b`); US-region hosting (`NF-039c`); pen test / SAST / DAST / dep scanning in CI/CD (`NF-039d`); centralized secrets mgmt (`NF-039e`).

### 5.5 AI Governance

No AI clinical content to patients without provider sign-off — limited admin auto-responses exempt (`NF-040`); AI-generated artifacts labeled + source-cited (`NF-041`); no in-visit interrupting popups for non-emergency alerts (`NF-042`); bias / disparity testing pre-launch + cadence (`NF-043`); AI model cards / intended use disclosure (`NF-044`); training-data consent (`NF-045`).

### 5.6 Media & Data Handling

Secure media storage w/ encryption + retention + patient deletion right (`NF-050`); patient data export per HIPAA right of access (`NF-051`); records retention + automated disposition (`NF-052`).

### 5.7 Patient Safety

Pre-op checklist alert if not confirmed by procedure −24h (`NF-060`); vulnerable-population / shared-device safeguards (`NF-061`).

### 5.8 Measurement Guardrails

Phone-call-reduction KPI excluded for 70+ cohort with alternative metrics defined (`NF-070`); org-wide call-reduction target scoped to displaceable calls (`NF-071`); demographic-stratified adoption + disparity remediation (`NF-072`); provider performance dashboards with guardrails (ratio metrics, peer ranges, coaching framing) (`NF-073`).

### 5.9 Compliance & Audit

Information-blocking compliance (`NF-074`); 42 CFR Part 2 if SUD in scope (`NF-075`); state-privacy-law matrix (`NF-076`); privileged-user access logging (`NF-077`); annual HIPAA risk assessment (`NF-078`); audit-review workflow w/ anomaly detection (`NF-079`).

### 5.10 Observability

Telemetry baseline w/ PHI minimization (`NF-080a`); OCR-compliant tracking-tech posture (`NF-080b`); ops monitoring tied to error budgets (`NF-080c`); on-call rotation w/ clinical-leader real-time notification (`NF-080d`); A/B testing framework restricted to non-clinical UX (`NF-080e`).

### 5.11 Content Governance

Translation governance — qualified human review for clinical content (`NF-081`); content versioning per patient interaction (`NF-082`); notification template approval workflow (`NF-083`).

### 5.12 Training, Helpdesk, Change Mgmt

Provider training program (`NF-084`); champion / super-user program (`NF-085`); helpdesk model + tiered SLA (`NF-086`); multilingual onboarding (`NF-087`); accessibility-specific onboarding (`NF-088`).

### 5.13 Interoperability

FHIR R4 US Core (`NF-089`); SMART on FHIR / OAuth 2.0 (`NF-089b`); reference terminologies — LOINC/SNOMED CT/RxNorm/CPT/ICD-10 (`NF-089c`); published API rate limits + deprecation policy ≥ 12 months (`NF-089d`).

### 5.14 Billing & PCI

PCI-DSS-compliant processor; no card data in app boundary (`NF-089e`).

### 5.15 Should-Have NFRs

Wearable-data liability scope policy (`NF-090`); session persistence across context switches (`NF-091`); consult-note delivery confirmation (`NF-092`); trainee actions w/ attending sign-off (`NF-093`); OS-integration (Apple Wallet etc.) (`NF-094`); usability testing w/ low-vision + elderly (`NF-095`); TEFCA / QHIN strategy decision recorded (`NF-096`); vendor evaluation framework (`NF-097`); vendor data-portability on termination (`NF-098`); OSS license inventory (`NF-099`); vendor SLA reviews (`NF-099b`).

**Have:**
- Complete NFR set covering accessibility, performance, security, privacy, AI governance, observability, compliance, training, interop, billing, vendor mgmt.
- Each NFR cross-referenced to risk register and gap analysis.

**Need to validate:**
- All gap-sourced NFRs (`🆕`) require stakeholder validation — see [requirements-gap-analysis.md § Summary](requirements-gap-analysis.md#summary--additional-stakeholders-to-interview) for stakeholder list (CISO, Privacy Officer, Legal, SRE, Health Equity, etc.).
- Performance SLO targets need Epic-API latency validation (`A-024`, `D-033`).
- `NF-029i` RTO/RPO targets are TBD per `A-042`.
- `NF-070` / `NF-071` measurement-guardrail acceptance requires Operations leadership commitment (`A-017`).

---

## 6. Technical Architecture

> The brief identifies Epic MyChart as the underlying platform direction and the open question is whether HealthConnect builds on MyChart or builds custom. This section assumes a **"build on Epic MyChart + custom experience layer"** model as the working hypothesis, which best fits the brief's constraints, Phase 1 timing, and budget. Custom-from-scratch is not ruled out but is treated as a significant scope and risk increase requiring explicit stakeholder decision.

### 6.1 Architectural Principles

1. **Epic is the system of record; HealthConnect is the experience layer.** Avoid duplicating EHR state.
2. **Standards over proprietary.** FHIR R4 US Core, SMART on FHIR / OAuth 2.0, LOINC / SNOMED / RxNorm, NCPDP SCRIPT, X12.
3. **Event-driven over polling.** FHIR Subscriptions + internal event bus for notifications, state propagation, and analytics.
4. **Defense in depth on PHI.** Encryption in transit + at rest; classification-aware access control; centralized secrets; audit-by-default.
5. **AI is a feature, not a platform.** RAG-grounded patterns; provider in the loop; source-cited; never autonomous on clinical content.
6. **Designed for degraded modes.** Each external dependency has a defined failure behavior visible to users; info-blocking-compliant partial-data state.
7. **Equity is an architectural concern, not a UX afterthought.** Performance budgets validated on mid-tier devices + LTE; offline-critical surfaces; multilingual content + translation governance.

### 6.2 Logical Architecture (Phase 1 starting point)

```
┌─────────────────────────────────────────────────────────────────────┐
│                          Patient & Provider Surfaces                 │
│  ┌──────────┐  ┌──────────────┐  ┌──────────┐  ┌──────────────────┐│
│  │ iOS App  │  │ Android App  │  │ Web App  │  │ Provider mobile  ││
│  │ (native) │  │ (native)     │  │ (PWA)    │  │ (Epic Haiku +    ││
│  │          │  │              │  │          │  │  thin patient    ││
│  │          │  │              │  │          │  │  at-a-glance)    ││
│  └────┬─────┘  └──────┬───────┘  └────┬─────┘  └────────┬─────────┘│
└───────┼───────────────┼─────────────────┼──────────────────┼──────────┘
        │               │               │                  │
        ▼               ▼               ▼                  ▼
┌─────────────────────────────────────────────────────────────────────┐
│              Experience APIs (BFF, OIDC, rate limit, kill-switch)   │
└─────────────────────────────────────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────────────────────────────────────┐
│  Domain services                                                     │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐  │
│  │Messaging │ │ Appts    │ │ Results  │ │Meds/Rx   │ │ Billing  │  │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘  │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐  │
│  │ Identity │ │ Proxy /  │ │ Consent /│ │Notifs /  │ │ Audit /  │  │
│  │ & Auth   │ │ Family   │ │ Sharing  │ │Channels  │ │ Logging  │  │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘  │
│  ┌────────────────────┐ ┌──────────────────┐ ┌──────────────────┐  │
│  │ Content (curated   │ │ AI orchestration │ │ Analytics /      │  │
│  │ lifecycle, i18n)   │ │ (RAG + LLM +     │ │ telemetry        │  │
│  │                    │ │ source citation) │ │ (OCR-compliant)  │  │
│  └────────────────────┘ └──────────────────┘ └──────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
        │                                          │
        ▼                                          ▼
┌──────────────────────────────────┐  ┌────────────────────────────────┐
│ Integration / event bus          │  │ AI providers (BAA-covered)     │
│ (FHIR Subscriptions, webhooks,   │  │ Azure OpenAI / Anthropic /     │
│ iPaaS — Redox / Health Gorilla)  │  │ similar; vector store          │
└──────────────────────────────────┘  └────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────────────────────────────────────┐
│  External systems (BAA, secured connectivity, defined degraded modes)│
│  Epic EHR / MyChart   Surescripts   Payers   HIE/TEFCA QHIN          │
│  Telehealth vendor    Payment processor   Wearables (HealthKit,      │
│  Health Connect, Dexcom)   ID verification vendor                    │
└─────────────────────────────────────────────────────────────────────┘
```

### 6.3 Key Architectural Choices

| Area | Direction | Rationale | Risk |
|---|---|---|---|
| Build-on-Epic-MyChart vs custom | Build on MyChart as base; HealthConnect = experience + integration + AI layer | Aligns with brief; fastest path to Phase 1; minimizes EHR re-implementation | `R-VEN-01` Epic platform lock-in |
| Cloud | Microsoft Azure (working assumption — Epic + Microsoft partnership) | Native Epic + Azure OpenAI integration patterns; BAA available; widespread healthcare adoption | Revisit if org has different cloud preference |
| LLM | Azure OpenAI (BAA-covered) for Phase 1 features; abstraction layer for portability | Avoids consumer-tier risk; portable design avoids vendor lock-in | `R-VEN-02` model deprecation |
| Mobile | Native iOS + Android with shared experience APIs | Brief explicitly requires native; market validates native preference for engaged users | `R-TECH-04` native dev capacity |
| Provider mobile | Epic Haiku-mediated, supplemented by thin patient-at-a-glance surface | Conflict 10 resolution; reduces scope; uses Epic-supported channel | `R-ORG-04` specialist friction |
| Integration | Mix of direct FHIR + iPaaS for non-Epic vendors | Avoids point-to-point sprawl; FHIR US Core baseline | `R-TECH-06` sprawl |
| Telehealth | Vendor partner (selection TBD per `A-037`) | Build-vs-buy clearly buy at this scope | `R-VEN-04` vendor capability |
| Identity | OIDC + IAL2 proofing via vendor; SMART on FHIR for third-party patient apps | Standards-based; Cures Act compliance | `R-SEC-07` helpdesk recovery |
| AI pattern | RAG (hybrid retrieval) + provider-in-loop; curated content store as source of truth for patient-facing explanations | Market standard; addresses hallucination risk; aligns with content lifecycle | `R-TECH-02` hallucination |
| Audit / observability | Append-only audit store (≥ 6yr retention); separate ops telemetry path with PHI minimization | HIPAA + market trend toward OCR-compliant analytics | `R-REG-01` tracking tech |

### 6.4 Cross-Cutting Concerns

- **Feature flags / kill switches** wrap every major capability (`NF-029g`).
- **Secrets management** via centralized vault; rotation policy.
- **CI/CD security gates** — SAST/DAST/dep scanning/secrets scanning (`NF-039d`).
- **Cost guardrails on LLM** — per-feature token budgets, alerts, throttling at boundary.
- **Caching / CDN** for static assets and non-PHI content.

### 6.5 Reference Standards & Regulations

HIPAA, HITECH, 21st Century Cures Act / information-blocking, ONC HTI-1 + HTI-2, 42 CFR Part 2 (if SUD in scope), NIST 800-63-3 IAL2, WCAG 2.1 AA, OCR online-tracking guidance, state privacy laws (CA, NY, etc.), DEA EPCS, NSA / Good Faith Estimates, PCI-DSS, NIST AI RMF (reference).

**Have:**
- Brief's technical constraints, target stack (Epic EHR), HIPAA + accessibility + uptime requirements, FHIR direction.
- Market analysis informing pattern choice (RAG default, Azure OpenAI maturity, FHIR baseline, TEFCA direction).

**Need to validate:**
- **Critical decision:** build on Epic MyChart vs. custom (Open Question in brief).
- Cloud platform (Azure is working assumption — confirm org cloud strategy + security review status).
- Telehealth vendor strategy (`A-037`).
- TEFCA / QHIN affiliation (`A-038`).
- LLM provider selection (Azure OpenAI assumed for Phase 1).
- Identity-proofing vendor choice (`A-033`).
- Payment processor selection (`D-019`).
- iPaaS strategy (Redox / Health Gorilla / direct).
- DR RTO / RPO targets (`A-042`).

---

## 7. Success Metrics

### 7.1 Tier 1 — Sponsor-level Metrics

| Metric | Baseline | Target | Window | Source |
|---|---|---|---|---|
| Portal registration rate | 22% | 60% | 18 mo post-Ph1 | Brief |
| Monthly active users | 12% | 40% | 18 mo post-Ph1 | Brief |
| Self-scheduled appointments | 55% | 75% | 12 mo post-Ph1 | Brief |
| Phone-call volume (displaceable calls only — `NF-071`) | TBD baseline | −50% | 18 mo post-Ph1 | Brief + Conflict 6 |
| CAHPS percentile | 62nd | 85th | 24 mo | Brief |
| NPS | TBD | ≥ 50 | 12 mo post-Ph1 | Brief |
| Provider time on inbox + admin | TBD baseline | −30% | 12 mo post-Ph3 | Brief |
| Provider satisfaction with portal tools | TBD | ≥ 90% | 12 mo post-Ph3 | Brief |
| Medication adherence (chronic conditions) | TBD | +15% | 24 mo | Brief |
| No-show rate | TBD | −10% | 12 mo post-Ph1 | Brief |

### 7.2 Tier 2 — Equity & Guardrail Metrics

| Metric | Target | Source |
|---|---|---|
| Adoption stratified by age cohort (under 35 / 35–54 / 55–64 / 65–74 / 75+) | All cohorts trend positive; no cohort declines | `NF-072` |
| Adoption stratified by primary language, SVI quintile, accessibility designation | Comparable trends; disparity triggers remediation | `NF-072`, `B-006` |
| Phone-call wait time / abandonment (preserved channel) | No degradation post-launch | `NF-070`, `B-008` |
| Patient-experience scores for 70+ cohort | Net positive change | `NF-070`, `B-007` |
| Helpdesk call volume vs. capacity | Within SLA tier | `NF-086` |

### 7.3 Tier 3 — Operational / Product Metrics

| Metric | Target |
|---|---|
| Task completion rate (refill, reschedule, view immunizations, pay bill) | ≥ 90% |
| Self-service rate per task category | Trend up |
| Time-to-result-acknowledgement | Decrease quarter over quarter |
| Message-acknowledgement SLA hit rate | ≥ 95% (per `F-019`) |
| AI-draft acceptance rate (sent vs. discarded) | Tracked; no target year 1 |
| AI-draft edit distance | Tracked |
| Inbox time per provider (with AI vs. without) | Decrease |
| Telehealth video session quality SLO hit rate | Per `NF-029b` |
| Per-capability SLO error-budget consumption | Within budget |

### 7.4 Tier 4 — Safety & Compliance Metrics

| Metric | Target |
|---|---|
| HIPAA / OCR complaints attributed to portal | 0 |
| Information-blocking complaints | 0 |
| AI clinical-safety incidents (red-flag false negatives, harmful drafts sent) | 0 / tracked + reviewed |
| Audit-review anomalies investigated within SLA | 100% |
| Sensitive-data sharing violations | 0 |
| Breach notifications meeting required timeline | 100% |

**Have:**
- Sponsor-level metrics from the brief.
- Guardrail metric framework from conflict resolutions (esp. Conflict 6).
- Discovery- and gap-driven operational and safety metrics.

**Need to validate:**
- Baselines for any "TBD baseline" metrics — analytics team engagement required.
- Stratification scheme for equity metrics (`A-040`).
- Org commitment to publishing phone-channel guardrail metrics (`A-017`).
- Sensitivity analysis on no-show, adherence, and call-reduction targets (`R-BUD-01` exposure).
- Whether AI-specific metrics need formal targets or only tracking in year 1.

---

## 8. Risks and Mitigation

> Full risk register in [risk-analysis.md](risk-analysis.md). This section summarizes the **top 10** with mitigation framing.

| # | Risk | L / I | Mitigation | Owner | Detective control |
|---|---|---|---|---|---|
| 1 | `R-ORG-01` Nurse-triage + async-messaging staffing not funded before launch → load lands on physicians or response degrades | H / H | Staffing model + budget approval as launch gate for `F-019`, `F-100`, `F-019b`. Tied to async-billing model (`B-010`). | Clinical operations leadership | Message-ack SLA dashboard + provider burnout survey |
| 2 | `R-REG-01` HIPAA tracking-tech / third-party SDK exposure on PHI pages | H / H | OCR-compliant telemetry baseline (`NF-080b`) defined before any analytics ships; periodic third-party-asset scan; Privacy Officer sign-off gate. | Privacy Officer + Engineering | Automated third-party request inventory in CI/CD |
| 3 | `R-TECH-01` Epic API latency / availability constrains performance SLOs | H / H | Performance-budget validation in Phase 0 against Epic sandbox; caching + denormalized read models where allowed by Epic license; escalation path with Epic vendor mgmt. | Integration + SRE | Per-capability latency dashboards tied to error budgets (`NF-029d`) |
| 4 | `R-ORG-02` Provider in-basket time *increases* despite AI features | M / H | Time-motion studies pre-launch + 30 / 90 / 180 day post. AI-draft edit-distance + acceptance tracked. Provider advisory council (`B-012`) governance over AI tuning. | Clinical informatics | Inbox-time dashboards per provider w/ guardrail framing (`NF-073`) |
| 5 | `R-SEC-01` Sensitive-category data leakage via family / proxy access | M / H | Proxy lifecycle (`F-002`) with explicit revoke + time-bound expiration; sensitive-category access requires re-consent (`F-095`, `NF-038`); pre-launch threat-modeling on proxy flows. | Privacy + Product | Audit-review anomaly detection (`NF-079`); patient-visible audit log (`F-003`) |
| 6 | `R-REG-02` Information-blocking exposure from over-conservative result holds | M / H | Carve-out list owned by clinical leadership, reviewed quarterly. Hold-rule review process tied to information-blocking exceptions (per risk §8 candidate requirement). | Compliance + Clinical | Hold-duration metrics + complaint log |
| 7 | `R-ORG-03` Digital divide — 75+ and accessibility-impaired cohorts abandoned | M / H | Equity-stratified metrics (`NF-072`) tracked from launch; in-person onboarding (`F-210`) funded (`D-022`); phone-channel preservation (`NF-070`, `NF-071`); accessibility audit (`NF-010`); usability testing w/ low-vision + elderly (`NF-095`). | Health equity + Product | Stratified adoption dashboards; phone wait-time monitoring |
| 8 | `R-TECH-02` Patient-facing AI hallucination causing clinical harm | M / H | RAG-grounded curated content (`F-022`); strict "no answer without source" guardrail; pre-launch clinical validation; ongoing sampling + adverse-event review. | Clinical informatics + AI gov | AI clinical-safety incident log; sample audits |
| 9 | `R-VEN-01` Epic platform changes / pricing disrupt roadmap | M / H | Abstraction layer over Epic where feasible; quarterly vendor-roadmap review; multi-year contract negotiation; budget contingency. | Vendor mgmt | Epic release-note review cadence |
| 10 | `R-BUD-01` Scope creep across 5 personas + ~90 gap requirements blows Phase 1 | H / M | Phase 1 scope locked by steering committee; gap-sourced requirements explicitly deferred unless promoted with budget; change-control board. | Product + PMO | Phase 1 burndown + scope-change log |

**Executive escalations** (steering / sponsor decisions required before PRD sign-off):

1. Nurse-triage staffing commitment (R-ORG-01).
2. Phone-channel preservation policy with measurable guardrails (R-ORG-03 / R-ORG-05).
3. Tracking-tech / analytics posture decision (R-REG-01).
4. Epic vs. custom + ambient-scribe coordination governance (R-VEN-01 / R-VEN-06).
5. Phase 1 scope lock and deferred-list approval (R-BUD-01).
6. TEFCA / QHIN affiliation strategy (R-REG-13).
7. AI-governance committee charter (R-ORG-11).

**Have:**
- Full risk register with ~80 risks across 6 categories.
- Top 10 critical risks with proposed owners.
- Risk-driven requirement gaps identified.

**Need to validate:**
- Risk owners — currently candidates, not assigned.
- Whether the executive escalations have been raised with the sponsor.
- Probability/impact ratings on the largest risks — calibration with org-internal experience.

---

## 9. Timeline and Milestones

> The brief mandates a **12-month** development cycle with Q3 2026 Phase 1 launch and a $7M budget. The gap analysis and risk review surface meaningful schedule and budget exposure that should be discussed with the sponsor.

### 9.1 Proposed Phasing (aligned to brief; reflects PRD scope)

#### Phase 0 — Foundation (Months 0–3, pre-Phase-1)

- Vendor decisions: Epic vs. custom; cloud; LLM provider; ID proofing vendor; telehealth vendor; payment processor; iPaaS.
- AI-governance committee charter; clinical-content informatics ownership; provider advisory council seated.
- Helpdesk + nurse-triage staffing model approved and funded.
- Performance budgets validated against Epic sandbox.
- Compliance review gates established (Privacy, Security, Legal, Health Equity).
- DR RTO/RPO targets set.
- Phase 1 scope locked.

#### Phase 1 — Patient Foundation (Months 1–4, build) → Q3 2026 launch

- Unified dashboard, scheduling, secure messaging (with AI-draft + provider sign-off), lab results (immediate release + carve-outs), prescription mgmt, native mobile w/ feature parity.
- Identity & access (MFA + IAL2 + biometric + RBAC), audit log, granular sharing controls.
- Family-account MVP (single account + linked dependents + proxy lifecycle).
- Provider workflow primitives: triaged inbox, "patient at a glance" (PCP default config), Epic Haiku integration.
- Notifications per channel preference, info-blocking-compliant degraded modes.
- WCAG 2.1 AA conformance + independent audit.
- OCR-compliant telemetry + DR plan + incident runbooks.
- Multi-language launch (English + top 2 by population per `F-195` / `A-036`).

#### Phase 2 — Enhanced Patient Experience (Months 5–8)

- Health record full access, consolidated bill pay + payment plans, family-account scoped caregiver access expansion, telehealth video, health tracking (patient-side; wearable patient-only), medication reminders.
- Async nurse-triage chat (gated on staffing).
- Async-messaging billing workflow (gated on `F-181` / `B-010` decision).
- Adolescent-privacy expansion (`F-110`) if multi-state scope.
- Specialty-configurable summary view (cardiology Phase-2 MVP).

#### Phase 3 — Provider Tools & Care Coordination (Months 9–12)

- Referral mgmt + intelligent intake + consult-back loopback.
- Shared care plan (PCP + specialist + patient).
- Population-health surfaces + care-gap review.
- Patient education with content lifecycle.
- Wearable provider-side review (opt-in, per `F-200` Phase 2 in roadmap nomenclature).
- Trainee / supervised access mode (Conflict 15 resolution).
- Specialty outcomes dashboards.

### 9.2 Milestones

| Milestone | Target | Gate |
|---|---|---|
| Phase 0 complete: vendor decisions + AI-gov + staffing | M3 | Steering go/no-go |
| Phase 1 design freeze | M4 | Stakeholder sign-off |
| Phase 1 alpha (internal) | M8 | Compliance + Security |
| Phase 1 pilot (limited clinic) | M10 | Clinical leadership |
| Phase 1 GA — Q3 2026 launch | M12 | Sponsor |
| Phase 2 launch | M16 | Phase 1 metrics review |
| Phase 3 launch | M20 | Phase 2 metrics review |
| 18-mo program review (against BO targets) | M30 | Sponsor |

### 9.3 Schedule / Scope / Budget Exposure

The PRD as scoped is **at risk** against the 12-month / $7M envelope for the following reasons surfaced by gap and risk analysis:

- Gap analysis added ~90 candidate requirements; only those explicitly promoted to Must in Phase 1 are sized into the schedule above. **The gap-sourced Must-Have items are not free** — IAL2 proofing, break-glass workflow, comprehensive audit log, DR plan, OCR-compliant telemetry, vendor BAA framework, FHIR US Core conformance, content lifecycle, training program, helpdesk model are all material scope.
- Nurse-triage staffing (`D-020`), helpdesk staffing (`D-026`), provider training (`D-028`), ambient-scribe coordination, and accessibility audit (`NF-010`) are **OPEX** items that should be reflected in the first-year operating budget, not just CAPEX.
- Independent security review + remediation typically adds 2–6 weeks late in the cycle (`R-BUD-05`).
- Phase 2 pull-forward pressure on family-account expansion (`R-BUD-08`) is likely.

**Recommendation:** explicit steering-committee decision on scope vs. schedule vs. budget trade-off **before** Phase 1 design freeze.

**Have:**
- Brief-defined 12-month / 3-phase rollout with month-by-month breakdown.
- $7M total budget envelope.
- Q3 2026 target launch.

**Need to validate:**
- Whether the Phase 0 / pre-Phase-1 foundation work is funded and staffed.
- Whether the gap-sourced Phase 1 Must-Have scope has been costed against the $7M envelope.
- OPEX vs. CAPEX framing of staffing dependencies (`D-020`, `D-026`, `D-028`).
- Steering posture on Phase 2 pull-forward requests.
- Vendor lead times (accessibility audit, ID-proofing vendor, telehealth vendor) against milestone dates.

---

## 10. Open Questions & Decisions Needed

> Full open-questions catalogue (43 items) is in [consolidated-requirements.md § Ambiguities & Open Questions](consolidated-requirements.md#ambiguities--open-questions). The list below is the **subset that blocks PRD finalization** and should be resolved with stakeholders during the PRD review cycle.

### Sponsor / Steering decisions

1. **Build on Epic MyChart vs. custom** (brief open question).
2. **Funded operational staffing model** for nurse-triage, helpdesk, training (`D-020`, `D-026`, `D-028`).
3. **Phone-channel preservation policy** with measurable guardrails (`A-017`, `NF-070`).
4. **Phase 1 scope lock + deferred-list approval** (`R-BUD-01`, `R-BUD-08`).
5. **AI-governance committee charter** (`D-050`).
6. **Ambient-scribe initiative coordination** (`B-011`).

### Regulatory / Compliance decisions

7. **42 CFR Part 2 applicability** (`A-035`).
8. **State-privacy-law matrix and Phase 1 launch states** (`A-007`, `NF-076`).
9. **TEFCA / QHIN affiliation strategy** (`A-038`).
10. **AI patient-disclosure policy** (CA AB 3030 et al., risk §8).
11. **Information-blocking exception review process** (risk §8).

### Product / Design decisions

12. **Lab carve-out list for provider-review window** (`A-001`).
13. **Symptom triage (`F-121`) and red-flag detection (`F-016`) phase placement** (`A-002`, `A-019`).
14. **Languages supported at launch** (`A-036`).
15. **Granular sharing UX complexity vs. usability** (`A-003`).
16. **Co-equal parent / split-custody policy** (`A-006`).
17. **Adolescent-privacy default access model and emergency override** (`A-007`, `A-011`).
18. **Provider visibility into patient-logged data — opt-in by whom?** (`A-004`).

### Technical decisions

19. **Cloud platform** (Azure working assumption).
20. **LLM provider** (Azure OpenAI working assumption).
21. **Identity-proofing vendor** (`A-033`).
22. **Telehealth vendor strategy** (`A-037`).
23. **Payment processor** (`D-019`).
24. **DR RTO/RPO targets** (`A-042`).
25. **Performance budget enforcement model** (`A-024`).

### Operational decisions

26. **Coverage / handoff scope per `F-103`** (`A-023`).
27. **Phase-1 specialties for configurable summary view** (`A-025`).
28. **Outage-alert pre-notice window** (`A-022`).
29. **Helpdesk operating model and PHI-aware account-recovery process** (`A-034`).
30. **Trainee access model phasing and supervision rules** (`A-028`).

---

## Appendix Alert Convention

Several appendices below contain content that requires org-specific stakeholder input that cannot be drafted responsibly from the discovery and gap-analysis material alone. Those sections use the following alert convention:

> ### 🟥 STAKEHOLDER INPUT REQUIRED
> **Why this section is incomplete:** [reason]
> **Who needs to provide the input:** [role(s)]
> **What is needed:** [specific decisions, data, or artifacts]
> **Blocking for:** [downstream PRD sections, milestones, or decisions]

Where this block appears, the surrounding content is a **framework / template only** — the actual organization-specific content is a precondition for PRD finalization, not a Phase 1 deliverable.

---

## 11. Appendix A — Legacy Portal Migration & Cutover Plan

### 11.1 Scope of Migration

The 2012 legacy portal is in scope to be sunset. Migration covers:

1. **Patient accounts** — credentials, identity attributes, MFA enrollment, communication preferences, accessibility preferences.
2. **Proxy / family relationships** — existing parent/guardian/caregiver grants that must be re-validated under the new proxy lifecycle (`F-002`).
3. **Patient-initiated content** — saved messages, attachments, uploaded documents (insurance cards, IDs, photos), patient-entered self-tracking data.
4. **Patient-state data** — bill balances, payment history references, scheduled appointments, open refill requests, in-flight messages.
5. **Audit log** — legacy access log (treated as historical, append-only, retained per `NF-032` and `NF-052`).
6. **URL / SEO surface** — patient-facing inbound links, deep-link redirects, email-link redirects.

Out of scope (remain in source systems): EHR clinical data (Epic remains system of record); claims and billing source data (revenue-cycle systems remain authoritative); analytics history from the legacy portal beyond what is needed for stratified-cohort baseline metrics.

### 11.2 Migration Strategy

**Approach:** parallel-operation with phased patient cutover, **not** big-bang.

| Stage | What happens | Patient experience |
|---|---|---|
| Pre-launch (M-3 to M-1) | Identity-graph reconciliation; proxy-relationship discovery; data-quality audit on legacy; design of patient communications; legal review of consent re-acknowledgement strategy. | No change. |
| Soft launch (M0–M1) | New portal opens for net-new registrations and opt-in migration of existing accounts. Legacy portal continues to function. | Existing users see invitation, can opt-in. New users go directly to HealthConnect. |
| Cohort migration (M1–M5) | Existing patients migrated in cohorts (clinic-by-clinic, aligned with pilot rollout per §16). Each cohort gets a 30-day overlap window with both portals available. | Email/SMS/voice invitation per channel pref; in-clinic enrollment support; printed quick-start for 70+. |
| Sunset (M5–M6) | Legacy portal placed in read-only mode for 30 days; then redirected to HealthConnect with a static account-recovery surface. | Users hitting legacy URLs are redirected with a banner explaining the change. |
| Post-sunset (M6+) | Legacy data retained per retention schedule; legacy URLs maintain HTTP 301 → HealthConnect equivalent for ≥ 12 months. | Inbound links continue to resolve. |

### 11.3 Data Migration Specifics

- **Credentials:** passwords are **not** migrated. Existing users must complete first-time login flow that re-verifies identity at IAL2 (`NF-030b`); legacy password hashes are securely destroyed post-cutover. This is the secure default and aligns with `F-004` / `NF-030b`.
- **MFA enrollment:** users re-enroll MFA factors at first login — drives improvement in MFA coverage; aligns with `NF-030`.
- **Proxy relationships:** legacy proxy grants are **not auto-trusted**. Each existing relationship is re-validated through the new proxy-lifecycle workflow (`F-002`), with both parties notified. This is necessary because legacy proxy permissions are not at parity with the new model's granularity (`F-095` / `NF-038`).
- **Communication preferences:** migrated by channel and event-type per `F-070`; defaults applied where legacy data is incomplete; banner on first login asks the user to confirm.
- **Consent re-acknowledgement:** privacy notice, terms, and any net-new consents (data sharing, AI-assistance disclosure per California AB 3030 / state-law equivalents) re-acknowledged on first login per `F-098`.
- **In-flight content:** open messages, unfilled refill requests, and scheduled appointments are migrated as live state. Provider-side counterparts in Epic remain authoritative; HealthConnect references via the existing EHR linkage.
- **Attachments / uploaded documents:** copied to the new media boundary (`NF-050`), validated for integrity, and re-linked. Legacy storage retained per `NF-052` retention schedule until disposition.
- **Audit log:** legacy log is preserved as an append-only historical archive; HealthConnect audit log (`NF-032`) begins at user's cutover moment. Both are retained ≥ 6 years.

### 11.4 Patient Communications

- 30 / 14 / 7 / 1 day pre-cutover notices via each patient's preferred channel.
- In-clinic posters and ambassador support (`F-210`).
- Printed quick-start guides for 70+ cohort (`NF-014`).
- Multilingual notice in supported launch languages (`F-195`).
- Dedicated cutover helpdesk surge plan (see §19 staffing alert).
- Trusted-clinic branding on all comms (`F-191`) — anti-phishing concern.

### 11.5 Rollback Strategy

- During parallel-operation, **per-cohort rollback** is supported by re-enabling legacy access (since legacy is live during overlap).
- Post-sunset, full rollback is impractical; instead, **per-feature kill switches** (`NF-029g`) and **degraded-mode operation** (`F-075`, `F-076`) provide bounded recovery options.
- Any "halt cutover" decision is owned by the steering committee; criteria documented in the pilot exit criteria (§16).

### 11.6 Migration-Specific Risks (additions to risk register)

| ID | Risk | L / I | Mitigation |
|---|---|---|---|
| R-MIG-01 | Patients abandon during forced IAL2 re-proofing → adoption regression vs. legacy baseline | M / H | Multiple proofing paths (in-clinic, KBA, remote vendor); helpdesk surge; phased per-cohort observation |
| R-MIG-02 | Legacy proxy relationships not re-validated → loss of caregiver access at cutover | H / M | Proactive outreach; extended re-validation grace period; helpdesk-assisted re-establishment |
| R-MIG-03 | Inbound links / emails from third parties break post-sunset | M / M | 301 redirect map maintained ≥ 12 months; comms to known third parties |
| R-MIG-04 | Data-quality issues in legacy export surface late | M / M | Data-quality audit in pre-launch stage; reconciliation reports per cohort |
| R-MIG-05 | Helpdesk swamped during cutover windows | H / H | Surge staffing planned per cohort; see §19 |

> ### 🟥 STAKEHOLDER INPUT REQUIRED — Sub-items in §11
> - **Legacy proxy-relationship volume and distribution** (how many active grants, by type) — needed to size re-validation workload.
> - **Legacy data-quality assessment** — needed before final cutover stages are scheduled.
> - **State-by-state legal-notice requirements** for portal-change communications.
> - **Decision: opt-in migration or auto-migrate-with-opt-out for existing accounts** — legal + UX trade-off.

### 11.7 Migration Acceptance Criteria

- 100% of cohort 1 patients receive at least one cutover notice via preferred channel ≥ 14 days before their migration date.
- ≤ 5% drop in active-user rate per cohort 30 days post-cutover relative to pre-cutover legacy baseline (rollback trigger if exceeded).
- Zero data-loss incidents for in-flight messages, refill requests, or scheduled appointments.
- 100% of proxy grants either re-validated or explicitly revoked within the grace period.
- Legacy URLs return successful 301 redirect to a valid HealthConnect resource for ≥ 95% of recorded legacy inbound paths.

---

## 12. Appendix B — Cost Breakdown (Stakeholder Input Required)

> ### 🟥 STAKEHOLDER INPUT REQUIRED — Cost decomposition
> **Why this section is incomplete:** The $7M envelope in the brief is asserted as a single number with no decomposition. A defensible cost model requires real vendor quotes, internal labor rate cards, cloud committed-spend posture, LLM consumption projections, and a clear CAPEX vs. OPEX framing per the org's accounting policy. None of that is available in the discovery artifacts.
>
> **Who needs to provide the input:** Finance partner; Procurement; IT Engineering leadership (for internal labor rates and squad sizing); Cloud / FinOps; Vendor mgmt; HR (for new operating roles); Clinical Operations leadership (for nurse-triage and helpdesk staffing — see §19).
>
> **What is needed:**
> - Internal labor rates by role (engineer, designer, PM, clinical informatics, SRE).
> - Squad-sizing plan tied to scope in §9.
> - Vendor pricing for: Epic platform deltas, telehealth vendor, ID-proofing vendor, payment processor, accessibility-audit vendor, iPaaS (if selected), ambient-scribe coordination.
> - Cloud commitment / reservation posture (Azure EA vs. PAYG).
> - LLM consumption projection at projected message volume, with per-token pricing assumption documented.
> - Year-2 / year-3 run-rate model (the brief covers year 1 only).
> - Org capitalization policy for platform investment vs. OPEX.
>
> **Blocking for:** §1 / §9.3 budget-envelope confirmation; sponsor go/no-go on Phase 1 scope; vendor RFP cycles.

### 12.1 Framework / Template

The following template is provided to structure the cost discussion once stakeholder inputs are available. It is **illustrative**, not committed. Categories are derived from the PRD scope and risk register.

**One-time / Phase 0–1 build (CAPEX or expensed per policy)**

| Category | Drivers | Status |
|---|---|---|
| Internal engineering labor | Squad count × duration × loaded rate | TBD |
| Internal product / design / UX | Roles × duration | TBD |
| Clinical informatics | Content lifecycle build, AI safety validation | TBD |
| Cloud build-out + non-prod | Environment count × footprint | TBD |
| Vendor implementation fees | Telehealth, ID proofing, payment processor, iPaaS | TBD |
| Epic integration deltas | Per Epic statement of work | TBD |
| Independent accessibility audit | Pre-launch + remediation | TBD |
| Penetration testing | Pre-launch + remediation | TBD |
| Translation / multi-language launch | Per language scope (`F-195` / `A-036`) | TBD |
| Migration tooling + comms | Per §11 | TBD |
| Training program development | Per `NF-084`, `NF-088` | TBD |
| Contingency reserve | Recommended ≥ 15% given gap-analysis exposure | TBD |

**Year-1 OPEX**

| Category | Drivers | Status |
|---|---|---|
| Nurse-triage staffing | See §19 alert | TBD |
| Helpdesk staffing | Per `NF-086` + cutover surge | TBD |
| Cloud run | Steady-state footprint | TBD |
| LLM consumption | Tokens × per-token cost × utilization | TBD |
| Telehealth vendor | Per session or per provider seat | TBD |
| Audit log storage (6-year retention) | Volume growth × hot/cold tiering | TBD |
| Vendor SaaS subscriptions | iPaaS, ID proofing, payment processor, etc. | TBD |
| Ongoing accessibility audit cadence | Per `NF-010` | TBD |
| Ongoing pen test / SAST/DAST | Per `NF-039d` | TBD |
| Patient-education content lifecycle | Per `F-175`, `NF-082` | TBD |
| Translation maintenance | Per `NF-081` | TBD |

**Year-2+ run-rate items**

- Cloud growth (audit log + media compound).
- LLM consumption growth with adoption.
- License renewals.
- DR exercise cadence (`NF-029i`).
- Annual HIPAA risk assessment (`NF-078`).
- Provider training refreshers (`NF-084`).
- Vendor SLA reviews (`NF-099b`).

### 12.2 Sensitivity Analysis (placeholder)

Once a base cost model exists, sensitivity analysis is recommended against:

- ±25% on LLM consumption (token-cost is the most volatile and most uncertain line item).
- ±25% on audit-log retention storage cost.
- ±50% on nurse-triage staffing (see §19).
- ±20% on helpdesk staffing during cutover months.
- ±3 months on Phase 1 schedule.

---

## 13. Appendix C — Acceptance Criteria for Phase 1 Must-Have Requirements

> Acceptance criteria expressed in Given / When / Then form for testability. IDs match [consolidated-requirements.md](consolidated-requirements.md). Where a requirement has multiple criteria, each is listed separately. This appendix is intentionally focused on Must-Have IDs for Phase 1; Should-Have / Nice-to-Have acceptance criteria are deferred to v0.2.

### 13.1 Identity & Access

**F-001 — Single account with linked dependents**
- Given a patient with at least one verified linked dependent, when they log in, then a UI affordance shows all accounts they can act on and switching is one tap/click.
- Given a logged-in user acting on behalf of a dependent, when they perform any action that writes to the record, then the audit log records both the actor identity and the patient identity.

**F-002 — Proxy / delegated access with full lifecycle**
- Given a patient (delegator), when they grant proxy access, then the system requires evidence of relationship/guardianship per the configured policy and both parties receive notification within 5 minutes.
- Given an active proxy grant, when the delegator (or, in defined scenarios, the delegate) revokes it, then access is removed within 60 seconds and both parties are notified.
- Given a proxy grant with a time-bound expiration, when the expiration time is reached, then access is automatically removed and the audit log records the expiration event.
- Every grant, modification, revocation, and expiration event is queryable by the patient via `F-003` within 5 minutes.

**F-003 — Patient-visible audit log**
- Given a patient, when they open the audit log, then they see entries for every PHI-record access including proxy, privileged-user, and break-glass entries, with actor identity (or role), timestamp, action, and record category.
- Privileged-user entries are distinctly flagged.
- Log entries are read-only from the patient surface.

**F-004 — IAL2 account recovery**
- Given an account-recovery request, when the requester cannot complete IAL2-equivalent verification, then the helpdesk has no override that grants PHI-bearing access.
- Every account-recovery action is logged with method used, evidence captured, and operator identity.

**F-005 — Break-glass / emergency clinical access**
- Given a provider invoking break-glass, when the workflow is initiated, then a justification is required (free-text + reason code), the action proceeds, and notification is sent to Compliance and to the patient within 1 hour (or per defined SLA).
- Every break-glass event appears in the audit log with full justification text.

**F-006 — Adolescent-privacy state transitions**
- Given a patient reaching a protected-age threshold in a state where the policy applies, when the transition date is reached, then the access model defined for that state is enforced from that moment, parent and teen are notified per the policy, and the new graded-access map is applied.
- See §17 for the state-by-state policy matrix that drives this requirement.

### 13.2 Messaging

**F-010 — Secure messaging with delivery + read confirmation**
- Given a patient sends a message, when delivery to the recipient inbox succeeds, then a "delivered" indicator appears within 30 seconds.
- When the recipient opens the message, then a "viewed at [time]" indicator appears for the patient within 5 minutes.
- Given a transient network failure on send, when retry is performed, then idempotency key prevents duplicate message creation; user sees either success or an actionable error (per `F-074`), never silent failure.

**F-011 — Message routing (admin/billing/scheduling away from physician)**
- Given a patient-composed message classified as administrative, billing, scheduling, or form-request, when routing executes, then the message is delivered to the configured non-physician queue and does **not** appear in the physician inbox.
- Per-practice routing rules are configurable by an authorized administrator without engineering deployment.
- Mis-classified messages can be re-routed by any inbox holder with a single action; the system learns from re-classifications (tracked for tuning, not auto-applied).

**F-012 — Tiered response SLAs in compose UX**
- Given a patient composing a message, when they select a message type, then the compose UI displays the expected response window for that message type.
- Displayed SLAs are configurable per practice and per message type without engineering deployment.

**F-013 — Physician inbox triage view**
- Given a physician opens the inbox, when they apply filters by urgency, type, or patient, then the view updates in < 1 second (per `NF-020`).
- Default sort order is configurable per provider.

**F-014 — AI-assisted message drafting**
- Given an inbound patient clinical message, when the AI-draft feature is enabled, then a draft reply is generated with the source patient message clearly visible and the AI label per `NF-041`.
- The draft cannot be sent without an explicit provider edit-confirm-sign action.
- The system records the original draft, all edits, and the final sent text in the audit log for medical-legal reconstruction.

**F-015 — AI summarization + classification**
- Given a long patient message, when summarization is requested, then a summary is generated with the source message available in one click.
- Classification confidence is exposed where below a threshold; below-threshold messages are not auto-routed.

**F-016 — Red-flag detection (gated by clinical safety sign-off)**
- Given a patient message containing one or more configured red-flag signals, when classification runs, then the message is flagged in the provider view with the matched signal(s) shown.
- Provider override is one click; override reason is captured.
- False-negative review process runs at defined cadence (operational SLA).

**F-017 — Provider-to-provider messaging**
- Provider-to-provider messages appear in a queue distinct from the patient inbox with its own SLA display and read receipts.
- Routing into the patient inbox from provider-to-provider is not possible by default.

**F-018 — Off-scope redirect**
- Given a provider receives a message outside their scope, when they invoke off-scope redirect, then they select target provider/team from a directory, the message is re-routed, both parties are notified, and audit trail captures both endpoints.

**F-019 — Urgent-message escalation SLA**
- Given an inbound message tagged urgent, when the configured ack window elapses without acknowledgement, then escalation fires to the configured backup/on-call.
- Escalation event is logged.

**F-019b — After-hours warning**
- Given a patient initiates a message outside configured business hours, when the compose UI loads, then a clear warning appears with alternate paths (urgent care, nurse triage line, 911) before submit is enabled.

### 13.3 Lab Results

**F-020 — Immediate release with carve-outs**
- Given a lab result not in a carve-out category, when the result is finalized in the EHR, then it is patient-visible within the platform-defined SLO (target ≤ 5 minutes).
- Given a result in a carve-out category, when finalized, then it is held for the configured provider-review window with a documented exception code per information-blocking rules.
- Carve-out categories are maintained as configuration, not code.

**F-021 — Lab result trends + "what changed"**
- Given a result with a comparable prior value, when displayed, then the prior value, delta, and trend over the last 12 months are shown.
- Personal target ranges, where defined for the patient, override population ranges.

**F-022 — Plain-language explanation**
- Given a result with a curated explanation in the content store, when displayed, then the explanation is shown with version identifier captured to the audit log (per `NF-082`).
- Given no curated explanation exists, when displayed, then the result is shown without explanation rather than with AI-generated free-form content.

**F-023 — Result-available notification**
- Given a patient with channel preferences set, when a result becomes patient-visible, then a notification fires per their per-event channel preference (`F-070`).

**F-024 — Inline message-care-team CTA on results**
- Given a patient viewing a result, when they tap/click the message CTA, then the compose surface opens with the result reference pre-populated.

### 13.4 Appointments

**F-030 — Self-service booking**
- Given a patient and a provider with bookable availability, when the patient searches, then real-time availability is returned within 2 seconds.
- Booking confirmation is delivered per `F-070` preferences.

**F-031 — Same-day / sick-visit booking**
- Given a patient searching for same-day availability, when the search runs, then results include any same-day slots across providers in the practice, not only the patient's primary.

**F-032 — Unified family appointment view**
- Given a logged-in user with linked dependents, when they open the appointments view, then upcoming appointments for all linked accounts are visible in a single chronological view with clear actor attribution.

**F-033 — Self-service reschedule/cancel**
- Given an existing appointment within reschedule policy, when the patient initiates reschedule, then the system displays available alternative slots and confirms the change without phone-call required.

**F-034 — Visit-prep info**
- Given an upcoming appointment with prep instructions, when the patient views it, then directions, parking, what-to-bring, fasting requirements (where applicable) are visible.

**F-035 — Voice-call appointment reminders**
- Given a patient with voice-call selected as their reminder channel, when reminder cadence triggers, then a voice call is placed with the configured script and successful delivery is logged.

### 13.5 Medications

**F-040 — Refill requests with proactive alerts**
- Given an active prescription approaching expiration or remaining-refills threshold, when threshold is reached, then patient and prescriber receive notifications per their channel preferences.

**F-041 — Refill status visibility**
- Given a submitted refill request, when status changes, then the patient sees status updates (submitted → received by prescriber → approved/denied → sent to pharmacy → ready/picked up where Surescripts data is available).
- Controlled-substance refills observe DEA/EPCS constraints (no online auth bypass).

**F-042 — Standing-order MA delegation w/ daily batch sign-off**
- Given a configured standing-order rule, when an MA processes refills under it, then the action is staged for physician daily sign-off and not transmitted to pharmacy until signed.

**F-043 — EPCS**
- Given a prescriber with EPCS credentials, when they prescribe a controlled substance, then the workflow enforces DEA two-factor authentication and produces a compliant audit record.

**F-044 — Pharmacy fill-data integration**
- Given a prescription transmitted to a pharmacy participating in Surescripts fill data, when fill events occur, then the events are displayed in the prescriber's view of the patient's medication list.
- Patient is informed in the privacy notice that fill data is visible to their care team (per Conflict 12).

**F-045 — Immunization records quick-share**
- Given a patient, when they request an immunization summary, then a PDF is generated within 5 seconds with the patient's name, DOB, immunizations, dates, and the issuing org.

### 13.6 Provider Workflow & Chart Review

**F-050 — Role- and specialty-configurable "patient at a glance"**
- Given a provider with a configured role/specialty layout, when they open a patient's at-a-glance view, then the configured layout renders within `NF-020` chart-open SLO with role-relevant data sections.
- Layout configuration is performed by clinical informatics without engineering deployment.

**F-051 — Outside-data provenance**
- Given a data element sourced externally (wearable, outside lab, HIE), when displayed, then source attribution is visible and clearly distinguishable from EHR-validated data.

**F-052–F-055 — Referral intake / structured referral / triage queue / consult-back loopback**
- Given an incoming referral, when intake runs, then required fields per specialty configuration are validated; missing fields trigger an auto-request to the referring provider.
- Triage queue applies configured urgency-classification rules; ambiguous cases escalate to physician.
- Given a completed consult, when consult-back is sent, then delivery confirmation is captured for both in-system and outside referrers (where outside-referrer scope permits).

**F-056 — Pre-op patient checklist**
- Given a scheduled procedure, when ≤ 24 hours before procedure time and patient has not confirmed checklist, then alert fires to the configured care team per `NF-060`.

**F-057 — Post-procedure messages to procedure-team nurse**
- Given a post-procedure patient message, when routed, then it goes to the procedure-team nurse queue first, not the specialist physician inbox.

**F-058 — Documentation stub creation**
- Given a portal-mediated clinical encounter (message exchange that meets defined criteria for documentation), when the encounter completes, then a documentation stub with structured fields is created in the EHR for provider completion.

**F-059 — Panel ownership view**
- Given a provider, when they open the panel view, then they see the patients assigned to their panel with last-touch dates and configurable filters.
- Reassignment requires the defined approval workflow.

### 13.7 Telehealth (F-060)

- Given a scheduled telehealth visit, when the join time arrives, then both patient and provider can join via a one-click action; provider can send a text message to the patient mid-visit.

### 13.8 Notifications, Errors, Channels

**F-070 — Channel preferences per event type**
- Given a user, when they configure preferences, then per-event-type channel selection (push, email, SMS, voice, in-app) is persisted and respected by all originating services.

**F-071 — Hard separation of clinical vs. marketing notifications**
- Marketing notifications are opt-in; cannot share infrastructure channel with clinical (no marketing message can be sent via a clinical notification template or channel).

**F-072 — SMS never contains login links**
- All clinical SMS templates pass an automated check; any template containing a login URL fails CI and cannot ship.

**F-073 — Proactive provider outage alerts**
- Given a detected or scheduled degraded state, when triggered, then providers receive a banner in the EHR and Teams notification ≥ configured pre-notice window before the event.

**F-074 — Friendly error messages with human fallback**
- Every user-facing error message states (a) what failed in plain language, (b) what the user can do, (c) a human-channel fallback for clinical workflows.

**F-075 / F-076 — Dependency failure + info-blocking-compliant degraded mode**
- Given a partial outage of Epic (or any documented external dependency), when patient surfaces render, then they show a visible "partial / loading" state for affected data, do not silently suppress access, and audit-log the suppressed-data event.

### 13.9 Mobile

**F-080 — Patient native mobile parity**
- Acceptance test plan validates every Phase 1 Must-Have functional ID on iOS, Android, and web. Any Phase 1 feature that ships on web must ship on mobile in the same release.

**F-081 — Provider mobile via Epic Haiku + thin patient-at-a-glance**
- Provider mobile path consists of (a) Epic Haiku for chart, inbox, EPCS as supported by Epic, and (b) a thin HealthConnect surface accessible from Haiku context that renders the at-a-glance configured view.
- No standalone provider native app is in Phase 1.

### 13.10 Dashboard (F-090)

- Given a logged-in user, when they open the home dashboard, then one of the variants ("Essentials," "Family," "Health Tracking") is rendered based on the user's selected default (suggestion only — never auto-applied based on demographic attribute).
- The user can switch variants from the dashboard in one tap/click; preference is persisted.

### 13.11 Privacy & Consent

**F-095 — Granular sharing controls**
- Given a patient, when they open sharing controls, then per-category sharing (with elevated controls for sensitive categories per `NF-038`) is configurable, with the current state visible.
- A change to a sensitive-category sharing setting is logged with timestamp and reason (where required by policy).

**F-096 — Data-subject-rights workflows**
- Right of access: patient request → fulfillment ≤ 30 days, with tracking visible to patient and operations.
- Amendment, accounting of disclosures, restriction request: each has a defined intake, tracking, and response surface.

**F-097 — Versioned consent records**
- Every consent action records: consent text version, time, IP/device, user, action taken; records are retrievable on demand for ≥ 6 years.

**F-098 — Versioned legal copy with re-acknowledgement**
- Given a material change to privacy notice / terms / consent, when the change ships, then existing users must re-acknowledge before their next sensitive action; re-ack is logged per `F-097`.

---

## 14. Appendix D — Data Model & Key Sequence Diagrams

> This appendix is illustrative. The canonical data model emerges from engineering design once §10 build-vs-buy decisions resolve. The entities and flows below establish vocabulary and surface design questions.

### 14.1 Domain Entity Inventory

**Identity & Access**
- `Person` — base identity (patient, provider, staff).
- `PatientAccount` — patient-specific account state (preferences, consents, MFA factors).
- `ProviderAccount` — provider-specific (specialty, role, panel membership).
- `ProxyGrant` — directed relationship between Persons (delegator, delegate, scope, expiration, lifecycle state).
- `Session` — auth session, device, IP, MFA factor used.

**Clinical (reference Epic as system of record where applicable)**
- `Patient` — clinical patient (Epic linkage).
- `Encounter` — visit, message thread, telehealth session (with type classifier).
- `Observation` — lab result, vital, patient-reported value.
- `Medication` — active med entry (Epic + Surescripts + patient-reported, with provenance flag).
- `Order` — refill request, referral, etc.
- `Referral` — first-class entity referencing source/destination providers, required fields by specialty, state.
- `CarePlan` — shared care plan with sections owned by different providers; version history.

**Messaging**
- `MessageThread` — conversation between patient and care team (or provider-to-provider).
- `Message` — single message; classification, urgency, routing target, AI-draft lineage.
- `MessageAttachment` — media reference w/ retention policy reference.

**Notifications**
- `NotificationEvent` — emitted by any service when an event of interest occurs.
- `NotificationDelivery` — per-channel delivery attempt for a given user × event.
- `UserChannelPreference` — per-event-type channel preference.

**Privacy / Consent**
- `Consent` — versioned consent record (subject, scope, action, time, evidence).
- `SharingPolicy` — patient's granular-sharing choices per data category × per recipient class.
- `SensitiveCategoryClassifier` — mapping from data element / source code → sensitive category (per §18).

**Audit & Compliance**
- `AuditEvent` — immutable record of every PHI access / state change.
- `BreakGlassEvent` — special audit subtype with justification.
- `PrivilegedAccessEvent` — admin / support / integration access.

**Content**
- `ContentItem` — patient-education, plain-language explanation, notification template; versioned.
- `ContentVersion` — each version with effective date, review date, approver.
- `Localization` — language-specific variant with translation provenance.

**AI**
- `ModelCard` — registry entry per AI feature (intended use, scope, performance, owner).
- `AIInvocation` — log of model call (feature, model version, prompt template version, retrieved sources, output, downstream action).

**Billing**
- `Bill` — patient bill (linked to encounter, guarantor account).
- `PaymentMethod` — tokenized payment method reference (no PAN in scope).
- `Payment` — payment event.

**Operations / Telemetry**
- `FeatureFlag` — flag state with audience targeting.
- `Incident` — incident record with severity, impact, runbook reference.

### 14.2 Sequence Diagram — AI Message Draft with Provider Sign-Off (F-014)

```
Patient        Portal API     Inbox Svc    AI Orchestrator   Provider UI    Audit
  |                |              |              |                |             |
  |---compose---->|              |              |                |             |
  |                |--persist---->|              |                |             |
  |                |              |--classify-->|                |             |
  |                |              |              |--retrieve-->  |             |
  |                |              |              |    (RAG)      |             |
  |                |              |              |--generate-->  |             |
  |                |              |<-draft + sources-|            |             |
  |                |              |--log invocation--------------|------------>|
  |                |              |--route to inbox--------------|->            |
  |                |              |                              |--render-->  |
  |                |              |                              |  (with     |
  |                |              |                              |   label,   |
  |                |              |                              |   sources) |
  |                |              |                              |             |
  |                |              |  Provider reviews, edits     |             |
  |                |              |  ---sign + send-->           |             |
  |                |              |<------------------------------|             |
  |                |              |--log original + edits + final--------->|
  |                |              |--deliver-->                  |             |
  |<--notification-|              |                              |             |
```

### 14.3 Sequence Diagram — Proxy Grant Lifecycle (F-002)

```
Delegator   Portal     Proxy Svc    Identity Svc    Delegate    Audit    Notification
   |          |             |             |             |          |            |
   |--grant->|             |             |             |          |            |
   |          |--validate->|             |             |          |            |
   |          |             |--proof of relation->     |          |            |
   |          |             |<-evidence captured-      |          |            |
   |          |             |--create grant (state=PENDING_DELEGATE_ACK)----->|
   |          |             |                          |          |            |
   |          |             |--notify delegate------------------>|----------> |
   |          |<--success---|                          |          |            |
   |          |             |                          |--accept->|            |
   |          |             |<--ack--                  |          |            |
   |          |             |--update state=ACTIVE--------------->|            |
   |          |             |--notify both parties--------------->|----------> |
   |          |             |                                                  |
   ...time passes...
   |          |             |--scheduled job: check expirations--------------->|
   |          |             |--update state=EXPIRED----------->|              |
   |          |             |--notify both------------------------------------>|
```

### 14.4 Sequence Diagram — Info-Blocking-Compliant Degraded Mode (F-075, F-076)

```
Patient      Portal API    Results Svc    Epic Adapter    Audit
   |             |              |               |             |
   |--view lab-->|              |               |             |
   |             |--get results->|              |             |
   |             |              |--fetch------>|              |
   |             |              |       (Epic API failing)    |
   |             |              |<--error / partial-|         |
   |             |              |--log degraded event------->|
   |             |<-partial data + reason-|                   |
   |<-show partial data + visible "loading" state + last update time-|
   |                                                          |
   (no silent suppression; user informed; event in audit log)
```

### 14.5 Sequence Diagram — Sensitive-Category Sharing Change (F-095, NF-038)

```
Patient      Portal     Sharing Svc   Sensitive Cat Classifier   Consent Svc   Audit
   |          |             |                |                       |             |
   |--change->|             |                |                       |             |
   |          |--update---->|                |                       |             |
   |          |             |--classify changed scope---->          |             |
   |          |             |<--sensitive category set-              |             |
   |          |             |--require explicit re-consent on sensitive change->| |
   |          |             |<-consent recorded with version-                    | |
   |          |             |--apply change-->                       |             |
   |          |             |--log change with before/after-------------------->|
   |          |<--confirmed-|                                                    |
```

### 14.6 Open Modeling Questions

- Read-model strategy against Epic: pass-through vs. materialized vs. hybrid (constrained by Epic license terms).
- Audit-event partitioning strategy at scale (6-year retention, immutability).
- Sharing-policy effective-time model (point-in-time consent vs. current-state, for retrospective queries).
- AI invocation log retention (medical-legal lookback window TBD).

> ### 🟥 STAKEHOLDER INPUT REQUIRED — Engineering input
> A formal data model and the canonical sequence diagrams emerge from engineering design after §10 build-vs-buy decisions. The model above is a starting vocabulary, not a committed schema.

---

## 15. Appendix E — Testing Strategy

### 15.1 Test Layers

| Layer | Scope | Tooling pattern | Owner |
|---|---|---|---|
| Unit | Pure logic, branch coverage targets ≥ 80% for safety-critical modules (consent, sharing, audit, messaging, AI orchestrator) | Per-stack standard | Engineering |
| Service / contract | Domain services in isolation; consumer-driven contracts with downstream | Pact-style or equivalent | Engineering |
| Integration | End-to-end across HealthConnect services with mocked Epic / vendor surfaces | Per-stack | Engineering |
| FHIR conformance | US Core profile conformance for resources we emit/consume | Inferno / Touchstone | Integration |
| Accessibility | Automated (axe-core) on every PR for patient + provider surfaces; manual audit per `NF-010` | axe-core + independent audit vendor | Design + QA + external |
| Performance | SLO targets per `NF-020`, `NF-026–028`; load test pre-release per `NF-029e` | k6 / Gatling / JMeter | SRE + QA |
| Security | SAST/DAST/dep scan in CI (`NF-039d`); pen test pre-release | Per security partner | Security |
| Privacy | Data-flow tests verifying PHI does not leak to non-BAA destinations | Custom + audit-log analysis | Privacy + Engineering |
| AI safety eval (new) | See §15.2 | See §15.2 | Clinical informatics + AI gov |
| Clinical validation (new) | See §15.3 | See §15.3 | Clinical informatics + Clinical leadership |
| UAT | Provider, patient, staff representative cohorts pre-release | Manual + script | Product + Clinical ops |
| Compatibility / device | iOS 15+, Android 11+ device matrix; major browsers | BrowserStack / Sauce Labs | QA |
| Localization | Multi-language UI + content rendering | Manual + automated | QA + Translation governance |

### 15.2 AI Safety Evaluation

Applies to every AI feature (`F-014`, `F-015`, `F-016`, `F-022`, and any AI-assisted content surface).

**Pre-release gates per feature:**
1. **Intended-use definition + model card** complete (`NF-044`).
2. **Eval set construction:** representative held-out test set sized per risk class, curated by clinical informatics; includes adversarial / edge / sensitive-category prompts.
3. **Performance evaluation:**
   - Accuracy / faithfulness vs. expert-labeled ground truth.
   - Hallucination rate (% of outputs containing claims not supported by retrieved sources for RAG features).
   - Source-citation completeness.
   - Refusal-when-uncertain behavior.
4. **Bias / disparity evaluation:** performance disparities across demographic stratifications per `NF-043`; remediation if threshold breached.
5. **Prompt-injection / adversarial input resistance** (per risk §8 candidate requirement).
6. **PHI-leakage testing:** no PHI in logs sent to non-BAA destinations; no PHI in non-prod environments per the same candidate requirement.
7. **Patient-disclosure compliance:** if feature is patient-facing clinical content, disclosure UI verified per state law (California AB 3030 et al.).
8. **Clinical safety sign-off:** documented review by clinical informatics + AI governance committee.

**Post-release monitoring:**
- Acceptance / edit-distance / discard rate per feature.
- Sampling-based human review at defined cadence.
- Adverse-event log w/ root-cause review.
- Re-evaluation on every model version change or prompt-template change.

### 15.3 Clinical Validation

Applies to features whose failure could affect patient safety: red-flag detection (`F-016`), pre-op checklist alerting (`F-056` / `NF-060`), AI-drafted reply if any clinical content (`F-014`), lab-result release flows (`F-020`), care-plan changes (`F-178`), AI-derived chart summarization (`F-050` AI elements).

**Validation activities:**
1. **Clinical-safety case** per feature, documenting hazards, mitigations, residual risk, accepted by clinical leadership. (Format borrows from UK DCB0129/0160 even if not formally required in U.S.)
2. **Workflow / time-motion study** pre- and post-release for provider-facing changes.
3. **Pilot in limited clinic** before broad release (see §16).
4. **Patient-safety event reporting integration** so incidents traceable to portal features flow into the org's safety-event system.
5. **Periodic re-validation** on material change.

### 15.4 Migration Testing

Per §11:
- Cutover dry runs per cohort with rollback rehearsal.
- Data-reconciliation reports comparing legacy ↔ HealthConnect counts.
- Inbound-link redirect smoke tests.
- Patient communications dry run.

### 15.5 DR & Resilience Testing

- DR exercise annually per `NF-029i`.
- Chaos / fault-injection on non-prod targeting Epic adapter, LLM provider, telehealth vendor, payment processor degraded modes (`F-075`).
- Feature-flag / kill-switch rehearsal (`NF-029g`).

### 15.6 Continuous Quality

- Every PR: unit + automated accessibility + SAST + dep scan + lint + smoke.
- Every release candidate: contract + integration + perf-budget + DAST + AI safety regression on changed features.
- Quarterly: pen test, accessibility-audit cadence per `NF-010`, DR exercise (annual).

---

## 16. Appendix F — Pilot Plan (Framework + Stakeholder Input Required)

### 16.1 Pilot Objectives

- Validate Phase 1 functional and non-functional behavior with real users before broad release.
- Surface workflow disruption, training adequacy, helpdesk-load actuals, and AI-feature acceptance with low blast radius.
- Establish cohort-level migration playbook before broader cohort migrations begin (§11).
- Generate stratified baseline metrics for equity guardrails (`NF-072`).
- Test pilot-exit criteria as a repeatable GA gate.

### 16.2 Pilot Cohort Selection — Criteria Framework

A pilot clinic / cohort should ideally:

1. Span both PCP and at least one specialty surface used by the configurable summary view (`F-050`).
2. Include a meaningful proportion of each major patient cohort (chronic-condition managers, families, seniors, mobile-primary users) so equity stratification is meaningful.
3. Have engaged clinical leadership willing to act as program partners and surface friction quickly.
4. Have a manageable, observable patient volume (large enough to generate meaningful signal, small enough to be helpdesk-supportable).
5. Have an existing in-clinic staffing model that can support ambassador / assisted-onboarding (`F-210`).
6. Not be in an active labor disruption, EHR change, or other parallel transformation.

### 16.3 Pilot Phases

| Phase | Duration | Population | Scope | Exit criteria |
|---|---|---|---|---|
| P0 — Internal alpha | 4 weeks | Employees & families opting in | Full Phase 1 scope | No SEV-1 in 2 weeks; AI safety eval passed; pen-test critical findings closed |
| P1 — Single-clinic pilot | 8 weeks | One pilot clinic; opt-in patient registration | Full Phase 1 scope | Exit criteria §16.4 met |
| P2 — Multi-clinic expansion | 6 weeks | 3–5 clinics covering different specialties | Full Phase 1 scope | Exit criteria §16.4 met at scale; helpdesk capacity validated |
| GA — Broad release | — | All patients via phased migration per §11 | Full Phase 1 scope | Steering go/no-go based on P2 results |

### 16.4 GA Exit Criteria from Pilot

**Functional / quality**
- All Phase 1 Must-Have requirements (Appendix C) pass acceptance criteria for ≥ 95% of relevant interactions.
- No open SEV-1 incidents; no patient-safety incident with portal causation.
- AI-feature acceptance rate and adverse-event review meet predefined thresholds.
- Accessibility audit findings remediated to defined severity SLA per `NF-010`.
- Migration data-quality and proxy re-validation per §11.7 meets acceptance criteria.

**Performance / reliability**
- `NF-020`, `NF-026`, `NF-027`, `NF-028` SLOs met at pilot load with documented headroom for projected GA load.
- Concurrent-user load test against projected peak passes (`NF-029e`).
- DR plan tested and acceptable per `NF-029i`.

**Operational readiness**
- Helpdesk volume per registered user within budgeted SLA tier.
- Runbooks exercised; on-call rotation staffed.
- Incident response runbook validated (`NF-029h`).

**Equity / experience**
- Stratified adoption metrics (`NF-072`) show no cohort regressing materially vs. baseline.
- 70+ cohort engagement guardrail (`NF-070`) shows acceptable trend.
- Phone-channel preservation (`NF-071`) holding.
- NPS / patient experience baseline established.

**Provider**
- Provider satisfaction baseline established; no provider attrition attributable to portal.
- Inbox-time trend per `R-ORG-02` mitigation acceptable.

**Compliance / safety**
- Zero open HIPAA / OCR escalations attributable to portal.
- Clinical safety case re-affirmed post-pilot per §15.3.
- AI safety eval re-run on prod telemetry and accepted.

### 16.5 Rollback / Halt Criteria

Any of the following triggers a halt of further rollout and steering committee review:
- Any patient-safety incident with plausible portal causation.
- SEV-1 incident not contained within defined incident-response SLA.
- Sustained breach of `NF-070` 70+ cohort engagement guardrail.
- Measurable phone-channel degradation per `NF-071`.
- Statistically significant adoption disparity in stratified metrics with no actionable remediation.

> ### 🟥 STAKEHOLDER INPUT REQUIRED — Pilot specifics
> **Why this section is incomplete:** Pilot clinic selection is an organizational and clinical-political decision that cannot be made from outside the org. Patient-volume targets and SLA thresholds depend on org capacity and risk appetite.
>
> **Who needs to provide the input:** Sponsor; Clinical Operations leadership; Clinical Informatics; specialty-leadership reps; Patient Experience; Health Equity.
>
> **What is needed:**
> - Clinic / cohort selection for P1 and P2.
> - Quantitative thresholds on each pilot-exit criterion (e.g., acceptable helpdesk volume per registered user; AI-feature acceptance threshold; stratified-disparity thresholds).
> - Patient communication and consent approach specific to the pilot clinics.
> - Decision authority on halt/proceed at each pilot phase.
>
> **Blocking for:** §9 milestone gates from "Phase 1 pilot" → "Phase 1 GA."

---

## 17. Appendix G — Adolescent-Privacy State Matrix (Stakeholder Input Required)

### 17.1 What This Section Should Contain

A state-by-state matrix governing F-006 / F-110 access rules for each U.S. state where HealthConnect patients reside, covering:

- Age of consent for various care categories (general medical, mental health, reproductive health, substance use, contraception, HIV/STI, gender-affirming care).
- Parent-vs-minor access rules per category and per age range.
- Transition events (e.g., birthday triggering access change, emancipation status, custody-change events).
- Required notifications (parent / minor / both) at each transition.
- Emergency parental-override conditions and definition of "emergency."

### 17.2 Framework Template

Per state, the matrix would express rules as:

| State | Age range | Care category | Minor sole consent? | Parent access default | At threshold age | Notification requirement | Notes |
|---|---|---|---|---|---|---|---|
| (State) | 0–11 | All | No | Full | — | — | — |
| (State) | 12–17 | General medical | Per state law | Per state law | Per state law | Per state law | — |
| (State) | 12–17 | Mental / behavioral | Often minor-only at varying ages | Restricted per state | — | Per state law | Highly variable |
| (State) | 12–17 | Reproductive | Per state law (rapidly changing) | Restricted per state | — | Per state law | Post-Dobbs especially variable |
| (State) | 12–17 | Substance use | 42 CFR Part 2 + state | Restricted | — | Per rule | If SUD records in scope |
| (State) | 12–17 | HIV / STI | Most states minor-only | Restricted | — | Per state law | — |
| (State) | 18 | All | Adult | None (proxy only by consent) | Birthday | Both | Transition event |

### 17.3 Operationalization

Once the matrix is built:
- Encoded as `SharingPolicy` × `Person.stateOfResidence` × `Person.age` × `CareCategory` rules in the sharing engine.
- Driven by the `SensitiveCategoryClassifier` (§18) to map data elements to categories.
- Versioned with effective dates; rule changes are auditable and trigger patient notifications where required.
- Reviewed for legal accuracy at least annually and on any material state-law change.

### 17.4 Default Conservative Posture

Until the matrix is built per state, **operational default for F-006 enforcement should be the most restrictive applicable rule** — i.e., assume minor-only consent for sensitive categories and full lockout of parent access at the adult-transition age, with no automatic re-grant.

> ### 🟥 STAKEHOLDER INPUT REQUIRED — State matrix
> **Why this section is incomplete:** The matrix requires per-state legal analysis for every state in HealthConnect's Phase 1 patient population. This is a legal deliverable, not a product deliverable. The matrix is also subject to rapid change (post-Dobbs trajectory and state legislative cycles).
>
> **Who needs to provide the input:** Legal (with state-specific counsel where needed); Compliance; Clinical leadership (definition of sensitive-care categories in scope); Privacy Officer.
>
> **What is needed:**
> - List of states in Phase 1 patient population.
> - Per-state policy matrix for at least: general medical, mental/behavioral health, reproductive health, HIV/STI, substance use (if in scope), contraception, gender-affirming care (where state law addresses).
> - Definition of "emergency" for parental override.
> - Update / review cadence for the matrix and process for emergent legal changes.
>
> **Blocking for:** F-006 Phase 1 enforcement; F-110 Phase 2 scope; R-REG-03 mitigation; A-007, A-011 closure.

---

## 18. Appendix H — Sensitive-Category Data Segmentation Plan

### 18.1 Scope

Categories treated as sensitive — subject to elevated access controls per `NF-038` and granular sharing controls per `F-095`:

1. **Mental / behavioral health** — diagnoses, encounters, medications, notes.
2. **Substance use disorder** — diagnoses, treatment, medications; if in 42 CFR Part 2 scope, additional rules apply (`NF-075`, `A-035`).
3. **Reproductive health** — pregnancy, contraception, fertility, abortion-related encounters (post-Dobbs heightened sensitivity, state-variable).
4. **HIV / STI** — diagnoses, testing, treatment.
5. **Genetic** — genetic test results, family-history specifics, GINA-relevant.
6. **Adolescent-specific** — care delivered under minor-consent rules per state matrix (§17).
7. **Gender-affirming care** — where state law treats as distinct category.

### 18.2 Classification Approach

A `SensitiveCategoryClassifier` maps source data elements to category set(s). Mapping inputs:

- ICD-10 codes (DSM/F-codes for mental health; F10–F19 for SUD; O00–O9A / Z3A for reproductive; B20 for HIV; A50–A64 for STI).
- SNOMED CT problem-list concepts.
- CPT / HCPCS procedure codes.
- LOINC observation codes for relevant lab panels.
- RxNorm medication classes (psychotropics, MAT meds, contraceptives, antiretrovirals).
- Source encounter type / department-of-service flags.
- Free-text classification on notes (NLP-based; treated as supplementary signal, not authoritative).
- Explicit patient declaration (patient-asserted category opt-in).

Each data element may carry multiple category tags. Access control evaluates the union.

### 18.3 Segmentation Mechanics

**Storage and access:**
- Sensitive-category tags propagate with the data element through the data model (not as a separate "is sensitive?" view).
- Access control evaluates per request: (subject role) × (category tags on data) × (patient's sharing policy) × (state-law overlay per §17) → allow / deny / require step-up.

**UI rendering:**
- Sensitive-category data redacted by default in views accessible to broader roles (e.g., admin staff) unless explicit need exists.
- Patient sees an indicator on the sharing UI showing which categories are flagged and who currently has access.

**Sharing changes:**
- Per `F-095`, increasing share scope on a sensitive category requires explicit patient action with re-consent recording (`F-097`); decreasing scope is one click.

**Proxy interaction:**
- Proxy grants do **not** by default extend to sensitive-category data; sensitive-category proxy access requires explicit, separately-recorded grant.

**Logging:**
- Sensitive-category access is logged with the category indicator so audit-review workflows (`NF-079`) can prioritize.

**Disclosure / export:**
- Right-of-access exports (`F-096`) include sensitive-category data with explicit category labeling.
- TEFCA / HIE outbound traffic respects sensitive-category sharing policy.

### 18.4 Failure Modes & Mitigations

| Failure mode | Mitigation |
|---|---|
| Classifier misses a data element → data not tagged → broader access than intended | Periodic sampling audit; conservative default for unmapped codes; explicit patient-declared opt-in always honored |
| Multi-tag conflicts (data element in multiple categories) | Most-restrictive-wins rule |
| Free-text leakage of sensitive content into non-sensitive notes | Authoring-time guidance; periodic NLP scan; patient request channel |
| State-law change reclassifies category | Matrix versioning (per §17) + bulk re-evaluation job + patient notification |
| Cross-portal / HIE replication of un-tagged data | Outbound segmentation gate; do not propagate without category metadata |

### 18.5 Operational Governance

- **Owner:** Privacy Officer + Clinical Informatics (joint).
- **Review cadence:** quarterly classifier-accuracy review; annual full policy review; ad hoc on regulatory change.
- **Change control:** new code-set additions to classifier go through clinical informatics review.
- **Patient transparency:** sharing UI surfaces "what is treated as sensitive" with plain-language explanations (per `F-022` content style).

### 18.6 Phase Placement

| Capability | Phase |
|---|---|
| Classifier + tagging infrastructure | Phase 1 |
| Patient sharing UI w/ sensitive-category controls (`F-095`) | Phase 1 |
| Elevated access controls (`NF-038`) | Phase 1 |
| Right-of-access export with category labeling (`F-096`) | Phase 1 |
| HIE outbound segmentation gate | Phase 1 if interop active, else when needed |
| 42 CFR Part 2 segmentation (if applicable) | Determined by `A-035` scope |
| NLP-based free-text classifier | Phase 2 (supplementary) |

> ### 🟥 STAKEHOLDER INPUT REQUIRED — Sub-items in §18
> - **Final code-set boundaries** per category — requires clinical informatics + compliance sign-off.
> - **42 CFR Part 2 applicability decision** (`A-035`).
> - **Default access-control matrix** for each (role × category) pair — requires Privacy Officer + Compliance + Clinical leadership.
> - **Patient-asserted opt-in UI scope** — UX design + Privacy Officer.
> - **Outbound interop segmentation scope** — depends on TEFCA / QHIN decision (`A-038`).

---

## 19. Appendix I — Nurse-Triage & Async-Messaging Staffing (Stakeholder Input Required)

### 19.1 Why Staffing Is a Launch Gate

Per top risk `R-ORG-01` and Conflict 2 resolution, async nurse-triage chat (`F-100`), urgent-message escalation (`F-019`), and the message-routing rules that send admin/billing/scheduling away from physicians (`F-011`) **all assume non-physician clinical staff capacity** to absorb the resulting message and triage workload. Industry experience (per the market analysis) consistently shows that mature portal messaging programs **increase**, not decrease, the need for clinical messaging staff.

Without funded staffing, the failure mode is predictable: load lands on physicians, response degrades, or messages back up — eroding all the program's clinical-experience and provider-burnout goals.

### 19.2 Sizing Framework

Staffing sizing requires:

1. **Projected patient registration and active-user counts** by phase (drives total message volume).
2. **Message-per-active-user-per-month** estimate (industry benchmark range: 0.5–2.0 messages/user/month at maturity; higher in chronic-condition populations).
3. **Distribution across message categories** (clinical vs. admin/billing/scheduling, urgent vs. routine) — drives nurse vs. MA vs. scheduler vs. billing staffing mix.
4. **Target SLA per category** — drives staffing-to-volume ratio.
5. **Operating hours** — business-hours-only vs. extended-hours vs. 24/7 — drives coverage shifts.
6. **After-hours model** — per `F-019b` warning + alternate paths, or staffed after-hours triage.
7. **Geographic / state-licensure scope** for nurse triage (telehealth nurse triage is a licensed activity).
8. **Async-messaging billing model** (`B-010` / `F-181`) — billable CPT 99421–99423 messaging may offset cost.

### 19.3 Staffing Roles in Scope

| Role | Function | Volume driver |
|---|---|---|
| Triage RN | Clinical triage, async chat, urgent-message acknowledgement | Clinical message volume + urgent escalations |
| MA | Refill workflow under standing orders, admin message handling | Refill volume + admin message volume |
| Scheduler | Scheduling messages, appointment changes | Scheduling message volume |
| Billing specialist | Billing-question messages | Billing message volume |
| Helpdesk Tier 1 | Patient-side technical help; account recovery (PHI-aware) | Registered-user base × support-rate |
| Helpdesk Tier 2 | Escalations | Tier 1 escalation rate |
| Provider champion / super-user (per clinic) | Adoption support, change mgmt | Per-clinic count |
| Cutover surge staff | Migration windows (per §11) | Cohort schedule |

### 19.4 Operational Decisions Required

- Centralized triage team vs. clinic-embedded model vs. hybrid.
- In-house vs. partner (nurse-triage outsourcing exists; quality and HIPAA / state-licensure implications).
- Hours of coverage and after-hours fallback.
- Escalation tree from triage RN to on-call provider.
- Standing-order delegation policy (per `F-042` MA delegation).
- Charge-capture workflow for billable async messaging.
- KPI dashboard ownership.

> ### 🟥 STAKEHOLDER INPUT REQUIRED — Staffing model and cost
> **Why this section is incomplete:** Staffing model and FTE counts depend on the org's existing clinical operations model, current message-handling baseline, projected patient volume by phase, hours-of-coverage policy decisions, and licensure scope. None of these are knowable from outside the org. This is the single largest **OPEX** line item not yet sized, and is a **launch gate** per `R-ORG-01`.
>
> **Who needs to provide the input:** Clinical Operations leadership (primary); Clinical leadership; Nursing leadership; Revenue Cycle (for billing model); HR (for hiring lead times); Finance (for OPEX sizing); Patient Access leadership (for helpdesk).
>
> **What is needed:**
> - Projected message volume per category at end-of-Phase-1, Phase-2, Phase-3.
> - Target SLA per message category.
> - Coverage policy (hours, geography, after-hours model).
> - Sourcing decision (in-house vs. partner).
> - FTE plan + hiring timeline.
> - Funded OPEX line in the year-1 and year-2+ budgets.
> - Billing-model decision for async messaging (`B-010`).
> - Helpdesk model + funding (`NF-086`).
>
> **Blocking for:** Launch of `F-019`, `F-100`, `F-019b`, `F-181`; Phase 2 GA decision; budget envelope confirmation in §12; pilot-to-GA exit criteria in §16; Phase 1 sponsor go/no-go.

### 19.5 Interim Risk Posture

Until staffing is sized and funded, the following capabilities should be treated as **conditionally Should-Have, not committed Phase 2** until the staffing gate is met:
- `F-100` async nurse-triage chat.
- `F-019` urgent-message acknowledgement SLA monitoring as a contractual SLA (operational monitoring can ship without the staffing).
- Any expansion of patient-initiated messaging volume beyond Phase 1 baseline.

`F-011` (admin/billing/scheduling routed away from physician inbox) and `F-013` (physician inbox triage view) ship in Phase 1 regardless; their value to physicians is significant even before nurse-triage scales.

---

**End of PRD draft v0.1 + Appendices A–I.** Review with sponsor + steering committee, resolve §10 blocking items and the alert-flagged appendices, then incorporate into v0.2.
