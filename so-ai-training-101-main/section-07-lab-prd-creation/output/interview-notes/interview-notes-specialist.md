# Interview Notes — Specialist

**Participant:** Dr. R. Okonkwo, MD — Cardiology, 7 yrs in system, mixed clinic + cath lab
**Date:** May 18, 2026, 7:15–8:10 AM (before his first case)
**Interviewer:** M. Mettler
**Format:** Teams. He was in his office, coffee, scrubs. Cut off at 8:10 sharp — "I'm scrubbing in"

---

## Practice context

- Specialty: general cardiology + interventional. Sees ~12 clinic patients on clinic days (Mon/Wed/Fri AM), procedures the rest
- Case mix: ~60% referral from PCPs (internal), ~25% from outside PCPs, ~10% internal specialist (e.g., endo sending diabetics), ~5% self
- Week: 2.5 days clinic, 1.5 days cath lab, on-call q5 weekends
- Systems: Epic, the cath lab reporting system (separate), PACS, Teams, fax queue ("don't ask"), occasional outside-record portals

## Referral intake — **biggest source of pain**

- Process today: referral hits a shared queue, his nurse triages, schedules. Sometimes the queue sits 3–5 days before triage
- Must-have on a referral: **reason for consult, recent ECG, recent echo (or note it's needed), current meds, problem list, what the PCP has already tried**
- What's usually missing: "the actual question they want answered. I get 'cardiac eval' — eval for WHAT"
- Triage urgency: nurse uses a sheet of rules, escalates ambiguous ones to him. ~5/week she escalates
- Lag: avg referral → seen is **6 weeks for new patient.** Urgent ~5 days. "Both are too long"
- Stuck points: incomplete info → call back to PCP office → PCP not available → patient doesn't answer scheduling call
- Loop-closing: he dictates a consult note that auto-routes to referring PCP if in-system. **Outside PCPs:** fax. "I have no idea if they read it"
- Incomplete referrals: wants intelligent intake — "if PCP didn't include an ECG, system should auto-request before it hits my nurse"

## Pre-visit prep

- Needs: recent ECG image (not just report), echo report + key measurements, lipid panel, hsCRP if available, meds, family hx
- Outside records: nightmare. Manual chase. Patient brings CD-ROMs sometimes (!). "It's 2026"
- Ideal "specialist-ready" summary: cardiac-focused — recent imaging, relevant labs trended, current cardiac meds w/ dose changes, prior interventions w/ dates, recent vitals trends. NOT just a generic problem list dump
- Delegation: nurse does first pass, he reviews in ~3-5 min per pt morning of clinic

## Cross-provider coordination

- Most often communicates with: referring PCP, endocrinology, nephrology (CKD + cardiac patients), cardiac surgery
- Broken: PCPs change meds he started without telling him (and vice versa, he admits). "We need a 'cardiac med ownership' flag"
- Wants: structured "assessment + plan + what I changed + what PCP should do" back to referring provider — not just the note dump
- Co-management of CHF / AFib patients across PCP + cards is "a coordination nightmare"
- Avoiding stepping on toes: relies on personal relationships. "I know which PCPs to text. The rest, I hope"
- Provider-to-provider chat: yes please. Different queue from patient messages. Async, but ideally with read receipts

## Procedures & scheduling

- Cath scheduling: nurse + scheduler do most of it. He approves the case list
- Pre-op patient info: instructions for fasting, meds to hold (huge — anticoagulants!), arrival time, what to bring. Currently a paper handout. "Half the patients don't bring it"
- Wants: digital pre-op checklist patient confirms in portal, system alerts on un-confirmed checklist 24hrs out
- Pre-auth: separate team handles, but he gets pulled in for peer-to-peer calls way too often. Wants pre-auth status visible in his patient view
- Post-procedure: discharge instructions + 2-week follow-up call from nurse + 4-6 wk clinic visit. Patients message a LOT in the first 72 hrs ("is this normal")
- Procedure messages need separate routing — should go to **procedure-team nurse first**, not him directly

## Patient communication / education

- Highest-value education topics: post-cath wound care, anticoagulation mgmt, AFib lifestyle, CHF symptom self-monitoring (weight, sx)
- Wants condition-specific education auto-pushed: "if I diagnose AFib today, the patient should get an AFib education module by tomorrow morning"
- Off-scope messages: gets a lot of "my knee hurts" type Qs. Wants easy redirect to PCP w/o being rude
- Specialty-specific workflows he wants:
  - Weight log w/ alert if >2 lb/day or >5 lb/week (CHF) — sent to his nurse not him
  - AFib symptom check-ins
  - Post-op day 1/3/7/14 templated check-ins

## Care plans / long-term

- Tracks today: in his head + dictated notes. "Honestly it's bad"
- Useful shared care plan would have: dx, target goals (BP, LDL, weight, EF if known), current regimen, what to escalate, who to call. Editable. Visible to PCP
- Patient participation: yes, but read-mostly w/ ability to log relevant data + ask Qs against the plan

## Reliability / workflow fit

- Workflow assumption that breaks: he is rarely at a desk. Between cases, in scrubs, on a workstation he doesn't own. Sessions need to be **fast to resume + auto-log-out for security**
- Mobile: yes — view-only chart access on phone for after-hours calls is huge. Currently uses Epic Haiku, "it's ok"
- Downtime on procedure days: "if Epic goes down mid-cath I have bigger problems than your portal. But on clinic days, same as Dr. Alvarez — zero tolerance"

## Data / outcomes

- Wants: outcomes data for his patients — 30/60/90 day readmits, post-PCI complication rates, AFib control rates
- Specialty-specific metrics general portal might miss: time-in-therapeutic-range for anticoag, EF trending, device interrogation data (pacemakers/ICDs!)
- ❓ Device interrogation data integration — currently a totally separate vendor portal per device manufacturer. "If you could solve THAT, you'd be a hero"

## Wrap-up

- If coordination "just worked": "I'd see fewer redundant referrals, fewer phone calls, fewer surprises in patient med lists"
- Specialist-built vs. retrofit: wants specialty-customizable views ("don't show me a primary-care dashboard"), procedure-aware workflows, referral-loop closure
- Missed: brought up trainees — fellows and residents need supervised access. "Don't forget about teaching workflows"

---

## Researcher observations

- Less inbox-volume pain than PCP, but **referral and coordination pain is severe**
- Procedural workflow is a distinct surface area — easy to under-scope if we only design w/ PCPs
- Outside-record integration came up unprompted — interop is a v1 concern, not a v2 polish item
- Device manufacturer data integration is a longer-term ask but worth scoping
- Trainee/teaching workflows = new persona to consider (not in current persona set)

## Action items

- [ ] Intelligent referral intake — required-info validation, auto-request missing pieces from PCP
- [ ] Structured "consult note back to referring provider" template w/ delivery confirmation
- [ ] Specialty-configurable patient summary views (cardiology view ≠ generic view)
- [ ] Procedure pre-op patient checklist + nurse alerting workflow
- [ ] Procedure-team nurse routing for post-op patient messages
- [ ] Provider-to-provider messaging — separate queue, read receipts, distinct SLA
- [ ] Shared care plan design — co-edit between PCP + specialist, patient-visible
- [ ] Specialty outcomes dashboards — define cardiology MVP metrics
- [ ] Outside-records ingestion — interop scope decision needed
- [ ] Add to backlog: trainee / teaching workflow persona
- [ ] Explore: device manufacturer (pacer/ICD) data ingestion — longer-term
