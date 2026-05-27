---
title: "Sensitive-category data gated through proxy paths with elevated controls / re-consent"
parent_epic: "documentation (output)/epics/epic-02-family-accounts-proxy-lifecycle-audit-log.md"
summary: "Proxy access to sensitive-category data (e.g., behavioral health, reproductive, SUD where in scope) requires explicit elevated controls / re-consent per `F-095` / `NF-038`; default proxy grants do NOT inherit sensitive-category access."
owner: "Identity & Access Platform Team — Family & Proxy squad"
priority: "P0"
sprint: "Family/Proxy Sprint 5"
story_points: 8
personas:
  - "Linda R. — Chronic Condition Manager (sensitive-category sharing context, UC-08)"
  - "Eleanor W. — delegator scenario"
  - "All patients — universal default-deny on sensitive categories through proxy"
acceptance_criteria:
  - "Default proxy grant does NOT include sensitive-category access (PRD §5.4 `NF-038`; §4.1 `F-095`)"
  - "Sensitive-category access through proxy requires explicit elevated controls / re-consent (PRD §5.4 `NF-038`; §8 R-SEC-01)"
  - "42 CFR Part 2 segmentation honored where SUD is in scope (PRD §5.9 `NF-075`)"
  - "Every sensitive-category access through proxy is logged and surfaced in patient-visible audit within 5 min (PRD §13.1 F-003; §5.4 `NF-032`)"
  - "Zero confirmed sensitive-category sharing violations (PRD §7.4)"
dependencies:
  - "Privacy, Sharing & Consent epic — sensitive-category classifier + `F-095` controls"
  - "Story 02 (grant)"
  - "Story 04 (patient-visible audit log)"
  - "Adolescent-privacy state decision for `F-006` if in scope (PRD §10 decision 17; `A-007`)"
tasks:
  - "Integrate sensitive-category classifier into proxy-access enforcement layer"
  - "Implement default-deny on sensitive categories for new + existing proxy grants"
  - "Implement re-consent / elevated-control flow scoped per category"
  - "Emit sensitive-category-access audit events with the sensitive-flag"
  - "Add anomaly alert on sensitive-category-through-proxy events"
  - "Privacy Officer + Legal sign-off; tabletop on re-consent UX"
  - "Penetration test focused on IDOR / category-bypass through proxy"
links:
  - "context (ingestion)/prd.md"
  - "documentation (output)/epics/epic-02-family-accounts-proxy-lifecycle-audit-log.md"
---

> **Author reminder:** Every story MUST link to its parent epic via `parent_epic` and cite the originating PRD section (e.g., `(PRD §<section>)`) when establishing acceptance criteria, NFRs, and telemetry. Stories without epic linkage and PRD citations should not be accepted into a sprint.

## User Story

**Trigger scenario:** Linda has a mental-health diagnosis and uses `F-095` to set behavioral-health notes as not visible to her primary-care team without re-consent. Independently, she has granted her spouse a general proxy. The proxy must NOT silently inherit access to her behavioral-health notes — and the policy must hold for every patient with any sensitive category, not just Linda (PRD §3.2 UC-08; §5.4 `NF-038`).

As a **patient**, I can **trust that my proxies do not inherit access to sensitive-category data unless I explicitly grant elevated controls or re-consent** so that **a general-purpose caregiver grant never silently exposes my behavioral-health, reproductive, or other sensitive records**.

## Acceptance Criteria (Gherkin-style)

| # | Scenario | Given | When | Then | PRD Source |
|---|----------|-------|------|------|------------|
| 1 | Default-deny on sensitive categories | A patient with sensitive-category data and an active general proxy grant | The delegate attempts to view sensitive-category records | Access is denied; a non-PHI generic "not authorized" message is shown; the attempt is logged | (PRD §5.4 `NF-038`; §4.1 `F-095`) |
| 2 | Elevated control / re-consent enables access | A delegator who chooses to grant sensitive-category access | They complete the re-consent / elevated-control flow with category scope | The delegate gains scoped access to only the chosen categories; scope and re-consent evidence audited | (PRD §5.4 `NF-038`; §8 R-SEC-01) |
| 3 | 42 CFR Part 2 segmentation | A patient with SUD records (if in scope) | A proxy attempts access | Part-2-segmented data is gated independently per regulation, regardless of general re-consent | (PRD §5.9 `NF-075`) |
| 4 | Audit visibility for sensitive access | Any sensitive-category access through proxy | The patient opens the audit log | The entry is visible within 5 min, flagged as sensitive-category | (PRD §13.1 F-003; §5.4 `NF-032`) |
| 5 | Anomaly alert | A burst of sensitive-category-through-proxy access events | The detector evaluates | An anomaly alert is raised to the audit-review workflow within SLA | (PRD §5.9 `NF-079`; §7.4) |
| 6 | Zero violation gate | All test + production data | Pre-launch validation runs | Zero confirmed sensitive-category sharing violations are required to GA | (PRD §7.4) |

