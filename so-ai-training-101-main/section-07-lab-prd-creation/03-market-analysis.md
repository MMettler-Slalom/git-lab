# Phase 3: Market & Competitive Analysis

**Goal:** Validate your requirements against market standards, understand the competitive landscape, and ensure your PRD is grounded in external reality — not just internal assumptions.

---

## Use Case 1: Competitive Landscape Research

### Understand Who's Solving Similar Problems

```text
**Example Prompt: Competitive Landscape**

I'm building a customer service chatbot for healthcare/medical device 
companies.

Research and summarize:

1. What are the leading customer service chatbot solutions in 
   healthcare/medical devices?
2. What features do they commonly offer?
3. What are their key differentiators?
4. What do user reviews commonly praise or criticize?
5. What integration capabilities do they provide?
6. What pricing models do they use?

Organize as a competitive landscape overview with:
- Top 5-7 competitors
- Feature comparison
- Strengths and weaknesses
- Market positioning

Focus on enterprise healthcare solutions, not consumer chatbots.
```

**After you run this:**

- Validate the competitor list: are these actually the solutions your client would evaluate?
- Check for any obvious gaps — niche players in the exact vertical may not be well-represented in AI training data.
- Use the output to inform a more targeted competitor deep-dive below.

### Deep Dive on Specific Competitors

```text
**Example Prompt: Competitor Deep Dive**

For [Specific Competitor - e.g., "HealthcareAI ChatBot"], research:

1. Technical architecture approach (if publicly available)
2. Key features and capabilities
3. Integration ecosystem (what systems do they connect with)
4. Implementation timeline and complexity
5. Customer success stories in medical device space
6. Known limitations or common complaints
7. Pricing structure and total cost of ownership

Provide a comprehensive profile that helps us understand their 
solution deeply.
```

**After you run this:**

- Note any differentiation opportunities that align with your stakeholder priorities.
- Add findings to your PRD's Competitive Positioning section.

### Output for Your PRD

- **Competitive Positioning**: Where does your solution fit in the market?
- **Feature Gap Analysis**: What do competitors offer that you don't (and should you)?
- **Differentiation Strategy**: How are you different?

## Use Case 2: Feature Benchmarking

### Validate Requirements Against Market Standards

```text
**Example Prompt: Feature Benchmarking**

For enterprise customer service chatbots in healthcare, categorize 
features as:

**Must-Haves** (table stakes - customers expect these):
- List features with brief descriptions

**Standard** (expected by sophisticated buyers):
- List features with brief descriptions

**Advanced** (competitive differentiators):
- List features with brief descriptions

**Emerging** (cutting edge but not yet expected):
- List features with brief descriptions

Focus on:
- B2B/Enterprise context
- Healthcare/regulated industries
- Integration capabilities
- Security and compliance features
- AI/LLM capabilities
```

**After you run this:**

