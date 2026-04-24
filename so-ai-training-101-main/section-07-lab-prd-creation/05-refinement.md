# Phase 5: Refinement & Quality Checks

**Goal:** Systematically review your PRD for completeness, consistency, clarity, and stakeholder-readiness before it goes to formal review.

---

## Quality Check 1: Completeness Assessment

### Ensure All Sections Are Covered

```text
**Example Prompt: Completeness Check**

Review this PRD for a customer service chatbot and identify:

1. What sections are present vs. what's typically expected in a 
   comprehensive PRD for this type of project?
2. Which sections feel underdeveloped or lacking sufficient detail?
3. What questions would a technical team likely ask that aren't 
   answered in the current document?
4. What questions would a business stakeholder likely ask that 
   aren't answered?
5. Are there any standard sections missing for AI/chatbot projects 
   in regulated industries?

Current PRD:
[Paste your document]

Provide a detailed gap analysis.
```

**After you run this:**

- Work through the gap analysis and address each item: either add the missing content or document why it doesn't apply to your project.
- Re-run a targeted completeness check after filling gaps to verify.

### Deep Dive on Gaps

```text
**Example Prompt: Section Development**

For the [Technical Architecture] section that you identified as 
underdeveloped, what information should be added?

Current content:
[Paste current section]

Provide:
1. What's missing that readers need to understand the approach?
2. Specific examples of details to add
3. Diagrams or visuals that would help
4. Related sections that should cross-reference this content
5. Questions this section should answer but doesn't yet
```

**After you run this:**

- Be specific in your follow-up prompt: the more precisely you describe what the section currently says and what it's meant to accomplish, the better the suggestions.

### Output for Your PRD

- Gap analysis report
- Checklist of sections to expand
- Specific questions to research or ask stakeholders

## Quality Check 2: Internal Consistency

### Ensure Alignment Across Sections

```text
**Example Prompt: Consistency Check**

Review this PRD for internal consistency:

[Paste complete PRD or key sections]

Check for alignment:

1. **Objectives ↔ Requirements**: Do functional requirements align 
   with stated business objectives?
2. **Requirements ↔ Metrics**: Are success metrics measurable given 
   the proposed solution?
3. **Architecture ↔ Requirements**: Do technical architecture 
   decisions support all functional requirements?
4. **Timeline ↔ Scope**: Are timeline estimates realistic given the 
   scope of requirements?
5. **Risks ↔ Architecture**: Do identified risks match the technical 
   approach described?
6. **Resources ↔ Scope**: Are resource requirements consistent with 
   project scope?

Identify any contradictions, misalignments, or logical inconsistencies. 
For each issue, suggest how to resolve it.
```

**After you run this:**

- Address inconsistencies in order of severity. A misalignment between timeline and scope is a blocker; a missing cross-reference is not.
- If you find a fundamental conflict (e.g., requirements that are impossible given the stated architecture), revisit the affected section before moving on.

### Quality Check 2 Output

- Consistency issues report
- Alignment recommendations
- Sections requiring revision

## Quality Check 3: Requirements Clarity & Testability

### Make Requirements Unambiguous and Verifiable

```text
**Example Prompt: Requirements Clarity Check**

Review these requirements for clarity and testability:

[Paste requirements section]

For each requirement, assess:

1. **Specificity**: Is it specific and unambiguous, or vague and 
   open to interpretation?
2. **Testability**: Can this be verified/validated? How would you test it?
3. **Acceptance Criteria**: Does it have clear, measurable acceptance 
   criteria?
4. **Implied Requirements**: Are there implied requirements that 
   should be made explicit?
5. **Multiple Interpretations**: Could this requirement be understood 
   differently by different teams?

For problematic requirements:
- Flag the issue
- Suggest more specific language
- Provide measurable acceptance criteria
- Offer test cases that would validate it
```

**After you run this:**

