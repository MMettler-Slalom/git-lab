# Phase 4: Risk Analysis

**Goal:** Identify risks you might not catch on your own, develop mitigation strategies, and use the risk register to strengthen your requirements.

---

## Use Case 1: Comprehensive Risk Identification

### Generate a Complete Risk Register

```text
**Example Prompt: Initial Risk Identification**

I'm developing a customer service chatbot for a healthcare/medical 
device company with these characteristics:

**Project Profile:**
- Azure Foundry AI with SharePoint integration
- Handles customer inquiries for orthopedic medical devices
- Regulated industry (FDA oversight, HIPAA compliance)
- Mix of technical troubleshooting and administrative support
- Pilot with orthopedic product line, potential expansion to other lines
- 3-month implementation timeline
- Small team (1 SO, 2 developers, 1 designer)

Identify comprehensive risks across these categories:

**Technical Risks:**
- Architecture, integration, performance, scalability

**Organizational Risks:**
- Adoption, change management, resources, stakeholder alignment

**Regulatory/Compliance Risks:**
- FDA requirements, HIPAA, audit requirements

**Data/Security Risks:**
- Data privacy, access control, information leakage

**Vendor/Dependency Risks:**
- Azure service dependencies, third-party integrations

**Timeline/Budget Risks:**
- Scope creep, resource availability, unexpected complexity

For each risk:
- Describe the specific risk
- Rate likelihood (High/Medium/Low)
- Rate impact (High/Medium/Low)
- Provide brief rationale for ratings

Format as a structured risk register.
```

**Expected Output:**

| Risk ID | Risk Description | Category | Likelihood | Impact | Rationale |
| --- | --- | --- | --- | --- | --- |
| R001 | SharePoint content is outdated/inconsistent | Technical | High | High | No content governance currently in place |
| R002 | Users don't trust AI responses | Organizational | Medium | High | Previous AI project had mixed reception |

**After you run this:**

- Review each risk and remove any that clearly don't apply to your project context.
- Add project-specific risks the AI missed based on what you learned in discovery.
- Rate items the AI left unrated using your judgment.

### Output for Your PRD

- **Risk Register**: Complete catalog with ratings
- **Top 5–10 Critical Risks**: Focus areas for mitigation planning

## Use Case 2: Domain-Specific Risk Deep Dives

### Healthcare/Regulated Industry Risks

```text
**Example Prompt: Regulatory Risk Analysis**

For AI chatbots in medical device customer service, deep dive into 
regulatory and compliance risks:

**FDA Compliance:**
- What are FDA requirements for AI in customer service for medical devices?
- How do companies handle liability when AI provides product information?
- What documentation and validation requirements typically apply?
- Are there restrictions on what AI can/cannot advise on?

**Quality Systems:**
- How does this fit into QMS (Quality Management System)?
- What complaint handling requirements affect chatbot design?
- How are adverse events or product issues escalated?

**Audit Requirements:**
- What records must be maintained?
- How long must conversation logs be retained?
- What audit trail capabilities are required?

**Common Pitfalls:**
- What regulatory mistakes do companies commonly make?
- What are early warning signs of compliance issues?
- How can we design for compliance from the start?

Provide specific, actionable guidance with examples of what works 
and what doesn't.
```

**After you run this:**

- Flag any compliance requirements surfaced here that aren't yet reflected in your functional or non-functional requirements — add them.
- If your project involves a regulated industry, plan a compliance review gate before the PRD goes to stakeholders.

### Compliance & Technical Output

- **Technical Constraints Section**: Limitations to design around
- **Non-Functional Requirements**: Driven by risk mitigation
- **Operations Plan**: Monitoring, alerting, incident response

### Technology Stack Risks

```text
**Example Prompt: Azure/Technical Risk Analysis**

For Azure Foundry AI implementations with SharePoint integration, 
identify:

**Azure Service Risks:**
- Common performance or scaling issues
- Azure service limits that might constrain the solution
- Azure OpenAI capacity and quota challenges
- Model deprecation or API changes
- Geographic restrictions or data residency concerns

**Integration Risks:**
- SharePoint API limitations or throttling
- Authentication/authorization complexities
- Data synchronization challenges
- Version compatibility issues

**Technical Debt Risks:**
- Quick fixes that create future problems
- Configuration choices that limit flexibility
- Hard-coded assumptions that break at scale

**Operational Risks:**
- Monitoring and alerting gaps
- Incident response preparedness
- Disaster recovery and business continuity
- Cost overruns from unexpected usage patterns

For each risk category, provide:
- Specific examples of what goes wrong
- Early detection methods
- Preventive measures
- Mitigation if it occurs
```

