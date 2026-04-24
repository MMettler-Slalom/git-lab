# Lab Exercise: Creating PRDs with AI

## Objective

Practice the end-to-end workflow for using AI to produce a comprehensive Product Requirements Document. By the end of this lab, you will have:

- Used AI to accelerate stakeholder discovery and domain research
- Synthesized raw discovery materials into structured PRD content
- Validated requirements against market standards and competitive benchmarks
- Identified and mitigated risks across technical, organizational, and compliance dimensions
- Refined your PRD through AI-assisted quality checks

**Estimated time:** 2–3 hours (full pass); individual phases can be completed in 30–45 minutes each

---

## Prerequisites

Before starting, confirm you have the following:

- [ ] **GitHub Copilot Chat** (or another AI assistant) accessible
- [ ] A project or scenario to work from — see the **Reference Materials** section below
- [ ] A working folder for your PRD output

---

## Lab Overview

This lab walks through five sequential phases. Each phase builds on the last — but they can also be used independently as reference prompts when you need them.

| Phase | File | Activity | Time |
| --- | --- | --- | --- |
| **1** | [01-discovery.md](01-discovery.md) | Prepare for stakeholder interviews, build domain knowledge, synthesize findings | ~45 min |
| **2** | [02-synthesis.md](02-synthesis.md) | Transform discovery materials into structured PRD sections | ~45 min |
| **3** | [03-market-analysis.md](03-market-analysis.md) | Research the competitive landscape, validate requirements against market standards | ~30 min |
| **4** | [04-risk-analysis.md](04-risk-analysis.md) | Identify risks, develop mitigation strategies, strengthen requirements | ~30 min |
| **5** | [05-refinement.md](05-refinement.md) | Run quality checks and prepare your PRD for stakeholder approval | ~30 min |

---

## Folder Structure

```text
section-07-lab-prd-creation/
├── README.md                    ← You are here
├── 01-discovery.md              ← Phase 1
├── 02-synthesis.md              ← Phase 2
├── 03-market-analysis.md        ← Phase 3
├── 04-risk-analysis.md          ← Phase 4
└── 05-refinement.md             ← Phase 5

section-05-lab-core-workflow/
└── reference (examples)/
    └── briefs/
        └── 01-healthcare-portal.md   ← Example product brief (used throughout this lab)
```

---

## Why This Workflow Matters

### Traditional PRD Timeline: 4–6 Weeks

- Weeks 1–2: Discovery and research
- Weeks 3–4: Document drafting
- Week 5: Review and rework
- Week 6: Final approval

### AI-Accelerated Timeline: ~2 Weeks

- Days 1–5: Discovery (with AI preparation and real-time synthesis)
- Days 3–6: Market analysis (can run in parallel)
- Days 6–8: Synthesis and structuring
- Days 7–9: Risk analysis (can run in parallel)
- Days 9–10: Refinement and quality checks
- Day 11+: Stakeholder review and approval

The time savings come not from cutting corners — they come from AI handling research, synthesis, and gap detection so you can focus on stakeholder engagement and strategic decisions.

---

## Reference Materials

The prompts in this lab work with **any product or domain** — and they work best when grounded in something real. Before you start, choose your scenario:

**Option A — Use your own project (recommended)**
Bring a current or recent client engagement, an internal product initiative, or a side project you're familiar with. Even rough notes, a problem statement, or a one-page brief is enough to get started. Working from real context will make this lab significantly more valuable.

**Option B — Use the provided example**
A pre-built healthcare patient portal product brief is included if you don't have a project handy or want a consistent reference to follow the examples in each phase file.

> **Example file:** [01-healthcare-portal.md](../section-05-lab-core-workflow/reference%20(examples)/briefs/01-healthcare-portal.md)

**How to attach your materials in GitHub Copilot Chat:**
- Type `#file:` and select your file, or drag it into the chat window
- For notes or documents outside the workspace, paste the relevant content directly into the prompt
- When a prompt says `[paste your context here]`, that's the cue to add your materials

