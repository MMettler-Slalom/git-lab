# Opportunities — TPCi AR / PCEN

Identified opportunities across the onboarding notes, grouped by category. Each entry includes a description, potential value, potential cost/effort, and the systems and departments that would be involved. "Unknown" indicates the information wasn't stated in the source material.

---

## Open Questions

Items the source notes do not answer; recommend asking during follow-up conversations to size and prioritize.

### Sizing / Value Estimation
- **Most opportunities have no formal cost estimate.** Cost columns reflect qualitative directional language from the notes, not sized work.
- **Most opportunities have no ROI estimate.** Value columns reflect strategic framing from interviewees, not modeled returns.
- **Per-unit economics target** — Stefan says current per-unit is ~2x sustainable; specific target unit economics not stated.
- **Demand-planning financial upside** — "unlocks additional financial opportunities" — size not stated.
- **Event-merging revenue** — "millions in sales" referenced for tournament/event purchase merging; precise figure not given.
- **UK fleet target size** — "120 is hypothetical" per Joe; planned size unknown.
- **Hillman labor + parts savings potential** — current spend stated (~$115k/mo personnel, ~$2.1M/yr parts); achievable reduction not modeled.
- **DataDog projected cost** — ~$3.1M/yr for 1,800 machines is the current quote; achievable cost via negotiation unknown.
- **Digital ad network revenue potential** — Stefan said "huge potential value/upside" but never sized; second presentation was an action item.

### Sequencing / Dependencies
- **Priority ordering of opportunities** — Olga is waiting on leadership for top 1–2 priorities for the next two quarters.
- **Stefan's D2C priorities** — promised as an ACTION item; not yet shared in the notes.
- **PWA MVP+ priority list** — Phil/Alex/Stefan need a session to lock in groupings and priorities.
- **Order in which payment / email / OMS work should sequence relative to international expansion.**
- **Whether to do SF receipt migration first or wait for full AXP cutover** — both paths discussed.
- **Whether to scrap-and-rebuild PIM AR repo or extend the current structure** — two paths discussed; no decision.

### Decisions Outstanding
- **CyberSource vs. Adyen** — conversations happening in parallel; decision criteria not stated.
- **Whether DM is used standalone or as part of payment hardware swap.**
- **Tooling choice for IMS** — Oracle, Oracle+Fluent sync, Auger, or something else.
- **Whether VN client-side dev moves in-house, or only cloud dev** — Alex mentioned cloud-side may be more viable.
- **Whether to pursue VN M&A** — "likely not until AR teams are better integrated."
- **Whether Pigment can actually build planograms** — feasibility check pending.
- **Whether computer vision is worth the investment** — Rory skeptical; not yet decided.
- **Retailer-led restocking model** — needs retailer benefit definition before pursuit.
- **Hybrid merchandizer/tech model for UK** — viable approach unclear.
- **Whether to pursue Excel Marketing acquisition** — offer is out; status unknown.

