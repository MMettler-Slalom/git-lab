# Mary's Place — Technology Opportunities & Constraints

> **Audience:** TPM preparing to scope a software initiative for Mary's Place.
> **Source:** Intro call transcript, November 14, 2025. Attendees: Jason Gortney (Chief Program & Innovation Officer), Mike Komola (Chief HR & Operations Officer), Casey Frith-Smith and Lauren Milosky (Slalom).

---

## Product Ideas Raised by Stakeholders

### 1. AI-Powered Family Intake & Journey Navigator ("Virtual Advocate")
*Raised by Jason Gortney*

- A conversational AI tool that walks families through intake at their own pace — replacing fragmented, multi-team assessments
- Collects health, housing, financial, and youth services information in a single, unified flow
- Uses that data to generate a **prioritized, sequenced plan** of steps toward housing stability (e.g., "start this on day one because it takes 3 months")
- Provides a **timeline estimate** for the family's housing journey to set expectations and support motivation
- When families meet with specialists, the data is pre-populated so staff can focus on high-value work rather than re-collecting information
- Supports **12–15 languages** (language mix shifts over time)
- Enables **capacity and demand forecasting** for Mary's Place internally
- Self-serve capable; could be accessed before or during shelter intake

### 2. Inventory Management & Supply-Demand Matching System
*Raised by Mike Komola*

- Real-time tracking of donated goods across all inventory categories — currently tracked only by bin count, no SKU-level detail
- Centralized demand visibility across all three service areas: shelter, outreach, and prevention
- Enable outreach specialists and potentially families themselves to **view available inventory and submit requests** (vs. calling the warehouse ad hoc)
- Targeted donation coordination: give development staff real-time needs data so corporate donors (e.g., REI, Amazon, Microsoft) are directed to actual needs rather than generic wish lists
- Redistribution pathway for excess/unusable donations to other community organizations
- Currently uses **Amazon Wish Lists** for donation asks — a potential integration or replacement point

### 3. Extended Marketplace for Outreach & Prevention Families
*Raised by Mike Komola*

- Shelter locations have an in-person "marketplace" where guests can shop for goods — this does not exist for outreach or prevention families
- Concept: create a physical or digital marketplace at one facility accessible to non-shelter families
- Could complement the existing **"Make a Home" program** (one staff coordinator who sources household goods for families transitioning into housing across all service lines)

---

## Pain Points with Clear Technology Implications

| Pain Point | Current State | Technology Need |
|---|---|---|
| Fragmented intake | Multiple teams assess families separately; no unified record at intake | Unified intake flow + shared case record |
| No journey mapping | No system to sequence or estimate timeline of steps to housing | AI-driven case planning and prioritization |
| Double data entry | Internal system and county HMIS (Homelessness Management Information System) are not integrated; staff re-enter all data manually | HMIS integration / sync layer |
| Outdated case management database | Open-source SQL system from the 1990s, customized in-house; no modern UX | Replacement or modernization of core data system |
| No inventory management | Bin counts only; no SKUs, no barcodes, no real-time visibility | Inventory management system with receiving/tracking |
| No demand tracking | Demand across shelter, outreach, and prevention is unknown in real time | Centralized demand aggregation |
| Ad hoc goods fulfillment | Outreach specialists call warehouse manager by phone; fulfillment is hit-or-miss | Structured request and fulfillment workflow |
| Unusable donated inventory | ~80–85% of donations are not usable; no system to redistribute | Redistribution matching / partner network tool |

---

## Existing Technology Relationships & Constraints

### Microsoft
- **Primary technology vendor** — "We're a Microsoft shop"
- Staff use Microsoft 365 (email, Office suite, Windows)
- Actively using and training **Microsoft Copilot** for HR use cases (benefits Q&A, employee handbook chatbot)
- No Azure cloud infrastructure in use (relationship is primarily productivity software)

### Amazon
- **Very close strategic partner** — Amazon built an 8-story family shelter on their corporate campus in Seattle
- Existing partnership with **Amazon Legal**, which connects Mary's Place to pro bono law firms
- Collaborated on a prior AI project (see below)
- No known AWS infrastructure usage

### Internal IT & Data Teams
- Small internal IT team manages hardware and software contracts
- Separate internal **data team** maintains the legacy SQL database, runs queries, and produces reports
- IT Director reports to Jason Gortney
- No dedicated software engineering team; no history of building custom systems internally

---

## Prior AI Project: Asylum Application Chatbot

- Built in partnership with **Amazon Legal** and a pro bono law firm (~2024)
- Problem: Large influx of asylum-seeking families; legal application process was 4+ hours of attorney time per family
- Solution: Multilingual, trauma-informed AI chatbot that walked families through the asylum application before meeting with an attorney
- Result: Attorney prep meeting reduced from **4 hours to 1 hour**
- Supported all 12–15 languages spoken by guest population
- **Not owned by Mary's Place** — owned by the law firm; used as a proof-of-concept for scalable legal document automation
- This project directly inspired Jason's vision for the "Virtual Advocate" intake tool

---

## Desired Outcomes & Engagement Constraints

- Stakeholders are interested in a **prototype or well-developed concept** with enough substance to shop for external funding
- Open to follow-up discovery sessions with:
  - A **care coordinator** (for intake/journey navigator use case)
  - A **goods intake and distribution staff member** (for inventory/supply-demand use case)
- Timeline framing: Casey referenced a 60–90 day window for something actionable
- Budget is grant/donation-dependent; any solution should be pitchable to funders
- Scalability is a stated value — solutions that could extend beyond Mary's Place to other organizations are viewed positively

---

## Open Questions

**Scoping & Prioritization**
- Are the intake navigator and the inventory system intended as one initiative or two? Which is the higher priority if they must be sequenced?
- Is the 60–90 day target for a working prototype, a defined concept, or a funded proposal? Who defines "done"?
- Has Mary's Place evaluated any off-the-shelf products for either problem (e.g., case management platforms like Apricot, inventory tools like Pantry Soft)? If so, what ruled them out?

**Virtual Advocate / Intake Navigator**
- What data privacy and consent regulations apply to client information collected at intake (HUD HMIS standards, Washington state law, HIPAA for health data)?
- What devices do families have access to at intake — shared kiosks, staff-assisted tablets, personal smartphones? Is internet access reliable at all shelter locations?
- What is the current intake time per family, end to end? What would an acceptable target be?
- Are there literacy or digital literacy constraints that should shape the UX (e.g., voice-first, icon-heavy design)?
- Who would own and update the prioritization logic (the rules that determine step sequencing)? Is this clinical/program knowledge held by specific staff?

**Inventory & Supply-Demand System**
- What is the actual name of the open-source SQL database used for case management? Is it the same system used to track inventory, or a separate tool?
- Does the warehouse have any existing barcode or RFID infrastructure, or would that need to be introduced?
- Who are the other community organizations that might receive redistributed goods? Are there existing relationships, or would an outreach effort be needed?
- Would corporate donors (Amazon, Microsoft, REI) have direct access to a donation request portal, or would that remain mediated by the development team?
- What financial audit requirements drive inventory valuation — who is the auditor, and what format do they require?

**Technology Relationships**
- Is there an active Microsoft nonprofit grant or Azure credit program in place that could be used to host a solution?
- Is Amazon willing to contribute engineering resources, credits, or funding beyond the existing legal partnership?
- What is the IT Director's name and role in evaluating or approving new technology? Should they be included in discovery sessions?
- Does the existing Copilot deployment use any Microsoft 365 data connectors that could be extended to support intake or inventory use cases?
