# Phase 2: Synthesis

**Goal:** Transform raw discovery materials into structured PRD content — organized requirements, user personas, use cases, success metrics, and draft section text.

---

## Step 1: Upload and Organize Discovery Materials

### Gather Your Sources

Before starting synthesis, collect:

- Meeting notes and transcripts from all stakeholder conversations
- Existing documentation (current state processes, technical specs)
- Competitive research or market insights
- Internal reference materials (like Azure Foundry patterns)
- Any artifacts or examples shared by stakeholders

```text
**Example Prompt: Initial Organization**

I'm creating a PRD for a customer service chatbot for a healthcare 
company. I have the following discovery materials:

- Interview notes from Customer Service Director (focus: operational 
  needs, metrics)
- Interview notes from IT/AI Innovation team (focus: technical 
  architecture, Azure capabilities)
- Interview notes from Compliance Officer (focus: regulatory 
  requirements)
- Existing Azure Foundry reference architectures
- Competitor product documentation

Please help me organize these into a structured outline with these 
sections:
1. Executive Summary
2. Business Objectives
3. User Personas and Use Cases  
4. Functional Requirements
5. Non-Functional Requirements
6. Technical Architecture
7. Success Metrics
8. Risks and Mitigation

For each section, indicate which source materials are most relevant.
```

**After you run this:**

- Review the content mapping — does each source map to the right section?
- Note any sections that have no source material yet; those are your open gaps.
- Keep this outline open as your working structure throughout the rest of Phase 2.

## Step 2: Extract and Structure Requirements

### Transform Conversations into Requirements

Requirements are scattered across conversations, sometimes contradictory, often vague. AI helps you extract and organize them systematically.

```text
**Example Prompt: Requirement Extraction**

Review these stakeholder interview notes:

[Paste meeting notes]

Extract all requirements mentioned. For each requirement:
- Categorize as Functional, Non-Functional, Business, or Technical
- Assign priority level (Must-Have, Should-Have, Nice-to-Have)
- Note which stakeholder mentioned it
- Identify any constraints or dependencies mentioned
- Flag if the requirement is vague or needs clarification

Format as a structured table.
```

**After you run this:**

- Correct any requirements that were misunderstood or over-simplified.
- Add requirements you recall from the conversations that didn't appear in the output.
- Flag anything marked "needs clarification" for a stakeholder follow-up.

### Identify Conflicts and Ambiguities

```text
**Example Prompt: Conflict Analysis**

Compare these extracted requirements:

[Paste requirement list from multiple stakeholders]

Identify:
1. Conflicting requirements across stakeholders (e.g., one wants 
   feature X, another says it's out of scope)
2. Ambiguous requirements that could be interpreted multiple ways
3. Implied requirements that weren't explicitly stated but are 
   necessary for the solution to work
4. Missing requirements based on standard patterns for this type 
   of project

For each issue, suggest:
- Why it's a problem
- Questions to ask to resolve it
- Potential impact if not addressed
```

**After you run this:**

- Prioritize the conflicts by impact on scope or architecture.
- For each implied requirement surfaced, decide: add it, or flag it as an open question for stakeholders.
- Resolve critical conflicts before drafting sections that depend on them.

## Step 3: Develop Key PRD Sections

### User Personas

Transform stakeholder descriptions into actionable personas.

```text
**Example Prompt: Create User Personas**

Based on these stakeholder interviews describing customer service 
workflows:

[Paste relevant excerpts about users]

Create 2-3 detailed user personas for this customer service chatbot:

For each persona include:
- Role and responsibilities
- Current pain points and frustrations
- Goals and motivations
- Technical proficiency level
- Success criteria (what would make them love this tool)
- Typical use scenarios
- Quote that captures their perspective

Make personas realistic and specific, not generic.
```

**After you run this:**

- Review the personas against your actual stakeholder notes — adjust any details that feel generic rather than specific to this project.
- If a key user type is missing, prompt a follow-up persona.

### Use Cases and User Stories

```text
**Example Prompt: Generate Use Cases**

Based on these functional requirements and user personas:

**Requirements:**
[Paste key functional requirements]

**Personas:**
[Paste persona summaries]

Generate the top 8-10 use cases for this customer service chatbot.

For each use case, provide:
- Title and unique ID
- Primary actor (which persona)
- Preconditions (what must be true to start)
- Main flow (step-by-step happy path)
- Alternative flows (variations or exceptions)
- Expected outcome
- Success criteria

Prioritize use cases that address the most common or highest-value 
scenarios mentioned in discovery.
```

**After you run this:**

- Check that the top use cases reflect the highest-value scenarios from your stakeholder conversations, not just the easiest ones to describe.
- For each use case, verify the happy path is realistic given your technical constraints.

### Success Metrics

```text
**Example Prompt: Define Success Metrics**

Based on these business objectives:

[Paste business objectives from discovery]

And these stakeholder priorities:
- Customer Service Director wants to reduce support costs by 30%
- IT wants high system reliability and performance
- Compliance wants audit trail and regulatory compliance
- End users want faster query resolution

Propose specific, measurable success metrics including:

**North Star Metric** (single most important measure of success)

**Leading Indicators** (early signals that predict success):
- What to measure
- Target value
- How frequently to measure

**Operational Metrics**:
- System performance and reliability
- User adoption and satisfaction
- Cost and efficiency
- Quality and compliance

For each metric:
- Define precisely what's measured
- Provide baseline (if available) and target
- Specify measurement method and frequency
- Note who owns the metric
```