**After you run this:**

- For each high-severity failure mode, check whether your current requirements already address it. If they don't, add a requirement.
- Note which failure modes feel most relevant to your specific project context.

## Use Case 3: Learning from Failures

### Understand Common Failure Modes

```text
**Example Prompt: Failure Mode Analysis**

What are the most common reasons customer service chatbot projects 
fail or underperform in healthcare/regulated industries?

Categorize failures:

**Technical Failures:**
- Architecture doesn't scale
- Performance degrades over time
- Integrations break or are unreliable
- AI responses are inaccurate or inconsistent

**Adoption Failures:**
- Users don't use the tool
- Users prefer human support
- Change management ineffective
- Training insufficient

**Business Failures:**
- Doesn't deliver expected ROI
- Solves wrong problem
- Business case assumptions were flawed
- Success metrics poorly chosen

**Organizational Failures:**
- Lack of stakeholder alignment
- No clear ownership or accountability
- Competing priorities derail project
- Budget or resources insufficient

For each failure mode:
- Why does it happen?
- What are the early warning signs?
- Could we be at risk for this?
- How do successful projects avoid it?

Provide specific, actionable insights.
```

**After you run this:**

- Review the failure taxonomy against your discovery notes — did stakeholders hint at any of these patterns?
- Prioritize the 3–5 failure modes most likely to apply to your project and create mitigation plans for those first.

### Develop Mitigation Strategies

```text
**Example Prompt: Mitigation Planning**

For each of these high-priority failure modes:

[Paste specific failure modes most relevant to your project]

Develop mitigation strategies:

**Preventive Measures:**
- What can we do to reduce likelihood of this occurring?
- What requirements or design choices prevent this?
- What validation steps detect this early?

**Detective Controls:**
- How will we know if this is starting to happen?
- What metrics or signals indicate this risk?
- Who monitors and at what frequency?

**Corrective Actions:**
- If this risk materializes, what do we do?
- What's our response plan?
- What's the escalation path?

**Ownership:**
- Who is accountable for managing this risk?
- What resources do they need?
- What authority to make decisions?

Format as an action-oriented mitigation plan, not just descriptions.
```

**After you run this:**

- Assign a real owner (by name or role) to each major risk before the PRD review — unowned risks don't get managed.
- Include this mitigation plan in the PRD's Risk section, not as an appendix.

### Failure Mitigation Output

- **Risk Mitigation Matrix**: Risk → Owner → Strategy → Metrics
- **Control Framework**: How you manage risk proactively
- **Incident Response Plan**: What happens when things go wrong

## Use Case 4: Stakeholder-Specific Risks

### Identify Organizational Dynamics Risks

Based on what you learned in discovery about stakeholder dynamics, use AI to identify organizational risks.

```text
**Example Prompt: Organizational Risk Assessment**

Based on these stakeholder dynamics from discovery:

**What We Learned:**
- Customer Service has limited technical resources and relies heavily 
  on IT
- IT innovation team is separate from IT operations (different 
  priorities)
- Compliance team hasn't been engaged yet but has veto power
- Previous AI projects had mixed reception - some saw as threat to jobs
- Leadership is enthusiastic but hasn't allocated dedicated resources
- Content ownership is unclear - multiple teams contribute to 
  SharePoint

What organizational risks should we plan for?

Include risks around:
- Stakeholder alignment and buy-in
- Decision-making bottlenecks or conflicts
- Resource availability and commitment
- Change resistance or fear
- Competing priorities pulling resources away
- Unclear ownership and accountability
- Political dynamics or turf battles

For each risk:
- Why is this a problem?
- What's the worst-case scenario?
- How can we mitigate proactively?
- What early signs indicate this is becoming an issue?
```

**After you run this:**

- Review each organizational risk against the stakeholder dynamics you observed in discovery.
- For risks that require executive decisions, plan how you'll surface them before the formal PRD review.

### Stakeholder Risks Output

- **Stakeholder Engagement Strategy**: Who, when, what
- **Governance Model**: Decision rights and accountability
- **Change Management Plan**: Addressing resistance
- **Resource Plan**: Commitment secured

## Use Case 5: Risk-Driven Requirements

### Connect Risks Back to Requirements

Risks often reveal missing requirements. Use AI to identify gaps.

