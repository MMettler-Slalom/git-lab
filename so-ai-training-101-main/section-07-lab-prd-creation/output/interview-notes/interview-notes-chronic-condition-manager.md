# Interview Notes — Chronic Condition Manager

**Participant:** "Linda R." (pseudonym), 58, T2 diabetes + HTN, ~6 yrs in our system
**Date:** May 12, 2026, 2:00–3:05 PM
**Interviewer:** M. Mettler (PM) / J. Patel (UX research, notetaker)
**Format:** Zoom, video on
**Recording:** Yes, w/ consent. Transcript pending.

---

## Background / Warm-up

- Conditions: T2 diabetes (dx 2018), HTN, mild hypothyroid. "Borderline" cholesterol — on statin since last yr
- Care team: PCP, endo, cardiologist (added Feb), eye doc annual, podiatrist 2x/yr. **5 providers** across 3 different practices, 2 different health systems (!)
- Self-rates tech comfort 7/10. Uses iPhone, banking apps, Amazon, FaceTime w/ grandkids
- Uses iPad mostly at home in evenings. Phone during day. Doesn't own a laptop anymore

## Current experience — pain points

- "I have three different patient portals open in my browser right now." — quote
- Last task: tried to get A1C from January sent to new cardiologist. Ended up faxing (!!) from PCP office. Took 2 wks
- Most frustrating: **nobody has the full picture**. Each doc only sees their slice. She's become "the messenger"
- Has a paper binder w/ tabs for each specialist. Brings to every appt. "I shouldn't have to do this in 2026"
- Stopped using old portal ~2023 — "kept asking me to reset password, lab results were just numbers w/ no context, made me anxious not informed"
- Workaround: keeps a Google Doc w/ med list, recent labs, BP readings. Shares link w/ daughter

## Care team communication

- Today: phone calls during business hrs, plus MyChart messages to PCP (other 2 don't have portal access for her)
- Response time PCP: usually 1–2 days, **endo office takes 4–5 days** which is too long when adjusting insulin
- "Reasonable" = same day for med questions, 48 hrs for general
- Wants: **direct line to her diabetes educator** — currently has to go through endo office which adds days
- Notification pref: push on phone + email backup. NO texts ("I get scam texts all day, I'd miss it")
- Lost message story: sent question re: dizziness in March, never got reply, called 5 days later, "no record of it." Scary
- ❓ FOLLOW-UP: confirm whether old portal had read receipts / delivery confirmation

## Lab results & health info

- Wants results **same time as doctor** ideally — "I'm an adult, I can handle a number"
- BUT wants context: "is 6.8 good for me? Last time was 7.1, so... better? Worse?"
- Current explanations: "useless. It says 'discuss with your provider' on everything"
- Compares results over time: screenshots into Notes app, then makes her own graph in Excel (!)
- Wants: **trend lines, color coding (green/yellow/red w/ explanation), personal target ranges set by her doc**
- Wants ability to annotate — "I was sick that week, that's why glucose was high"
- Detail level: wants full report available, but a "what changed since last time" summary on top

## Medications & adherence

- 8 meds + 2 supplements. Tracks in Apple Health + paper list in wallet
- Refills: nightmare. Different pharmacies for different meds (mail order for some, local CVS for others)
- "I've run out of metformin twice this year because the refill auth expired and nobody told me"
- Reminders: yes please, but **smart** — "don't ping me at 8am if I already logged that I took it"
- Side effects: googles them. "I know I shouldn't." Would love a 'is this normal / call doctor / ER' triage tool
- Devices: Dexcom CGM (!), Omron BP cuff (BT), Apple Watch. **None currently feed into portal.** Frustrated
- ❓ FOLLOW-UP: CGM data integration — Dexcom API? Apple HealthKit pass-through?

## Appointments

- Books online when possible. Endo office is phone-only — "I dread calling them"
- Needs to see: provider name, location (3 office locations confuse her), what to bring, fasting requirements, copay estimate
- Coordination across specialists is "manual Tetris" — she keeps a wall calendar
- Wants: ability to see all family + her own appts in one view. Reschedule should be 2 taps, not a phone call
- No-show cause once: appt moved by office, notification went to old email. Got billed. Took 3 months to resolve

## Health tracking & trends

- Logs BP 2x/day, weight weekly, glucose continuous (CGM)
- WANTS providers to see this. Endo "doesn't have time" to look at her CGM data — "what's the point of wearing it then?"
- Most-wanted surfaced trends: A1C trajectory, BP averages by week, **correlation between meds and BP** (started new BP med in Feb)

## Trust / privacy / accessibility

- Generally comfortable w/ digital records. "Already breached probably." (cynical laugh)
- Sensitive: doesn't want therapy notes visible to non-mental-health providers. Currently isn't in therapy but "if I were"
- Wants control: granular sharing — "endo can see everything, dentist doesn't need my mental health hx"
- Accessibility: reading glasses needed. Default text on current portal "too small." Color-blind husband — relies on her for color-coded stuff (note: design implication for color-only signaling)
- Proxy access: wants daughter (RN, lives out of state) to have view + message access. Husband nope, "he wouldn't use it"

## Vision / wrap-up

- Magic wand: **"one place where every doctor sees the same thing I see, and we're all on the same page."**
- What would make her a daily user: CGM integration + smart trend alerts + actually-fast messaging
- Other: worried about "AI summaries" being wrong. Wants to see source data, not just AI interpretation. "I want to verify"

---

## Researcher observations

- Highly engaged participant. Sophisticated user. Edge case in some ways (CGM, tracks own data) but represents where chronic-care patients are heading
- Strong negative emotion around: lost messages, expired refill auths, fragmented records
- Strong positive cues: control, transparency, integration w/ devices she already owns
- Mentioned "anxiety" 3x. Lack of info = anxiety, not reassurance

## Action items / follow-ups

- [ ] Confirm Epic MyChart message delivery confirmation behavior
- [ ] Research Dexcom + Apple HealthKit integration paths
- [ ] Add to req backlog: granular sharing controls per provider
- [ ] Add to req backlog: "what changed since last time" lab summary view
- [ ] Add persona note: chronic patients often manage care across MULTIPLE health systems — interop scope question
- [ ] Schedule 30-min follow-up re: device integration — Linda willing
