# Meeting Notes: Mary's Place Pro Bono Intro Call
**Date:** November 14, 2025  |  **Duration:** ~53 minutes
**Participants:**
- Jason Gortney — Chief Program & Innovation Officer, Mary's Place
- Mike Komola — Chief HR & Operations Officer, Mary's Place
- Casey Frith-Smith — Pro bono team
- Lauren Milosky — Pro bono team (Product)

## Meeting-Wide Summary

**Key Decisions Made:** 16 total across features
- **Agreed:** 11 (most directional / scope decisions reached consensus)
- **Tentative:** 4 (deliverable format, family-direct vs. staff-mediated supply, HMIS integration scope, sequencing of step-duration data sources)
- **Not Decided / Deferred:** 1 (rebuild vs. wrap of existing SQL system)

**Total Action Items:** 3 — all assigned to the pro bono team (Casey / Lauren); zero new commitments from Mary's Place beyond agreeing to participate in follow-ups.

**Open Questions:** ~35 across all features — the agenda for the follow-up calls with the care coordinator and warehouse/donations staff.

**Cross-Cutting Themes:**
- **Two coherent problem clusters**, not seven independent features: (a) intake & journey (#1–#3), (b) goods supply chain (#4–#7). Likely candidates for two parallel concept tracks.
- **Multilingual + trauma-informed** is a baseline expectation, not a future-phase enhancement.
- **Microsoft/Copilot stack** + small IT/data team is a hard constraint on technology choices.
- **Don't break donor relationships** is a non-negotiable that shapes Features #6 and #7.
- **Proven AI precedent** (asylum chatbot, 4hr → 1hr meetings) is the anchor case for funder conversations.

**Next Steps:**
1. Casey sends validation email with the consolidated use case list.
2. Schedule the two follow-up interviews (care coordinator + warehouse/donations staff).
3. Pro bono team narrows scope and decides on deliverable format (prototype vs. concept doc) before deep design work.

---

## Feature 1: Virtual Intake & Journey Navigator (AI Case-Management Assistant)

### Requirements
- AI agent that prompts a family through all required intake information at their own pace *(Jason, ~min 12–13)*
- Single coordinated assessment replacing today's separate health, housing, and youth services assessments *(Jason, ~min 11–12)*
- Prioritization/sequencing engine that breaks the ~50 steps to rehousing into "do this on day 1, this on day 2" guidance *(Jason, ~min 13, 16–17)*
- Sequencing must be informed by step duration (e.g., "this thing takes 3 months, so start it day one") *(Jason, ~min 16–17)*
- Estimated journey length / expected length of stay for each family at intake *(Jason, ~min 17)*
- Output must feed into specialist meetings so staff can "cut to the important work" *(Jason, ~min 16–17)*
- Must be trauma-informed and emotionally attuned (modeled on prior asylum chatbot) *(Jason, ~min 14)*
- Each family retains a central navigator (case manager); the AI supports — does not replace — that role *(Jason, ~min 19)*
- Visibility into the family's goals/progress for all teams (housing, health, youth services) *(Jason, ~min 19)*
- *Implied:* Length-of-stay estimate must allow flexibility — no hard time limits on shelter stays *(Jason, ~min 17)*

### Decisions

**Decision: Primary problem to solve with AI**
- Initial framing (~min 9–10): Major pain point is shelter capacity / length of stay
- Refinement (~min 11–17): Since adding shelter capacity isn't feasible short-term, focus on improving *throughput* by streamlining the intake-to-rehousing journey
- **Status: Agreed** — journey navigator is Jason's top-priority AI use case

**Decision: Scope of prioritization — outcomes vs. capacity-based triage**
- Question raised (~min 15): Lauren asked whether prioritization is for the family's outcomes only, or also for Mary's Place capacity allocation
- Clarification (~min 16): Jason confirmed that intake prioritization (who gets in) works pretty well already; new system should focus on *per-family* sequencing of steps once in the program
- **Status: Agreed** — scope is per-family journey prioritization, not org-wide triage

**Decision: AI as augmentation, not replacement**
- Position (~min 13, 19): AI should "scaffold" the experience and help families gain skills, not remove staff
- **Status: Agreed** — central case-manager navigator role preserved

### Action Items
- None explicit. (Implied next step: scope into prototype — see Feature #8.)

### Open Questions
- What data sources would feed the sequencing logic (existing case data, county HMIS, external)?
- How are "step durations" (e.g., "3 months for X") sourced — historical data, expert input, or both?
- How does the family interact with the agent — kiosk, mobile, web, staff-mediated?
- Should the estimated length-of-stay be shared with the family directly, or used internally?
- How does the system handle re-prioritization when circumstances change mid-stay?

### Dependencies & Connections
- **Depends on:** Feature #3 (Shared Case Data & HMIS Integration) — needs unified family data to function
- **Depends on:** Feature #2 (Multilingual / Trauma-Informed Communication) — must work across 12–15 languages from day one
- **Informs:** Capacity & demand forecasting for Mary's Place internally *(Lauren, ~min 18)*

---

## Feature 2: Multilingual / Trauma-Informed Communication Layer

### Requirements
- Support for the 4–8 languages active in shelters at any given time *(Mike, ~min 14)*
- Coverage breadth of ~12–15 languages across the year to handle shifting populations *(Mike, ~min 14–15)*
- Communication in each family's preferred language **and** cultural style — not just translation *(Mike, ~min 14)*
- Trauma-informed, emotionally attuned tone (modeled on the asylum-application chatbot) *(Jason, ~min 14, 45)*
- Language layer must overlay the Journey Navigator (Feature #1) — same intake flow, multiple languages *(Mike, ~min 14)*
- *Implied:* Language set must be reconfigurable as population trends shift *(Mike, ~min 14–15)*
- *Implied:* Family-facing surfaces (intake, marketplace, notifications) all need language support — not just the intake agent

### Decisions

**Decision: Multilingual is a baseline requirement, not a "phase 2" nice-to-have**
- Mike layered it onto Jason's pitch immediately (~min 14): "to do what Jason described in a language and communication style they're familiar with would also greatly add to enablement"
- Reinforced by precedent (~min 45): the asylum chatbot did this successfully across all the languages Mike mentioned
- **Status: Agreed** — treated as a foundational capability of the journey navigator

**Decision: Cultural attunement, not just translation**
- Position (~min 14): Mike specifically called out "communication style they're familiar with" alongside language
- Reinforced (~min 45): Jason described the asylum chatbot as "trauma-informed and really emotionally attuned"
- **Status: Agreed (tone-setting)** — depth of "cultural attunement" not yet defined

### Action Items
- None explicit.

### Open Questions
- Which specific 12–15 languages need to be supported on day one?
- What translation/LLM approach meets both accuracy and trauma-informed tone requirements?
- Who validates linguistic and cultural appropriateness — internal staff, community reviewers, or vendor?
- How does the system handle low-resource languages where AI translation quality is weaker?
- Is voice/audio input required for families with low literacy, or text-only sufficient?

### Dependencies & Connections
- **Foundational to:** Feature #1 (Journey Navigator) — same families, same flows
- **Foundational to:** Feature #5 (family-facing supply/marketplace surfaces, if exposed to families)
- **Precedent / proof point:** Asylum-application chatbot built pro bono with a law firm + Amazon Legal — cut attorney meeting time from 4 hours to 1 hour *(Jason, ~min 44–46)*

---

## Feature 3: Shared Case Data & HMIS Integration

### Requirements
- Single shared data store across teams (housing, health, youth services) so all staff can see a family's goals and progress *(Jason, ~min 19)*
- Eliminate double entry between Mary's Place's internal system and the county Homelessness Management Information System (HMIS) *(Jason + Mike, ~min 20)*
- Automated integration/data push from internal system → HMIS for demographic data *(Casey/Jason, ~min 20)*
- Data layer must support the Journey Navigator's per-family sequencing (goals, barriers, step status) *(implied from Feature #1)*
- Must be maintainable by Mary's Place's small internal data team that already stewards the current system *(Jason, ~min 43–44)*
- *Constraint:* External parties (other than HMIS demographics) do not get access to family data *(Jason/Lauren, ~min 20)*

### Decisions

**Decision: Replace vs. wrap the existing data system**
- Current state (~min 47–48): Open-source SQL database originally built by a homeless services provider, customized in-house; "looks like something from the 1990s"
- Implicit position (~min 19): Jason called the existing system "clunky but we have it" — kept usable but not loved
- **Status: Not decided** — no explicit call on rebuild vs. integrate vs. wrap

**Decision: HMIS integration is a real problem worth solving**
- Surfaced (~min 20): Casey asked if there was an integration; Jason: "I wish... it is a double entry nightmare"
- **Status: Tentative** — acknowledged as a pain point, not yet scoped as in/out for the pro bono effort

### Action Items
- None explicit.

### Open Questions
- Rebuild the existing SQL system, wrap it with new services, or integrate alongside it?
- What is the HMIS integration interface (API, file drop, manual export)?
- What family-level data fields must be shared across teams vs. kept private to a specific team (e.g., behavioral health)?
- Are there compliance/regulatory constraints (HIPAA, county HMIS rules) governing what can move where?
- Who owns and maintains the new data layer — internal data team, external partner, or hybrid?

### Dependencies & Connections
- **Foundational to:** Feature #1 (Journey Navigator) — sequencing needs unified family data
- **Connects to:** Feature #4 (Inventory Management) — family needs may need to link to inventory requests
- **Stack context:** Mary's Place is a Microsoft / Copilot shop; no current AWS or Azure-native infrastructure beyond Microsoft 365 *(Jason + Mike, ~min 48–49)*

---

## Feature 4: In-Kind Inventory Management System

### Requirements
- Lightweight inventory visibility for goods on hand at the central warehouse and at each shelter "marketplace" *(Mike, ~min 34, 36–37)*
- Track inventory at a granularity above today's audit-driven bin counts, but does **not** require SKU/barcode-level tracking *(Mike, ~min 35)*
- Preserve existing audit/valuation workflow: bins per category with assigned per-item values; food tracked by weight *(Mike, ~min 33–36)*
- Capture intake at point of receipt (warehouse staff sort donations into categories on arrival) *(Mike, ~min 34–35)*
- Surface inventory to non-warehouse staff (outreach, prevention, "Make a Home" coordinator) — today they have to phone the warehouse *(Mike, ~min 37–38, 42)*
- Distinguish usable-for-shelter, usable-for-outreach/prevention move-ins, and not-usable-for-us goods *(implied from Mike + Casey discussion, ~min 28–30)*
- *Constraint:* Solution must work within Mary's Place's small operational footprint — no heavy hardware investment (no barcoding/scanning) *(Mike, ~min 35)*
- *Implied:* Must integrate with the marketplace "shopping" experience used by shelter guests today *(Mike, ~min 36–37)*

### Decisions

**Decision: Inventory tracking granularity**
- Initial frame (~min 34): Mike noted no system exists; problem has been worked for 1.5 years driven by audit
- Constraint stated (~min 35): "no way in heck you can [do SKU/item counts] without a system, without barcoding and scanning"
- Current approach (~min 35–36): Bin-level categorization with prescribed per-item values
- **Status: Agreed (constraint)** — any new system should improve on bin-level visibility but not require barcoding infrastructure

**Decision: Inventory system is the foundation for solving the larger supply/demand problem**
- Framing (~min 33–34): Mike pivoted from "information flow" pain to "how do you currently catalog?" question from Lauren
- Implication: An inventory layer enables Features #5, #6, and #7
- **Status: Agreed (implicit)** — treated as the substrate, though not labeled as such

### Action Items
- None explicit.

### Open Questions
- What is the right unit of tracking — category, bin, item — and how is that captured at receipt without slowing intake?
- How is the inventory layer kept in sync with the marketplace "shopping" activity by guests?
- Does food inventory (weight-based) live in the same system as durable goods (bin-based), or in parallel?
- What's the data entry burden on warehouse staff, and what's acceptable?
- Can the existing audit/valuation reports be generated from the new system to avoid parallel work?

### Dependencies & Connections
- **Foundational to:** Feature #5 (Supply-Demand Matching) — outreach/prevention needs inventory visibility
- **Foundational to:** Feature #6 (Targeted Donor Signaling) — can't tell donors what's needed without knowing what's on hand
- **Foundational to:** Feature #7 (Partner Redistribution) — need to identify "usable but not for us" stock
- **Connects to:** "Make a Home" program (1-person coordinator who sources household goods for families moving into housing) *(Mike, ~min 41–43)*

---

## Feature 5: Supply-Demand Matching for Outreach & Prevention Families

### Requirements
- Mechanism for outreach/prevention staff to surface upcoming household needs **with lead time**, not only on move-in day *(Mike, ~min 28–29, 40)*
- Match family-level needs against current and forecastable inventory *(Mike, ~min 31, 39–40)*
- Allow needs to be queued/reserved even when inventory isn't on hand yet — system should signal "we don't have a microwave now, but we'll have one within a week" *(Mike, ~min 40)*
- Coordinate with the "Make a Home" program (single coordinator, Olga) who already sources household items for any family — shelter, outreach, or prevention — moving into housing *(Mike, ~min 41–43)*
- Extend the existing "marketplace shopping" model (used by shelter guests today) to outreach and prevention populations *(Mike, ~min 36–37, 41)*
- Optional family-facing surface: families directly view inventory and submit requests, with or without staff in the loop *(Mike, ~min 39–40)*
- Consider a *physical* marketplace location for outreach/prevention families to shop in person, mirroring the in-shelter model *(Mike, ~min 40–41)*
- *Constraint:* Mary's Place has very limited offsite storage capacity for outreach staff *(Mike, ~min 39)*

### Decisions

**Decision: Staff-mediated vs. family-direct request flow**
- Question raised (~min 38–39): Lauren asked whether outreach families would have direct inventory access or always go through an outreach coordinator
- Mike's reflection (~min 39): "We were just talking about this the other day" — internal team had been actively debating this
- Position (~min 41): "I think maybe it's a combination of the two" — both staff-mediated supply matching AND a possible family-shoppable marketplace
- **Status: Tentative** — leaning toward hybrid, but not locked in

**Decision: Service extension scope**
- Initial state (~min 37–38): Marketplace model only serves shelter guests today
- Recognized gap (~min 38): "It's an opportunity for us there. An outreach specialist will just call into our warehouse manager..."
- Proposed expansion (~min 40–41): Marketplace concept extended to outreach AND prevention populations
- **Status: Agreed (directional)** — clear intent; specific delivery model still open

**Decision: Lead time matters more than instant fulfillment**
- Position (~min 40): Families don't always need everything day one — "you can move in and we'll get... we'll have one within a week"
- **Status: Agreed** — informs design (forecasting + scheduling beats real-time-only)

### Action Items
- None explicit.

### Open Questions
- Hybrid model split: which request types go family-direct vs. staff-mediated?
- If a physical outreach/prevention marketplace is built, where does it live and who staffs it?
- How do outreach families travel to/access a marketplace if mobility is a barrier?
- What lead-time window for move-in needs is realistic to expect from outreach staff (Mike said "couple of days lead time, sometimes a little longer")?
- How does this coordinate with — vs. replace or augment — the "Make a Home" coordinator's manual sourcing process?
- Does this surface need to be multilingual on day one (yes if family-facing — see Feature #2)?

### Dependencies & Connections
- **Depends on:** Feature #4 (Inventory Management) — can't match without inventory visibility
- **Depends on:** Feature #2 (Multilingual) — if family-facing surface is built
- **Connects to:** "Make a Home" program — overlapping function with one-person team
- **Informs:** Feature #6 (Donor Signaling) — known forecasted needs become targeted donor asks

---

## Feature 6: Targeted Donor Signaling / Smart Wish Lists

### Requirements
- Replace generic, evergreen Amazon wish lists with real-time, needs-driven asks reflecting current inventory gaps and forecasted family needs *(Mike, ~min 32, 33)*
- Give the development team visibility into actual needs across shelter, outreach, and prevention so they can direct corporate/community giving *(Mike, ~min 31–32)*
- Support both ongoing baseline needs (diapers, microwaves, toasters) and targeted, campaign-specific asks *(Mike, ~min 32–33)*
- Provide feedback/closed-loop to donors so they can see their contribution was used (implied from Feature #6 persona pain point + "we don't want to tell them" tension, ~min 33)
- Must preserve donor relationships — cannot result in "please stop giving" messaging to corporate partners like Microsoft, REI, Amazon *(Mike, ~min 26, 32)*
- *Constraint:* Asks need to be specific enough to be useful but not so granular they're unfulfillable by a corporate drive
- *Implied:* Surface should be accessible to development team for outreach to donors, not just internal ops

### Decisions

**Decision: Solve donor channeling via better information, not by turning donations away**
- Initial tension surfaced (~min 26): "It's not a simple matter of saying please don't give us stuff anymore... our development folks would scream at me"
- Reframed (~min 31–32): "Shortening the demand and supply chain through better information... would go a long way"
- **Status: Agreed** — better signal beats refusing donations

**Decision: Donor signaling is downstream of inventory + needs visibility**
- Implication throughout (~min 31–34): Smart wish lists require both inventory awareness (Feature #4) and known/forecasted family needs (Feature #5)
- **Status: Agreed (implicit)** — sequencing makes #4 and #5 prerequisites

### Action Items
- None explicit.

### Open Questions
- Who in the development team owns the wish-list generation surface, and what's their workflow today?
- How is "need" quantified for a donor-facing ask (units, dollar value, family-impact framing)?
- How does this integrate with existing donor channels — Amazon wish list, corporate drive intake forms, direct outreach?
- How are donors notified when an ask is fulfilled (or no longer needed) to avoid over-supply of the same item?
- Should individual donors see different asks than corporate partners (different scales)?
- How is donor-facing language reconciled with the diplomatic constraint of not signaling "your previous donation wasn't useful"?

### Dependencies & Connections
- **Depends on:** Feature #4 (Inventory Management) — must know what's on hand
- **Depends on:** Feature #5 (Supply-Demand Matching) — must know what's needed/forecasted
- **Informs:** Feature #7 (Partner Redistribution) — items that consistently exceed need become redistribution candidates
- **Stakeholder dependency:** Mary's Place development team — needs their workflow input

---

## Feature 7: Partner Redistribution of Non-Usable Donations

### Requirements
- Process and/or platform to redirect the ~80–85% of donated goods that aren't usable by Mary's Place families to other community organizations that can use them *(Mike, ~min 25–27)*
- Recognize that "not usable to us" doesn't mean "no value" — items have inherent value and community need exists elsewhere *(Mike, ~min 25)*
- Coordinate/centralize/systematize information flow between Mary's Place's surplus inventory and partner orgs' needs — explicitly *not* full automation *(Mike, ~min 31)*
- Avoid landfill as default disposition for non-usable goods *(Mike, ~min 25)*
- Support alternative disposition paths: redistribute to partner orgs, resell to fundraise for Mary's Place, or absorb cost of disposal *(Casey/Mike, ~min 30–31)*
- *Constraint:* Selling goods takes resources, time, and effort that Mary's Place doesn't currently have *(Mike, ~min 31)*

### Decisions

**Decision: Redistribution network is the preferred disposition over disposal or resale**
- Position (~min 25–27): Mike: "I am 99% certain there's community need out there that other people, other organizations... could use that stuff"
- Resale option (~min 30–31): Acknowledged but explicitly deprioritized — "takes resources and time and effort and figuring out how to shop all that stuff"
- **Status: Agreed (directional)** — community redistribution is the target; resale is a fallback

**Decision: Systematized information flow, not full automation**
- Mike's phrasing (~min 31): "If the flow of information around from need through supply were coordinated, centralized, streamlined, not automated. Systematized maybe is the right word."
- **Status: Agreed** — solution favors structured information sharing and process design over autonomous systems

### Action Items
- None explicit.

### Open Questions
- Which partner organizations are in scope (existing relationships? new network to build?)
- Who at Mary's Place would own the partner redistribution coordination role?
- What's the disposition logic — auto-route items by category, or staff decides item-by-item?
- Is there a regional/county hub model already in play (e.g., adjacent to HMIS) that could host this network?
- How are partner-org needs surfaced and kept current — do they reciprocate by sharing their inventory/needs too?
- What's the legal/liability posture on transferring donated goods to third parties?

### Dependencies & Connections
- **Depends on:** Feature #4 (Inventory Management) — must identify "usable but not for us" stock
- **Connects to:** Feature #6 (Donor Signaling) — recurring redistribution-only items may signal a "please redirect future drives elsewhere" message to donors
- **External dependency:** Requires buy-in and participation from partner community organizations
- **Process dependency:** Logistics (transportation, handoff) between Mary's Place warehouse and partner orgs

---

## Feature 8: Engagement Model & Next Steps (Meta Topic)

### Requirements
- Define what the pro bono team will produce for Mary's Place — prototype vs. concept document vs. fundable proposal *(Casey, ~min 21–22)*
- Deliverable should be useful for fundraising / "something we could shop" to potential funders *(Jason, ~min 22)*
- Include conceptual exploration beyond Jason's initial ideas — "probably cooler things than I'm thinking of right now" *(Jason, ~min 22)*
- Validate identified use cases back with Mary's Place via follow-up email *(Casey, ~min 50–51)*
- Conduct deeper follow-up interviews with subject-matter staff *(Lauren, ~min 51–52)*

### Decisions

**Decision: Deliverable format**
- Initial framing (~min 21–22): Casey offered options — prototype, concept with "enough meat on it," or additional ideas
- Jason's preference (~min 22): "A prototype would be really interesting... even a concept with enough meat on it... could be something we could shop"
- **Status: Tentative** — leaning toward prototype + concept hybrid; final scope not locked

**Decision: Combined scope vs. picking one problem area**
- Casey's recap (~min 49–50): Summarized both intake/journey and inventory/donations as the use case set; asked if anything was missing
- Jason + Mike (~min 51): "There's a good starter list" — accepted both problem areas as in-scope for exploration
- **Status: Agreed (for discovery phase)** — both problems remain on the table; eventual narrowing is a future decision

**Decision: Follow-up interviews approved**
- Lauren's request (~min 51–52): Asked for additional calls with a care coordinator (Feature #1 depth) and goods intake/distribution staff (Features #4–7 depth)
- Jason + Mike (~min 52): Both agreed
- **Status: Agreed**

### Action Items
- [ ] **Casey** — follow up via email with the consolidated list of use cases identified for Mary's Place to validate *(Casey, ~min 50–51)*
- [ ] **Casey / Lauren** — schedule follow-up call with a Mary's Place care coordinator (intake/journey deep dive) *(Lauren, ~min 51–52; Jason confirmed)*
- [ ] **Casey / Lauren** — schedule follow-up call with Mary's Place goods intake / distribution staff (inventory + donations deep dive) *(Lauren, ~min 51–52; Mike confirmed)*

### Open Questions
- Final scope of deliverable — prototype, concept document, fundable proposal, or all of the above?
- Which of the seven feature areas does the team prototype/concept against — pick one, or address several at a high level?
- Engagement timeline (60–90 days was floated by Casey at ~min 23 in a hypothetical framing)?
- Will Amazon Legal or other existing Mary's Place pro bono partners be looped in given their close relationship?
- Does the deliverable need IP/ownership clarity (the asylum chatbot is owned by the law firm, not Mary's Place — precedent worth flagging)?

### Dependencies & Connections
- **Informs all features (#1–#7):** Engagement scope decision determines which features advance to design/prototype
- **Precedent reference:** Prior asylum-chatbot engagement with Amazon Legal + law firm (~min 44–46) — proven model for Mary's Place pro bono AI work
- **Stack context:** Mary's Place is Microsoft/Copilot-grounded; not AWS-native — relevant for prototype tech choices *(Jason + Mike, ~min 48–49)*

---

## All Action Items (Consolidated)

**Assigned to Casey:**
- [ ] Follow up via email with the consolidated list of use cases for Mary's Place to validate

**Assigned to Casey / Lauren:**
- [ ] Schedule follow-up call with a Mary's Place care coordinator (intake/journey deep dive)
- [ ] Schedule follow-up call with Mary's Place goods intake / distribution staff (inventory + donations deep dive)

**Assigned to Mary's Place (Jason / Mike):**
- None — both confirmed availability for the follow-up calls but took no other commitments

---

## All Open Questions (Consolidated)

### Intake & Journey (Features #1–#3)
- What data sources feed the sequencing logic (existing case data, county HMIS, external)?
- How are "step durations" sourced — historical data, expert input, or both?
- How does the family interact with the agent — kiosk, mobile, web, staff-mediated?
- Should the estimated length-of-stay be shared with the family directly?
- How does the system handle re-prioritization mid-stay?
- Which specific 12–15 languages need to be supported on day one?
- What translation/LLM approach meets accuracy + trauma-informed tone requirements?
- Who validates linguistic and cultural appropriateness?
- How does the system handle low-resource languages with weaker AI translation?
- Is voice/audio input required, or text-only sufficient?
- Rebuild the existing SQL system, wrap it, or integrate alongside it?
- What is the HMIS integration interface (API, file drop, manual export)?
- What family-level data fields are shared across teams vs. kept private?
- HIPAA / county HMIS compliance constraints?
- Who owns and maintains the new data layer?

### Inventory & Supply Chain (Features #4–#7)
- What's the right unit of tracking — category, bin, item — without slowing intake?
- How is the inventory layer kept in sync with marketplace "shopping" by guests?
- Does food inventory live in the same system as durable goods?
- What's the data entry burden on warehouse staff, and what's acceptable?
- Can existing audit/valuation reports come from the new system?
- Hybrid request model: which requests go family-direct vs. staff-mediated?
- If a physical outreach/prevention marketplace is built, where does it live and who staffs it?
- How do outreach families access a physical marketplace given mobility barriers?
- What lead-time window is realistic for outreach staff to forecast move-in needs?
- How does the matching system coordinate with the "Make a Home" coordinator?
- Does the family-facing surface need multilingual day-one support?
- Who in the development team owns the wish-list generation surface?
- How is "need" quantified for a donor-facing ask (units, $, family-impact)?
- How does smart wish-list integrate with existing donor channels?
- How are donors notified when an ask is fulfilled to avoid over-supply?
- Different asks for individual vs. corporate donors?
- How is donor-facing language reconciled with the "don't signal your past gift was wasted" constraint?
- Which partner orgs are in scope for redistribution?
- Who at Mary's Place owns partner redistribution coordination?
- Disposition logic — auto-route by category, or staff decides item-by-item?
- Is there a regional/county hub model already operating that could host this network?
- How are partner-org needs surfaced and kept current?
- Legal/liability posture on transferring donated goods to third parties?

### Engagement (Feature #8)
- Final deliverable scope — prototype, concept doc, fundable proposal, or all?
- Which feature areas does the team prototype/concept against?
- Engagement timeline (60–90 days hypothetical)?
- Will Amazon Legal or other pro bono partners be looped in?
- Does the deliverable need IP/ownership clarity given the asylum chatbot precedent?
