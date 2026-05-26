# Requirements Extract — Specialist

**Source:** [interview-notes-specialist.md](interview-notes-specialist.md)
**Stakeholder:** Dr. R. Okonkwo, MD (provider persona — Specialist, Cardiology / Interventional)
**Extracted by:** M. Mettler
**Date:** May 19, 2026

---

## Functional Requirements

### Must-Have

| ID | Requirement | Source | Notes / Clarification |
|---|---|---|---|
| F-SP-01 | Intelligent referral intake — system validates required information before referral hits specialist queue; auto-requests missing pieces from referring provider | Dr. Okonkwo — biggest pain | Define "required information" per specialty. |
| F-SP-02 | Structured referral with required fields: reason for consult / clinical question, recent diagnostics (ECG, echo for cards), meds, problem list, prior workup | Dr. Okonkwo | Specialty-configurable required-fields. |
| F-SP-03 | Referral triage queue with urgency classification (configurable rules + escalation to physician for ambiguous cases) | Dr. Okonkwo — nurse triages, ~5/wk escalated | |
| F-SP-04 | Consult-note loopback to referring provider with delivery confirmation; works for in-system AND outside (non-Epic) referrers | Dr. Okonkwo — "fax, no idea if read" | Cross-system / fax-replacement scope. |
| F-SP-05 | Specialty-configurable "patient at a glance" — cardiology view ≠ generic view (recent imaging, cardiac labs trended, current cardiac meds w/ dose changes, prior interventions, vitals trends) | Dr. Okonkwo | Cross-coordinate w/ F-PCP-07 — same surface, different config. |
| F-SP-06 | Provider-to-provider messaging — separate queue from patient inbox, with read receipts and distinct SLA | Dr. Okonkwo — matches Dr. Alvarez | |
| F-SP-07 | Pre-op patient checklist (fasting, meds to hold, arrival time, what to bring) — patient confirms in portal; un-confirmed flag at 24 hrs | Dr. Okonkwo — anticoag-hold is critical | Patient-safety implications. |
| F-SP-08 | Procedure-team nurse routing — post-procedure patient messages route to procedure nurse FIRST, not directly to specialist | Dr. Okonkwo — high message volume first 72 hrs | Routing rule + workflow. |
| F-SP-09 | Mobile / handheld view-only chart access for between-cases and after-hours use | Dr. Okonkwo — rarely at desk | Parity with Epic Haiku capability. |
| F-SP-10 | Fast resume / auto-logout for shared / non-owned workstations | Dr. Okonkwo — "workstation I don't own" | Security + UX tension. |

### Should-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| F-SP-11 | Outside / non-Epic records ingestion (imaging, prior op notes, outside labs) — eliminate CD-ROM and fax workflows | Dr. Okonkwo — "patients bring CD-ROMs" | Interop scope — Carequality, eHealth Exchange, DICOM portal? |
| F-SP-12 | Pre-authorization status visible in specialist patient view | Dr. Okonkwo — gets pulled into peer-to-peer | Payer integration dependency. |
| F-SP-13 | Auto-pushed condition-specific patient education on diagnosis (e.g., AFib module triggered by AFib dx code) | Dr. Okonkwo | Content library + ICD/dx-trigger engine. |
| F-SP-14 | Structured consult-back template ("assessment + plan + what I changed + what PCP should do") | Dr. Okonkwo | Documentation template. |
| F-SP-15 | "Medication ownership" flag on cardiac meds (or extensible per specialty) to coordinate med changes across providers | Dr. Okonkwo — PCPs change his meds w/o telling him | Cross-provider workflow. |
| F-SP-16 | Specialty-specific patient check-in workflows (e.g., CHF daily-weight log w/ alert >2 lb/day or >5 lb/wk → nurse, not physician) | Dr. Okonkwo | Configurable alert thresholds; routing to non-physician role. |
| F-SP-17 | Shared care plan: co-editable by PCP + specialist(s), patient-visible read-mostly with annotation + question capability | Dr. Okonkwo | Cross-cuts every persona. |
| F-SP-18 | Specialty outcomes dashboards (cardiology MVP: 30/60/90-day readmits, post-PCI complication rates, AFib control, time-in-therapeutic-range for anticoag) | Dr. Okonkwo | Analytics dependency. |
| F-SP-19 | Trainee / fellow / resident supervised access mode | Dr. Okonkwo — flagged unprompted | **New persona surface** — not currently in product brief. |
| F-SP-20 | "Redirect to PCP" easy action for off-scope patient messages | Dr. Okonkwo — "my knee hurts" | Routing + patient-comms template. |

### Nice-to-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| F-SP-21 | Templated post-procedure check-ins (day 1 / 3 / 7 / 14) | Dr. Okonkwo | |
| F-SP-22 | Device-manufacturer integration for cardiac devices (pacemaker / ICD interrogation data) | Dr. Okonkwo — "you'd be a hero" | Long-term; multiple vendors (Medtronic, Abbott, Boston Scientific). |
| F-SP-23 | Care-plan goal tracking (target BP, LDL, weight, EF) w/ progress visualization | Dr. Okonkwo | |

