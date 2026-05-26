# Requirements Extract — Busy Parent

**Source:** [interview-notes-busy-parent.md](interview-notes-busy-parent.md)
**Stakeholder:** "Marcus T." (patient persona — Busy Parent, 38, 3 kids)
**Extracted by:** M. Mettler
**Date:** May 19, 2026

---

## Functional Requirements

### Must-Have

| ID | Requirement | Source | Notes / Clarification |
|---|---|---|---|
| F-BP-01 | Single sign-on / single account with ability to switch between linked family members (self + dependents) | Marcus — "Notes app full of usernames" | Core pain point. |
| F-BP-02 | Co-parent / shared-guardian access model — multiple adults with equal rights to a child's record | Marcus — spouse parity | ⚠️ AMBIGUOUS: how is co-equal vs. primary determined? Legal-guardian verification process needed. |
| F-BP-03 | Family-wide unified inbox/notification view with per-member badging | Marcus — "badge counts per kid" | |
| F-BP-04 | Real-time appointment booking (not request-and-callback) | Marcus — "if I have to wait for callback I'll just call" | |
| F-BP-05 | Same-day / sick-visit booking with visibility into other providers in practice (not just primary pediatrician) | Marcus | |
| F-BP-06 | Prescription refill requests, including visibility into controlled-substance refill status | Marcus — ADHD med took 4 days, opaque | Cannot bypass DEA/EPCS; can improve transparency of where request stands. |
| F-BP-07 | Mobile-first native app (iOS + Android) with feature parity to web | Marcus — "if it's a web wrapper I'll uninstall" | Aligns with product brief Phase 1. |
| F-BP-08 | Notification taxonomy: separate clinical channels from marketing/health-tips; user-controllable per channel | Marcus — "one 'flu shots' email and I'll uninstall" | Important brand-trust requirement. |
| F-BP-09 | Async messaging with care team for non-urgent questions | Marcus — "rashes, eye issues" | |
| F-BP-10 | Access to immunization records on-demand (for school/camp forms) | Marcus — "most-needed on short notice" | Should support quick-share/PDF export. |

### Should-Have

| ID | Requirement | Source | Notes / Clarification |
|---|---|---|---|
| F-BP-11 | Async nurse-triage chat for pediatric questions | Marcus — "big yes" | Staffing / SLA implications. |
| F-BP-12 | Photo and video attachments in clinical messages (esp. pediatric: rashes, eyes) | Marcus | Secure storage; retention policy; patient deletion rights — must be defined. |
| F-BP-13 | Stacked / family-batch appointment booking (e.g., 3 kids back-to-back) | Marcus — "life-changing" | Requires scheduler logic for related-account chaining. |
| F-BP-14 | Family-wide consolidated bill view + pay (incl. Apple Pay / Google Pay) | Marcus — pays wrong bills currently | |
| F-BP-15 | Day-of-morning appointment reminder (in addition to 24-hr) | Marcus — "panic-mode helpful" | |
| F-BP-16 | Telehealth video visits, particularly for low-acuity pediatric cases | Marcus — "didn't have to load 3 kids in the car" | Aligns w/ brief Phase 2. |
| F-BP-17 | Adolescent-privacy transition workflow as dependents age into protected periods | Marcus — anxious about 11yo turning 13 | ⚠️ State-by-state variation. Legal review required. |
| F-BP-18 | Temporary / scoped caregiver access (e.g., view-only immunization for grandparent) | Marcus | New access tier beyond proxy/full. |
| F-BP-19 | Quick "emergency info / allergies / current meds" share (PDF or shareable card) | Marcus — "just give me a PDF I can text" | |
| F-BP-20 | Insurance card image storage (photo capture) | Marcus | Storage classification — is this PHI? |

