# Systems — TPCi AR / PCEN

Tech systems referenced across the onboarding meeting notes. "Unknown" indicates the information was not stated in source material.

---

## Open Questions

Items the source notes do not answer; recommend asking during follow-up conversations.

### System Identity / Meaning
- **EP** — used multiple times as the PCEN ecom platform (e.g., "EP guest checkout"). Full name / vendor / version not stated.
- **PIMDAM** — referenced once ("product content including images comes from PIM and PIMDAM"). Full name, vendor, and whether it is a separate product from Enterworks PIM is unclear.
- **PC Hub** — described as a legacy product data source feeding PIM; replacement discussion mentions a PLM tool. Vendor, current scope, and replacement candidate are not specified.
- **CDP** — the actual CDP product/vendor is never named (Simon owns it; many feeds in/out).
- **LMS** — described as "a vendor has been contracted to do this" — vendor name and selected product not given.
- **Demand Planning Tool** — CELA bringing it on; product/vendor not stated.
- **Dedicated IMS** — BizApps owning; tool not yet selected.
- **Cybersecurity testing vendor for VN backend** — VN was contracting a third party for backend (vs. TPCi-contracted RSI for machine software). Vendor name not stated.

### Owners / Contacts
- TPCi-side owner of **DataDog** beyond Joe Stutzman.
- Owner / TPCi POC for **Adyen** and **CyberSource** evaluations.
- Vendor-side contacts at Vendnovation, VML/Gorilla, TPGI, RSI, T-ROC, Hillman, Brendamoor, Flextronics, DragonMan/CDI, ModSquad, MailGun, DataDog.
- Owner of **Verizon data plan** contract.
- Owner of **Ingenico** device fleet.
- Owner of **CC token storage** in VN (referenced as "being solutioned to remove" — current solutioner not named).
- TPCi-side owner of **Bloomreach** beyond Erica/Matt A — who runs the BR build process today?
- TPCi-side owner of **Fluent** and **Oracle** (BizApps is involved in IMS work but the system owners are not stated).
- Owner of the **PC Hub → PIM** flow.
- Owner of the **Airtable** instance(s); who has admin rights.

### Capabilities / Status
- **VN cybersecurity contracting** — Alex was "out of the loop"; current contracting status unclear.
- **Pen-test (RSI) timeline** — proposal SoW arrived 4/2/26 with 3–6 week timeline TBD; current state unconfirmed.
- **DataDog pricing** — vendor "may be open to a better pricing model"; final pricing unconfirmed.
- **VN multi-region/multi-tenant capability** — Alex referenced "orgs" as a possible regionalization mechanism but said it depends on cross-org data/code sharing; actual feasibility unconfirmed.
- **VN i18n** — full scope of language/currency work to support UK/EU not estimated.
- **PWA MVP+ backlog** — Phil/Alex/Stefan need a session to lock in groupings/priorities; current contents and priorities not finalized.
- **Whether Pigment can build planograms** — explicitly called out as "need to check if this is actually possible."
- **Airtable → Databricks migration** — direction stated, timeline and owner unknown.
- **PIM multi-channel "enabler" initiative** — in intake; resourcing/timeline unknown.
- **Receipt logic migration** — VN builds receipts today; whether the logic moves to SF, REACT, or a TPCi Lambda is undecided.
- **PTC Login** — feed into CDP is "planned" but timeline unknown.
- **Qualtrics → CDP** feed — "planned" with no timeline.
- **SMS enablement** — blocked by martech script scope; current InfoSec status unclear.
- **JAWS/TPGI status** — "one remaining corner case issue" — current state unconfirmed.

---

## Validation Recommended

Records where details are present but were inferred rather than directly stated.