- Rewrite any requirement that relies on subjective language ("fast", "easy", "good") using the AI's more specific alternatives.
- Make sure every must-have requirement has an acceptance criterion before the PRD goes to engineering.

### Quality Check 3 Output

- Updated requirements with clear acceptance criteria
- Test cases for validation
- Traceability to objectives

### Refinement Prompt

```text
**Example Prompt: Requirement Refinement**

These requirements are vague or untestable:

1. "Easy to use interface"
2. "Fast search capabilities"
3. "Secure data handling"
4. "Reliable performance"

For each one, provide:
- More specific, measurable language
- Quantifiable acceptance criteria (with thresholds)
- Test cases that would validate the requirement
- Any implied requirements that should be explicit

Context: Healthcare customer service chatbot with SharePoint 
integration, must be HIPAA compliant.
```

**After you run this:**

- Review the refined requirements against the originals — make sure the meaning wasn't changed in ways stakeholders haven't approved.

### Quality Check 3 Refinement Output

- Updated requirements with clear acceptance criteria
- Test cases for validation

## Quality Check 4: Traceability Analysis

### Ensure Every Requirement Has Business Value

```text
**Example Prompt: Traceability Matrix**

Create a traceability matrix showing:

Business Objectives → User Needs → Requirements → Success Metrics

**Business Objectives:**
[Paste objectives]

**User Personas/Needs:**
[Paste user needs]

**Requirements:**
[Paste requirements]

**Success Metrics:**
[Paste metrics]

Analyze:

1. Which requirements don't clearly support a business objective? 
   (May be unnecessary scope)
2. Which business objectives lack supporting requirements? (Gaps)
3. Which requirements don't have measurable success criteria?
4. Are there "nice to have" requirements masquerading as "must haves"?
5. Can we trace the value chain from business goal → user need → 
   requirement → metric for top priorities?

Format as a matrix and provide gap analysis.
```

**Expected Output:**

| Business Objective | User Need | Requirement | Success Metric |
| --- | --- | --- | --- |
| Reduce support costs 30% | Quick access to product docs | SharePoint search <3sec | 40% deflection rate |
| Improve satisfaction | 24/7 availability | Always-on chatbot | CSAT 4.0+ |

**After you run this:**

- Remove or explicitly descope any "orphaned" requirements that can't be traced to a business objective — these are scope creep candidates.
- For any broken chains, either fill the gap or escalate the decision to stakeholders.

### Quality Check 4 Output

- Traceability matrix
- Requirement prioritization validation
- Gap identification

## Quality Check 5: Assumption & Dependency Validation

### Make the Implicit Explicit

```text
**Example Prompt: Assumption Identification**

Based on this PRD, what assumptions are we making that aren't 
explicitly stated?

[Paste PRD]

Consider assumptions about:

**User Behavior:**

- Will users actually use the chatbot?
- Will they trust AI-generated responses?
- Will they provide clear, complete queries?

**Technical Infrastructure:**

- Performance and reliability assumptions
- Data quality and availability
- API stability and backward compatibility

**Organizational Readiness:**

- Resources availability and commitment
- Stakeholder support and prioritization
- Change management capacity

**Data Quality:**

- SharePoint content is complete and accurate
- Documentation is up-to-date
- Metadata and tagging is consistent

**Third-Party Services:**

- Azure OpenAI capacity available when needed
- Service SLAs will be met
- Pricing remains stable

Also identify dependencies on:
- Other systems or teams
- External vendors or partners
- Decisions that haven't been made yet
- Prerequisites that must be completed first

For each assumption/dependency:
- How critical is it?
- What's the risk if it's wrong?
- How can we validate it?
- Who owns it?
```

**Expected Output:**

**Assumptions Table:**

| Assumption | Category | Risk if Wrong | Validation Method | Owner |
| --- | --- | --- | --- | --- |
| SharePoint contains complete product docs | Data Quality | High | Content audit | CS Manager |
| Users will refer customers to chatbot | User Behavior | Medium | Pilot user interviews | Training Lead |

