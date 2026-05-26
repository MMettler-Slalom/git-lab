# Cross-Persona Requirement Conflicts & Proposed Resolutions

**Sources:** All five persona requirements extracts in this folder
**Author:** M. Mettler
**Date:** May 20, 2026
**Status:** Draft for Phase 2 synthesis review

> This document consolidates the 🔁 conflict flags raised in each persona extract, plus tensions that emerge only when looking across personas. Each conflict includes the personas involved, the underlying tension, a proposed resolution, and follow-up actions. Resolutions are **proposals** — they require stakeholder sign-off before being locked into the PRD.

---

## Index

1. [Lab-result release timing](#1-lab-result-release-timing)
2. [Message-volume expectations vs. provider inbox capacity](#2-message-volume-expectations-vs-provider-inbox-capacity)
3. [Notification channel preferences](#3-notification-channel-preferences)
4. [AI assistance scope and autonomy](#4-ai-assistance-scope-and-autonomy)
5. [Dashboard / home-screen content density](#5-dashboard--home-screen-content-density)
6. [Phone-call reduction as a success metric](#6-phone-call-reduction-as-a-success-metric)
7. [Family-account roadmap sequencing](#7-family-account-roadmap-sequencing)
8. [Wearable / device data ingestion and provider liability](#8-wearable--device-data-ingestion-and-provider-liability)
9. [Specialty-customizable UI vs. unified provider experience](#9-specialty-customizable-ui-vs-unified-provider-experience)
10. [Mobile experience — one app or two](#10-mobile-experience--one-app-or-two)
11. [Authentication friction vs. security posture](#11-authentication-friction-vs-security-posture)
12. [Patient consent and pharmacy fill visibility](#12-patient-consent-and-pharmacy-fill-visibility)
13. [Release cadence and UI stability](#13-release-cadence-and-ui-stability)
14. [Care-plan ownership and editorship](#14-care-plan-ownership-and-editorship)
15. [Trainee / teaching workflows — persona scope](#15-trainee--teaching-workflows--persona-scope)
16. [Cross-system interop scope](#16-cross-system-interop-scope)
17. [Medication coordination across providers](#17-medication-coordination-across-providers)

---

## 1. Lab-result release timing

**Personas involved:** Chronic Condition Manager (Linda), Tech-Limited Senior (Eleanor), Primary Care Physician (Dr. Alvarez)

**Conflict:**
- Linda wants lab results visible at the same moment her provider sees them (`F-CCM-03`).
- Eleanor wants proactive notification of results — both normal and abnormal — because silence is anxiety-producing (`F-TLS-06`).
- Dr. Alvarez's workflow assumes she reviews results before they hit patients, especially for sensitive findings; instant release creates risk of patients seeing concerning results without context.
- Federal information-blocking rules (21st Century Cures Act) generally require timely release; this constrains how long results can be held.

**Proposed resolution:**
- **Default policy:** results are released to the patient immediately on availability, in compliance with information-blocking rules.
- **Carve-out categories** (e.g., oncology biopsies, genetic testing, certain imaging) follow a short, defined provider-review window — defined by clinical leadership, not per-provider preference.
- For every released result, surface a plain-language explanation, the target range, the trend vs. prior result, and an inline "message your care team" CTA so patients have a path to context without waiting.
- A `result_status` notification fires for both normal and abnormal results (Eleanor's need) — patient controls channel.

**Follow-up actions:**
- [ ] Clinical leadership defines the carve-out category list.
- [ ] Legal confirms alignment with information-blocking and state-law requirements.
- [ ] UX designs the "result + context + action" landing pattern.

---

## 2. Message-volume expectations vs. provider inbox capacity

**Personas involved:** Busy Parent (Marcus), Chronic Condition Manager (Linda), Primary Care Physician (Dr. Alvarez), Specialist (Dr. Okonkwo)

**Conflict:**
- Marcus and Linda want fast, frequent, multi-channel communication with care teams (async nurse chat, faster response SLAs, direct lines to specific care-team members).
- Dr. Alvarez is already at message-volume breaking point and warns adding channels without staffing changes will accelerate burnout.
- Dr. Okonkwo gets significant off-scope messaging volume that should be redirected.

**Proposed resolution:**
- Treat messaging volume as an **operations + staffing problem**, not a product-features problem. Product can route, triage, and assist, but cannot independently solve volume.
- **Routing and intake rules** (`F-PCP-01`) keep admin, scheduling, billing, and form-request messages out of the physician inbox entirely.
- **Tiered response SLAs** by message type, communicated in the patient UI at compose time ("a nurse typically replies within 4 hours" vs. "your physician typically replies within 1 business day").
- **Async nurse-triage chat** (`F-BP-11`) becomes the front door for clinical questions for both pediatric and adult patients; staffing model owned by clinical operations and must be funded before the feature ships.
- **AI assists** with summarization, classification, and drafting (`F-PCP-04`, `F-PCP-05`) — never autosend.
- **Off-scope redirect** (`F-SP-20`) is available as a one-click action for specialists and PCPs alike.

**Follow-up actions:**
- [ ] Clinical operations commits to nurse-triage staffing model and FTE budget.
- [ ] Revenue cycle defines the async-messaging billing/compensation model (`B-PCP-02`).
- [ ] Set explicit SLA targets per message tier; embed them in patient compose UX.

---

## 3. Notification channel preferences

**Personas involved:** All five

**Conflict:**
- Linda: push + email; explicit no-SMS (scam fear).
- Marcus: push primary; hard no on marketing emails.
- Eleanor: voice-call reminders preferred; SMS would be invisible to her.
- Providers: in-system alerts (EHR banner, Teams) preferred over email/SMS.

**Proposed resolution:**
- Adopt a **channel-by-event-type preference model**. For each notification event (appointment reminder, result available, message reply, refill ready, marketing/health-tip), each user configures channel(s) independently from a fixed set: push, email, SMS, voice call, in-app only.
- Reasonable defaults per cohort (e.g., 70+ default to voice + email; <30 default to push); user can override at any time.
- **Hard separation between clinical and marketing/health-promotion notifications** (`NF-BP-05`). Marketing must be opt-in, not opt-out, on a distinct channel set.
- Anti-phishing affordance: clinical SMS, when used, must never contain a login link; only direct user to open the app (`NF-TLS-08`).

**Follow-up actions:**
- [ ] Define the canonical notification-event taxonomy.
- [ ] Marketing/comms agree to opt-in model for non-clinical messaging.
- [ ] Default preferences-by-cohort proposed by UX and reviewed for ageism / bias.

---

## 4. AI assistance scope and autonomy

**Personas involved:** Chronic Condition Manager (Linda), Primary Care Physician (Dr. Alvarez), Specialist (Dr. Okonkwo)

**Conflict:**
- Linda wants AI-surfaced insights (trends, correlations) but with full transparency into source data — "I want to verify."
- Dr. Alvarez supports AI assistance for inbox drafting, summarization, classification, and red-flag detection — but draws a hard line at any AI autosending in her name.
- General organizational AI-governance posture is still being formed.

**Proposed resolution:**
- **Foundational AI policy** for the portal (applies to all AI features):
  1. AI never sends clinical content to patients without provider review and explicit signoff.
  2. Every AI-generated artifact (summary, draft, suggestion) is labeled as AI-generated.
  3. Source data and citations are always one click away from any AI output.
  4. AI is assistive only; clinical recommendations and decisions remain with licensed providers.
- **Limited exception:** purely administrative/templated autoresponses (e.g., "your refill request was received and routed to the nurse") may be system-sent without clinical content. These should be reviewed against the no-clinical-content test before deployment.
- **Patient-facing AI features** (trend insights, plain-language summaries) follow the same labeling + source-visibility rules.

**Follow-up actions:**
- [ ] Confirm policy with the org's AI-governance owner.
- [ ] Define the test for "clinical vs. administrative" content with clinical + legal input.
- [ ] Design the standard "AI-generated" labeling and source-link affordances.

---

## 5. Dashboard / home-screen content density

**Personas involved:** Tech-Limited Senior (Eleanor), Busy Parent (Marcus), Chronic Condition Manager (Linda)

**Conflict:**
- Eleanor wants a stripped-down home screen with at most three items.
- Marcus wants family-member badges, multiple consolidated views, and quick switching.
- Linda wants trend visualizations and at-a-glance health information.

**Proposed resolution:**
- **Personalized / role-aware home dashboard** with a small fixed set of layout variants (e.g., "Essentials," "Family," "Health Tracking").
- Patients can switch variants from settings; sensible defaults assigned at onboarding based on age range and family-account composition (but never imply ageism — defaults are suggestions, not gates).
- All variants share the same underlying actions; what changes is information density and layout, not feature availability.
- **Do not** auto-apply "Essentials" mode based solely on age — let users opt in.

**Follow-up actions:**
- [ ] UX designs three variant layouts and validates with each persona segment.
- [ ] Define onboarding flow that surfaces variant choice without making it feel ageist.

---

## 6. Phone-call reduction as a success metric

**Personas involved:** Tech-Limited Senior (Eleanor), business stakeholders (product brief)

**Conflict:**
- Product brief targets a 50% reduction in phone-call volume.
- Eleanor will not adopt the portal at all if the phone channel is degraded; many seniors fall into the same pattern.
- Optimizing aggressively for call reduction risks harming the cohort least able to advocate for itself.

**Proposed resolution:**
- Keep the 50% call-reduction metric, but **scope it explicitly** to call types that the portal is designed to displace (appointment scheduling, refill requests, simple admin questions) — measured across the entire patient population.
- **Carve out a "human-channel preservation" guardrail:** call-volume reduction in the 70+ cohort is **not** a portal success criterion. For that cohort, success is measured by satisfaction, completion of digital tasks attempted, and absence of harm.
- Operations cannot use portal adoption as justification for closing the phone channel or reducing front-desk staffing serving this cohort.

**Follow-up actions:**
- [ ] Rewrite the success-metric section of the PRD to scope the call-reduction target.
- [ ] Get operations leadership commitment to the human-channel preservation guardrail.
- [ ] Define alternative engagement metrics for the 70+ cohort.

---

## 7. Family-account roadmap sequencing

**Personas involved:** Busy Parent (Marcus)

**Conflict:**
- Product brief places "Family Account Management" in Phase 2 (Months 5–8).
- Marcus's interview makes clear that for the busy-parent segment, family management is a Phase 1 must-have; without it, that segment's adoption will be weak.
- Phase 1 adoption KPIs (60% registration, 40% MAU) depend on broad segments adopting quickly.

**Proposed resolution:**
- **Pull "minimum viable family account" forward into Phase 1.** Scope it tightly:
  - Single login with linked dependents.
  - View / message / schedule on behalf of dependents.
  - Co-guardian access for a second adult.
- Defer to Phase 2: temporary caregiver access, adolescent-privacy transitions, custody-conflict workflows, granular per-delegate permissions.
- This requires explicit roadmap and budget tradeoff — likely deferring something else from Phase 1.

**Follow-up actions:**
- [ ] Confirm decision with product owner; identify the Phase 1 scope item to defer if any.
- [ ] Legal scopes the minimal-viable family-account model for guardianship verification.

---

## 8. Wearable / device data ingestion and provider liability

**Personas involved:** Chronic Condition Manager (Linda), Primary Care Physician (Dr. Alvarez), Specialist (Dr. Okonkwo)

**Conflict:**
- Linda wants her CGM, BP cuff, and Apple Watch data visible in the portal and to her providers.
- Dr. Alvarez is cautious; wants provenance labeling on every external data point and is concerned about implied liability to monitor continuous streams.
- Dr. Okonkwo is open in principle and would value device-manufacturer interrogation data (pacemaker/ICD), but treats it as longer-term.

**Proposed resolution:**
- **Phase 1:** patient-facing ingestion only. Patient can connect Apple HealthKit / Google Health Connect; data is visible to the patient in trend views; data is NOT pushed into the provider's chart by default.
- **Phase 2:** opt-in provider review with a clearly defined review-expectation policy:
  - Provider opts in per patient per data type.
  - Data is summarized (not raw streams); provenance labeled.
  - System-generated alerts only for clinically meaningful thresholds defined per condition (e.g., CHF weight gain).
  - Policy artifact (drafted with legal + clinical) explicitly states the provider is NOT expected to review continuous data outside of scheduled visits or triggered alerts.
- **CGM, pacemaker/ICD vendor integrations:** out of scope for Phase 1; Phase 2+ depending on vendor agreements.

**Follow-up actions:**
- [ ] Draft the provider-review-expectation policy with legal + clinical leadership.
- [ ] Define which conditions get system-generated alerts and their thresholds.
- [ ] Identify vendor integration priorities for Phase 2+.

---

## 9. Specialty-customizable UI vs. unified provider experience

**Personas involved:** Primary Care Physician (Dr. Alvarez), Specialist (Dr. Okonkwo)

**Conflict:**
- Dr. Alvarez wants a primary-care-optimized workflow (broad scope, panel-level views, care gaps).
- Dr. Okonkwo wants specialty-specific surfaces (cardiology-relevant data, procedure workflows) and explicitly does not want to be "retrofit from a PCP design."
- Building two separate apps is cost-prohibitive and creates training fragmentation.

**Proposed resolution:**
- **One application, role- and specialty-configurable.** Specialty configuration drives:
  - Patient-summary content and layout (`F-PCP-07` and `F-SP-05` share a framework).
  - Default chart-review surfaces.
  - Available workflows (e.g., procedure pre-op checklist only enabled for procedural specialties).
- Configuration owned by clinical informatics, not individual providers; new specialties added via configuration, not new releases.
- Phase 1: PCP, cardiology, one additional high-volume specialty. Additional specialties added in subsequent releases.

**Follow-up actions:**
- [ ] Architecture decision: build a configurable summary/chart framework, not hard-coded views.
- [ ] Clinical informatics identifies the Phase 1 third specialty and the config-ownership model.

---

## 10. Mobile experience — one app or two

**Personas involved:** Busy Parent (Marcus), Tech-Limited Senior (Eleanor), Primary Care Physician (Dr. Alvarez), Specialist (Dr. Okonkwo)

**Conflict:**
- Marcus and Eleanor expect a patient-facing native mobile app with full feature parity.
- Dr. Alvarez and Dr. Okonkwo want mobile chart review and after-hours messaging, but their needs are read-heavy and different in shape (Epic Haiku exists for that).
- Brief specifies mobile patient app with full feature parity; provider mobile is implicit.

**Proposed resolution:**
- **Two distinct mobile experiences:**
  - **Patient app** (iOS + Android native, full feature parity per brief).
  - **Provider mobile access** delivered primarily via existing Epic Haiku integration; the portal adds messaging notification and a thin "patient at a glance" mobile view. Avoid building a parallel provider mobile app in Phase 1.
- Re-evaluate provider native mobile in Phase 3 if Haiku integration proves insufficient.

**Follow-up actions:**
- [ ] Confirm Haiku integration scope with EHR / integration team.
- [ ] Define the thin provider mobile surface scope for Phase 1.

---

## 11. Authentication friction vs. security posture

**Personas involved:** Tech-Limited Senior (Eleanor), Busy Parent (Marcus), all providers

**Conflict:**
- Eleanor cannot get past CAPTCHA and complex MFA flows; wants long sessions and biometric login.
- Marcus wants secure but low-friction daily use; biometric strongly preferred.
- HIPAA security review board will demand MFA for PHI access; identity-proofing is required at registration.
- Provider workflows on shared workstations need fast resume + auto-logout (`NF-SP-02`) — different requirements again.

**Proposed resolution:**
- **Patient authentication:**
  - One-time identity proofing at registration (per HIPAA-acceptable methods; could leverage existing in-clinic proofing).
  - Daily use: biometric (Face ID / Touch ID / Android equivalent) on registered device + device trust.
  - Step-up authentication required for: first use on a new device, accessing sensitive categories (e.g., adolescent records, financial data), proxy access changes.
  - **No CAPTCHA in normal flows.** Bot protection via device-trust, rate limiting, and risk-based signals instead.
- **Provider authentication on shared workstations:** SSO with auto-logout on inactivity; tap-to-resume with badge or biometric on persisted session.

**Follow-up actions:**
- [ ] Security review board reviews and approves the proposed patient-auth model.
- [ ] Confirm device-trust framework and risk-based-auth tooling.

---

## 12. Patient consent and pharmacy fill visibility

**Personas involved:** Primary Care Physician (Dr. Alvarez), all patient personas (implicitly)

**Conflict:**
- Dr. Alvarez wants visibility into whether patients are actually picking up prescriptions (`F-PCP-10`) for genuine medication reconciliation.
- No patient persona explicitly objected, but this is sensitive data and patients may not realize providers see it.
- Some states treat pharmacy data as having heightened privacy protections.

**Proposed resolution:**
- Pharmacy fill data is surfaced to providers as part of the medication-reconciliation workflow, with **clear disclosure to patients** in the privacy notice and during portal onboarding ("Your care team can see whether your prescriptions are being filled, to help coordinate your care.")
- Patient has a **right-to-restrict** workflow if state law or personal preference requires it; restriction state is itself visible to providers ("patient has restricted pharmacy fill sharing").
- Surescripts data already flows to many EHRs today; this aligns with existing practice rather than introducing new disclosure.

**Follow-up actions:**
- [ ] Legal reviews state-by-state heightened-protection requirements (e.g., controlled substances, mental-health-related meds).
- [ ] Privacy team drafts patient-facing disclosure language.

---

## 13. Release cadence and UI stability

**Personas involved:** Tech-Limited Senior (Eleanor), provider personas (implicit), product/engineering (implicit)

**Conflict:**
- Eleanor experiences UI changes as distressing and wants UI stability with advance notice.
- Modern product development assumes rapid iteration to address bugs and capture learnings.
- Providers will also resent surprise UI changes during clinic hours.

**Proposed resolution:**
- **Release-communication policy:**
  - Visual / navigation changes batched and previewed with at least 2 weeks' notice via in-app banner, email summary, and (for the 70+ cohort) printed materials at clinic check-in.
  - Bug fixes and back-end changes deploy continuously without notice.
  - Major UI updates ship with an opt-in "preview" period followed by mandatory adoption after a defined window.
- **No deploys during clinic hours** for changes that touch provider-facing surfaces (mirror of `NF-PCP-02`).
- "What's new" surface in-app, dismissible, with link to short video / written walkthrough.

**Follow-up actions:**
- [ ] Define the release-communication SOP with engineering, product, and clinic operations.
- [ ] Establish change-advisory process for provider-facing changes.

---

## 14. Care-plan ownership and editorship

**Personas involved:** Chronic Condition Manager (Linda), Primary Care Physician (Dr. Alvarez), Specialist (Dr. Okonkwo)

**Conflict:**
- Linda wants a single coordinated care plan visible across all providers.
- Dr. Alvarez and Dr. Okonkwo both want to participate in care planning but have different scopes (whole-patient vs. condition-specific).
- Multiple specialists may have overlapping interest (e.g., cardiology + endocrinology for a diabetic with CAD).
- Editorship conflicts (who is the source of truth?) are real and not solved by software alone.

**Proposed resolution:**
- **Shared care-plan data model** with explicit roles:
  - **PCP** is the default care-plan owner / coordinator.
  - **Specialists** contribute condition-specific sections that are clearly attributed and editable only by that specialist (or their delegated team).
  - **Patient** has a view-mostly experience with the ability to log relevant data, add annotations, and ask questions that route to the appropriate section owner.
- Care plan is versioned with full edit history.
- Conflicting recommendations (e.g., conflicting med changes) trigger a **coordination alert** to all section owners — no silent overwrites.
- When no PCP is identified for a patient, ownership falls to the most-active specialist by default, with explicit re-assignment workflow.

**Follow-up actions:**
- [ ] Clinical leadership confirms the ownership / editorship model.
- [ ] Design coordination-alert workflow.
- [ ] Define data model for plan sections, attribution, and version history.

---

## 15. Trainee / teaching workflows — persona scope

**Personas involved:** Specialist (Dr. Okonkwo) raised; not in original product brief

**Conflict:**
- Dr. Okonkwo flagged that fellows / residents need supervised access — an entire persona currently missing from the brief.
- Including trainees expands scope (supervision model, audit, attending sign-off workflows).
- Excluding them leaves academic-affiliated practices with a workflow gap.

**Proposed resolution:**
- **Treat trainee workflow as a Phase 3 add-on** rather than expanding Phase 1 scope. Phase 1 ships with trainees using attending credentials (current state) and a clear note in release docs that supervised-access workflows are coming.
- Run a brief discovery effort in parallel with Phase 1 to scope the trainee persona properly for Phase 3 planning.
- If an academic-affiliation strategic partner is identified earlier, revisit prioritization.

**Follow-up actions:**
- [ ] Add trainee discovery to Phase 1 backlog (parallel research track).
- [ ] Get product-owner decision on scope expansion.

---

## 16. Cross-system interop scope

**Personas involved:** Chronic Condition Manager (Linda), Specialist (Dr. Okonkwo)

**Conflict:**
- Linda spans two health systems; her "unified view" need (`F-CCM-01`) implies cross-system data aggregation.
- Dr. Okonkwo's outside-records pain (`F-SP-11`) implies cross-system ingestion too.
- The brief is scoped to our health system + Epic; cross-system interop is significantly larger.

**Proposed resolution:**
- **Phase 1 scope: within-system unified view only.** Set this expectation explicitly with patients (visible labeling: "Records from [Our System] providers").
- **Phase 1 add:** Carequality / eHealth Exchange connection for read-only patient summary documents (low cost relative to value).
- **Phase 2+:** structured outside-records ingestion (labs, imaging, op notes) prioritized by referral volume from top partner systems.
- Be explicit in patient-facing UX about what is and isn't in scope to avoid trust damage.

**Follow-up actions:**
- [ ] Confirm Carequality connection feasibility with EHR / integration team.
- [ ] Identify top 3 external referrer systems for Phase 2 ingestion prioritization.
- [ ] Design "scope of records" disclosure UX.

---

## 17. Medication coordination across providers

**Personas involved:** Chronic Condition Manager (Linda), Primary Care Physician (Dr. Alvarez), Specialist (Dr. Okonkwo)

**Conflict:**
- Linda is frustrated by inconsistent med information across providers.
- Dr. Alvarez wants pharmacy fill data for real reconciliation (`F-PCP-10`).
- Dr. Okonkwo wants a "med ownership" flag so PCPs don't change his cardiac meds without notification (`F-SP-15`).
- These are three facets of one underlying problem: medication coordination.

**Proposed resolution:**
- Treat as a **single "Medication Coordination" capability** in the PRD, with three components:
  1. **Authoritative active med list** sourced from EHR + Surescripts fill data, with patient self-report layered visibly on top.
  2. **Ownership / attribution per med** — provider who initiated, last-updated-by, with a soft "primary owner" flag for high-risk classes (cardiac, anticoag, controlled substances).
  3. **Change notification** — when any provider modifies a flagged med, the owner is notified; patient sees a unified change history.
- Patient view shows current meds + recent changes + who made each change.

**Follow-up actions:**
- [ ] Define the med classes that get ownership flags and notification rules with clinical leadership.
- [ ] Confirm Epic schema supports ownership attribution; design alternative if not.
- [ ] Design the patient-facing med-change history view.

---

## Open items requiring leadership decisions

A short list of items from above that need explicit decisions before Phase 2 synthesis can lock requirements:

- [ ] Lab-result carve-out categories (Conflict 1)
- [ ] Async-messaging billing model and nurse-triage staffing commitment (Conflict 2)
- [ ] Org AI-governance policy ownership and timeline (Conflict 4)
- [ ] Phone-call-reduction metric scoping (Conflict 6)
- [ ] Family-account roadmap pull-forward and the Phase 1 scope item to defer (Conflict 7)
- [ ] Wearable-data provider-review-expectation policy (Conflict 8)
- [ ] Trainee persona inclusion / phasing (Conflict 15)
- [ ] Cross-system interop scope and phasing (Conflict 16)
