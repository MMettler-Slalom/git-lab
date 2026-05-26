# Requirements Extract — Primary Care Physician

**Source:** [interview-notes-primary-care-physician.md](interview-notes-primary-care-physician.md)
**Stakeholder:** Dr. K. Alvarez, MD (provider persona — Primary Care Physician)
**Extracted by:** M. Mettler
**Date:** May 19, 2026

---

## Functional Requirements

### Must-Have

| ID | Requirement | Source | Notes / Clarification |
|---|---|---|---|
| F-PCP-01 | Message routing rules — administrative, billing, scheduling, and form-request messages must NOT reach physician inbox | Dr. Alvarez — biggest source of pain | Requires intake taxonomy + routing config. |
| F-PCP-02 | Physician inbox triage view — sort/filter by urgency, type, and patient | Dr. Alvarez | |
| F-PCP-03 | AI-assisted message drafting — physician reviews + signs every outbound reply (no autosend) | Dr. Alvarez — "will quit if you ship auto-reply" | ⚠️ HARD CONSTRAINT: AI may draft, never send autonomously. |
| F-PCP-04 | AI-assisted message summarization (collapsing long patient messages) and classification (urgency / topic) | Dr. Alvarez | Must show source content alongside summary. |
| F-PCP-05 | AI red-flag-symptom detection in patient messages (with provider override) | Dr. Alvarez | Clinical-safety validation required. |
| F-PCP-06 | Provider-to-provider messaging in a **separate** queue from patient inbox, with its own SLA | Dr. Alvarez | New surface; design effort. |
| F-PCP-07 | "Patient at a glance" summary view: problem list, active meds with recent changes flagged, last relevant vitals/labs, what-changed-since-last-visit, open orders, overdue care gaps | Dr. Alvarez — first 3–5 things she looks for | |
| F-PCP-08 | External / outside data source attribution and provenance visible in chart (e.g., wearable BP vs. validated cuff) | Dr. Alvarez — liability concern | Cross-cut w/ wearables roadmap. |
| F-PCP-09 | Refill workflow that supports standing-order delegation to MA with physician daily batch sign-off | Dr. Alvarez | EHR/Epic capability mapping. |
| F-PCP-10 | Pharmacy fill-data integration showing whether patient is actually picking up prescriptions | Dr. Alvarez — true med rec | Surescripts / pharmacy integration. |
| F-PCP-11 | EPCS / controlled-substance e-prescribing supported (current friction acceptable) | Dr. Alvarez | Regulatory mandate regardless. |
| F-PCP-12 | Telehealth one-click join + ability to text patient mid-visit ("turn on light") | Dr. Alvarez | |
| F-PCP-13 | Proactive outage / degraded-performance alerting BEFORE physician encounters it (banner in EHR + Teams) | Dr. Alvarez — "tell me at 7:55, not 8:01" | Cross-cut w/ ops/monitoring. |
| F-PCP-14 | Mobile / handheld access for view-only chart review and after-hours messaging | Inferred + cross-persona | Epic Haiku already exists; ensure portal parity. |