**After you run this:**

- Validate each metric with at least one stakeholder before committing to it in the PRD. Metrics create accountability — make sure stakeholders have actually agreed to them.
- Remove or defer any metric that has no clear owner or measurement method.

## Step 4: Fill Knowledge Gaps

### When You Need More Information

As you draft sections, you'll identify areas where you need additional context or validation.

```text
**Example Prompt: Research Knowledge Gaps**

I'm working on the technical architecture section for a healthcare 
customer service chatbot. I need more information about:

1. Industry standard response time SLAs for healthcare support chatbots
2. Typical deflection rates for AI chatbots in regulated industries
3. Azure OpenAI capacity planning for expected load of 10,000 
   queries/day
4. SharePoint search performance with document libraries of 50,000+ 
   documents

For each topic, provide:
- Best practices or standards
- Typical ranges or benchmarks
- Key considerations for a healthcare/regulated environment
- Sources or references for validation
```

**After you run this:**

- Spot-check the benchmarks against a second source — AI research is a starting point, not a final reference.
- Treat any benchmark that will be cited in the PRD to stakeholders as requiring validation.

## Step 5: Create Comprehensive Section Drafts

### Technical Architecture

```text
**Example Prompt: Draft Technical Architecture**

Create a technical architecture section for a PRD based on:

**Requirements:**
[Paste technical and non-functional requirements]

**Constraints:**
- Must use Azure Foundry AI services
- Must integrate with SharePoint for knowledge base
- Must comply with HIPAA and FDA regulations
- Must support 10,000 queries/day at launch, scale to 50,000
- Response time under 2 seconds for 95% of queries

**Available Patterns:**
- Existing Azure Foundry customer service agent patterns
- RAG (Retrieval Augmented Generation) architecture
- Azure OpenAI with GPT-4

Include:
1. High-level architecture diagram description
2. Component breakdown (UI, API, LLM, knowledge base, etc.)
3. Data flow for typical query
4. Integration points
5. Security and compliance controls
6. Scalability approach
7. Monitoring and observability

Write for both technical and business audiences.
```

**After you run this:**

- Review the technical architecture draft with someone technical before it goes into a PRD — this section requires more validation than most.
- Flag any assumptions embedded in the architecture (e.g., Azure capacity, SharePoint access) that need confirmation.

### Implementation Approach

```text
**Example Prompt: Implementation Approach**

Based on this project scope:
[Paste project summary]

And these constraints:
- Timeline: 3-month pilot for orthopedic products
- Budget: [if known]
- Team: 1 Solution Owner, 2 developers, 1 designer
- Risk tolerance: Low (healthcare/regulated environment)

Recommend an implementation approach covering:

**Phasing Strategy:**
- MVP scope vs. future phases
- Pilot rollout plan
- Validation gates between phases

**Development Approach:**
- Agile sprint structure recommendation
- Key milestones and deliverables
- Testing and validation strategy

**Risk Mitigation:**
- What to validate early
- Proof of concept recommendations
- Fallback options if key assumptions fail

**Change Management:**
- User training approach
- Communication plan
- Success monitoring

Provide specific, actionable recommendations.
```

**After you run this:**

- Review the phasing strategy against your actual timeline and team constraints — adjust if it assumes more capacity than you have.
- Validate the MVP scope with your key stakeholders before moving to Phase 3.

## The Iterative Flow

**Key Teaching Point**: This isn't linear. You'll cycle through:

1. **Draft section with AI** → Initial content based on discovery
2. **Review and identify gaps** → What's missing or unclear?
3. **Research or validate** → Fill gaps with AI research or stakeholder check-ins
4. **Refine section** → Improve based on new information
5. **Move to next section** → Repeat process

AI makes each cycle faster, but critical thinking and validation are still essential.

## Connecting Everything Together

### Ensure Traceability

```text
**Example Prompt: Verify Traceability**

Review these PRD sections for traceability:

**Business Objectives:**
[Paste objectives]

**Requirements:**
[Paste requirements]

**Success Metrics:**
[Paste metrics]

Create a traceability matrix showing:
- Which requirements support which business objectives
- Which success metrics measure which objectives
- Any requirements that don't clearly trace to business value
- Any objectives that lack supporting requirements or metrics

Identify gaps or disconnects.
```

**After you run this:**

- For any orphaned requirements (no clear business value), decide: cut them or find the objective they support.
- For any broken chains, either add the missing requirement or escalate the unresolved objective to stakeholders.

## Reflection

Before moving on, review your drafted PRD outline:

- Which sections feel most uncertain or thinly sourced?
- Are there requirements that still feel vague or untestable?
- Do your success metrics reflect what stakeholders actually said they care about?

---

**Next:** [Phase 3 — Market & Competitive Analysis](03-market-analysis.md)
