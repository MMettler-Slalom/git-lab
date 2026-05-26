# Requirements Extract — Chronic Condition Manager

**Source:** [interview-notes-chronic-condition-manager.md](interview-notes-chronic-condition-manager.md)
**Stakeholder:** "Linda R." (patient persona — Chronic Condition Manager, 58, T2 diabetes + HTN)
**Extracted by:** M. Mettler
**Date:** May 19, 2026

> Prioritization uses MoSCoW-style buckets: **Must-Have / Should-Have / Nice-to-Have**. Priority reflects *this stakeholder's* perspective; final PRD priority will be set after cross-persona synthesis.

---

## Functional Requirements

### Must-Have

| ID | Requirement | Source | Notes / Clarification |
|---|---|---|---|
| F-CCM-01 | Unified view of patient health information across providers in the same system | Linda — "one place where every doctor sees the same thing I see" | ⚠️ AMBIGUOUS: scope of "every doctor" — Linda uses 2 different health systems. Cross-system interop is broader than Epic-only. Needs scope decision. |
| F-CCM-02 | Secure messaging with care team with delivery + read confirmation | Linda — lost-message story; "your nurse Sarah saw this at 2pm" | Must include audit trail showing delivery, viewed-by, and responder. |
| F-CCM-03 | Lab results visible to patient at the same time as provider | Linda — "I'm an adult, I can handle a number" | Conflict potential w/ provider workflow (Dr. Alvarez may want review-before-release for sensitive results). FLAG for policy. |
| F-CCM-04 | Lab results displayed with personal target ranges, trends over time, and "what changed since last time" summary | Linda — Excel screenshots workaround | Personal ranges must be settable by provider per patient. |
| F-CCM-05 | Prescription refill requests with proactive expiration / auth-renewal alerts | Linda — "ran out of metformin twice this year" | Alert both patient AND provider when refill auth nearing expiration. |
| F-CCM-06 | Appointment self-scheduling with real-time availability across providers | Linda — dreads calling endo office | |
| F-CCM-07 | Single view of all upcoming appointments across providers in same system | Linda — "manual Tetris" | |
| F-CCM-08 | Plain-language explanation alongside clinical lab values | Linda — "what does 6.8 mean for me" | NLP / templated content? Scope TBD. |

### Should-Have

| ID | Requirement | Source | Notes / Clarification |
|---|---|---|---|
| F-CCM-09 | Patient ability to annotate results / log context (e.g., "sick that week") | Linda | Determine whether annotations are visible to providers (likely yes). |
| F-CCM-10 | Smart medication reminders that suppress if dose already logged | Linda — "don't ping me at 8am if I already logged it" | Requires med-administration logging input from patient or device. |
| F-CCM-11 | Symptom triage tool (is-this-normal / call-doctor / ER) | Linda — currently googles side effects | ⚠️ AMBIGUOUS: clinical-decision-support liability. Needs clinical + legal review. |
| F-CCM-12 | Granular sharing controls — patient chooses which providers see which categories of data | Linda — mental health hx example | Major IA + privacy design implication. |
| F-CCM-13 | Proxy / delegated access — view + messaging rights, configurable per delegate | Linda — daughter (RN, out of state) | Tie-in w/ broader proxy model from other personas. |
| F-CCM-14 | Trend visualizations for self-logged data (BP, weight, glucose) with provider visibility toggle | Linda | |
| F-CCM-15 | Notification preferences per channel (push, email; explicit opt-out of SMS) | Linda — "scam texts" fear | |
| F-CCM-16 | Self-service appointment reschedule / cancel without phone call | Linda | |

### Nice-to-Have

| ID | Requirement | Source | Notes / Clarification |
|---|---|---|---|
| F-CCM-17 | Integration w/ Dexcom CGM data | Linda — wears one | ⚠️ Dependency: Dexcom API access + BAA. |
| F-CCM-18 | Integration w/ Apple HealthKit (BP cuff, Apple Watch) | Linda | |
| F-CCM-19 | Correlation insights — surface relationships between med changes and tracked metrics | Linda — BP med started in Feb | Likely v2+. May require ML; clinical validation needed. |
| F-CCM-20 | "What changed since last time" summary on lab results landing page | Linda | Could be templated, not necessarily AI-generated. |
| F-CCM-21 | Copay / cost estimate visible at time of appointment booking | Linda | Dependency on billing system integration. |