| System | Field(s) to Validate | Why |
|---|---|---|
| **Vendnovation (VN)** | Description of VN as "doesn't deal with payment today" | Source clarifies this but also notes VN does hold CC tokens (being solutioned to remove). Owners listing includes inferred TPCi-side roles |
| **REACT PWA** | "Future owners" list (Kevin, Erica, Matt A, architect) | Architect not yet hired; Erica/Matt A AR vs. CELA placement is inferred |
| **Bloomreach** | "Erica evaluating replacements" | Stated; but who else is involved in the evaluation is unknown |
| **Enterworks (PIM)** | "Two-person bottleneck" framing | Reflects James's stated concern, not a formal capacity statement |
| **Airtable owners** | Aileen, Alan N, Olga, Zach listed as users | Multiple people use it; formal owner not stated |
| **Mulesoft "Mudbray"** | "Recently merged with PCEN Mulesoft" | Stated by Kevin; merge details/owner uncertain |
| **AWS Lambda (DRI)** | "Owned by Vendnovation (Alex's team)" | Vendnovation-hosted per source ("AWS lambda in their cloud"); Alex's team association is via TPCi-side relationship, not direct ownership |
| **TPCi Cloud** | "VML cloud stuff has been moved into TPCi cloud" | Confirmed; owner ("TPCi DevOps") is general — specific team unnamed |
| **DataCap / Chase / Ingenico owners** | "Bryan (Treasury oversight); Steve Yin (incoming)" | Bryan name itself uncertain in source; Steve Yin's ownership is upcoming, not current |
| **CyberSource / Adyen owners** | "Under evaluation; Alex Doumani, Stefan" | Stefan is driving; Alex was in the conversation. Formal evaluation owner not named |
| **Salesforce — Kiosk 360 owners** | Olga listed as "likely TPM" | Source says "Olga likely going to own this" for SalesOps SF — generalized to Kiosk 360 |
| **LMS** | "Vendor contracted (unnamed); sponsor unknown" | Lisa says "a vendor has been contracted to do this" — vendor not named; sponsoring team uncertain |
| **CS QR Code Form** | "~50% of inbound CS volume" | Source: "About half come in through form, half through phone" |
| **AXP / MailGun owners** | Midori, Jen | Both names appear in the SF Email meeting; AXP-specific ownership inferred |
| **CDP** | Owner = Simon Wittingham; Rohit | Simon owns CDP/Email/Analytics; CDP product itself unnamed |
| **QuantumMetric owner** | "Rohit (likely); PWA team" | Inferred from analytics ownership; not explicit |
| **Pen Testing (RSI)** | Owners listed include InfoSec, VN | Source says VN was contracting a separate third party for backend; RSI scope for machine SW is TPCi-side. Final owner mapping inferred |
| **DRI logic** | "Potential move to CyberSource Decision Manager" | Stated as possible direction, not committed |
| **Hardware integrations** | "Zach (hardware); Alex (integration)" | Inferred division of responsibility based on roles |
| **TPCi Jira owners** | Liz, Phil Shen, Olga | Multiple people drive AR-into-Jira migration; system owner not explicit |
| **VML Confluence/Jira migration** | "Hard to migrate; not sure why" per Phil | Difficulty stated but not specified |
| **Intake (CELA)** | Owner = Olga, CELA leadership | Olga drives AR intake submissions; broader intake process owner unstated |
| **EP** | "PCEN ecommerce platform; potential AR guest checkout path" | Full system identity unknown — only referenced by acronym |
| **PIMDAM** | "Product digital asset / image management" | Inferred from "PIM and PIMDAM" reference; full identity unknown |
| **PC Hub** | "Legacy product data source feeding PIM" | Limited context in source; replacement direction (PLM) noted |

---

## Core AR Platform & Customer-Facing