### Nice-to-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| F-BP-21 | HSA-eligibility tagging on bills / receipts | Marcus | |
| F-BP-22 | Payment plan setup self-service with transparent fees | Marcus — "don't bury fees" | |
| F-BP-23 | Audit / access-log visibility for parents (who saw kid's records) | Marcus — privacy reassurance | Likely required by some state laws regardless. |

---

## Non-Functional Requirements

### Must-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| NF-BP-01 | Sub-3-tap completion of common tasks (refill, reschedule, view immunizations) | Marcus — "90 seconds or I'll call you" | Translate to UX performance budget. |
| NF-BP-02 | Native mobile performance — feels app-like, not web-wrapper | Marcus | Implies React Native / native, not pure WebView. Architecture decision. |
| NF-BP-03 | Secure storage + lifecycle policy for user-uploaded photos/videos (encryption at rest, defined retention, patient deletion) | Marcus — concerned about photos | HIPAA + org policy. |
| NF-BP-04 | MFA support without being onerous for daily use | Marcus — wants security but not friction | Biometric / device-trust strategy needed. |
| NF-BP-05 | Notification channel separation enforced — clinical alerts cannot be commingled with marketing | Marcus | Org-policy + technical enforcement (separate notification topics). |

### Should-Have

| ID | Requirement | Source | Notes |
|---|---|---|---|
| NF-BP-06 | Push notification reliability — delivered promptly even if app backgrounded | Marcus — appt reminders critical | iOS/Android platform consideration. |
| NF-BP-07 | App-to-OS integrations for storing insurance cards / sharing PDFs (Apple Wallet, Files, share sheet) | Marcus | |

---

## Business Requirements

| ID | Requirement | Source | Priority | Notes |
|---|---|---|---|---|
| B-BP-01 | Reduce family-care no-shows via reliable, channel-correct reminders | Marcus — billed for missed dentist visit | Should | Maps to brief's 10% no-show reduction. |
| B-BP-02 | Improve consolidated billing experience to reduce billing-call volume + collection cycle | Marcus — pays wrong bills | Should | |
| B-BP-03 | Family-account model must be a v1 differentiator (drive parent-segment adoption) | Marcus | Must | Brief lists family management as Phase 2 — Marcus's pain suggests pulling forward. **FLAG for roadmap discussion.** |

---

## Constraints & Dependencies

- **D-BP-01** — Adolescent-privacy workflows depend on state-specific consent laws (varies by state). Legal review required pre-design.
- **D-BP-02** — Co-guardian verification depends on identity-proofing process and legal-guardian documentation handling. Compliance dependency.
- **D-BP-03** — Real-time scheduling depends on Epic MyChart API + practice scheduling templates being open for online booking.
- **D-BP-04** — Photo/video attachments depend on PHI-grade media storage + retention/deletion policy.
- **D-BP-05** — Apple Pay / Google Pay depend on payment-processor integration + PCI scope decision.
- **D-BP-06** — Apple Wallet integration depends on Apple developer program + pass-design effort.

---

## Ambiguities & Open Questions

- **A-BP-01** — "Co-equal parent" rights: what if parents are divorced w/ split custody? How are conflicts resolved (e.g., one parent revokes the other)?
- **A-BP-02** — Adolescent-privacy: lockout model vs. graded-access model? Default state at age threshold?
- **A-BP-03** — Temp caregiver access: time-bound? Auto-expiring? Audit notification to primary guardian?
- **A-BP-04** — Photo retention: keep indefinitely w/ record, or auto-delete after defined window?
- **A-BP-05** — Family-bill model: does each family member's bill have separate financial responsibility, or is one guarantor account model used? Confirm w/ revenue cycle.
- **A-BP-06** — Adolescent-privacy: should there be parent override for emergencies? How is "emergency" defined?

---

## Cross-Persona Conflict Flags

- 🔁 Marcus wants async-nurse-chat as a core capability ↔ Dr. Alvarez (PCP) is at message-volume breaking point — staffing model needed before promising SLA.
- 🔁 Family-account is Phase 2 per brief ↔ identified as Must-Have for Busy Parent adoption — roadmap-sequence flag.
- 🔁 Push notifications as primary channel (Marcus) ↔ SMS-distrust (Linda) ↔ phone-call preference (Eleanor) — confirms need for fully user-configurable notification preferences per channel per event type.
