# Interview Notes — Primary Care Physician

**Participant:** Dr. K. Alvarez, MD — PCP, 11 yrs w/ system, panel ~1,900
**Date:** May 15, 2026, 12:10–1:05 PM (lunch slot — she ate during the call)
**Interviewer:** M. Mettler
**Format:** Teams, audio only. Got pulled away once for ~2 min (urgent staff Q)

> Dr. A was direct, occasionally exasperated. Several "off the record but please put that in the notes" moments — flagged below w/ ⚠️

---

## Practice context

- Panel: 1,900 — "too many, but the org-wide target is 2,200, which is insane"
- Day: 18–22 scheduled visits, ~30 min lunch (rarely uninterrupted), 1 hr "admin" blocked at end of day (gets eaten by inbox)
- Systems she touches daily: Epic, MyChart (provider side), Surescripts, the org's intranet, Teams, sometimes Dragon (dictation), occasionally the fax queue (yes, 2026)
- Good day: home by 6:30, inbox <20
- Bad day: home by 8, inbox 80+, 2 hrs of "pajama time" charting

## Pain points / burnout

- "The inbox is killing primary care. Full stop."
- Duplicate work: same med change has to be entered in Epic + sent to pharmacy + documented in note + replied to in MyChart message. "Four places. For one decision."
- Pajama time: ~6–10 hrs/week. Mostly notes + inbox cleanup
- Last time tech saved her time: smart phrases / dot phrases in Epic. "When something just inserts what I need, I love it"
- Recently angry at: MyChart messages from patients with 8-paragraph essays containing 3 different unrelated concerns. "I bill for none of this"

## Inbox / messaging — **biggest topic**

- Triage today: MA filters first pass, escalates clinical to her. Works OK when MA is good. Fails when float MA is covering
- Self vs. delegate: anything refill-non-controlled → MA / standing order. Anything new sx → her. Anything billing → front desk
- Sustainable volume: "maybe 15–20 messages/day that need MY brain. I'm getting 40–60"
- Compensation: ⚠️ "If you want me to do meaningful clinical work in messages, the org needs to bill for it AND give me time. Right now it's free labor"
- Should NEVER reach her inbox: appt scheduling, billing Qs, form requests for school/work (template), basic Rx refills with standing order
- AI assistance: cautiously YES for: drafting replies, summarizing long msgs, classifying urgency, flagging red-flag symptoms
- AI should NOT: send anything without her review, make clinical recommendations to patient, auto-close messages
- ⚠️ "I will quit if you ship an AI that auto-replies to patients in my name without my signoff. Quote me."

## Chart review

- First 3 things she looks for: problem list, recent meds + changes, last visit note
- Then: recent labs, recent imaging, any new specialist notes since last visit
- Ideal prep time: 90 sec to 2 min per patient — she has ~5 min between visits
- Hardest to find: outside records (imaging from non-Epic facility), specialist notes that came in as PDFs, prior auth status
- Great "patient at a glance" would include: problem list, active meds (w/ recent changes flagged), last A1c/BP/whatever's relevant, **what changed since last visit**, open orders, overdue care gaps
- External data: yes wants it, but **needs provenance** — "I need to know if a BP came from a validated cuff or the patient's wrist device that overreads"
- ❓ Wearables: skeptical but open. Wants summary stats not raw streams. Definitely doesn't want to be liable for not reviewing 24/7 data

## Care team / referrals

- Communicates w/ MA/nurses via Epic in-basket messages + Teams + walking down the hall (still the fastest)
- Referrals: she sends, then "they disappear into a black hole." Often hears about the visit from the patient before the consult note arrives
- Provider-to-provider messaging: wants it, but needs to be **scoped** — separate from patient inbox, with its own SLA. "Don't dump everything into one queue"
- Handoffs: vacation coverage is "a disaster." Coverage doc gets her full inbox w/ no context

## Prescribing / refills

- Refill workflow: ideally standing-order-driven, MA processes, she signs daily batch
- Patient-initiated refills: fine if: med on her formulary, no recent labs needed, no red flags. AI-assisted screening would help
- EPCS: works but is friction (token + push). She accepts it
- Med rec: "it's never reconciled. We pretend it is. Patients show up on things I didn't prescribe and don't know about"
- Wants: clean integration w/ pharmacy fill data → "is the patient actually picking this up"

## Telehealth

- Good fit: med checks, mental health follow-up (when she does it), result reviews, simple URIs, post-op follow-ups
- Bad fit: anything abdominal, new neuro complaints, anything pediatric "where I can't see how sick they actually look in person"
- Issues today: video quality, patient tech problems eat 5–8 min of visit, "waiting room" UX bad
- Wants: one-click join, ability to text the patient mid-visit ("can you turn on your light"), automatic visit note draft

## Performance / reliability

- Downtime tolerance during clinic: "zero. Five minutes during clinic and I'm 30 min behind for the rest of the day"
- Screen load time: chart open <2 sec or she notices. Order screen <1 sec
- Outage alerts: wants proactive notification BEFORE she finds out by clicking. Banner in EHR + Teams message ideal
- "If your portal goes down at 8am Tuesday I want to know at 7:55 with workaround instructions"

## Data / population health

- Useful alerts: overdue A1c on diabetics, BP not at goal w/ no recent visit, high-risk patients overdue for follow-up
- Noise: pop-up alerts during a visit interrupting her thought. "Hard no"
- Pop health views: yes — gaps in care, quality metric performance, panel risk stratification
- Quality metrics: wants it dashboard-style, **not** weekly emails she ignores

## Wrap-up

- Remove one task: "the inbox. All of it. I want to practice medicine, not be a call center"
- Would advocate for portal if: messaging volume is contained + AI drafts genuinely save time + chart review is faster
- ⚠️ "Honestly, the bar is low. Just don't make my life worse. Most 'improvements' make it worse."
- Missed: asked about documentation/AI scribe — said "if you're building a portal please coordinate with whoever owns the scribe project, don't make me have two AI tools that don't talk to each other"

---

## Researcher observations

- Strong, opinionated, credible. Should consider for ongoing advisory role
- Major themes: **inbox containment, AI w/ human-in-the-loop, no auto-replies in her name, fast performance, no in-visit interruptions**
- Direct tension w/ patient persona expectations (faster responses, more channels) — must be reconciled at policy + staffing level, not just UX
- Concern about liability around continuous device data is a real risk that needs legal + clinical policy input
- Coordinate w/ ambient-scribe initiative (separate workstream — confirm owner)

## Action items

- [ ] Define message taxonomy + routing rules (admin → never reach physician inbox)
- [ ] Draft AI-assist policy: drafting OK, autosend NOT OK, must show source/citations
- [ ] Provider-to-provider messaging: separate queue, separate SLA, design review needed
- [ ] Wearable/device data: develop "review expectation" policy w/ legal + clinical leadership
- [ ] Engage Dr. Alvarez for ongoing provider advisory council
- [ ] Cross-team sync w/ ambient-scribe project — who owns?
- [ ] Performance budget: chart open <2s, order screen <1s. Document as NFR
- [ ] Define "billable messaging" workflow w/ revenue cycle team