| System | Role / Function | Owner(s) / Workers | Integrated / Connected With |
|---|---|---|---|
| **Vendnovation (VN)** | Core AR machine platform: backend, REACT app delivery, planograms ("templates"), product DB, DRI logic (AWS Lambda), telemetry generation, receipt generation, machine grouping/orgs | Vendor: Vendnovation (~8 client-side devs funded by Stefan, 2 leads — one backend, one client). TPCi side: Alex Doumani (tech lead), Phil Shen (intake/JIRA migration), Kevin O'Neil (incoming dev mgmt) | DataCap (payments), Chase PaymentTech, PIM via S3 (product data pull), Airtable (slot/machine data), Zendesk (telemetry tickets), Salesforce (planned, via Mulesoft), Bloomreach (content), PWA/REACT app, AWS Lambda (DRI) |
| **REACT PWA** (new) | Customer-facing UI on machines; replaces "Vector"; supports BR integration; supports per-machine-group UI variants | Built by VML/Gorilla. Future owners: Kevin O'Neil (dev), Erica Matsuda (content PO on Yannick's team), Matt Alspaugh (content SME). Architect being hired | Vendnovation (delivery/groups), Bloomreach (content, currently via manual build), PIM/PIMDAM (product data/images via S3), QuantumMetric (analytics), JAWS/TPGI (accessibility) |
| **Vector (legacy app)** | Prior customer-facing machine app being replaced by PWA | unknown | Vendnovation |
| **JAWS (TPGI)** | ADA accessibility — headphone keypad voice navigation on machines | Vendor: TPGI | REACT PWA |
| **Attract Screen** | Pre-interaction display content on machine (top banner, bottom banner, product scroll) | Erica Matsuda, Matt Alspaugh | Bloomreach |

## Content / Product Data

| System | Role / Function | Owner(s) / Workers | Integrated / Connected With |
|---|---|---|---|
| **Bloomreach (BR)** | CMS for AR (attract screens, banners, cart/checkout text); also PCEN search/browse | Erica Matsuda, Matt Alspaugh (content); Erica evaluating replacements (contract expires June 2027) | REACT PWA (manual build push today), PCEN web |
| **Enterworks (PIM)** | Product master data; AR product attributes; channel-specific validation (future state) | James, Mike (engineering, two-person bottleneck); Alan N (AR product entry — manual) | PC Hub, Oracle, user input (sources); Mulesoft, REACT PWA (via S3), VN, EP (PCEN ecom), Airtable (planned) |
| **PIMDAM** | Product digital asset / image management | unknown | PIM, REACT PWA |
| **PC Hub** | Legacy product data source feeding PIM | unknown | PIM |
| **Airtable** | Machine/slot/planogram data, machine group management, warehouse mapping, production data | Aileen (warehouse mapping), Alan N (planograms), Olga (production data — incomplete), Zach Dizard (wants involvement) | VN (planned PIM → Airtable → VN path), Databricks (migration target) |
| **Databricks** | Business-centric data lake | unknown | Airtable (planned migration), CDP feeds |
| **Pigment** | Possible planogram-building tool (feasibility TBD) | unknown | Would replace/augment Airtable + VN planogram flow |

## Integration / Middleware

