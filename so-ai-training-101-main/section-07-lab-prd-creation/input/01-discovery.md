# Phase 1: Discovery

**Goal:** Build the context, questions, and frameworks you need before and during stakeholder conversations — so your discovery is faster, more comprehensive, and less dependent on personal experience alone.

---

## Step 1: Internal Discovery (Before Client Conversations)

### Check Internal Assets First

Before jumping into external research, understand what your organization has already built or learned.

**Key questions to ask your internal team:**

- What has your organization already built in this space?
- What patterns exist in your practice areas?
- Who on your team has done similar work?

```text
**Example Prompt: Preparing for Internal Conversations**

I'm about to talk to our team implementing Azure Foundry for customer 
service in the EU. What questions should I ask to inform requirements 
gathering for a similar US-based medical device project?

Focus on:
- What's worked well vs. challenges encountered
- Reusable components and patterns
- Technical gotchas or constraints
- Realistic timelines and effort estimates
```

**Value**: Go into client meetings more confident, ask better questions, provide more accurate estimates.

## Step 2: Domain Research & Context Building

### Understanding the Business Domain

Before stakeholder conversations, use AI to quickly build domain knowledge.

```text
**Example Prompt: Domain Research**

I'm meeting with the Customer Service Director at a medical device 
company to discuss requirements for an AI chatbot. 

Please help me understand:
1. Common pain points in medical device customer service
2. Regulatory considerations (FDA, quality systems, complaint handling)
3. Typical customer support scenarios for orthopedic products
4. Industry-specific compliance requirements

Provide a concise overview that will help me ask informed questions.
```

**After you run this:**

- Skim the output for accuracy — AI may not know your specific regulatory context. Correct any gaps.
- Save the overview as a reference before your stakeholder meeting.
- Highlight 2–3 domain-specific terms or concepts to work into your questions naturally.

### Generating Stakeholder-Specific Interview Guides

Create targeted question sets for different stakeholder types.

```text
**Example Prompt: IT/Technical Team Interview Guide**

I'm meeting with an IT team working on AI innovation at a healthcare 
company. They're considering an Azure-based customer service chatbot 
with SharePoint integration.

Generate an interview guide covering:

**Technical Landscape:**
- Current Azure services and AI/ML workloads
- Azure OpenAI deployment status
- SharePoint structure and content management
- Security and compliance requirements

**AI Maturity & Lessons Learned:**
- Existing AI initiatives and outcomes
- Reusable patterns or frameworks
- User adoption challenges
- Organizational dynamics

**Project Context:**
- What's driving interest in this chatbot
- Scope considerations (internal, customer-facing, or both)
- Timeline and resource constraints
- Success criteria

Format as open-ended questions that encourage detailed responses.
```

**After you run this (IT/Technical guide):**

- Review each question — remove any that are too generic or already answered.
- Add questions specific to the technical constraints you already know about.
- Flag any questions that might feel threatening to the stakeholder and soften the framing.

```text
**Example Prompt: Business Stakeholder Interview Guide**

I'm meeting with Customer Service Leadership at a healthcare company
about implementing an AI chatbot.

Generate an interview guide covering:

**Current State:**
- Pain points in current support processes
- Volume and types of inquiries handled
- Existing tools and systems
- Team structure and responsibilities

**Goals & Success:**
- What would success look like
- Metrics they currently track
- Cost and efficiency goals
- Quality and customer satisfaction priorities

**Concerns & Constraints:**
- What worries them about AI adoption
- Change management considerations
- Integration with existing workflows
- Training and support needs

Include follow-up questions for common responses.
```

**After you run both guides:**

- Combine the most important questions from each into a single prioritized list for your meeting.
- Aim for 10–15 questions per stakeholder — enough to drive a 45–60 minute conversation without rushing.

## Step 3: During and After Stakeholder Conversations

### Real-Time Synthesis

Transform conversational notes into structured insights.

```text
**Example Prompt: Extract Requirements from Notes**

Here are my notes from a stakeholder interview:

[Paste your meeting notes]

Please:
1. Extract all requirements mentioned (functional, non-functional, 
   business, technical)
2. Categorize each as Must-Have, Should-Have, or Nice-to-Have
3. Note which stakeholder mentioned each requirement
4. Identify any constraints or dependencies
5. Flag requirements that seem ambiguous or need clarification

Format as a structured list.
```

**After you run this:**

- Review the extracted requirements and correct any misinterpretations.
- For anything marked ambiguous, write down the clarifying question you'll ask in the next conversation.
- Add requirements you recall from the meeting that the AI missed.

### Identify Conflicts Early

```text
**Example Prompt: Identify Requirement Conflicts**

Based on these requirements from different stakeholders:

**From Customer Service Director:**
[List requirements]

**From IT Team:**
[List requirements]

**From Compliance Officer:**
[List requirements]

Please identify:
1. Conflicting requirements across stakeholders
2. Technical requirements that may conflict with business goals
3. Regulatory requirements that constrain the solution
4. Implied requirements that weren't explicitly stated but are necessary
5. Missing requirements based on this type of project

For each conflict, suggest questions to resolve it.
```

**After you run this:**

- Prioritize the conflicts by how much they'd affect scope or architecture.
- Schedule follow-up questions with the right stakeholders to resolve the most critical conflicts before drafting begins.

## Step 4: Gap Identification

### Completeness Checking

Ensure you've covered all necessary areas before moving forward.

```text
**Example Prompt: Gap Analysis**

I'm gathering requirements for a customer service chatbot for a 
healthcare company with Azure Foundry and SharePoint integration.

Here are the requirements gathered so far:
[Paste current requirements]

What critical areas haven't been adequately addressed? Consider:
- User authentication and authorization
- Data privacy and security
- Performance and scalability
- Error handling and escalation workflows
- Content management and updates
- Monitoring and analytics
- Training and change management
- Compliance and audit requirements

For each gap, provide specific questions to ask stakeholders.
```

**After you run this:**

- For each gap: either schedule a follow-up question, or note it as an open item in your discovery notes.
- Don't wait until synthesis to surface gaps — resolve what you can now.

## Step 5: Building Your PRD Foundation

### Creating the Initial Structure

Before writing the full PRD, organize your findings into a logical structure.

```text
**Example Prompt: PRD Structure from Discovery**

Based on these discovery materials:
- [Summary of stakeholder conversations]
- [Key requirements identified]
- [Constraints and dependencies noted]

Create an outline for a comprehensive PRD with these sections:
1. Executive Summary
2. Business Objectives
3. User Personas and Use Cases
4. Functional Requirements
5. Non-Functional Requirements
6. Technical Architecture
7. Success Metrics
8. Risks and Mitigation
9. Timeline and Milestones

For each section, note what information I already have and what still 
needs to be gathered or validated.
```

**After you run this:**

- Review what the AI flagged as already known vs. still needed.
- Use the "still needed" list to guide your remaining stakeholder conversations.
- This outline becomes your starting point for Phase 2.

## The Meta Question

End every stakeholder conversation with this powerful question:

> **"If you were in my shoes starting this discovery process, what's the one thing you'd make sure to understand or validate early that would save headaches later?"**

This often surfaces:

- Unwritten organizational rules
- Political dynamics
- Technical gotchas
- Past project failures and lessons learned

## Reflection

Before moving on to Phase 2, consider:

- Which stakeholder conversation gave you the most useful signal? Why?
- What gaps or conflicts did you surface that you wouldn't have caught without AI assistance?
- Is there any area where you still feel uncertain about the requirements?

---

**Next:** [Phase 2 — Synthesis](02-synthesis.md)