---

## Non-Functional Requirements

### Must-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| NF-CCM-01 | Accessibility: configurable text size, sufficient contrast | Linda — needs reading glasses, color-blind husband | Baseline WCAG 2.1 AA per reference brief. |
| NF-CCM-02 | Information must not rely on color alone for meaning (color-blindness) | Linda's husband example | WCAG 1.4.1. |
| NF-CCM-03 | Audit log of who accessed which records, viewable by patient | Linda — proxy access notifications | Aligns w/ HIPAA accounting-of-disclosures. |
| NF-CCM-04 | Message delivery + acknowledgement guarantees (no silent loss) | Linda — lost message March | NFR + functional confirmation UI. |

### Should-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| NF-CCM-05 | Transparency of AI-generated content — show source data, label AI-generated summaries | Linda — "I want to verify" | Aligns w/ likely org AI-governance policy. Cross-cut w/ provider personas. |
| NF-CCM-06 | Data export — patient ability to download own health data | Linda — keeps Google Doc copy today | Required for HIPAA right-of-access; also business value. |

---

## Business Requirements

| ID | Requirement | Source | Priority | Notes |
|---|---|---|---|---|
| B-CCM-01 | Reduce administrative burden Linda experiences as "the messenger" between providers | Linda — paper binder | Should | Maps to broader operational-efficiency goal in product brief. |
| B-CCM-02 | Support patient retention by reducing portal-abandonment friction | Linda abandoned old portal | Should | Adoption metric in brief (60% registration, 40% MAU). |

---

## Constraints & Dependencies

- **D-CCM-01** — Cross-system interop: Linda spans 2 health systems. Resolving "unified view" depends on external data ingestion (FHIR, HIE, Carequality?). Scope decision required.
- **D-CCM-02** — Dexcom CGM integration depends on vendor API + BAA.
- **D-CCM-03** — Apple HealthKit integration depends on iOS-only support (Android-equivalent: Google Health Connect — confirm parity strategy).
- **D-CCM-04** — Symptom triage feature depends on clinical-decision-support governance + medical-legal sign-off.
- **D-CCM-05** — Granular sharing (per-provider, per-category) depends on Epic / EHR data-segmentation capability — feasibility unknown.
- **D-CCM-06** — Cost estimate at booking depends on billing system / payer eligibility integration.

---

## Ambiguities & Open Questions

- **A-CCM-01** — Scope of "unified view": single health system only, or cross-system aggregation? Major scope driver.
- **A-CCM-02** — Lab-result release timing: immediate to patient vs. provider-review-window for sensitive results (e.g., oncology). Conflicts likely w/ provider preference. Needs cross-persona policy.
- **A-CCM-03** — Symptom triage: in-scope for v1, defer, or out-of-scope entirely? Liability material.
- **A-CCM-04** — Granular sharing UI complexity vs. usefulness — needs design exploration; may overwhelm less-savvy users.
- **A-CCM-05** — Provider visibility into patient-logged data: opt-in by patient, opt-in by provider, or both? Workflow + liability implications.
- **A-CCM-06** — AI summary / interpretation features: where on roadmap, and how labeled?
- **A-CCM-07** — Wearable / device data scope (CGM, BP, watch) — v1 inclusion is open question per product brief.

---

## Cross-Persona Conflict Flags

- 🔁 Lab-results-instant-release (Linda) ↔ provider-review-window (potential Dr. Alvarez preference) — reconcile in synthesis.
- 🔁 Push for AI-assisted insights (Linda wants trends) ↔ skepticism / liability concerns (providers) — reconcile in governance.
- 🔁 SMS opt-out (Linda) ↔ assumption that SMS is a default reminder channel — confirm channel strategy is fully patient-configurable.