---

## Non-Functional Requirements

### Must-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| NF-SP-01 | Patient-safety NFRs around pre-op checklist (e.g., anticoagulation hold) — system must alert if not confirmed by procedure − 24 hrs | Dr. Okonkwo | Patient-safety classification. |
| NF-SP-02 | Fast session resume between procedures (target: < a few seconds to chart) + auto-logout on inactivity for shared workstations | Dr. Okonkwo | Cross-NFR-PCP-01. |
| NF-SP-03 | Performance reliability on clinic days equal to PCP (zero unplanned downtime, 99.9% uptime minimum) | Dr. Okonkwo — agrees w/ Dr. Alvarez | |
| NF-SP-04 | Mobile parity: secure view-only access from phone, biometric login, no PHI cached locally beyond session | Dr. Okonkwo | |

### Should-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| NF-SP-05 | Consult-note delivery confirmation tracked and surfaced — system tracks whether referring provider opened / acknowledged | Dr. Okonkwo | Audit + workflow. |
| NF-SP-06 | Trainee actions require attending sign-off where applicable; full audit trail | Dr. Okonkwo | Compliance / teaching-hospital. |

---

## Business Requirements

| ID | Requirement | Source | Priority | Notes |
|---|---|---|---|---|
| B-SP-01 | Reduce referral-to-seen lag (currently 6 weeks new, 5 days urgent) | Dr. Okonkwo | Should | Operational KPI. |
| B-SP-02 | Reduce redundant referrals and duplicate workups via better coordination | Dr. Okonkwo | Should | Maps to "care coordination" value in brief. |
| B-SP-03 | Specialty-customizable portal experience — not retrofitted from PCP design | Dr. Okonkwo | Must | Architectural / product-strategy implication. |
| B-SP-04 | Add trainee / teaching workflow as scoped persona for academic-affiliated practices | Dr. Okonkwo | Should | Persona-scope expansion. |

---

## Constraints & Dependencies

- **D-SP-01** — Outside-records ingestion depends on interop partner selection (Carequality, eHealth Exchange, direct HIE connections). Strategic decision required before design.
- **D-SP-02** — Pre-auth status visibility depends on payer integration (CoverMyMeds, payer portals). Coverage varies by payer.
- **D-SP-03** — Specialty-configurable summary views depend on a flexible data-presentation framework (avoid hard-coded layouts).
- **D-SP-04** — Device-manufacturer integration depends on per-vendor agreements; each vendor has own API + data model.
- **D-SP-05** — Procedure-team-nurse routing depends on org staffing model — is there a defined procedure-team nurse role in all practices?
- **D-SP-06** — Trainee workflows depend on academic-affiliation status of practice and credentialing system integration.
- **D-SP-07** — Med-ownership flag depends on Epic schema flexibility — feasibility unknown.
- **D-SP-08** — Auto-pushed dx-triggered education depends on a maintained education content library + governance of triggers.

---

## Ambiguities & Open Questions

- **A-SP-01** — Specialty-configurable summary view: how many specialties supported at launch? Configuration owned by IT, clinical informatics, or specialty lead?
- **A-SP-02** — Pre-op checklist non-confirmation: who is alerted (scheduler, nurse, both)? What's the fallback workflow?
- **A-SP-03** — Procedure-team-nurse routing: applies only to interventional specialties or broader? Different per specialty?
- **A-SP-04** — Trainee access model: scope of supervision required varies by training stage (resident vs. fellow vs. attending-supervised) — needs clinical-education input.
- **A-SP-05** — Med-ownership flag: who can override? PCP or specialist? Conflict workflow undefined.
- **A-SP-06** — Outside-records ingestion: how much normalization is done (e.g., LOINC mapping for labs) vs. presented as-is?
- **A-SP-07** — Care-plan ownership when multiple specialists involved — who is editor of record?
- **A-SP-08** — Trainee workflow inclusion may require board-level decision (academic strategy).

---

## Cross-Persona Conflict Flags

- 🔁 Dr. Okonkwo wants specialty-customizable surfaces ↔ Dr. Alvarez wants PCP-focused workflow — confirms need for **role/specialty-configurable UI framework**, not parallel apps.
- 🔁 Shared care plan: editable by PCP + specialist + visible to patient — all 5 personas mention pieces of this. Strong cross-persona signal but coordination complexity is high.
- 🔁 Med-ownership flag (Dr. Okonkwo) ↔ Dr. Alvarez's pharmacy-fill visibility (F-PCP-10) — both target the same root problem (med reconciliation); unify into a med-coordination capability.
- 🔁 Mobile view-only access (Dr. Okonkwo, Dr. Alvarez) ↔ patient-facing mobile native app (Marcus) — confirm we need TWO mobile experiences (provider vs. patient) or one app w/ role-based mode.
- 🔁 Trainee persona introduced here — not in original product brief — needs scope decision before Phase 2 synthesis.
