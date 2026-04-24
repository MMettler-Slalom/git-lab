# SO AI Training 101 (Lab Materials)
This repository is a comprehensive training program that provides hands-on labs, exercises, and supporting materials for Solution Ownership AI Enablement. Its purpose is to help Solution Owners develop practical skills for leading AI-enabled product teams throughout the entire product delivery lifecycle.

The repository includes structured sections covering core tooling setup, workflows, agent creation, PRD development, backlog creation, and skill development—progressively building competencies for managing AI-driven product initiatives.

---

## 📚 Curriculum Syllabus

This training program is structured as a progressive series of labs that build competency across the entire product delivery lifecycle. Each section builds on previous learning to develop mastery in using AI tools for product leadership.

### **Section 04: Lab - Core Tooling Setup**
**Duration:** 60 minutes | **Foundation Layer**

Establish the development environment and tools you'll use throughout the program.

- **Lab: VS Code, Git, and GitHub Copilot Setup**
  - Install and configure Visual Studio Code
  - Initialize Git and understand version control basics
  - Authenticate and activate GitHub Copilot
  - Verify your AI assistant is working locally

**Outcome:** Working development environment with GitHub Copilot integrated and ready for AI-assisted workflows.

---

### **Section 05: Lab - Core Workflow**
**Duration:** 90 minutes | **Workflow Layer**

Learn the foundational workflow for converting raw materials into structured context for AI processing.

- **Lab: Context Ingestion & AI-Assisted Synthesis**
  - Step 1: Signal Assessment — evaluate source documents for decision-relevance
  - Step 2: Context Ingestion — use GitHub Copilot Agent mode to synthesize high-signal materials into structured context files
  - Step 3: Gap Identification — use Ask mode to identify missing context and refine
  - Step 4: Version Control — commit artifacts using VS Code Source Control
  - Reference Example: Healthcare Portal brief structure

**Outcome:** Three structured context files (overview, challenges summary, technology opportunities) from raw discovery materials, versioned in Git.

---

### **Section 06: Lab - Create Agent**
**Duration:** 60 minutes | **Tool Building Layer**

Build custom AI agents to extend Copilot's capabilities for domain-specific tasks.

- **Lab: Creating Copilot Agents**
  - Define agent name and description
  - Write agent instructions and guardrails
  - Upload product documentation and FAQs
  - Create suggested prompts for common user questions
  - Example: Product FAQ Assistant agent

**Outcome:** A functional Copilot Agent configured to answer questions about a product using uploaded documentation.

---

### **Section 07: Lab - PRD Creation**
**Duration:** 120 minutes | **Product Requirements Layer**

Master the AI-accelerated workflow for creating comprehensive, high-quality Product Requirement Documents in 2 weeks vs. 4-6 weeks.

- **Phase 1: Discovery Acceleration**
  - Conduct AI-prepared stakeholder interviews
  - Synthesize findings in real-time
  - Identify gaps early

- **Phase 2: Synthesis**
  - Extract and structure requirements
  - Develop user personas and use cases
  - Define success metrics

- **Phase 3: Market & Competitive Analysis**
  - Research competitive landscape
  - Benchmark features and pricing
  - Identify industry trends

- **Phase 4: Risk Analysis**
  - Identify comprehensive risks
  - Develop mitigation strategies
  - Validate assumptions

- **Phase 5: Refinement & Quality Checks**
  - Assess completeness and consistency
  - Validate requirements clarity
  - Prepare for stakeholder approval

**Outcome:** A comprehensive, validated PRD ready for team alignment and implementation planning.

---

### **Section 08: Lab - Backlog Creation**
**Duration:** 120 minutes | **Backlog Planning Layer**

Transform PRD requirements into actionable epics and user stories with proper scope, acceptance criteria, and traceability.

- **Templates & Patterns**
  - Epic template structure with scope, requirements, and success metrics
  - User story template with acceptance criteria and compliance notes

- **Authoring from Source**
  - Extract epics from major capability areas in the PRD
  - Create user stories tied to personas and scenarios
  - Maintain citations back to source requirements
  - Organize by feature area and priority

- **Provided Epics & Stories**
  - 15+ example epics covering: RBAC, RAG, integrations, security, compliance, monitoring, performance
  - 40+ example user stories demonstrating patterns for common features

**Outcome:** A complete, structured product backlog with epics and stories ready for sprint planning and development.

---

### **Section 09: Lab - Create Skill**
**Duration:** 150 minutes | **Skill Development Layer**

Build reusable, packaged workflows that extend your AI assistant's capabilities for your team's specific processes.

- **Part 1: Using Skills**
  - Understand skill architecture (SKILL.md, references, templates, scripts)
  - Experience the brief-builder skill end-to-end
  - Learn natural language triggering

- **Part 2: Customizing Skills**
  - Adapt existing skills to your domain
  - Modify instructions and templates
  - Add project-specific references

- **Part 3: Creating Skills**
  - Identify repeatable workflows on your team
  - Package instructions and reference materials
  - Create multi-step workflows with checkpoints
  - Test and validate with real tasks

- **Provided Setup Guides**
  - GitHub Copilot skill setup
  - Claude Code skill setup
  - OpenCode skill setup

**Outcome:** Custom skills your team can use immediately to accelerate product work—with knowledge packaged, templates included, and workflows automated.

---

## 🎯 Learning Progression

```
Foundation → Workflow → Tools → PRD → Backlog → Skills
   Lab 04      Lab 05    Lab 06   Lab 07   Lab 08   Lab 09
```

Each lab builds on the previous:
- **Lab 04** gives you the tools
- **Lab 05** teaches the core workflow
- **Lab 06** shows how to extend tools for your needs
- **Lab 07** applies the workflow to real PRD creation
- **Lab 08** converts PRDs to executable plans
- **Lab 09** packages everything into reusable team workflows

---

## 🚀 How to Use This Training

1. **Complete labs sequentially** — each builds on prior knowledge
2. **Use the provided examples** — each lab includes reference materials to follow if you don't have your own project
3. **Apply to a real project** — every lab supports bringing your own materials; working from real context produces more useful output
4. **Create artifacts you'll use** — each lab produces deliverables for your actual product work
5. **Build skills the team can share** — the final lab creates templates and workflows for your whole team

---

## 📁 Repository Structure

```
section-04-lab-core-tooling-setup/      → Dev environment & GitHub Copilot
section-05-lab-core-workflow/            → Signal assessment & context synthesis
section-06-lab-create-agent/             → Building custom AI agents
section-07-lab-prd-creation/             → AI-accelerated PRD workflow (5 phases)
section-08-lab-backlog-creation/         → Epic and story creation from PRD
section-09-lab-create-skill/             → Building reusable team skills
```

---