---

## How to Use This Lab in GitHub Copilot

Each phase file contains a set of **example prompts** along with **notes on what to do after you run them**. Here's the pattern to follow:

1. **Open GitHub Copilot Chat** — use the chat panel in VS Code (`Ctrl+Alt+I`) or your preferred AI assistant
2. **Open the phase file** — read through the prompt and any notes before running it
3. **Customize the prompt** — replace any `[bracketed placeholders]` with your actual content or paste in your reference materials
4. **Attach context when needed** — in Copilot Chat, type `#file:` and select the relevant file (e.g., `01-healthcare-portal.md`), or paste content directly into the prompt
5. **Run the prompt** — review the output critically before using it
6. **Follow the "After you run this" notes** — each prompt includes guidance on how to validate and refine the output

> **Heads up — don't lose your work:** In GitHub Copilot Chat, pressing `Enter` submits your message immediately. Use `Shift+Enter` to add line breaks when building multi-line prompts. It's easy to accidentally submit a half-finished prompt with a stray Enter keypress.

> **Tip:** For prompts that ask you to paste discovery notes or transcripts, keep a scratch document open alongside the phase file so you can copy content in quickly.
>
> **Don't have real data yet?** Use the mock generation prompts in the section below to have AI create realistic placeholder content for you before running each phase.

---

## Working Without Real Data

Many prompts in this lab ask you to paste in meeting notes, requirements, or stakeholder inputs that you may not have yet. **Don't let empty placeholders stop you** — use AI to generate realistic mock content first, then run the main prompt against it.

This is also a great way to practice the workflow before applying it to a live project.

### Generate Mock Discovery Notes

Use this before Phase 1 prompts that ask for meeting notes or stakeholder inputs:

```text
I'm practicing a PRD workflow using a healthcare customer service 
chatbot as my example scenario.

Generate realistic mock stakeholder interview notes for:

**Customer Service Director** (15-minute interview summary):
- Current pain points with support operations
- Volume and types of inquiries
- Goals for the AI chatbot
- Concerns about AI adoption

**IT / AI Innovation Lead** (15-minute interview summary):
- Current Azure and AI infrastructure
- Integration constraints (SharePoint, Dynamics, etc.)
- Security and compliance requirements
- Technical risks and preferences

**Compliance Officer** (10-minute interview summary):
- Regulatory concerns (HIPAA, FDA complaint handling)
- Audit and logging requirements
- Any past incidents or lessons learned

Make the notes realistic, specific, and slightly messy — 
the way real meeting notes look, not a polished summary.
```

### Generate Mock Requirements List

Use this before Phase 2 prompts that ask you to paste requirements:

```text
Based on these mock stakeholder notes:
[Paste the output from the mock discovery notes prompt above]

Extract a realistic requirements list for a healthcare customer 
service chatbot. Include a mix of:
- 8-10 functional requirements (what the system does)
- 4-5 non-functional requirements (performance, security, compliance)
- 2-3 business requirements (cost, adoption, reporting)

Use a realistic format with MoSCoW prioritization 
(Must / Should / Could / Won't).
```

### Generate Mock Gap Analysis Answers

Use this before Phase 1 gap identification prompts to pre-populate answers to common gap questions:

```text
For a healthcare customer service chatbot project in early discovery, 
generate realistic answers to these common gap analysis questions:

1. Has user authentication and authorization been addressed?
2. What data privacy and security requirements have been confirmed?
3. Are performance and scalability targets defined?
4. How will error handling and escalation workflows work?
5. Who owns content management and knowledge base updates?
6. What monitoring and analytics are required?
7. What training and change management support is planned?
8. What compliance and audit logging is required?

For each: write a short realistic answer that reflects 
a project in early stages — some things are known, 
some are open questions, a few have conflicting inputs.
```