```text
**Example Prompt: Risk-Based Requirement Gap Analysis**

Here are our top risks:

[List top 10 risks with descriptions]

And here are our current requirements:

[Paste requirements summary]

Identify missing requirements that would mitigate these risks:

**Examples:**
- If there's a content quality risk, do we have requirements for 
  content review workflows?
- If there's an adoption risk, do we have requirements for training 
  and change management?
- If there's a compliance risk, do we have requirements for audit 
  logging?
- If there's a performance risk, do we have requirements for load 
  testing and monitoring?

For each gap:
- What requirement is missing?
- Which risk does it address?
- How critical is it (must-have vs. should-have)?
- Where in the PRD should it be added?

This creates a feedback loop: Discovery → Risk Analysis → Refined 
Requirements.
```

**After you run this:**

- Add all identified missing requirements to your PRD before the next review cycle.
- Update acceptance criteria so they explicitly validate risk mitigation where relevant.

### Validate Existing Requirements Against Risks

```text
**Example Prompt: Requirement Risk Validation**

Review these requirements against identified risks:

**Requirements:**
[Paste requirements]

**Risks:**
[Paste risks]

Check:

1. Do any requirements introduce NEW risks not yet identified?
2. Are requirements specific enough to actually mitigate the risks 
   they're intended to address?
3. Are there conflicting requirements that create risk?
4. Are acceptance criteria sufficient to verify risk mitigation?

Identify issues and suggest refinements.
```

**After you run this:**

- Refine any requirements that are too vague to actually mitigate the risks they're meant to address.
- Resolve requirement conflicts before the PRD goes to stakeholders.

### Risk-Driven Requirements Output

- **Updated Requirements Section**: With risk mitigation built in
- **Acceptance Criteria**: That validate risk controls
- **Testing Plan**: That validates risk mitigation

## Use Case 6: Risk Prioritization & Communication

### Prioritize for Action

```text
**Example Prompt: Risk Prioritization**

Here are all the risks we've identified:

[Paste comprehensive risk list with likelihood and impact ratings]

Help me prioritize by:

**Immediate Action Required (Pre-Project):**
- Which risks must be addressed before project kickoff?
- What decisions need to be made now?
- What validation must occur before proceeding?

**Active Management (During Project):**
- Which risks require mitigation plans and active monitoring during 
  execution?
- What can be handled through normal project management?

**Monitor Only (Lower Priority):**
- Which risks are acceptable to monitor without active mitigation?
- What's the trigger for escalating these?

**Executive Escalation Required:**
- Which risks require executive stakeholder decisions?
- What decisions specifically? (Accept risk, allocate more resources, 
  change scope, etc.)

Organize by urgency and provide rationale.
```

**After you run this:**

- Any risk in the "Executive Escalation Required" tier should be surfaced to your sponsor before the PRD review, not during it.
- Set a monitoring cadence for each tier and assign it to someone on the team.

### Tailor Communication by Audience

```text
**Example Prompt: Risk Communication Strategy**

We need to communicate risks to different audiences. Help me tailor 
the message:

**For Executive Sponsor:**
- Top 3-5 risks only
- Business impact focus
- Decision/trade-off framing
- What format (summary slide, talking points)?

**For Project Team:**
- Full risk register
- Mitigation plan details
- Monitoring responsibilities
- What format (detailed document, workshop discussion)?

**For Steering Committee:**
- Risks requiring policy decisions or resource allocation
- Cross-functional coordination needs
- Escalation criteria
- What format (dashboard, quarterly review)?

For each audience, provide:
- Key messages
- Level of detail
- Format recommendations
- Frequency of updates
```

**After you run this:**

- Use the executive summary format when briefing your sponsor before the formal PRD review.
- Include the full risk register in the PRD appendix, not the body — the body should contain only the top critical risks with mitigation plans.

### Risk Prioritization Output

- **Executive Summary Risk Section**: Top priorities for leaders
- **Detailed Risk Appendix**: Complete register for the project team
- **Decision Log**: Decisions made about risk acceptance/mitigation

## Reflection

Before moving to Phase 5, consider:

- Which risks surprised you most — things you wouldn't have surfaced without AI assistance?
- Are there requirements you need to add or revise based on what the risk analysis surfaced?
- Who on the stakeholder team needs to be briefed on the top risks before the PRD review?

---

**Next:** [Phase 5 — Refinement & Quality Checks](05-refinement.md)