### Owners
- **Owner of the AR roadmap** — Olga is consolidating but final ownership/decision authority not stated.
- **Owner of the IMS effort** — BizApps owning, specific lead within BizApps unnamed.
- **Owner of receipt-logic migration** (SF vs. REACT vs. TPCi Lambda).
- **Owner of digital ad network buildout.**
- **Owner of computer vision and software-based telemetry roadmap.**
- **Owner of OCM / change management for AR → PCEN merger.**
- **Owner of AR escalation framework definition** (Rory asked Holly to draft, but AR won't commit to ownership).
- **Owner of brand strategy across AR tiers.**

### Scope / Feasibility Unknowns
- **Whether VN can support different planograms / UI / firmware per machine group at the scale needed** — Alex believes yes via templates/groups/orgs, but feasibility for ~A/B testing scale unconfirmed.
- **How much VN i18n work is required** for UK/EU language and currency support.
- **How easily VML Confluence/Jira can be exported** — Phil heard it's hard, not sure why.
- **Whether NFC/QR/hashed-CC identity merging is legally permissible** — not yet explored.
- **DRI logic portability to CSDM** — claimed possible but not validated.
- **Whether retailers will accept attributed-commission asks** if AR splash content drives PCEN sales (Erica's concern).
- **Status of the JAWS/TPGI ADA corner-case issue** — "near complete" but lingering.

---

## Validation Recommended

Records where details are present but were inferred or framed beyond what the source explicitly states.

| Opportunity | Field(s) to Validate | Why |
|---|---|---|
| **Double the machine fleet** | "1,800 today + 2–3k approved additional locations" framed as a doubling | Source: "1800 machines today, 2-3k approved additional locations" — wording supports near-doubling; explicit "double" framing comes from a separate statement |
| **Per-unit economics "~2x sustainable"** | Cost framing | Stated by Stefan as a directional claim; not a formal financial model |
| **AR as fan acquisition funnel** | Departments listed | Marketing is implied across notes but not explicitly identified as an owner for this work |
| **International expansion** | Cost list is comprehensive but speculative | Notes touch on each item but full scope/cost unspecified |
| **Digital ad network** | "Huge value/upside" | Source quote from Stefan; not modeled |
| **Trainer Club loyalty redemption** | "3–5 years out" | Source: "is probably 3-5 years"; rough estimate, not a roadmap commitment |
| **BOPIS lift "~5%"** | Stated figure | Source: "BOPIS with AR is like a 5% lift to ecomm" — speaker did not show data |
| **Receipt opt-in ~30%** | Stated figure | Source: "around 30%, but would likely go down when adding a marketing opt-in" |
| **DRI move to CSDM** | "Potential" | Possibility, not committed direction |
| **CyberSource hardware option** | "Hardware option new" | Source: "Cybersource does have hardware now, may be an option" — early exploration |
| **Adyen as international solution** | Vendor under evaluation | Conversations happening in parallel with CSDM; no decision |
| **DataDog "designed for server farms"** | Cost framing | Source: "they are meant for server farms, aren't really designed for AR" — Joe's framing |
| **Hillman cost figures** (~$115k/mo, ~$2.1M/yr parts) | Confirm scope | Stated by Joe; scope (Hillman only? all field?) should be confirmed |
| **PWA team timeline (May/June handoff)** | "Short timeline" framing | Source: "Have a 6month PO with VML through May/June" — confirmed end date, but actual handoff sequencing not finalized |
| **Vendnovation M&A** | "Long-term" framing | Source: "Talk to Phil/Stefan about VN acquisition opportunities, but likely not until AR teams are better integrated" |
| **Computer vision ROI** | "Rory skeptical" framing | Source: Rory "not confident that the data from computer vision will really improve inventory count" — opinion stated |
| **PIM "two-person bottleneck"** | "James and Mike will be a bottleneck without more resources" | Source statement; not an org-confirmed capacity assessment |
| **AXP migration "2027 timeframe"** | Stated by Midori/Jen | Source: "2027 timeframe is realistic" — directional, not committed |
| **BR contract expires June 2027** | Confirmed in source | Stated by Erica |
| **Stefan's "doing it right and doing it big"** quote | Used as framing for international expansion not having a fixed timeline | Source: "Stefan is not working towards specific timelines or goals, he is trying to do it right and do it big" |
| **"6 different ops areas in AR"** | Stated structure | Source line 1674 confirms; ownership across them is layered (Rory has 4, Joe has 1, Zach has 1) |
| **Map of opportunities to "departments involved"** | Inferred for most | Departments listed reflect best-guess based on system/topic ownership; not all are explicitly named as participants |
| **System dependencies between opportunities** | Inferred | Cross-opportunity dependencies (e.g., email move enables PII removal which enables UK) are sequenced from context, not stated explicitly |
| **Smaller machine form factor** | "Told to stop" | Source: Zach "started working on a new smaller machine, then was told to stop"; no current path forward stated |
| **Excel Marketing acquisition status** | "Offer out" | Source confirms; outcome unknown |
| **Hillman 1:500 ratio** | Stated | Joe Stutzman's stat for break/fix |
| **AR alerts ~32–34k/month** | Stated | Joe Stutzman's stat |
| **~650 field visits/month** | Stated | Joe Stutzman's stat |
| **T-ROC mgmt headcount** | "~10–12" | Source has both 10 and 12 in different places |
| **UK CS sue / refund issue** | Stated by Holly | "Got sued in UK because refunds weren't happening fast enough" — confirm details with Legal |

---

## 1. Revenue & Business Growth

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **Double the machine fleet** | 1,800 today + 2–3k approved additional locations; per-unit income would drop but stay profitable | Path to becoming largest TCG distribution channel in the world (only ~20% market penetration today); $223M AR revenue target this year, $60M already at time of notes | Per-unit economics currently ~2x sustainable (need to be reduced first); manufacturing capacity, field-ops scaling, vendor capacity | VN, REACT PWA, Manufacturing supply chain, NetOps tooling | AR (Stefan), Manufacturing (Zach), NetOps (Joe), Merchandizing/SalesOps (Rory), Sales |
| **Destination machines (Pokemon Center)** | Premium, elevated vending experience differentiated from cards-only TCG machines | Increased purchasing power for merch ordering → margin lift; new fan acquisition surface; potential digital signage / event tie-ins | More expensive machines, harder to support, different shelf configs cause installer confusion, "more to break" risk | REACT PWA (per-group UI), VN groups, PIM (channel records) | AR, Merchandizing, Manufacturing, Content (Erica/Matt A), Legal |
| **AR as fan acquisition funnel** | Use AR as on-ramp into PCEN, app, Trainer Club, tournaments | "Doubling the fanbase" — strategic brand engagement; ties to combined email/comms strategy | Requires identity unification (CDP / EP / PTC), combined email platform | CDP, AXP/SF, EP, REACT PWA, PTC | CDP/Analytics (Simon), Email (Midori/Jen), AR, Marketing |
| **Tier 1 Destination PC GTM plan** | Cross-company collective go-to-market plan for destination expansion | Aligns brand strategy across tiers; clarifies channel/product strategy | Requires cross-functional alignment that doesn't exist today | unknown | AR (Stefan), Marketing, Sales, Legal, PCEN |
| **International expansion (UK / EU / AU)** | 50 UK units on PO; world certifications in progress | Massive upside (international sales pressure is significant); Stefan working toward UK | International payment stack, GDPR work, VN i18n (currency/language), CS hours + local #, multi-vendor field ops, parts storage, hardware certification | VN, payments (DataCap → CyberSource/Adyen), AXP/SF email, Mfg cert, CS tooling | AR, Manufacturing, NetOps, Merchandizing, CS, Legal, BizApps |
| **Increase AR spread without cannibalizing wholesale** | More machine locations even if slight wholesale impact — same profitability | Acquisition + reach gains | Vendor/field-ops scaling | VN, field-ops vendors | AR, Sales |

---

## 2. New Revenue Streams / Use Cases

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **Digital advertising network on machines** | CMS-driven ads + QR/UTM tracking; first time anyone internal is offering a platform for marketing | "Huge potential value/upside" per Stefan | Tagging infrastructure may not be robust enough; regulation around marketing to kids vs consumer; lots to sort out | Bloomreach, REACT PWA, QuantumMetric, CDP | AR (Stefan), Marketing, Legal (Amy/Rose), CDP/Analytics |
| **Info kiosks / prize support / tournament distribution** | Same machines repurposed for non-commerce activities (machines too slow for retail/event commerce, but fine for info/prizes) | New utility from existing hardware; tournament + event experience uplift | Software work to support modes; some operational coordination | REACT PWA, VN per-group UI | AR Tech, Events, AR |
| **Pokestop / Pokemon GO integration** | Use machine network as Pokestops or other Niantic-style anchor points | Brand engagement, foot traffic, secondary use of fleet | Integration work with external partner | REACT PWA, VN | AR, Partner Mgmt |
| **Trainer Club loyalty point redemption at machines** | Spend loyalty points via AR | Strategic loyalty value, drives Trainer Club engagement | Probably 3–5 years out per Stefan | PTC, REACT PWA, VN, payments | AR, PCEN Accounts/Loyalty |
| **Combined email/comms strategy** | Branded comms tied to AR customer base; receipts as marketing entry point | Strategic — enables brand engagement at scale across tiers | Need email platform consolidation (SF or AXP), opt-in flow updates, language transparency | SF/AXP, MailGun, CDP, VN | Email (Midori/Jen), CDP (Simon), Legal, AR |
| **BOPIS via AR** | Buy online, pick up at AR machine | ~5% lift to ecom — "important but way less so than broadening AR reach" | OMS connection (Fluent ↔ AR), reservation flow | Fluent, VN, EP | AR, PCEN, BizApps |
| **Reserve inventory for Trainer Club / tournaments** | Hold stock for special events/audiences | Solves Worlds-style stockout-on-PCEN problem; strategic | IMS work; rules engine | New IMS (Oracle+Fluent or other), VN | AR, PCEN, BizApps |

---

## 3. Customer Data & Personalization

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **Get AR customer data into CDP** | Easiest via SF sending receipts → CDP; harder path is full EP customer account | "We definitely want to get the info into CDP"; enables personalization, paid media, marketing | Only ~30% of AR customers opt in to receipt; would likely drop with marketing opt-in; requires email migration | CDP, SF/AXP, VN, EP | CDP (Simon), Email, AR |
| **Customer transaction-to-identity mapping** | Tie machine transactions to customer accounts via login, NFC, QR, hashed CC, or EP guest checkout | Combine transactions across visits; unlock event merging (millions in sales potential) | Different payment processing currently breaks hashed-CC merging; legal implications of CC tokens for ID mapping not yet explored | VN, CDP, EP, payments | CDP, Legal, AR Tech, BizApps |
| **EP guest checkout for all AR purchases** | Make every AR purchase flow through EP | Auto-flows data to CDP; customer account benefits | Significant integration work | EP, VN, REACT PWA | PCEN, AR Tech |
| **Instrument AR machine interactions** | Rohit working to get tracking on machines | Visibility into in-machine behavior; conversion analytics | Tagging build-out | QuantumMetric, REACT PWA | Analytics (Rohit/Simon) |
| **AR landing page on PCEN** | Direct people to PCEN AR landing | Funnel into broader brand experience | Standard web work | PCEN web, BR | PCEN, Marketing |

---

## 4. Payments

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **Move payments into TPCi-controlled ecosystem** | Reduces PCI compliance burden on software vendors so they can scale | Unblocks software vendor scale; foundational for international | Significant tech and contracting work; choice between CyberSource and Adyen | DataCap → CyberSource/Adyen, VN, Ingenico, Treasury systems | AR Tech, Treasury (Bryan), Steve Yin, BizApps |
| **Adyen end-to-end international payments** | One provider for many countries | Fast path to multi-country support | Vendor relationship + integration; in conversation now | Adyen, VN | AR, Treasury, Legal |
| **CyberSource card-present + hardware** | Use CSDM as fraud + potentially full payment stack including hardware | TPCi may be big enough to dictate certified hardware; consolidates fraud + payments | No card-present support yet; hardware option new; needs demo/Q&A | CyberSource, Ingenico-equivalent, VN | AR Tech, Treasury, Bizapps |
| **Decision Manager (DM) for fraud/DRI alone** | Use CSDM standalone (separate from payment hardware) | Could handle DRI as well as fraud; flexibility | Classic CC fraud is currently small so ROI for fraud-only is unclear | CyberSource DM, VN, AWS Lambda (current DRI) | AR Tech, Treasury, NetOps |
| **Partial capture / refund / authorize-vs-capture support** | Authorize one amount, capture different amount, partial refund at machine | Required for many real machine scenarios | Demo/Q&A on vendor capabilities | Payment stack | AR Tech, Treasury, CS |

---

## 5. Email / Communications

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **Move email/comms to TPCi-controlled (SF first, AXP long-term)** | Remove VN from receipt-email flow; eventually all email on AXP | Removes PII/GDPR scope from VN (huge for international); enables marketing/CDP; brand consistency; 24/7/365 NOC support | Receipt-template logic needs to move to SF or REACT (currently VN builds it); need PII scrubbing in logs; AXP migration realistic ~2027; RFP needed for global usage | VN, SF, AXP, MailGun, CDP | Email (Midori/Jen), AR Tech, CDP, Legal |
| **AR-specific receipt email program in SF** | Either add AR flag to existing order-confirmation API or build net-new program | Faster path than full AXP migration | SF capacity, template work | SF, VN | Email, AR Tech |
| **PII removal from VN entirely** | Remove TPCi PII from Vendnovation systems | GDPR-ready; international expansion enabler | All comms must move first; data model changes | VN, SF/AXP, CDP | AR Tech, Legal, Email |

---

## 6. Order Management / Inventory / Supply Chain

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **Bring order/transaction data into Fluent** | "No one wants to own this, but it unlocks demand planning which unlocks additional financial opportunities" | Demand planning → financial gains; unifies sales channels | Heavy integration; ownership unclear | Fluent, VN, Mulesoft | BizApps, AR, PCEN |
| **Dedicated IMS for AR (between Oracle and Fluent)** | Inventory management across Ecom, Events, AR; prevents PCEN "eating" AR stock | Solves Worlds-stockout-style issue; foundational for reservations/events; significant operational value | Big project; contentious between teams; needs requirements; not Oracle alone | New IMS, Oracle, Fluent, VN, Auger (candidate) | BizApps (Bala/Deepika), AR (Alan/Ashley), PCEN |
| **Oracle GOP (Global Order Promising)** | Allocation rules and safety-stock by business line | Solves cross-channel inventory conflicts | Oracle config, demo + decision still pending | Oracle, Fluent | BizApps |
| **Auger (AI supply-chain stitching)** | Stitch multiple systems/spreadsheets, automate ordering/issue surfacing | Holistic supply-chain view, automation, human review escalation | Vendor evaluation; doesn't have to be Auger specifically | Auger or equivalent, Oracle, Fluent, VN | BizApps, AR Merch, Supply Chain |
| **OMS for AR (machine-as-customer model)** | Machines become "customers" — orders sent to merchandizers; vendor "ships" to machine | Enables true multi-vendor merchandizing; standardizes ordering; supports vendor-agnostic model | New process + system definition; VN holds this info today | Fluent/Oracle, VN, SF Kiosk 360 | AR Merch (Rory), BizApps, NetOps |
| **Virtual warehouses for merchandizing vendors** | Today T-ROC inventory treated as one big warehouse | More accurate inventory; supports multi-warehouse | IMS work | IMS, Oracle/Fluent | BizApps, AR Merch |
| **Demand planning tool** | CELA bringing on; AR involvement TBD | Better forecasting; dynamic replenishment | Need to understand AR-specific needs | New CELA tool, AR data feeds | CELA, AR, BizApps |
| **Dynamic replenishment** (replacing static per-machine) | Driven by business logic (revenue, actual demand) instead of fixed intervals | Better inventory efficiency; closer to 50% wholesale margin goal | Algorithmic + ops change; vendor process change | VN, IMS, T-ROC tooling | AR Merch (Rory), BizApps |
| **Route management tech (T-ROC proposing)** | Optimize merchandizer routes | T-ROC asking TPCi to invest | Cost + commitment to T-ROC stack | unknown | AR Merch, BizApps |
| **Transportation routing licensing** | T-ROC licensing routing software to vendors | unknown | unknown | unknown | AR Merch |

---

## 7. Vendor Strategy & Field Operations

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **Multi-vendor merchandizing model** | Decouple from T-ROC monolith; standardize so vendors are interchangeable | Reduces risk of losing/gaining a vendor; opens international flexibility | Rory says today's model has "too many hooks" — heavy lift; need OMS + work-order system first | SF Kiosk 360, OMS/IMS | AR Merch (Rory), NetOps, BizApps |
| **Retailer-led restocking model** | Have major retailers stock/restock AR machines (Hillman still does break/fix) | Machines largely live in a few major retailers — attractive option | Need to define benefit for retailer; significant model change | VN, OMS | AR Merch, Sales, Legal |
| **Hybrid merchandizer/tech for UK** | Combined role for UK ~120 machines | Cost-efficient for small fleet; could cover all UK with 1–2 people | No existing model; needs training | LMS, SF | AR Merch, NetOps, HR |
| **Uber/DoorDash-style on-demand merchandizing** | Same drivers could pick up product and deliver to machine | Massive flexibility | Untested model; integration work | OMS, partner integration | AR Merch |
| **Excel Marketing acquisition** | TPCi has offer out to acquire; handles distribution/merch for brands like Target | New distribution + merch capability | Acquisition cost; integration | unknown | Leon's team, Legal, AR Merch |
| **Vendnovation M&A** | Acquire VN long-term once AR teams are better integrated | Full control of platform | Major M&A; not immediate | VN | AR (Stefan), Phil, Legal |
| **In-house client-side dev (PWA team)** | Move PWA dev from VML to ~2 devs + architect on Kevin's team | Reduce VML dependency; tighter integration with PCEN | Short timeline to staff before VML contract ends (May/June); hiring + onboarding overhead; risk of slipping | REACT PWA, VN | CELA (Kevin, Liz, Phil), AR Tech (Alex) |
| **In-house VN cloud dev/management** | Move VN cloud-side work in-house (more familiar territory for CELA) | More viable than client-side per some perspectives | Significant project | TPCi Cloud, VN | AR Tech, CELA DevOps |
| **Reduce vendor count overall** | Strategic vendor consolidation | Reduces vendor mgmt overhead, clarifies ownership | Contracting, transitions | All vendor systems | AR, PCEN, BizApps, Legal |
| **Hold field techs accountable** | SF + Kiosk 360 with diagnosis-required work orders | Reduce wasteful parts orders (~$2.1M/yr parts, much RMA'd as fine); reduce Hillman labor (~$115k/mo); fix Hillman's 15-min-visit incentive misalignment | SF Kiosk 360 rollout; LMS; change mgmt | SF Kiosk 360, LMS, Zendesk (replace) | NetOps (Joe), AR Merch, Manufacturing (Zach) |
| **Multi-vendor SF setup from the get-go** | Salesforce configured for multiple service vendors | Future-proof for UK/international + multi-vendor model | SF config investment | SF Kiosk 360 | NetOps, Lisa Pappas |

---

## 8. Tech / Software Modernization

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **PIM multi-channel re-architecture** | Different validation/export rules for different systems; AR as proper channel rather than separate repo | Eliminates manual AR product entry (every 6–8 weeks); supports international planograms; data cascading; foundation for scale | James/Mike are bottleneck; PIM discovery work needed; "enabler" initiative in intake | Enterworks PIM, Mulesoft, VN, EP | PIM (James/Mike), AR (Alan), Mulesoft (Olga), BizApps |
| **Automatic Bloomreach content push to PWA** | Remove manual BR build step | Matt A shouldn't be triggering BR builds; foundational scalability; in PWA MVP+ backlog for UK | Tech build | BR, REACT PWA | Content (Matt A, Erica), AR Tech, CELA Dev |
| **Bloomreach replacement evaluation** | Contract expires June 2027; Erica evaluating search/browse first | Could improve cost/capability | Vendor selection + migration | BR replacement | Content (Erica), PCEN, AR |
| **Telemetry → Salesforce via Mulesoft (replacing Zendesk)** | Drive field repairs from SF instead of 1:1 Zendesk tickets | Reduces alert fatigue (~32–34k alerts/mo today); proper enterprise tooling | Mulesoft + SF + Zendesk decommission | VN, Mulesoft, SF, Zendesk | NetOps, Mulesoft (Olga), AR Tech |
| **Mobile app for managing field repairs** | Native app for field techs on Kiosk 360 platform | Faster field operations | App dev + LMS work | SF Kiosk 360, LMS | NetOps, CELA Dev |
| **Computer vision for inventory/theft** | Software-based inventory tracking + theft mitigation | Reduces hardware sensors; better inventory accuracy; theft mitigation | Big tech investment; Rory skeptical of ROI | Machine HW, VN, IMS | AR Tech, Manufacturing, AR Merch |
| **Move from hardware sensors to software compute** | Backlog item at VN side | Lower cost, more flexible | Significant dev work | Machine HW, VN | AR Tech, Manufacturing |
| **Standardize integration governance framework** | Process + framework for integrations | Reduces fragmentation | Process work | All integrations | Mulesoft, BizApps, PCEN/AR leadership |
| **Move Airtable data to Databricks** | Production/slot/machine data into proper data platform | Better reporting; fewer "holes" in production data | Migration; tooling | Airtable, Databricks, PIM | Olga, Zach, BizApps |
| **Per-machine-group UI variants on PWA** | New architecture allows different UIs per machine group (geos, tiers, A/B) | Enables targeted content + experiences | Groups must be managed (today added manually); attribute-based grouping wishlist | VN, REACT PWA | AR Tech, Content, Marketing |
| **PWA MVP+ backlog (post-pilot)** | Security items, BR auto-push, other enhancements | "Nothing super critical" but valued | Newly-formed CELA team capacity | REACT PWA | CELA Dev (Kevin), AR Tech, Phil |
| **Pen testing completion (RSI)** | 3–6 weeks once kicked off | Security assurance for machine SW | Cost; resource availability | Machine SW, VN backend (separate) | Phil, Alex, InfoSec |

---

## 9. Customer Service

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **Chat-based AR support** | Push to chat over phone | Faster, less dropped calls/requests; better agent satisfaction (AR customers extremely hostile) | Tooling + retraining | Zendesk/SF, ModSquad | CS (Holly), ModSquad |
| **AR escalation framework (PCCS-style)** | Define escalation issues + owners for AR | Currently Holly resorts to texting Stefan; clear ownership unlocks ops | Cross-team commitment (hard to get today) | unknown | CS, AR leadership |
| **Forecasting data from AR to CS** | Give CS visibility into upcoming machine installs/scale | Pre-emptive staffing; avoid missing ~50% of calls at launch | Reporting work | AR reporting, CS planning | AR Bizops (Steve), CS |
| **CS access to better customer lookup in VN** | Today CS uses Ctrl-F scrolling; can't look up card/email properly | Faster resolution; fraud support | VN UI changes or new tooling | VN, CS tools | CS, AR Tech |
| **Tech-issue escalation pathway from CS to AR** | E.g., "50 machines in Seattle screens aren't working" — no current path | Faster outage detection/response | Process + Kiosk 360 integration | SF Kiosk 360, CS | CS, NetOps |
| **UK CS readiness** | Hours change for UK, local #, international Zendesk form, legal policies | Legally required for UK launch (TPCi already sued in UK over refunds) | ModSquad ramp + tooling + legal | Zendesk, ModSquad, AXP | CS, Legal, AR |
| **QR-code on machine for support number** | Replace phone-number hardware add-on with QR code | Cheaper, more flexible | Legal review | Machine UI, CS systems | CS, Legal, AR Tech |
| **Data deletion process** | Currently no defined process for customer data deletion requests | GDPR/legal compliance | Process + tech work | VN, CDP | Legal, CS, AR Tech |

---

## 10. Manufacturing & Hardware

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **NetOps → Manufacturing feedback loop** | Bring Zach into break/fix loop and design conversations | Improved part design; reduces $2.1M/yr parts waste; reduces "embarrassing" oversized parts orders | Process change | SF Kiosk 360, NetOps tooling | Manufacturing (Zach), NetOps (Joe) |
| **Standards / train-the-trainer / LMS for field** | Better field training; documented common issues (top ~10 issues cover most tickets) | Reduces alert fatigue, parts waste, ticket-monkey perception; foundational for international ramp | LMS investment (already contracted); content creation | LMS, SF Kiosk 360 | NetOps, Manufacturing, Lisa Pappas |
| **Skills/process opportunity assessment for AR** | Holistic assessment of skill gaps and process maturity | Identifies real org gaps; right roles for Zach and others | Consulting/discovery cost | unknown | AR leadership, HR |
| **International machine certification (UK/EU/AU)** | All three world certs being done in parallel with Flextronics builds | Unlocks international expansion at once | Months instead of weeks without proper support; need on-call SME | Machine HW | Manufacturing (Zach), VN |
| **UK parts warehousing / storage** | Need permanent storage solution for 50 UK units sitting in holding | Avoid double-shipping; ready when deployment plan locks in | RFP + logistics planning | unknown | Manufacturing, AR Merch |
| **Smaller machine form factor** | Zach started one, then told to stop | New use cases; lower cost; unclear strategic fit | Design + tooling | Machine HW | Manufacturing, AR leadership |
| **Reduce machine variant fragmentation** | New machine has different front door = duplicate part SKUs; needs management | Cleaner inventory + service | Process + parts tracking | PIM, Airtable, IMS | Manufacturing, NetOps |

---

## 11. Monitoring & Operations

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **DataDog NOC POC** | Going to pilot; provides insights VN alerts can't (CC machine, cables unplugged, exterior lights, board offline) | More actionable monitoring than Zendesk; both Joe and Alex benefit | ~$3.1M/yr for 1,800 machines — designed for server farms; expensive; data usage on Verizon plan | DataDog, machine fleet, Verizon | NetOps (Joe), AR Tech (Alex) |
| **Replace Zendesk with enterprise tool** | Zendesk has 1:1 ticket:alert mapping → fatigue | Reduces ~32–34k alerts/mo to actionable subset | New tool selection + migration; ops overhead | Zendesk → SF Kiosk 360 or other | NetOps, CS |
| **Eliminate non-actionable alerts** | Many alerts trigger auto-monitor stuff techs don't need to see | Cuts ticket volume meaningfully | Triage rules; alert tuning | Zendesk/SF, VN telemetry | NetOps |

---

## 12. Process / Organization / Governance

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **Change management for AR → PCEN merger** | "Potential need for a major change management effort to guide this merger" | Critical for integrating AR maturity into PCEN | OCM resourcing | n/a (process) | AR, PCEN, HR, Leadership |
| **Clear decision-making framework / ownership for AR** | "Need a clear decision-making framework/operating model and ownership so people know who truly OWNS decisions" | Removes Stefan/Holly as default escalation; unlocks ops | Leadership alignment, governance | n/a (process) | AR leadership, PCEN, Cindy |
| **Submit AR initiatives through CELA Intake** | Help define priorities/epics/initiatives across sub-teams | Coordinates roadmap; reduces ad-hoc work | Discovery time with each AR sub-team | Jira, Intake | Olga, CELA leadership, AR sub-team leads |
| **Define AR roadmap aligned with CELA + resourcing** | Olga consolidating; needs leadership's top 1–2 priorities | Aligned execution post-reorg | Leadership time | Jira | Olga, Liz, Cindy, Stefan |
| **PWA TPM/SO assignment (Phil Shen)** | Stand up PWA team in PCEN structure | Mirrors Mulesoft/DevOps team model | Phil's bandwidth; team formation | Jira, PWA stack | Liz, Phil, Kevin |
| **Embed TPCi person in Vendnovation team** | Reduce VN bottleneck; gain insight | Slow progress historically; adds overhead VN side | Coordination cost | VN | AR Tech, VN |
| **AR Business Manager role (Steve Yin)** | Vendor accountability + reporting standardization | Takes vendor mgmt off tech folks; transparency into AR health | New headcount + ramp | AR reporting | AR, Steve Yin |
| **Reduce vendor headcount visibility gap** | Many TPCi-funded vendor staff run aspects of the business invisibly | Leadership clarity; risk reduction | Discovery + reporting | n/a | AR leadership, HR, Finance |
| **Architect hire for Kevin's team** | Strategic/big-picture role to weigh in on bring-in-house decisions | Unblocks Kevin's bandwidth; better tech direction | Hiring cost | n/a | CELA (Cindy, Kevin) |
| **Brand strategy alignment across AR unit tiers** | Which products in which tier; who manages channel strategy | Foundational for destination expansion | Cross-functional alignment | n/a | AR, Marketing, PCEN |
| **VML → CELA PWA handoff with overlap** | Get overlap time with VML to do clean handoff | Avoids losing institutional knowledge | Contract extension cost (6mo PO ends May/June) | VML Confluence/Jira → TPCi | CELA Dev, AR Tech, Phil |
| **Confluence/Jira export from VML** | Move PWA documentation in-house | Knowledge retention | "Phil heard this isn't easy to do" — TBD effort | VML systems → TPCi | CELA Dev, Phil |

---

## 13. Cross-Cutting / Misc

| Opportunity | Description | Potential Value | Potential Costs | Systems Involved | Departments Involved |
|---|---|---|---|---|---|
| **SMS enablement** | Currently blocked by martech script over-collection vs. least-data policy | Marketing channel expansion | InfoSec approval; script scope cleanup | CDP, martech scripts | CDP (Simon), InfoSec, Marketing |
| **Identify and automate/remove manual processes** | Stated overarching opportunity | Operating leverage at scale | Per-process discovery/automation | Multiple | All teams |
| **AR-specific UK legal policies** | TPCi already sued in UK over refunds; refund SLAs, data deletion, loitering, etc. | Legal protection; readiness for UK launch | Legal time + policy publication | n/a (policy) | Legal, AR, CS |
| **Media/PR escalation pathway** | No current pathway for issues like viral incidents or non-TPCi machines selling Pokemon | Brand/PR protection | Process definition | n/a | AR, PR, Legal, CS |