> **Note:** Mock outputs are useful for practicing the workflow, but always replace them with real stakeholder input before using a PRD in any actual project context.

---

## Pro Tip: Git Commit Hygiene

Treat your PRD work the same way you'd treat code — commit often and with intention. Here's a simple rhythm to follow:

| When | What to commit |
|------|----------------|
| Before starting a new phase | Commit any outputs from the previous phase |
| After saving a meaningful AI output | Commit the draft, even if it's rough |
| After making edits or refinements | Commit the revised version with a note on what changed |
| At the end of each session | Commit everything in progress before you close out |

**Suggested commit message format:**
```
prd(phase-1): initial discovery notes and domain research
prd(phase-2): first draft requirements and personas
prd(phase-2): revised requirements after stakeholder review
```

**Why this matters:**
- You can always roll back to a previous draft if a direction doesn't pan out
- Commit history becomes a log of your thinking and iteration process
- If you're working with a team, small commits make review and merging easier
- AI outputs can drift — having checkpoints lets you compare versions and spot regressions

> **Rule of thumb:** If you'd be annoyed to lose the last 15 minutes of work, commit it now.

---

## Pro Tip: Managing Context Drift

As you move through phases and feed earlier `.md` outputs back into new prompts, a subtle problem can emerge: **context drift**. The AI doesn't automatically remember what it said in a previous conversation — each prompt starts fresh. Over multiple iterations, this means:

- Requirements can silently shift between phases (e.g., a constraint mentioned in Phase 1 gets dropped by Phase 3)
- Conflicting versions of a requirement can coexist across files without the AI flagging the contradiction
- Decisions made in one phase may be reversed in a later one without explanation

**The AI is not maintaining a consistent "source of truth" across sessions — you are.**

### How to protect against drift

**1. Explicitly pass prior decisions forward**

When starting a new phase, don't just paste new notes — also include a brief summary of locked decisions from previous phases:

```text
Before you begin, here are requirements and decisions already 
confirmed in earlier phases that should NOT change:

- [REQ-001] Must integrate with SharePoint for knowledge base
- [REQ-007] Must comply with HIPAA and FDA complaint handling reqs
- Decision: RAG architecture selected over fine-tuning
- Decision: Pilot scope limited to orthopedic product line only

Now, given this context: [paste new materials]
```

**2. Run a drift check between phases**

At the end of each phase, use this prompt before moving on:

```text
Compare these two sets of requirements:

**Phase 1 output (baseline):**
[Paste Phase 1 requirements]

**Phase 2 output (current):**
[Paste Phase 2 requirements]

Identify:
1. Any requirements that changed meaning or scope
2. Any requirements that disappeared without explanation
3. Any new requirements that contradict earlier decisions
4. Any constraints from Phase 1 that are no longer reflected

Flag each issue and suggest whether it's an intentional refinement 
or a drift that needs to be reconciled.
```

**3. Maintain a running decisions log**

Keep a single file (e.g., `decisions.md`) alongside your phase outputs that captures locked requirements and key decisions. Update it at the end of each phase and reference it at the start of the next.

> This is another reason the Git commit hygiene above matters — your commit history is a lightweight audit trail that lets you spot when and where a requirement changed.

---

## Key Principles

Keep these in mind throughout the lab:

1. **AI is a collaborator, not a replacement.** You bring domain expertise, stakeholder relationships, and judgment. AI accelerates research, synthesis, and quality checks — it does not replace your thinking.

2. **Iterate, don't generate once.** Use AI across multiple cycles. Expect to draft, check, refine, and re-check.

3. **Validate, don't assume.** AI-generated insights should be confirmed with stakeholders and subject matter experts before they go into a PRD.

4. **Review every output.** The prompts in this lab will get you most of the way there. The last mile requires your judgment.

---

**Start with:** [Phase 1 — Discovery](01-discovery.md)
