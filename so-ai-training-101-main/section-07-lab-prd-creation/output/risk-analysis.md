# Risk Analysis — HealthConnect Patient & Provider Portal

**Date:** May 26, 2026
**Author:** M. Mettler
**Sources:** [consolidated-requirements.md](consolidated-requirements.md), [requirements-extracts/requirements-conflicts-and-resolutions.md](requirements-extracts/requirements-conflicts-and-resolutions.md), [requirements-gap-analysis.md](requirements-gap-analysis.md), [market-analysis.md](market-analysis.md), per-persona interview notes, and the reference brief at [input/00-healthcare-portal-reference.md](../input/00-healthcare-portal-reference.md).

**Status:** Draft — input for Phase 5 refinement and PRD risk section.

> **Note on scope:** The reference brief identifies Epic MyChart as the underlying platform direction and the org as a large U.S. integrated delivery network. "Azure service dependency" risks below cover the *most likely* cloud target (Microsoft Azure given the Epic / Microsoft AI partnership), but should be revised if a different cloud is selected.

---

## Conventions

- **Likelihood:** High / Medium / Low — probability of occurrence over the Phase 1–3 program horizon.
- **Impact:** High / Medium / Low — severity if it materializes (combination of patient safety, regulatory, financial, reputational, schedule).
- **Risk score:** H/H, H/M, M/H = critical; H/L, M/M, L/H = elevated; M/L, L/M, L/L = routine.
- **Linked requirements / open questions** cross-reference the consolidated requirements doc.

---

## Table of Contents