- Use the feature tiers to challenge any "must-have" requirements that are actually table stakes (and ensure they're in scope) or advanced features that might be out of scope for an MVP.

### Cross-Reference with Your Requirements

```text
**Example Prompt: Requirement Validation**

Here are the features our stakeholders requested:

[Paste your requirement list]

And here's the market benchmark:

[Paste AI research on feature categories]

Compare and identify:

1. Which requested features are table stakes (must deliver)
2. Which are differentiators (highlight in proposal)
3. What's missing from our requirements that competitors offer 
   (discuss with stakeholders)
4. What we're proposing that's ahead of market (flag as innovation/risk)
5. Features that might be over-scoped given market standards

Provide specific recommendations for scope adjustments.
```

**After you run this:**

- For features flagged as over-scope, discuss the trade-off with stakeholders — don't unilaterally remove them.
- Document your scope decisions and the market rationale behind them in the PRD.

### Feature Benchmarking Output

- **Feature Prioritization**: Justified by market standards
- **Scope Definition**: MVP vs. future phases
- **Competitive Advantages**: What makes you unique

## Use Case 3: Industry Trends & User Expectations

### Understand Market Evolution

```text
**Example Prompt: Industry Trends**

What are the current trends in AI-powered customer service for 
healthcare and medical device companies?

Include:

**Technology Trends:**
- Evolution from rule-based to generative AI
- RAG (Retrieval Augmented Generation) adoption
- Multimodal capabilities (text, voice, image)
- Integration patterns with ERP/CRM systems

**User Behavior Trends:**
- Changing expectations for self-service
- Adoption patterns across age groups
- Mobile vs. desktop usage
- Human escalation preferences

**Regulatory/Compliance Trends:**
- How companies balance AI automation with compliance
- FDA considerations for AI in medical device support
- HIPAA implications
- Audit and documentation requirements

**Business Model Trends:**
- ROI expectations and typical payback periods
- Success metrics evolution
- Staffing and organizational changes

Provide concrete examples and data where available.
```

**After you run this:**

- Flag any regulatory or compliance trend that your current requirements don't yet address.
- Use emerging technology trends to shape the "future phases" section of your PRD.

### Domain-Specific Deep Dive

```text
**Example Prompt: Healthcare-Specific Trends**

For medical device customer service specifically, research:

1. How are companies handling technical troubleshooting vs. 
   administrative inquiries with AI?
2. What's the trend in measuring chatbot success (beyond deflection 
   rates)?
3. How are companies managing the transition from FAQ-based to 
   complex problem-solving chatbots?
4. What role do chatbots play in complaint handling and adverse 
   event reporting?
5. How are companies addressing liability concerns with AI-generated 
   technical guidance?

Focus on practical implementation patterns, not just theory.
```

**After you run this:**

- Add relevant domain-specific findings to your PRD's context or background section.

### Industry Trends Output

- **Future-Proofing Considerations**: Design for where the market is heading
- **Scalability Requirements**: Plan for expected evolution
- **Technology Selection Rationale**: Why these choices make sense long-term

## Use Case 4: Best Practices & Implementation Patterns

### Learn from Others' Experiences

```text
**Example Prompt: Implementation Best Practices**

What are best practices for implementing customer service chatbots 
in healthcare/medical device companies?

Focus on:

**Rollout Strategies:**
- Pilot vs. full deployment approaches
- Which use cases to start with
- User group selection for pilots
- Expansion criteria and timing

**User Adoption:**
- Change management approaches that work
- Training strategies
- Communication patterns
- Handling resistance

**Technical Implementation:**
- Content management and curation approaches
- Quality assurance and testing
- Monitoring and continuous improvement
- Integration sequencing (what to connect first)

**Common Pitfalls:**
- What goes wrong most often
- Early warning signs of problems
- How to avoid or mitigate
- Recovery strategies when issues occur

Provide specific, actionable guidance with examples.
```

**After you run this:**

- Incorporate proven rollout and change management patterns directly into your PRD's Implementation Approach section.
- Flag any common pitfalls that seem particularly relevant to your project context.

### Success Patterns

```text
**Example Prompt: Success Case Studies**

Research successful customer service chatbot implementations in 
healthcare or regulated industries.

For each case study, extract:

1. Company profile and initial challenge
2. Solution approach and key features
3. Implementation timeline and methodology
4. Adoption strategy and change management
5. Quantified results (deflection rates, cost savings, satisfaction)
6. Lessons learned and recommendations
7. What made this implementation successful vs. others

Look for patterns across successful implementations.
```

**After you run this:**

- Identify 2–3 success patterns that are most applicable to your project and note them explicitly in your PRD.

### Implementation Patterns Output

- **Implementation Approach**: Informed by proven patterns
- **Risk Mitigation Strategies**: Based on common pitfalls
- **Change Management Plan**: Using approaches that have worked
- **Timeline Estimates**: Grounded in real implementations

## Use Case 5: Cost & ROI Benchmarks

### Set Realistic Financial Expectations

```text
**Example Prompt: Cost Benchmarking**

For implementing an Azure-based customer service chatbot in a 
healthcare company:

**Infrastructure Costs:**
- Azure OpenAI consumption at different query volumes
- Azure compute and storage requirements
- Data transfer and networking costs
- Typical monthly costs at 10K, 50K, 100K queries/month

**Implementation Costs:**
- Professional services for design and development
- Integration with existing systems (SharePoint, CRM, etc.)
- Content development and knowledge base setup
- Testing and QA
- Training and change management

**Ongoing Operational Costs:**
- Maintenance and support
- Content updates and curation
- Model retraining or updates
- Monitoring and analytics
- Staff time for oversight

**Typical Ranges:**
- What's a reasonable budget range for this type of implementation?
- What drives cost variation?

Provide ranges and benchmarks, not just general guidance.
```

**After you run this:**

- Sense-check cost ranges with your own project experience or a technical colleague — AI cost benchmarks can be stale.
- Use the ranges as a starting point for your Budget section, not as final figures.

### ROI and Business Case

```text
**Example Prompt: ROI Framework**

For a customer service chatbot expected to:
- Handle 10,000 inquiries/month initially
- Achieve 40% deflection rate
- Reduce average handle time by 30%
- Current support cost: $25 per human-handled inquiry

Calculate:

1. Break-even timeline
2. Typical payback period for similar implementations
3. 3-year ROI projection
4. Comparison to current support costs
5. Sensitivity analysis (what if deflection is 30% or 50%?)

Also identify:
- Non-financial benefits (faster response, 24/7 availability, 
  consistency)
- How to measure and communicate these
- Typical ROI benchmarks in healthcare customer service

Provide a framework for building the business case.
```

**After you run this:**

- Validate key assumptions in the model (deflection rate, handle time reduction) with your stakeholders before publishing the business case.
- Include a sensitivity analysis in the PRD if the ROI is highly dependent on one or two assumptions.

### Cost & ROI Output

- **Budget Section**: Market-informed cost estimates
- **ROI Projections**: Grounded in comparable implementations
- **Total Cost of Ownership**: Comprehensive financial view
- **Business Case**: Compelling value proposition

## Combining Market Research with Discovery

**The Key Insight**: Market research isn't separate from stakeholder input - it's a validation and enrichment layer.

### The Workflow

1. **Gather stakeholder requirements** (Discovery Phase)
2. **Research market standards** (AI-powered, this phase)
3. **Present back to stakeholders**: "Here's what you asked for, here's what the market is doing, here are gaps/opportunities"
4. **Refined requirements** that balance internal needs with external reality

### Example Conversation Framing

```text
**Example Prompt: Stakeholder Discussion Framework**

I need to present market research findings back to stakeholders. 
Here's the context:

**What Stakeholders Requested:**
[Paste key requirements]

**What Market Research Shows:**
[Paste relevant benchmarks, trends, competitor features]

**Gaps Identified:**
[Paste gaps or differences]

Help me create:

1. Executive summary of market findings (2-3 key points)
2. Specific recommendations for scope adjustments with justification
3. Discussion questions to align on priorities
4. Talking points for trade-offs (if we do X, we give up Y)

Frame this as strategic guidance, not pushback on their ideas.
```

**After you run this:**

- Present market findings back to stakeholders as context, not conclusions. The goal is to enrich their judgment, not override it.

## Reflection

Before moving to Phase 4, consider:

- Did the market research confirm or challenge your stakeholder-driven requirements?
- Are there any gaps between what your client wants and what the market suggests is table stakes?
- What's one finding from this phase that would change your PRD if you didn't act on it?

---

**Next:** [Phase 4 — Risk Analysis](04-risk-analysis.md)
