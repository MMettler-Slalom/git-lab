# Requirements Extract — Tech-Limited Senior

**Source:** [interview-notes-tech-limited-senior.md](interview-notes-tech-limited-senior.md)
**Stakeholder:** "Eleanor W." (patient persona — Tech-Limited Senior, 76, macular degeneration)
**Extracted by:** M. Mettler
**Date:** May 19, 2026

---

## Functional Requirements

### Must-Have

| ID | Requirement | Source | Notes / Clarification |
|---|---|---|---|
| F-TLS-01 | Phone channel must remain fully supported in parallel — portal complements, does not replace, the human channel | Eleanor — "will Marie still be there?" | Cross-cut org/policy requirement — not just product. |
| F-TLS-02 | Message-received confirmation visible to patient ("your nurse Sarah saw this at 2pm") | Eleanor | Mirrors F-CCM-02 from Linda's notes. |
| F-TLS-03 | Appointment reminders via voice call (in addition to digital channels) | Eleanor — current voice-call reminder loved | Don't deprecate existing phone reminders. |
| F-TLS-04 | Simple, configurable home/dashboard limited to a small number of key items (upcoming appt, message care team, medications) | Eleanor — "if I see 12 things I'll get lost" | Design constraint — implies "simple mode" or default minimalist layout. |
| F-TLS-05 | Plain-language explanation of test results, "what does this mean for me" framing | Eleanor — currently hears nothing if normal | Mirrors F-CCM-08. |
| F-TLS-06 | Notification to patient when a normal/abnormal result is available (don't rely on no-news-is-good-news) | Eleanor — anxious about silence | |
| F-TLS-07 | Proxy access with full rights for adult-child caregiver | Eleanor — daughter (RN) | Mirrors F-CCM-13. |
| F-TLS-08 | Patient-visible audit log of proxy access ("daughter viewed your record on...") | Eleanor — wants to know, not block | |
| F-TLS-09 | Visit-prep info: directions, parking, what to bring, fasting requirements | Eleanor — parking is hard | |

### Should-Have

| ID | Requirement | Source | Notes / Clarification |
|---|---|---|---|
| F-TLS-10 | Printable / downloadable medication list | Eleanor — purse list outdated | Should reflect live data. |
| F-TLS-11 | Self-service prescription refill simple enough for a low-tech user | Eleanor — "would feel proud" | Onboarding + UX design critical. |
| F-TLS-12 | Telehealth offer surfaced when appropriate (e.g., "this visit can be done from home") | Eleanor — won't drive in rain | Decision logic w/ provider. |
| F-TLS-13 | Change-management: UI/feature changes communicated in advance; option to defer or learn before forced upgrade | Eleanor — "they updated my email and I cried" | Implies feature-flag / staged rollout + in-app announcements. |
| F-TLS-14 | "Trusted clinic" branding in app — show clinic name, staff names (and optionally photos) to combat scam anxiety | Eleanor — "if it said Marie's name I'd believe it" | Anti-phishing UX. |

### Nice-to-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| F-TLS-15 | Audio readout / text-to-speech for results, messages, visit summaries | Eleanor — "if it could read it to me" | v2 candidate; iOS/Android system TTS could be MVP. |
| F-TLS-16 | Medication-identification aid — pill image alongside med name | Eleanor — "so I know orange one is my BP one" | Dependency on RxNorm + pill image library (NLM RxImageAccess). |
| F-TLS-17 | "Easy mode" / "simple mode" toggle with larger touch targets, fewer options, single-task focus | Inferred from Eleanor's pattern | Could be default for 70+ cohort. |
| F-TLS-18 | In-clinic / in-person onboarding support, ambassador program, printed quick-start guide | Eleanor — "learn better when someone sits next to me" | Service-design / change-mgmt, not pure product. |

---

## Non-Functional Requirements

### Must-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| NF-TLS-01 | Accessibility — WCAG 2.1 AA minimum; AAA-level contrast strongly preferred | Eleanor — macular degeneration | Brief mandates AA; this persona pushes toward AAA where feasible. |
| NF-TLS-02 | Large default text size; user-configurable scaling beyond OS default | Eleanor — current portal "too small" | |
| NF-TLS-03 | High-contrast color choices; **no yellow-on-white** combinations; never rely on color alone | Eleanor — explicit | |
| NF-TLS-04 | Touch targets sized for older / less dexterous users (≥44pt per Apple HIG / 48dp Android) | Inferred from osteoarthritis (hands) | |
| NF-TLS-05 | UI stability — minimize layout / navigation changes between releases; provide opt-in for new UI when changes are necessary | Eleanor — fear of "things moving" | |
| NF-TLS-06 | Low-friction authentication for senior cohort — biometric login, long sessions where security allows, no CAPTCHA | Eleanor — "what's a CAPTCHA" | Balance against MFA / HIPAA security. ⚠️ Tension flagged. |
| NF-TLS-07 | Engagement-success metrics for 70+ cohort must NOT include reduction in phone-call volume | Inferred — phone is preferred for this group | Policy / measurement guidance. |

### Should-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| NF-TLS-08 | Anti-phishing affordances — clinic identity verification, no unexpected SMS links, in-app secure inbox | Eleanor — "Medicare" scam calls | Cross-cuts security + UX. |
| NF-TLS-09 | Tested with low-vision and elderly participants explicitly (not just WCAG checklist) | Researcher recommendation | Usability-test requirement, not product feature. |

---

## Business Requirements

| ID | Requirement | Source | Priority | Notes |
|---|---|---|---|---|
| B-TLS-01 | Avoid creating a digital divide — equitable access for elderly / low-tech / accessibility-impacted patients | Eleanor's interview overall | Must | Maps to product-brief equity question. Org/strategic. |
| B-TLS-02 | Onboarding investment for 70+ cohort (in-person help, printed guides, ambassador staffing) | Eleanor — would not adopt otherwise | Should | Cost line item — needs funding. |
| B-TLS-03 | Phone call volume should NOT be a primary KPI for this cohort — measure engagement differently | Researcher | Should | Conflicts w/ brief's "50% reduction in phone call volume" target. ⚠️ |

---

## Constraints & Dependencies

- **D-TLS-01** — Pill-image feature depends on RxNorm / NLM RxImage data; coverage is incomplete for some generics.
- **D-TLS-02** — TTS may be deliverable via OS-native accessibility APIs without bespoke build; verify coverage.
- **D-TLS-03** — Biometric / passwordless login depends on device capability + HIPAA-acceptable authentication strength.
- **D-TLS-04** — "Simple mode" layout depends on design system supporting variant layouts.
- **D-TLS-05** — In-person onboarding depends on clinic staffing/budget; service-design dependency outside product team.

---

## Ambiguities & Open Questions

- **A-TLS-01** — Default mode for users 70+: "simple mode" by default, opt-in, or never auto-applied (avoid ageist defaults)?
- **A-TLS-02** — Tension between low-friction login (biometric, long sessions) and HIPAA / security review board expectations — needs explicit ruling.
- **A-TLS-03** — Audit-log notification to senior re: proxy access — push, in-app only, or summary email?
- **A-TLS-04** — TTS scope: v1 minimal (system TTS pass-through) vs. v2 full (curated audio summaries)?
- **A-TLS-05** — Telehealth eligibility surfacing: clinical rules engine vs. provider opt-in per visit type?
- **A-TLS-06** — How is "phone channel preserved" enforced organizationally if portal-adoption KPIs incentivize call-deflection?

---

## Cross-Persona Conflict Flags

- 🔁 Eleanor wants minimal home screen ↔ Marcus wants family badges + Linda wants trend dashboards — implies **per-user personalization / role-based defaults** rather than one-size-fits-all dashboard.
- 🔁 Eleanor prefers phone-call reminders ↔ Marcus would uninstall if calls came in ↔ Linda prefers push — confirms granular notification preferences as a hard requirement.
- 🔁 Eleanor's preference for stable UI ↔ provider personas may push for rapid iteration — release-cadence / change-mgmt policy needed.
- 🔁 Eleanor's adoption depends on phone-channel preservation ↔ business case in brief depends on 50% phone-call reduction — **reconcile the success metric framing**.
