# Mary's Place — Current Operational Challenges

> **Audience:** Product team scoping a software solution for Mary's Place.

---

## Shelter Services

- Length of stay is increasing due to housing affordability and economic pressures in King County
- Intake is manual and fragmented — families must be assessed separately by health, housing, and youth services staff
- No centralized journey mapping to estimate timelines or sequence complex steps toward housing stability
- Internal database is outdated (1990s-era SQL), difficult to customize, and not integrated with the county HMIS
- Staff must perform double data entry — entering the same information into both the internal system and the county-wide Homelessness Management Information System (HMIS)

---

## Mobile Outreach Services

- Outreach specialists have no visibility into warehouse inventory; must call the warehouse manager to request items
- Fulfillment is ad hoc — families receive whatever happens to be available, not what they actually need
- Short lead times (often only a few days) when families move into housing make it difficult to source needed goods

---

## Prevention Services

- No established system for distributing goods to prevention families
- Prevention families cannot access items the way shelter guests can (no marketplace equivalent)

---

## Goods Management & Distribution (Cross-Cutting)

- Only 15–20% of donated items are usable by Mary's Place families
- Inventory tracking is manual (bin counts only) — no SKU-level visibility
- No real-time demand data, making it impossible to target or direct corporate donations effectively
- Unusable excess inventory accumulates with no efficient path to redistribute to other community organizations
- No centralized demand tracking across shelter, outreach, and prevention populations
- Limited storage capacity at outreach specialist offices compounds distribution inefficiency

---

## Key Opportunity Areas (Product Implications)

| Gap | Potential Solution Area |
|---|---|
| Fragmented intake & case tracking | Unified intake + family journey mapping tool |
| HMIS double data entry | Integration / sync layer with county HMIS |
| No inventory visibility | Real-time inventory management system |
| Inability to target donations | Demand-driven donation matching |
| Goods inaccessible to outreach/prevention | Expanded distribution workflow beyond shelter |

---

## Open Questions

**Shelter Services**
- What is the current average length of stay, and what is the target? How is this tracked today?
- How many distinct steps are in the typical family journey from intake to stable housing? Who currently owns that process map?
- What is the name/product of the internal database system? Is there documentation of its schema or data model?
- How many hours per week does staff spend on HMIS double data entry? Who is responsible for it at each shelter location?
- What county HMIS platform is in use (e.g., Clarity Human Services, ServicePoint)? Does it expose an API?

**Mobile Outreach Services**
- How many active outreach families are being served at any given time?
- What is the typical lead time between an outreach family being identified as ready to move into housing and their actual move-in date?
- Do outreach specialists have smartphones or tablets in the field, or are they primarily desktop-based?

**Prevention Services**
- How many prevention families are active at any time? What is the typical duration of a prevention engagement?
- Are prevention families already in a housing unit (i.e., at risk of losing it), or are they pre-housed? This affects what goods they actually need.

**Goods Management & Distribution**
- What categories of goods make up the 15–20% that are usable? What are the most common unusable items?
- How much warehouse space does Mary's Place have, and how often does it hit capacity?
- Are there already partner organizations that receive redistributed goods, or would this network need to be built from scratch?
- Does the current bin-count system produce any reports used for grant reporting or audits? Any new system must preserve that capability.
