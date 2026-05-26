# Interview Notes — Tech-Limited Senior

**Participant:** "Eleanor W." (pseudonym), 76, widowed, lives alone (daughter lives ~20 min away)
**Date:** May 14, 2026, 10:30–11:35 AM
**Interviewer:** M. Mettler / J. Patel
**Format:** In-person at clinic (her preference). Daughter present for first 10 min, then left
**Notes:** Pace was slow — lots of pauses, that's the data. Eleanor brought a printed copy of our intro letter w/ handwritten Qs in the margin

---

## Background

- Conditions: HTN, osteoarthritis (knees, hands), early-stage macular degeneration (!! → accessibility), takes 5 meds
- Sees PCP q3mo, rheumatologist 2x/yr, eye doc q4mo
- Lives alone since husband passed in 2023. Daughter helps but "I don't want to be a burden"
- Tech: has an iPad (gift from daughter, 2 yrs ago). Uses for: FaceTime w/ grandkids, NYT crossword, email (sometimes)
- Does NOT have a smartphone. "Tried, gave it back. Too small, too confusing"
- "I'm not stupid with computers, they're just not built for me"

## Tech comfort — what works

- FaceTime: "wonderful. Big button, see the person, that's it"
- Crossword app: "I know exactly where everything is. It doesn't change"
- Email: "ok when it works. But sometimes things move around and I can't find them"
- Banking: does NOT do online banking. Goes to branch. "I want to look someone in the eye"
- **Frustration: things changing.** "They updated my email last year and I cried"

## Current experience — provider office

- Calls office for everything. Knows receptionist by name (Marie)
- Tried current portal once with daughter. Couldn't get past login. "What's a CAPTCHA"
- "I don't need a portal if Marie picks up the phone"
- BUT — "Marie isn't there on weekends and that's when I worry"

## Communication preferences

- Phone first. Voicemail OK if same-day callback
- If she used app: wants confirmation it was received (read receipt-style: "your nurse Sarah saw this at 2pm")
- "Too long" = more than a day for routine, more than a few hours if she said it was urgent
- Prefers callback over text reply. "I want to hear a voice"
- ⚠️ Strongly dislikes automated phone trees. "Press 1 for... I just want a person"

## Appointments

- Keeps a paper wall calendar. Daughter also has copy
- Reminders: phone call 2 days before (current system does this — she loves it)
- "If you send me a text I won't see it. If you send me an email I might"
- Wants: clear directions to office (parking is hard), what to bring (insurance card, list of meds), whether to fast
- Transportation: drives during day, won't drive at night or in rain. Has missed appts due to weather
- Would value: "tell me if I can do this visit on my iPad instead of driving" (telehealth offer)

## Prescriptions

- Mail-order through Express Scripts. "Works fine when it works"
- Has had wrong med arrive once — generic switch she wasn't told about. Scared her
- Memory aid: weekly pill organizer Sunday nights. Daughter checks during weekly visit
- Med list: "I'd love a real list. I have one in my purse but it's from 2024 I think"
- Wants: simple printable med list w/ pictures of the pills (!!) — "so I know orange one is my BP one"

## Understanding health info

- Test results: doctor calls if abnormal, otherwise she hears nothing. "I assume no news is good news but it makes me nervous"
- Wants results explained: "not the number, what it MEANS for me"
- Visit summaries: "I get a paper one sometimes. I save them in a folder. I don't always read them"
- Would prefer: short summary in plain English, option to "read more"
- **Accessibility (huge):** macular degeneration → needs LARGE text, high contrast, NO yellow on white, NO small icons
- Audio would be welcome — "if it could read it to me, that would be wonderful"

## Trust & safety

- Worried about scams. "I get calls every day from 'Medicare.' I don't trust any of it"
- Reassurance: "if the app said the same name as Marie when I logged in, I'd believe it"
- Daughter as proxy: yes please. "She's an adult, she's a nurse, she should be able to see everything"
- Wants notification when daughter accesses something — "not because I don't trust her, but I like to know"
- Privacy: not concerned about much. "At my age, who cares. But don't share with my insurance company any more than you have to"

## Simplicity

- Top 3 things on home screen: **upcoming appointment, message my nurse, my medications**
- That's it. "Don't show me 12 things"
- Prefers: reading > listening > watching. But large text required
- "I would feel proud if I could refill my own prescription without calling Marie. That would be something"

## Wrap-up

- "Made for me" = big text, clear words, doesn't change, phone backup always
- Other: asked if there'd be in-person training. "I learn better when someone sits next to me"
- Asked: "will Marie still be there?" — wants reassurance human channel remains

---

## Researcher observations

- This was the most emotionally significant interview of the round
- Real digital divide risk: she will not adopt unless extreme care is taken w/ onboarding + accessibility
- Macular degeneration is a critical accessibility input — WCAG 2.1 AA is minimum, AAA contrast preferred
- "Things changing" was a recurring fear → product implication: change communication, optional UI updates, training mode
- HUMAN BACKUP CHANNEL is not optional for this segment — portal must complement, not replace, the phone line
- Daughter-as-proxy is the norm, not the exception, for this persona

## Action items

- [ ] Accessibility audit plan — engage low-vision testers specifically (not just WCAG checklist)
- [ ] Onboarding strategy for 70+ — in-person training, printed quick-start, in-clinic ambassadors?
- [ ] "Trusted office contact" branding in app (e.g., show clinic staff names/photos to combat scam-fear)
- [ ] Audio readout / TTS — scope for v1 vs. v2
- [ ] Proxy access tier design (full vs. view-only vs. emergency)
- [ ] Pill-image / med-identification feature — research feasibility (RxNorm + image library?)
- [ ] Policy: phone channel must remain. Don't measure portal success by phone-call reduction in this cohort