### Should-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| F-PCP-15 | Configurable message-triage routing per practice / MA staffing model | Dr. Alvarez — "fails when float MA is covering" | |
| F-PCP-16 | Coverage / handoff mode — vacation coverage receives scoped context, not raw inbox dump | Dr. Alvarez — "a disaster" | |
| F-PCP-17 | Auto-draft telehealth visit note from session | Dr. Alvarez — cross-coordinate w/ ambient-scribe initiative | Don't duplicate scribe project. |
| F-PCP-18 | Population-health dashboard: gaps in care, quality-metric performance, panel risk-stratification | Dr. Alvarez | |
| F-PCP-19 | Care-gap and quality alerts shown in dedicated review surface, NOT as in-visit popups | Dr. Alvarez — "hard no on interrupting popups" | UX constraint. |
| F-PCP-20 | Smart-phrase / dot-phrase parity with EHR (or integration so providers don't lose existing library) | Dr. Alvarez — "loves dot phrases" | |

### Nice-to-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| F-PCP-21 | Wearable / device data presented as summary stats with provenance, not raw streams | Dr. Alvarez — skeptical-but-open | Liability framing in NF-PCP. |
| F-PCP-22 | Inbox volume dashboard for physicians to monitor own load | Dr. Alvarez — implicit | |
| F-PCP-23 | Patient-message templates for common responses | Inferred | |

---

## Non-Functional Requirements

### Must-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| NF-PCP-01 | **Performance budget:** chart open < 2 sec, order screen < 1 sec, message open < 1 sec | Dr. Alvarez — explicit | Must be measured and enforced. |
| NF-PCP-02 | **Reliability:** zero unplanned downtime during clinic hours; meets brief's 99.9% uptime target as a minimum | Dr. Alvarez — "five min down = 30 min behind" | Aligns w/ brief. |
| NF-PCP-03 | All AI outputs must be reviewable, attributable, and auditable; AI must not send patient-facing messages without provider signoff | Dr. Alvarez — strongest stated requirement | Org AI-governance policy alignment. |
| NF-PCP-04 | AI suggestions must display source content / citations | Dr. Alvarez | |
| NF-PCP-05 | No in-visit interrupting popups for non-emergency alerts | Dr. Alvarez | UX policy. |
| NF-PCP-06 | Outage notification SLA: proactive alert to providers ≥ X minutes before scheduled / detected unavailability (X TBD) | Dr. Alvarez | Operational NFR. |

### Should-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| NF-PCP-07 | Liability-bounded scope on continuous device-data review — provider not assumed to be reviewing 24/7 streams; policy documented | Dr. Alvarez | Legal + clinical-leadership artifact required. |
| NF-PCP-08 | Session persistence across short context switches (between visits) | Inferred | |

---

## Business Requirements

| ID | Requirement | Source | Priority | Notes |
|---|---|---|---|---|
| B-PCP-01 | Cap or measurably reduce physician message-handling time (target ties to brief's "30% reduction in admin time") | Dr. Alvarez | Must | Already in brief; this interview validates. |
| B-PCP-02 | Asynchronous clinical messaging must have an associated billing / compensation model | Dr. Alvarez — "free labor" comment | Should | Revenue cycle dependency. |
| B-PCP-03 | Coordinate w/ separate ambient-scribe initiative — single AI surface for physician, not two competing tools | Dr. Alvarez | Should | Cross-program dependency. |
| B-PCP-04 | Provider advisory council — ongoing input throughout build | Researcher recommendation | Should | Org/process. |

---

## Constraints & Dependencies

- **D-PCP-01** — AI-drafting capability depends on org AI-governance policy (still being drafted?). Confirm policy owner and status.
- **D-PCP-02** — Pharmacy fill-data depends on Surescripts integration scope + data-rights agreement.
- **D-PCP-03** — Population-health metrics depend on EHR data warehouse / analytics layer.
- **D-PCP-04** — Coordination with ambient-scribe initiative — owner / governance unknown. ⚠️ Open.
- **D-PCP-05** — Asynchronous-messaging billing depends on payer rules and revenue-cycle workflow.
- **D-PCP-06** — Standing-order workflows depend on state scope-of-practice rules for MAs/RNs.
- **D-PCP-07** — Performance budgets (chart open <2s) depend on Epic API latency — may not be fully under our control.

---

## Ambiguities & Open Questions

- **A-PCP-01** — Where exactly is the line between "AI draft" and "AI autoreply"? E.g., is a templated form-response with no clinical content allowed to autosend?
- **A-PCP-02** — Definition of "red-flag symptom" detection: which conditions, which sensitivity/specificity thresholds, how to surface false positives?
- **A-PCP-03** — Scope of provider-to-provider messaging: same-system only, or cross-system / referring outside PCPs?
- **A-PCP-04** — Wearable-data review expectation policy: who owns drafting, who signs off, how is it communicated to patients?
- **A-PCP-05** — Outage-alert pre-notice window — what is operationally feasible (X minutes)?
- **A-PCP-06** — Coverage / handoff scope model — clinical only? Inbox-rules? Auto-decline of new patient initiations?
- **A-PCP-07** — Performance budget enforcement: who measures, who is accountable when missed?

---

## Cross-Persona Conflict Flags

- 🔁 Dr. Alvarez at message-volume breaking point ↔ patients (Marcus, Linda) want faster + more communication channels. **Reconciliation requires staffing/policy, not just product features.**
- 🔁 Dr. Alvarez wants AI drafting w/ human signoff ↔ patient expectation of fast response — set expectations on response times in product UX.
- 🔁 Lab-result review window (provider preference) ↔ Linda's request for instant release — needs result-type policy.
- 🔁 Pharmacy-fill visibility (provider) ↔ patient privacy / "right not to be tracked" — confirm patient consent model.
- 🔁 Wearable data ingestion (Linda wants) ↔ provider liability for review (Dr. Alvarez concerned) — policy reconciliation needed.