| System | Role / Function | Owner(s) / Workers | Integrated / Connected With |
|---|---|---|---|
| **Mulesoft — "Mudbray" (AR-aligned)** | Integration layer feeding AR; consolidating AR initiatives | Olga (lead); recently merged with PCEN Mulesoft | PIM, Salesforce (planned Zendesk → SF telemetry route), VN |
| **Mulesoft — PCEN** | Integration layer for PCEN | Jim (lead) | PCEN systems broadly, AR Mulesoft (post-merge) |
| **AWS Lambda (VN-hosted)** | Hosts DRI tables/logic; transaction-cycle inventory availability checks; network-wide replenishment cadence logic | Vendnovation (Alex's team) | VN backend, REACT PWA (transaction flow) |
| **TPCi Cloud** | Hosts what was VML/VN cloud (migrated in); future PWA infra | TPCi DevOps | VN backend, REACT PWA |
| **S3 (PIM exports)** | Product data delivery from PIM to consumers (PWA pulls deltas at planogram-change time) | unknown | PIM, REACT PWA |

## Payments

| System | Role / Function | Owner(s) / Workers | Integrated / Connected With |
|---|---|---|---|
| **DataCap** | US payment gateway; tied to Ingenico devices | Bryan (Treasury oversight); Steve Yin (incoming business mgr ownership) | VN, Ingenico, Chase PaymentTech |
| **Chase PaymentTech** | US card processor / settlement | Bryan (Treasury) | DataCap |
| **Ingenico** | Physical payment device on machines | unknown | DataCap, VN |
| **CyberSource (CSDM)** | Candidate payment + Decision Manager for fraud / DRI alternative | Under evaluation; Alex Doumani, Stefan | Would replace/augment DataCap; could integrate with VN |
| **Adyen** | Alternative end-to-end international payment provider under evaluation | Under evaluation; Stefan | Would replace DataCap stack for international |

## Customer Service / Ticketing / Monitoring

| System | Role / Function | Owner(s) / Workers | Integrated / Connected With |
|---|---|---|---|
| **Zendesk** | Telemetry-alert tickets (1:1 with alerts → fatigue), hidden CS QR-code intake form | Joe Stutzman (NetOps), Holly Dominguez (CS) | VN (telemetry source), to be replaced with enterprise tool / SF Kiosk 360 |
| **DataDog** | Machine monitoring POC (running on dev + training machines; pilot next) | Joe Stutzman (NetOps), Vendnovation/Alex (primary beneficiary) | Machine fleet, Verizon data plan |
| **Salesforce — Kiosk 360** | Multi-vendor service management, work orders, NetOps tooling, future field-repair mobile app, AR business reporting target | Olga (likely TPM); Joe Stutzman; Lisa Pappas (workforce); Bizapps re-initiated SF for AR | VN telemetry via Mulesoft (planned), Hillman / T-ROC workflows, AXP (email), LMS |
| **LMS (vendor-built)** | Field tech training delivery | Vendor contracted (unnamed); sponsor unknown | Standalone — "info delivery only" per Lisa |
| **CS QR Code Form** | Hidden Zendesk form linked from QR code on machines (~50% of inbound CS volume) | Holly Dominguez | Zendesk |

## Email / Identity / Accounts

| System | Role / Function | Owner(s) / Workers | Integrated / Connected With |
|---|---|---|---|
| **Salesforce (transactional email)** | Sends some transactional emails today; candidate for AR receipt emails (interim before AXP) | Midori McSweeney, Jen Thorton | CDP (already connected, though transactional emails don't feed in yet), VN (data source), MailGun (potential consolidation) |
| **AXP (formerly PTC)** | Accounts/identity experience + transactional email platform with 24/7/365 NOC; uses MailGun underneath | Midori McSweeney, Jen Thorton | MailGun, CDP, SF (migration source) |
| **MailGun** | Underlying email transport (used by AXP); possible consolidation platform | Midori McSweeney, Jen Thorton | AXP, possibly SF (RFP/2027 timeframe) |
| **PTC Login** | Pokemon Trainer Club login/source | unknown | CDP (planned), accounts ecosystem |
| **Email receipt flow** | Sends optional email receipt from VN today (~30% opt-in rate) | Vendnovation today; moving to SF or AXP | VN (source), SF/AXP (target), CDP |

## Customer Data / Analytics / Marketing

| System | Role / Function | Owner(s) / Workers | Integrated / Connected With |
|---|---|---|---|
| **CDP** | Customer data platform; personalization, paid media activations, marketing/cookie consent, voice of customer | Simon Wittingham; Rohit (web analyst); planned AR data inflow | Databricks, PCOM/PCEN browsing, SF email engagement, OP player/event data, TCGL activity, PTC accounts, Qualtrics (planned), CS data (planned), AR transactions (planned) |
| **QuantumMetric** | PWA analytics (replacing GA4) | Rohit (likely); PWA team | REACT PWA |
| **GA4** | Current analytics being replaced by QuantumMetric on PWA | unknown | REACT PWA (current) |
| **Qualtrics** | Survey tool; feeds CDP (planned) | unknown | CDP |
| **Martech scripts (Meta, TikTok, etc.)** | Marketing pixels / partner data scripts | Simon Wittingham (managing scope) | CDP (currently over-collects vs. least-data policy; blocking SMS) |
| **AR Email Survey** | Survey embedded in AR receipt email to collect demographics + product interest | Vendnovation today | VN, CDP (limited) |

## Order / Inventory / Supply Chain

| System | Role / Function | Owner(s) / Workers | Integrated / Connected With |
|---|---|---|---|
| **Fluent** | OMS for PCEN ecommerce; not an IMS | unknown | Oracle, PCEN ecom; AR not connected today |
| **Oracle** | Sales orders globally; candidate IMS master | unknown | Fluent (candidate sync), BizApps stack |
| **GOP (Global Order Promising — Oracle)** | Allocation rules / safety-stock by business line; under evaluation | Bala, Deepika (BizApps); Alan / Ashley (AR side) | Oracle, Fluent (planned) |
| **Auger** | AI supply-chain stitching tool under evaluation; could automate ordering/issue bubbling | Under evaluation (BizApps) | Multiple supply chain feeds (would stitch) |
| **EP (Pokemon Center ecom)** | PCEN ecommerce platform; potential AR guest checkout path | unknown | PIM, Fluent, CDP |
| **Demand Planning Tool** | CELA bringing on; AR involvement TBD | unknown (CELA) | Oracle, Fluent, AR data (planned) |
| **Dedicated IMS** | Inventory management system (separate from Fluent) being seriously considered to manage inventory across Ecom, Events, AR | BizApps team owning; lead unknown | Oracle, Fluent, AR systems |

## Security

| System / Effort | Role / Function | Owner(s) / Workers | Integrated / Connected With |
|---|---|---|---|
| **Pen Testing (RSI)** | Pen testing for machine software; SoW arrived 4/2/26; 3–6 week timeline TBD | Phil Shen, Alex Doumani, InfoSec, VN | Machine software, VN backend (separate VN-contracted vendor) |
| **DRI (Dynamic Release Inventory) logic** | Bot mitigation + replenishment pacing (e.g., 5 items released over a week at weighted-random times) | Vendnovation (AWS Lambda); potential move to CyberSource Decision Manager | VN, REACT PWA, possibly CSDM |
| **InfoSec policy / least-data** | Data collection scope governance (blocking SMS enablement) | InfoSec; Simon Wittingham coordinating | Martech scripts, CDP |

## Hardware

| System | Role / Function | Owner(s) / Workers | Integrated / Connected With |
|---|---|---|---|
| **AR Machine (Flextronics body + DragonMan cladding)** | Physical vending unit ("looks like a fridge") | Zach Dizard; Flextronics; DragonMan/CDI | Ingenico, REACT PWA, VN, Verizon data plan |
| **Verizon Data Plan** | Cell connectivity for machines | unknown | All machine systems (PWA, telemetry, DataDog) |
| **CC card reader hardware** | On-machine card reader (Ingenico today); CyberSource has new hardware option under consideration | Zach (hardware); Alex (integration) | DataCap, VN |

## Dev / Collaboration Tooling

| System | Role / Function | Owner(s) / Workers | Integrated / Connected With |
|---|---|---|---|
| **TPCi Jira** | Standard intake/planning for engineering work; AR initiatives being migrated in | Liz, Phil Shen (driving AR migration); Olga | Confluence; intake process feeds into Mulesoft / PWA / AR teams |
| **TPCi Confluence** | Documentation; VML's Confluence still holds PWA docs (export needed) | unknown TPCi side; VML on source side | Jira; VML Confluence (migration source) |
| **VML Confluence / Jira** | PWA documentation + project tracking pre-handoff | VML (Gorilla) | Migration target: TPCi Confluence/Jira |
| **Intake (CELA)** | Cross-team intake process governing project prioritization | Olga, CELA leadership | Jira, all CELA/AR roadmap work |