**Dependencies Table:**

| Dependency | Type | Timeline | Owner | Risk |
| --- | --- | --- | --- | --- |
| Azure OpenAI capacity allocation | Technical | Week 1 | IT Team | High |
| Content review and cleanup | Data | Weeks 2-4 | CS Team | Medium |

**After you run this:**

- Assign an owner to each critical assumption before the PRD review. Unvalidated assumptions owned by no one are project risks.
- If an assumption is untestable before the project starts, document it explicitly as a project risk and include a mitigation plan.

### Quality Check 5 Output

- **Assumptions Section**: Explicit list with validation plans
- **Dependencies Section**: With ownership and timing
- **Validation Plan**: How and when to verify assumptions

## Quality Check 6: Stakeholder Perspective Review

### Anticipate Stakeholder Reactions

```text
**Example Prompt: Stakeholder Perspective Analysis**

Review this PRD from different stakeholder perspectives:

[Paste PRD]

**Executive Sponsor:**

- Will they understand the business value and ROI?
- Are risks adequately addressed without being alarming?
- Is the ask (resources, budget, timeline) clear and justified?
- What concerns might they raise?

**Engineering Team:**

- Can they build from this specification?
- Are technical requirements clear and complete?
- Are there technical red flags or concerns?
- What additional information will they need?

**Product Owner/Business Lead:**

- Is scope manageable and well-defined?
- Are priorities clear?
- Is there a path to value delivery in phases?
- What trade-offs might they question?

**Compliance/Legal:**

- Are regulatory requirements adequately covered?
- Are risks documented with mitigation plans?
- Is audit trail and documentation sufficient?
- What approval gates might they require?

**End Users:**

- Will this solve their actual problems?
- Are workflows realistic and practical?
- Is training and support addressed?
- What might cause them to resist or reject it?

For each perspective:
- Likely questions they'll ask
- Concerns they might raise
- Additional information they'd want
- What might cause them to not approve
- What would make them enthusiastic supporters

Provide specific, actionable insights.
```

**After you run this:**

- For any audience where the AI flagged likely concerns, add preemptive content to your PRD or prepare a FAQ section.
- If the engineering team would likely ask technical questions not answered by the current document, address them before the review.

### Quality Check 6 Output

- **Executive Summary**: Tailored to decision-makers
- **Technical Appendix**: For deep-dive technical questions
- **FAQ Section**: Preemptive responses to likely concerns

### Addressing Stakeholder Concerns

```text
**Example Prompt: Pre-emptive FAQ**

Based on the stakeholder analysis, create a FAQ section that 
addresses likely concerns:

**For executives worried about ROI:**
Q: How confident are we in the 30% cost reduction target?
A: [Data-backed response]

**For engineers concerned about feasibility:**
Q: What if SharePoint search is too slow?
A: [Technical mitigation]

**For compliance worried about risk:**
Q: How do we ensure AI doesn't provide dangerous advice?
A: [Guardrails and escalation]

**For users worried about job security:**
Q: Will this replace customer service representatives?
A: [Augmentation, not replacement framing]

Format as Q&A pairs that could be included in appendix or used in 
presentations.
```

**After you run this:**

- Add the FAQ to an appendix in your PRD or use the talking points to prepare for your review meeting.

### Quality Check 6 Concerns Output

- **FAQ Section**: Added as appendix
- **Stakeholder Engagement Plan**: Who to brief, when, on what

## Quality Check 7: Readiness Assessment

### Is the PRD Ready for Stakeholder Review?