## Non-Functional / Compliance Notes

- Performance: classifier evaluation in-line with access check; per-request overhead ≤ 50ms p95 to preserve `NF-028`.
- Security: server-side enforcement is authoritative; client cannot suppress the gate; pen test for category-bypass (PRD §5.4 `NF-039d`; §8 R-SEC-01).
- Privacy / Data handling: re-consent evidence stored per policy; OCR-compliant telemetry; no PHI in client-side analytics (PRD §5.10 `NF-080a`, `NF-080b`).
- Regulatory: HIPAA + state matrix (PRD §6.5; §5.9 `NF-076`); 42 CFR Part 2 if applicable (PRD §5.9 `NF-075`); information-blocking — deny path must be intentional & visible to patient (PRD §5.9 `NF-074`).
- Accessibility / UX: re-consent flow WCAG 2.1 AA; plain-language explanation of what is being shared (PRD §5.1 `NF-010`/`NF-017`).

## Telemetry and Reporting

- Events emitted: `sensitive.access.denied`, `sensitive.access.granted_via_reconsent`, `sensitive.proxy.access.recorded`, with non-PHI correlation IDs (category flag, not the data itself).
- Metrics tracked: sensitive-category access through proxy (count, alert on anomaly), re-consent completion rate, denial rate, classifier-eval latency p95.
- Dashboards / alerts: anomaly alert on sensitive-through-proxy spikes (`NF-079`); alert on classifier latency regression.
- Audit logging: every sensitive-category access (allow / deny / re-consent event) in immutable audit ≥ 6yr retention, with sensitive-flag (PRD §5.4 `NF-032`, `NF-038`).

## Dependencies

- Upstream services: sensitive-category classifier (Privacy epic), audit store, OIDC IdP, every domain service exposing PHI through proxy.
- Data sources / documents: category taxonomy + state-matrix decisions (`A-006`, decisions 8/16/17).
- Teams / sign-offs: Privacy Officer, Legal, CISO, Clinical Informatics (taxonomy), Pen-test partner.
- Blocking stories or epics: Story 02 (grant); Story 04 (audit visibility); Privacy, Sharing & Consent epic (classifier + `F-095`).

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| Classifier misses a sensitive category (under-classification) | Med | High | Conservative default-deny on ambiguous data; periodic taxonomy review with Clinical Informatics + Privacy; red-team test | Privacy + Clinical Informatics |
| Re-consent flow burdens patients into accidental over-grant | Med | High | Scope-per-category UI; plain-language summary; default opt-out per category; usability testing | Design + Privacy |
| 42 CFR Part 2 misapplication if SUD in scope | Low | High | Explicit Part-2 gate independent of general re-consent; Legal sign-off | Legal + Privacy |
| Performance regression from in-line classifier | Med | Med | Cache + async pre-compute; latency SLO + alarm | Identity Platform + SRE |

## Rollout / Validation Checklist

- [ ] Unit tests added and passing
- [ ] Integration tests cover acceptance criteria scenarios
- [ ] Manual QA spot-check against source documents completed
- [ ] Telemetry verified in staging dashboard
- [ ] Security / compliance review signed off (Privacy, Legal, CISO; pen test on category-bypass)
- [ ] Feature flag / rollout plan defined (shadow-mode classifier first; enforcement second)
- [ ] Documentation updated (runbook, patient help, helpdesk script)
- [ ] Parent epic acceptance criteria still satisfied

## Source References

- Parent epic: [epic-02-family-accounts-proxy-lifecycle-audit-log.md](../epic-02-family-accounts-proxy-lifecycle-audit-log.md)
- Source PRD: [context (ingestion)/prd.md](../../../context%20(ingestion)/prd.md)
- PRD sections cited: §3.1 Linda, §3.2 UC-08, §4.1 F-095, §5.1 `NF-010`/`NF-017`, §5.2 `NF-028`, §5.4 `NF-032`/`NF-038`/`NF-039d`, §5.9 `NF-074`/`NF-075`/`NF-076`/`NF-079`, §5.10 `NF-080a`/`NF-080b`, §6.5, §7.4, §8 R-SEC-01, §10 decisions 8/16/17, §13.1 F-003.
- Design / architecture docs: PRD §6.2 (Consent / Sharing + Audit / Logging services).

---

**Template reminders:**
- Replace every `<fill me>` before review.
- Confirm `parent_epic` points to a real epic file before opening the story for review.
- Each acceptance criterion, NFR, and telemetry metric must reference its PRD section in the `PRD Source` column or inline citation.
