# Lab Exercise: Creating a Copilot Agent

**Tool:** Microsoft Copilot Studio (via Microsoft Teams)
**Estimated Time:** 20 minutes

---

## Step 1: Create a New Agent

1. Open **Microsoft Teams**.
2. Click **Copilot** in the left navigation menu.
   > **Don't see it?** Click the **"..."** (More apps) button at the bottom of the left sidebar, search for **Copilot**, and click the result to open it. To pin it for future use, right-click the Copilot icon and select **"Pin"**.
3. In the Copilot panel, scroll to the bottom and click **"Create agent"**.
4. In the Agent Builder, navigate to the **Configure** tab.
5. In the **Name** field, enter:
   > `[Your Product Name] Assistant`
   *(e.g., "Slack Assistant")*
   > **Note:** This lab uses Slack as the example product — a Slack FAQ document is provided for you to upload in Step 3. This same approach works for any product, as long as you have a document (FAQ, user guide, etc.) you can reference.
6. In the **Description** field, add a short summary of what your agent does.
   > Example: *"An agent that answers simple FAQ questions about my product."*

---

## Step 2: Add Agent Instructions

1. Still in the **Configure** tab, locate the **Instructions** field.
2. Copy and paste the following instructions into the field:

```
You are a helpful product assistant. You have access to all of the key documentation about this product.

- Your role is to provide product guidance based on existing documentation, such as FAQs, product documents
- Your goal is to be as helpful as possible
- Do not make up any answers. If you cannot find an answer, let the user know you do not know
- Provide references and links to source information
```

---

## Step 3: Add Knowledge Sources

This is where you connect your agent to real product content so it can answer questions accurately.

1. In the **Configure** tab, scroll down to the **Knowledge** section.
2. Choose **one** of the following options:

   **Option A — Upload a file:**
   - Click **"Upload from device"**
   - Select your Product FAQ guide (PDF, Word doc, etc.)
   - If you don't have one available, use the example provided: [Slack_Product_FAQ.pdf](Slack_Product_FAQ.pdf)

   **Option B — Add a website URL:**
   - In the URL/name input field, enter the link to your product documentation website
   - Press Enter to add it

> **Tip:** You can toggle "Only use specified sources" to ON to prevent the agent from pulling in unrelated web results.

---

## Step 4: Add Suggested Prompts

Suggested prompts give users a quick-start experience when they open the agent. Add the following three prompts:

| # | Title | Message |
|---|-------|---------|
| 1 | Key Product Features | What are the key features of this Product? |
| 2 | Product Onboarding | How do I get started with this product? |
| 3 | Product Support | How do I get technical support for this product? |

**How to add each prompt:**
1. Scroll to the **Suggested Prompts** section in the Configure tab.
2. Click **"+ Add a suggested prompt"**.
3. Enter the **Title** and **Message** from the table above.
4. Repeat for all three prompts.

---

## Step 5: Create and Test Your Agent

1. Click the **"Create"** button in the upper right corner of the Agent Builder.
2. Once created, click the **"Try it"** tab to open a live preview of your agent.
3. You'll see your three suggested prompts displayed as clickable tiles:
   - *Key Product Features*
   - *Product Onboarding*
   - *Product Support*
4. Click each prompt tile and review the responses.

**Evaluate your agent:**
- Are the responses accurate based on your knowledge source?
- Does the agent cite or reference the source material?
- Does it admit when it doesn't know something (rather than making up an answer)?
- Are you satisfied with the overall quality of responses?

---

## Summary

By completing this exercise you have:
- Created a named agent aligned to a specific product goal
- Defined its role, behavior, and boundaries through instructions
- Connected it to real product documentation as a knowledge source
- Added guided prompts to help users interact with it
- Tested it to validate accuracy and behavior

---

## Optional: Other Agent Building Platforms

This lab uses Microsoft Copilot Studio, but it's one of many platforms where you can build AI agents. Here's a quick overview by category:

**Microsoft & Google Ecosystem**
| Platform | Notes |
|----------|-------|
| Microsoft Copilot Studio | Teams-integrated, no-code (what this lab uses) |
| Google Agentspace / Vertex AI Agent Builder | Google's equivalent, integrates with Google Workspace |

**Major AI Platform Builders**
| Platform | Notes |
|----------|-------|
| OpenAI GPT Builder | Create custom GPTs via ChatGPT's interface, very low barrier to entry |
| Anthropic Claude Projects | Build agents via the API or Claude.ai's Projects feature |
| Amazon Bedrock Agents | AWS-native agent builder with tool use and knowledge bases |

**CRM & Business Platforms**
| Platform | Notes |
|----------|-------|
| Salesforce Agentforce | Build agents directly inside Salesforce CRM workflows |
| ServiceNow AI Agents | Agents embedded in IT/HR service management |
| Zendesk AI Agents | Customer support focused |

**Low-Code / No-Code Builders**
| Platform | Notes |
|----------|-------|
| Voiceflow | Conversational agent builder with a visual canvas |
| Botpress | Open-source, strong for customer-facing chatbots |
| Stack AI | Drag-and-drop agent and workflow builder |

**Developer-Focused Frameworks**
| Platform | Notes |
|----------|-------|
| LangChain / LangGraph | Python-based, highly flexible agent orchestration |
| AutoGen (Microsoft) | Multi-agent framework for more complex workflows |
| CrewAI | Focuses on teams of specialized agents working together |
| Semantic Kernel | Microsoft's SDK for integrating AI into apps |

> The right choice usually comes down to a few factors — your technical skill level, where your data lives, and what the agent needs to do.

---

**Next:** [Section 07 — Creating PRDs with AI](../section-07-lab-prd-creation/README.md)