- [1. Top Critical Risks (At-a-Glance)](#1-top-critical-risks-at-a-glance)
- [2. Technical Risks](#2-technical-risks)
- [3. Organizational Risks](#3-organizational-risks)
- [4. Regulatory & Compliance Risks](#4-regulatory--compliance-risks)
- [5. Data & Security Risks](#5-data--security-risks)
- [6. Vendor & Dependency Risks](#6-vendor--dependency-risks)
- [7. Timeline & Budget Risks](#7-timeline--budget-risks)
- [8. Risk → Requirement Coverage Gaps](#8-risk--requirement-coverage-gaps)
- [9. Executive Escalation List](#9-executive-escalation-list)

---

## 1. Top Critical Risks (At-a-Glance)

| Rank | ID | Risk | L | I | Owner candidate |
|---|---|---|---|---|---|
| 1 | R-ORG-01 | Nurse-triage and async-messaging staffing not funded before launch | H | H | Clinical operations leadership |
| 2 | R-REG-01 | HIPAA tracking-tech / third-party SDK exposure on PHI pages | H | H | Privacy Officer + Engineering |
| 3 | R-TECH-01 | Epic API latency / availability constrains performance SLOs | H | H | Integration + SRE |
| 4 | R-ORG-02 | Provider in-basket time *increases* despite AI features | M | H | Clinical informatics |
| 5 | R-SEC-01 | Sensitive-category data leakage via family / proxy access | M | H | Privacy + Product |
| 6 | R-REG-02 | Information-blocking exposure from over-conservative result holds | M | H | Compliance + Clinical |
| 7 | R-ORG-03 | Digital divide — 75+ and low-tech cohorts abandoned | M | H | Health equity + Product |
| 8 | R-TECH-02 | Patient-facing AI hallucination causing clinical harm | M | H | Clinical informatics + AI gov |
| 9 | R-VEN-01 | Epic platform changes / pricing shifts disrupt roadmap | M | H | Vendor mgmt |
| 10 | R-BUD-01 | Scope creep across 5 personas + ~90 gap requirements blows Phase 1 | H | M | Product + PMO |

---

## 2. Technical Risks

### Architecture & Integration

| ID | Risk | L | I | Rationale | Linked |
|---|---|---|---|---|---|
| R-TECH-01 | Epic / MyChart API latency or throttling prevents meeting performance SLOs (chart open <2s, message open <1s). | H | H | Epic API behavior is partly outside our control; brief lists Epic as core dependency. Documented industry pattern. | NF-020, NF-026–028, D-010, D-033 |
| R-TECH-02 | AI-generated patient-facing content (plain-language lab explanations, AI-drafted replies) produces clinically inaccurate or harmful output. | M | H | Even RAG-grounded generation has residual hallucination risk; patient liability higher than provider-facing AI. | F-014, F-016, F-022, NF-040, NF-041, NF-044 |
| R-TECH-03 | Specialty-configurable summary view (F-050) becomes a multi-year platform build rather than a feature, slipping Phase 1. | M | H | Configurable framework is an architectural bet; market analysis flags this as "platform investment, not feature." | F-050, B-015 |
| R-TECH-04 | Mobile feature parity (F-080) requires native dev capacity org doesn't have. | M | M | Native iOS + Android with parity is a large engineering commitment. | F-080, NF-015–016 |
| R-TECH-05 | FHIR R4 US Core conformance gaps surface late in Phase 1 (e.g., missing resources for adolescent privacy, sensitive categories). | M | M | US Core profiles don't fully cover all sensitive-category segmentation needs. | NF-089, F-095, NF-038 |
| R-TECH-06 | Integration sprawl (20+ vendors per market analysis) creates fragile point-to-point coupling. | M | M | Without an integration platform strategy, every new vendor compounds. | D-010–019, NF-039 |
| R-TECH-07 | Outside-records / DICOM ingestion (F-173, F-196) requires viewer with security implications not yet scoped. | M | M | Embedded DICOM viewers historically a vulnerability surface. | F-173, F-196, D-017 |
| R-TECH-08 | Event-driven architecture (webhooks, FHIR Subscriptions) not in place; polling won't scale. | M | M | Brief KPIs (MAU, message volume, no-show reduction) depend on timely notifications. | F-197, F-070, NF-025 |
| R-TECH-09 | Telehealth video quality SLOs (NF-029b) depend on vendor choice not yet made. | M | M | Per market analysis, vendor strategy unresolved. | NF-029b, A-037, D-040 |
| R-TECH-10 | Configurable message-routing engine (F-011) becomes complex per-practice workflow tool rivaling EHR functionality. | M | M | Per-practice configurability tends to scope-creep. | F-011, F-102 |

### Performance & Scalability

| ID | Risk | L | I | Rationale | Linked |
|---|---|---|---|---|---|
| R-TECH-11 | Concurrent-user sizing under-provisioned for open-enrollment / flu-season / outage-recovery spikes. | M | H | Healthcare portals routinely see 5–10x peak vs. baseline. | NF-029, NF-029e |
| R-TECH-12 | Push notification reliability (NF-025) fails silently for percentage of users, eroding trust. | M | M | iOS/Android backgrounding behavior unpredictable; APNs/FCM rate limits. | NF-025, F-070, F-019 |
| R-TECH-13 | LLM provider rate limits / token throttling slow message draft + summarization at peak. | M | M | Azure OpenAI / Anthropic capacity is a known constraint. | F-014, F-015, F-050 |
| R-TECH-14 | Audit log volume + 6-year retention storage costs exceed budget projections. | M | M | Every PHI access logged across millions of users compounds quickly. | NF-032, NF-052 |
| R-TECH-15 | Disaster recovery RTO/RPO not defined (A-042); recovery exercise reveals unacceptable data loss. | M | H | Common to discover only after first DR test or incident. | NF-029i, A-042 |
| R-TECH-16 | Feature-flag / kill-switch capability not in place across all critical capabilities; rollback requires deploy. | M | M | Slows incident response when AI features misbehave. | NF-029g, NF-029h |

### Operational / Observability

| ID | Risk | L | I | Rationale | Linked |
|---|---|---|---|---|---|
| R-TECH-17 | OCR-compliant telemetry retrofitted late, requiring rework of analytics pipeline. | M | M | Tracking-tech compliance is non-trivial when analytics are added after launch. | NF-080a, NF-080b |
| R-TECH-18 | Incident response runbooks not in place; first major outage handled ad hoc. | M | H | New platform = no muscle memory. | NF-029h |

---

## 3. Organizational Risks

### Adoption, Change Management, Resources

| ID | Risk | L | I | Rationale | Linked |
|---|---|---|---|---|---|
| R-ORG-01 | Nurse-triage chat (F-100), async messaging at scale, message-acknowledgement SLA (F-019) launched without funded clinical staffing — load lands on physicians or response degrades. | H | H | Conflict 2 already flagged this as a launch gate. Market analysis: portal messaging *increases* clinical staff needs, not decreases. | F-019, F-100, B-009, B-010, D-020 |
| R-ORG-02 | Provider in-basket time *increases* despite AI message-drafting (F-014), because draft edits + new patient-initiated message volume outpace time saved. | M | H | JAMA / AMA studies through 2025 show mixed results on inbox-time savings. | F-014, F-015, B-009 |
| R-ORG-03 | Tech-limited senior (75+) and accessibility-impaired cohorts effectively excluded; digital-divide commitment (B-006) fails. | M | H | Persistent industry pattern; brief explicitly raises equity. | F-090, F-191, F-210, NF-010–017, NF-088, B-006, B-007 |
| R-ORG-04 | Provider mobile experience (Haiku-mediated per F-081) leaves specialists frustrated; pressure mounts for native provider app mid-Phase 1. | M | M | Conflict 10 resolution may be tested if specialists experience friction. | F-081 |
| R-ORG-05 | "Phone-channel reduction" KPI (B-008, NF-070) silently incentivizes call-channel atrophy despite explicit guardrail. | M | H | Hardest organizational risk to enforce; market analysis confirms common failure mode. | NF-070, NF-071, B-008, A-017 |
| R-ORG-06 | Provider advisory council (B-012) doesn't form or doesn't meet meaningfully; provider needs drift between releases. | M | M | Common ambition that fails on follow-through. | B-012 |
| R-ORG-07 | Adolescent-privacy workflow (F-006) launches without clear clinical / legal / parent-facing communication; trust incident in first months. | M | H | Multi-state legal complexity + emotionally charged topic. | F-006, F-110, A-007, A-011 |
| R-ORG-08 | Family-account MVP (F-001) ships without divorce / split-custody / co-equal-parent handling; legal exposure + bad PR. | M | H | Open question A-006 still unresolved. | F-001, F-002, A-006 |
| R-ORG-09 | Provider champion / super-user program (NF-085) under-resourced; per-clinic rollout uneven. | M | M | Identified gap, no current owner. | NF-085, D-027 |
| R-ORG-10 | Patient + provider helpdesk staffing (NF-086) underestimated; launch-week call volume overwhelms tier-1. | M | H | Universal portal-launch pattern. | NF-086, D-026 |

### Stakeholder Alignment / Governance

| ID | Risk | L | I | Rationale | Linked |
|---|---|---|---|---|---|
| R-ORG-11 | AI-governance committee not yet formed; AI requirements (NF-040–045) blocked at compliance review. | H | M | Per market analysis, mature IDNs have governance; HealthConnect's status unknown. | NF-040–045, D-050 |
| R-ORG-12 | Ambient-scribe initiative (B-011) and portal AI scope conflict; providers see two different AI experiences. | M | M | Brief flags this as separate program with unclear coordination. | B-011 |
| R-ORG-13 | Health-equity stakeholder not engaged early; equity-stratified metrics (NF-072) designed without input. | M | M | Common late-engagement pattern. | NF-072, A-040 |
| R-ORG-14 | Revenue cycle team not engaged on async-messaging billing (F-181, B-010); workflow not in place at launch. | M | M | Identified dependency; not yet owned. | F-181, B-010, D-021 |
| R-ORG-15 | Specialty leadership disagreement on which specialties get configured views in Phase 1 (A-025). | M | M | Political risk inherent in "one platform, many specialties." | F-050, A-025 |

---

## 4. Regulatory & Compliance Risks

> **FDA scope note:** Per the market analysis, most HealthConnect features are non-SaMD by current FDA interpretation. FDA-specific risks below are narrower than the brief's prompt suggests, but real.

| ID | Risk | L | I | Rationale | Linked |
|---|---|---|---|---|---|
| R-REG-01 | Tracking technologies (analytics, marketing pixels, session-replay, chat widgets) deployed on PHI-bearing pages without proper OCR-compliant handling. | H | H | Active OCR enforcement area through 2023–2025; multiple multimillion-dollar settlements. | NF-080b, NF-033 |
| R-REG-02 | Provider-review window on lab carve-outs (F-020) is over-broad or delays exceed clinical necessity, triggering information-blocking complaint. | M | H | Information-blocking penalties became real in 2024. Hard to prove negative once accused. | F-020, F-076, NF-074, D-002 |
| R-REG-03 | Adolescent-privacy access model (F-006) misaligned with state law in one or more states served; HIPAA / state-AG exposure. | M | H | 50-state complexity; states diverging post-Dobbs. | F-006, F-110, NF-076, A-007 |
| R-REG-04 | Sensitive-category sharing (mental/behavioral health, SUD, reproductive, HIV/STI) misconfigured; disclosure beyond patient consent. | M | H | 42 CFR Part 2 + state laws + post-Dobbs scrutiny. | F-095, NF-038, NF-075, A-035 |
| R-REG-05 | AI-assisted clinical communication shipped without patient-disclosure compliant with California AB 3030 (effective Jan 2025) or similar state laws. | M | M | Emerging multi-state patchwork; not yet captured as explicit requirement. | NF-041, NF-044 |
| R-REG-06 | Right-of-access workflow (F-096) doesn't reliably hit 30-day HIPAA window; OCR right-of-access initiative enforcement. | M | M | OCR right-of-access has been a consistent enforcement focus. | F-096, D-001 |
| R-REG-07 | AI red-flag detection (F-016) or symptom triage (F-121) inadvertently crosses into SaMD without FDA review. | L | H | Low likelihood if design discipline holds; high impact if it slips. | F-016, F-121, NF-040, A-019 |
| R-REG-08 | EPCS / DEA workflow (F-043) misconfiguration causes prescription audit finding. | L | H | Mature regulatory area but high-consequence. | F-043, D-007 |
| R-REG-09 | Breach notification timeline (NF-039b) missed due to unclear detection / escalation ownership. | L | H | Common gap when DR + incident response are immature. | NF-039b, NF-029h |
| R-REG-10 | Annual HIPAA risk assessment (NF-078) deferred; finding stack at first OCR or internal audit. | M | M | Common organizational deferral. | NF-078 |
| R-REG-11 | Audit log gaps for privileged-user access (NF-077) discovered during compliance review. | M | M | Privileged-user logging frequently incomplete in new platforms. | NF-077, NF-032 |
| R-REG-12 | ONC HTI-1 / HTI-2 AI transparency requirements (model cards, intended use disclosure) not met before certified-EHR usage. | M | M | Required for certified health IT integrating AI DSI. | NF-044, NF-041 |
| R-REG-13 | TEFCA / QHIN strategy unresolved (A-038); outside-records workflow built on architecture that needs to be revisited. | M | M | Active national policy shift through 2024–2026. | NF-096, A-038, D-017 |
| R-REG-14 | Cures Act SMART on FHIR / OAuth 2.0 third-party app authorization built without scope governance; "info-blocking" risk on third-party patient apps. | M | M | Third-party patient-app interface is a Cures Act requirement with nuanced "info-blocking" exceptions. | NF-089b, F-197 |
| R-REG-15 | Asynchronous-messaging billing (F-181) lacks proper patient consent + good-faith-estimate handling. | M | M | NSA + state laws on patient cost transparency. | F-181, F-152, B-010 |

---

## 5. Data & Security Risks

| ID | Risk | L | I | Rationale | Linked |
|---|---|---|---|---|---|
| R-SEC-01 | Family / proxy access (F-002) misconfigured allows ex-spouse, lapsed guardian, or unauthorized caregiver to view sensitive data after relationship change. | M | H | Lifecycle management is the hardest part of proxy access. | F-002, F-006, F-095 |
| R-SEC-02 | Adolescent transition (F-006) leaks data to parent after age threshold due to retention of prior proxy grant. | M | H | Specific failure mode of F-006 lifecycle. | F-006, F-002 |
| R-SEC-03 | Patient-uploaded media (photos, insurance cards) stored outside PHI boundary by misconfigured CDN / object store. | L | H | Configuration drift is common; impact severe. | NF-050, F-101, F-113 |
| R-SEC-04 | Vendor sub-processor without proper BAA discovered in supply chain post-launch. | M | H | Common with iPaaS / AI / analytics vendors. | NF-039, NF-099 |
| R-SEC-05 | Service account / system integration credential leak via repo, log, or misconfigured secret store. | M | H | Highest-frequency root cause of breaches industry-wide. | NF-039e, NF-030e |
| R-SEC-06 | MFA fatigue / push-bombing attack succeeds against patients or staff. | M | M | Risk-based step-up (NF-030) helps; never zero. | NF-030 |
| R-SEC-07 | Identity-proofing method (NF-030b) bypassed via account-recovery helpdesk shortcut (F-004). | M | H | Helpdesk social engineering is a leading attack vector. | F-004, NF-030b, A-034 |
| R-SEC-08 | Shared-device / household-abuse scenario (NF-061) not handled; patient harm. | L | H | Low likelihood per case but high human impact. | NF-061, A-041 |
| R-SEC-09 | Prompt injection in patient message manipulates AI draft (F-014) to send misinformation. | M | M | Active threat class for LLM workflows. | F-014, F-015, NF-040 |
| R-SEC-10 | PHI inadvertently sent to LLM provider not under BAA (e.g., dev / staging using consumer-tier API). | M | H | Common engineering oversight in early LLM rollouts. | NF-039, NF-035 |
| R-SEC-11 | Audit log tampering or insufficient integrity controls discovered in forensic review. | L | H | NF-032 must be append-only and integrity-protected. | NF-032 |
| R-SEC-12 | Cross-tenant data leak in multi-tenant SaaS dependency (e.g., shared analytics, shared content store). | L | H | Catastrophic if it occurs. | NF-039 |
| R-SEC-13 | Patient-facing API (F-197 webhooks, SMART on FHIR apps) abused for data scraping. | M | M | Patient APIs are increasingly attacker-targeted. | NF-089b, F-197, NF-089d |
| R-SEC-14 | Consent records (F-097) inconsistently versioned; sharing performed under stale consent. | M | M | Hard to validate without explicit consent-version checks. | F-097, NF-082 |
| R-SEC-15 | Mobile-app keychain / secure-storage misuse caches PHI longer than session policy. | M | M | Common mobile pitfall. | NF-023, NF-035 |

---

## 6. Vendor & Dependency Risks

| ID | Risk | L | I | Rationale | Linked |
|---|---|---|---|---|---|
| R-VEN-01 | Epic platform pricing, API changes, or policy shifts (MyChart, Haiku, Hello World) disrupt roadmap. | M | H | Single-vendor concentration; Epic's strategic moves materially affect dependent builds. | D-010, D-018, F-081 |
| R-VEN-02 | Azure OpenAI capacity / model deprecation forces re-platforming of AI features mid-program. | M | M | Model deprecation cycles tightened in 2024–2025. | F-014, F-015, F-050 |
| R-VEN-03 | Surescripts agreement / data-rights for fill data (F-044, F-143) restricts use cases. | M | M | Surescripts data has known use-restriction language. | F-044, F-143, D-011 |
| R-VEN-04 | Telehealth vendor selected (A-037) cannot meet NF-029b quality SLOs at scale. | M | M | Telehealth video quality varies meaningfully by vendor. | NF-029b, A-037, D-040 |
| R-VEN-05 | Payment processor selection (D-019) drags; F-150 / NF-089e blocked. | M | M | Vendor selection often slips. | F-150, NF-089e, D-019 |
| R-VEN-06 | Ambient-scribe vendor selected separately (B-011) creates duplicate AI surfaces in provider workflow. | M | M | Per market analysis, this is a real coordination risk. | B-011 |
| R-VEN-07 | Apple HealthKit / Google Health Connect / Dexcom (D-012, D-013) policy changes break wearable ingestion. | L | M | Platform-policy risk; lower for HealthKit, higher for Dexcom-class vendors. | F-200, D-012, D-013 |
| R-VEN-08 | iPaaS / HIE vendor (Redox, Carequality member, QHIN) outage cascades to multiple integrations. | M | H | Single dependency upstream of many flows. | D-017, NF-029h |
| R-VEN-09 | Independent accessibility audit vendor (NF-010) capacity not booked early; slips pre-launch. | M | M | Booking lead time for qualified auditors is real. | NF-010, G-COMP-07 |
| R-VEN-10 | Vendor BAA renewals / breach-notification SLAs not tracked centrally; expired BAA in production. | L | H | Common in orgs without vendor-mgmt discipline. | NF-039, NF-097–099b |
| R-VEN-11 | RxImage / pill-image database coverage (D-038) insufficient for promised UX. | L | M | Coverage gaps make F-208 less useful. | F-208, D-038 |
| R-VEN-12 | Open-source dependency with restrictive license (NF-099) discovered in production; remediation costly. | L | M | Common when license discipline is informal. | NF-099 |

---

## 7. Timeline & Budget Risks

| ID | Risk | L | I | Rationale | Linked |
|---|---|---|---|---|---|
| R-BUD-01 | Phase 1 scope (5 personas + ~90 gap requirements + multi-specialty configurability) exceeds capacity; slip or feature-cut crisis. | H | M | Consolidated requirements list is large; gap analysis added significant scope. | All sections of consolidated-requirements.md |
| R-BUD-02 | Helpdesk + nurse-triage staffing budget (D-020, D-026) added late; OPEX shock at launch. | M | H | Common late-discovery of operational cost. | F-100, NF-086, D-020, D-026 |
| R-BUD-03 | Audit log + analytics storage costs (R-TECH-14) under-projected; budget overrun in year 1. | M | M | Per market analysis trend. | NF-032, NF-052 |
| R-BUD-04 | LLM token consumption at scale exceeds budget projections (message drafts, summarization across all providers + all patients). | M | M | Per-token costs are volatile; usage hard to forecast pre-launch. | F-014, F-015, F-050 |
| R-BUD-05 | Independent security review / pen testing (NF-039d) cycles add unplanned remediation work, slipping launch. | M | M | Late security findings commonly cause 2–6 week slips. | NF-039d |
| R-BUD-06 | Multi-language launch scope (F-195) expands during stakeholder review; translation governance (NF-081) becomes critical path. | M | M | Languages frequently added late under equity pressure. | F-195, NF-081, NF-087, A-036 |
| R-BUD-07 | Native mobile parity (F-080) iOS + Android requires headcount org doesn't have; contractor cost spike. | M | M | Per R-TECH-04. | F-080 |
| R-BUD-08 | Phase 2 feature pull-forwards (family-account expansion, wearable-provider review) demanded by stakeholders during Phase 1, eroding Phase 1 schedule. | H | M | Conflicts 7, 8, 17 all reference deferred Phase 2 scope that stakeholders may push to pull in. | F-001, F-200, F-143 |
| R-BUD-09 | Specialty-configurable summary view (F-050) timebox slips; cascading impact on specialist Phase 1 launch. | M | H | Per R-TECH-03. | F-050, B-015 |
| R-BUD-10 | Compliance + Privacy review gates discovered late in cycle; mandatory rework. | M | M | Common in orgs without early compliance engagement. | All NF compliance items |
| R-BUD-11 | Provider training program (NF-084) development underestimated; go-live blocked or providers untrained. | M | M | Training content development is consistently underestimated. | NF-084, D-028 |
| R-BUD-12 | TEFCA / QHIN strategy decision (A-038) drives re-architecture of outside-records flow mid-build. | M | M | National policy timing is uncertain. | NF-096, A-038 |

---

## 8. Risk → Requirement Coverage Gaps

Risks that surfaced requirements **not yet captured** in [consolidated-requirements.md](consolidated-requirements.md):

| Gap | Suggested addition | Triggering risk |
|---|---|---|
| Patient-disclosure of AI use in clinical communication (state-law compliance, e.g., CA AB 3030) | New NF under AI Governance: "Patient-facing clinical communication generated or substantially assisted by AI is disclosed to the patient per applicable state law." | R-REG-05 |
| Prompt-injection / adversarial-input protection for AI features handling patient input | New NF under AI Governance: "AI features that consume patient-authored content implement prompt-injection mitigations and output validation before any provider draft is surfaced." | R-SEC-09 |
| Dev / non-prod environment data handling for LLM workflows | New NF under Data Security: "Non-production environments must not transmit PHI to LLM providers; synthetic / de-identified data only." | R-SEC-10 |
| Vendor BAA + license lifecycle tracking | New NF under Vendor Mgmt: "Central register of vendor BAAs, sub-processors, and license expirations with renewal SLA alerts." Strengthens NF-097–099b. | R-VEN-10, R-VEN-12 |
| Coverage / handoff scope clarification | Promote A-023 (coverage scope) to a definition decision before F-103 build. | R-ORG-04 (specialist friction) |
| Helpdesk-driven PHI account-recovery hardening | Add operational requirement: "Helpdesk account-recovery for PHI-bearing accounts requires multi-factor identity verification independent of password reset; recorded justification; periodic anomaly review." Strengthens F-004 / NF-030b. | R-SEC-07 |
| Adoption-anomaly stratified monitoring | Operationalize NF-072: monitoring dashboards by demographic / language / SVI quintile must exist by launch, not be deferred. | R-ORG-03 |
| Information-blocking risk-review process | Add governance requirement: clinical-leadership review of any new data hold / delay rule against information-blocking exceptions. | R-REG-02 |

---

## 9. Executive Escalation List

Risks that should be surfaced to the executive sponsor / steering committee **before** PRD sign-off:

1. **R-ORG-01** — nurse-triage and async-messaging staffing must be funded before any messaging capability ships at the scale the brief implies. This is a launch gate decision, not a delivery decision.
2. **R-ORG-03 / R-ORG-05** — equity vs. phone-channel-deflection KPI tension. Operations leadership needs to commit to phone-channel preservation in writing, or `NF-070` / `NF-071` are theatrical.
3. **R-REG-01** — tracking-technology compliance posture needs a Privacy Officer decision **before** any analytics or third-party SDK is added to the patient surface.
4. **R-VEN-01 / R-VEN-06** — Epic platform dependency + ambient-scribe coordination need program-level governance, not feature-level discussion.
5. **R-BUD-01 / R-BUD-08** — Phase 1 scope is at risk before build starts. Steering committee should explicitly approve the deferred / Phase 2 list and resist pull-forward.
6. **R-REG-13 (A-038)** — TEFCA / QHIN affiliation decision affects architecture; this should be made by interop strategy leadership before build.
7. **R-ORG-11 / D-050** — AI-governance committee charter and AI-feature review process should be in place before any AI capability passes compliance gate.

---

**Next:** Phase 5 refinement — use this register to:
1. Add missing requirements from §8 to the consolidated list.
2. Confirm risk owners on the top-critical list.
3. Build a mitigation plan in the PRD risk section that pairs each top-10 risk with an owner, preventive measure, detective control, and corrective action.