```text
**Example Prompt: Readiness Scorecard**

Assess this PRD's readiness for formal stakeholder approval using 
these criteria:

[Paste PRD]

**Completeness** ✅❓❌
- Are all standard sections present and sufficiently detailed?

**Clarity** ✅❓❌
- Are requirements unambiguous and testable?
- Is technical language appropriate for mixed audience?

**Consistency** ✅❓❌
- Are there internal contradictions or misalignments?
- Do all sections support the same story?

**Feasibility** ✅❓❌
- Is the technical approach realistic and well-justified?
- Are timelines achievable given scope?

**Value** ✅❓❌
- Is the business case clear and compelling?
- Are benefits quantified?

**Risk** ✅❓❌
- Are major risks identified with mitigation plans?
- Is risk/reward balance acceptable?

**Actionability** ✅❓❌
- Could a team start implementation from this document?
- Are next steps and decision points clear?

For each criterion:
- Status (✅ Ready / ❓ Needs Work / ❌ Major Gaps)
- Specific issues if not ready
- Estimated effort to address
- Priority for fixing

Provide an overall readiness recommendation:
- Schedule stakeholder review now
- Fix minor issues first (est. X hours)
- Address major gaps before review (est. X days)
- Additional discovery required
```

**Expected Output:**

**Readiness Scorecard:**

| Criterion | Status | Issues | Effort to Fix |
| --- | --- | --- | --- |
| Completeness | ❓ | Missing deployment plan section | 2 hours |
| Clarity | ✅ | Requirements well-defined | - |
| Consistency | ❓ | Timeline/scope misalignment | 1 hour |
| Feasibility | ✅ | Approach validated with tech team | - |
| Value | ✅ | Strong business case with ROI | - |
| Risk | ❌ | No mitigation plans for top risks | 4 hours |
| Actionability | ❓ | Dependencies not clearly assigned | 2 hours |

**Overall Recommendation:** Needs Work - Address risk mitigation and clarify dependencies before stakeholder review (estimated 1 day)

**After you run this:**

- If the recommendation is "Needs Work", treat the identified gaps as a concrete to-do list before scheduling the stakeholder review.
- Use the scorecard as a shared artifact with your team to align on what's blocking approval.

### Quality Check 7 Output

- Readiness recommendation
- Priority fixes list with effort estimates
- Go/no-go decision for review

## The Iterative Refinement Loop

This is not a one-time pass. After running all seven quality checks, use this prompt to consolidate and prioritize what to fix:

```text
**Example Prompt: Issue Prioritization**

Here are issues identified across multiple quality checks:

[Paste findings from all quality checks]

Prioritize these by:

**Blockers** (must fix before stakeholder review):
- Issues that would cause rejection or confusion
- Missing critical information

**Important** (should fix to avoid questions/rework):
- Issues that would trigger significant stakeholder questions
- Inconsistencies that undermine credibility

**Nice-to-Have** (polish but not critical):
- Improvements that enhance but aren't essential
- Minor formatting or style issues

For each priority tier, provide:
- Specific issues
- Estimated effort
- Recommended sequence
- Owner/action
```

**After you run this:**

- Address blockers first. Re-run targeted quality checks on changed sections before moving to lower-priority fixes.
- Keep iterating until the readiness scorecard gives a "Schedule Review" recommendation.

## Wrap-Up

You've now completed all five phases of the AI-accelerated PRD workflow. Here's what you practiced:

| Phase | Skill |
| --- | --- |
| Discovery | Building domain knowledge and structured interview guides with AI |
| Synthesis | Extracting and organizing requirements from messy discovery materials |
| Market Analysis | Validating requirements against competitive benchmarks and industry standards |
| Risk Analysis | Surfacing domain-specific risks and connecting them back to requirements |
| Refinement | Systematically checking a PRD for completeness, consistency, and clarity |

### Going Further

- Compare two versions of a requirement — one from your first draft, one after running Quality Check 3 — and notice what changed.
- Run the readiness scorecard on a real PRD from a past project and see how it scores.
- Try running all seven quality checks on a single PRD section back-to-back and see what each one catches that the others missed.
