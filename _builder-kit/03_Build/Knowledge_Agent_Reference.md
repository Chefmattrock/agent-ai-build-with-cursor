# Knowledge Agent Reference

> Documentation for building Knowledge Agents (Hubs) on Agent.AI

> **Authoritative source:** When generating or validating agent JSON, always follow `_builder-kit/03_Build/LLMs.txt` first. It contains the official Agent.AI action schema directly from the platform. The reference below provides context and examples, but LLMs.txt is the source of truth for action types, input fields, and valid values.

---

## Table of Contents

1. [Overview: Two Types of Agents](#overview-two-types-of-agents)
2. [What Are Knowledge Agents?](#what-are-knowledge-agents)
3. [Configuration](#knowledge-agent-configuration)
4. [Knowledge Base](#knowledge-base)
5. [Tools & Integration](#tools--integration)
6. [Conversations & Sharing](#conversations--sharing)
7. [Best Practices](#best-practices)

---

# Overview: Two Types of Agents

Agent.AI offers two types of agents that work powerfully together:

| Aspect | Knowledge Agent | Workflow Agent |
|--------|-----------------|----------------|
| **Interface** | Conversational chat | Step-by-step workflow |
| **How it works** | AI-driven, adaptive | Deterministic, predictable |
| **Best for** | Understanding + action | Automation + tasks |
| **Execution** | Decides what to do | Follows exact steps |
| **User interaction** | Collaborative dialogue | Input → Run → Output |
| **When to use** | Complex, varied requests | Repeatable processes |

## The Power of Combining Both

Knowledge agents invoke workflow agents as tools:

```
User: "Find 10 tech companies in SF and enrich them with LinkedIn data"
         ↓
Knowledge Agent understands the request
         ↓
Calls your "Company Search" workflow agent
         ↓
Gets results, then calls "LinkedIn Enrichment" workflow
         ↓
Presents enriched data conversationally
         ↓
User: "Now save the top 5 to a Google Sheet"
         ↓
Knowledge Agent calls "Export to Sheets" workflow
         ↓
Done! User can keep iterating
```

---

# What Are Knowledge Agents?

Knowledge Agents are conversational AI assistants that combine knowledge, reasoning, and the ability to take action. They're not just chatbots that answer questions - they're collaborative partners that can help you get work done.

Think of knowledge agents as building your own specialized AI assistant that:
- Understands your specific domain or expertise
- Converses naturally to understand what you need
- Calls tools and workflows to actually accomplish tasks
- Works iteratively with you to solve problems
- Gets better as you train it with more knowledge

**The key difference:** Knowledge agents don't just tell you how to do something - they can actually do it for you by invoking workflow agents and integrations.

### When to Use Knowledge Agents

Choose knowledge agents when you want to:

- **Build a Personal Clone or Expert Assistant** - Create an AI version of yourself or an expert in your domain
- **Create Interactive Tools** - Guided workflows, data analysts, content creators, report generators
- **Orchestrate Multiple Workflows** - Understand natural language requests and chain multiple workflows together

---

# Knowledge Agent Configuration

Configuration is where you define your knowledge agent's personality, behavior, and first impression. All configuration happens in the **Introduction** and **Sample Questions** tabs.

## System Instructions (The Most Important Setting)

System instructions are the "brain" of your knowledge agent. This is where you define:
- Who the agent is
- What it does
- How it should behave
- When to use tools
- What boundaries exist

### Anatomy of Good System Instructions

```
[Role & Identity]
You are [role/title]. You [primary function].

[Capabilities]
You can:
- [Capability 1]
- [Capability 2]
- [Capability 3]

[Behavior & Approach]
When users ask you to [task]:
1. [Step 1]
2. [Step 2]
3. [Step 3]

[Tools & When to Use Them]
- Use [tool name] when [condition]
- Call [workflow name] to [accomplish task]

[Boundaries & Limitations]
- Do not [restriction]
- Always [requirement]
- If [condition], then [action]
```

### Example: Research Assistant

```
You are a research assistant that helps users conduct thorough research and analysis.

You can:
- Search your knowledge base for information on topics you've been trained on
- Use the web research tool to find current information online
- Analyze data and generate insights
- Synthesize information from multiple sources

When users ask you to research something:
1. First, search your knowledge base for relevant information
2. If you need current data or information not in your knowledge, use the web research tool
3. Present findings in a clear, organized format with sources cited
4. Ask if they want you to dig deeper into any specific aspect

Use the "Company Research" workflow when users ask about specific companies.
Use the "Web Search" workflow when you need current events or news.

Always cite your sources. If you're not confident about something, say so.
Never make up information - use your tools to find real data.
```

## Welcome Message

The welcome message is the first thing users see. It should:
- Set expectations for what the agent can do
- Show personality/tone
- Encourage engagement
- Include a clear call-to-action

**Example:**
```
Hi! I'm your Research Assistant. I can help you:

- Research companies, industries, and trends
- Analyze information and generate insights
- Find and summarize content from multiple sources

I have access to [describe knowledge base] and can search the web for current information.

What would you like to research today?
```

## Prompt Hint

The prompt hint appears in the input field as placeholder text:
- `"Ask me to research a company or topic..."`
- `"What campaign are you working on?"`
- `"Enter a company name to research..."`

## Sample Questions

Sample questions appear as clickable buttons. Make them specific and actionable:

**Good:**
```
Research the top 10 SaaS companies and their pricing models
Create a social media campaign for our new product launch
Run tests on the authentication module
Analyze our competitors' content strategy
```

**Bad:**
```
Help me with research
Marketing stuff
Run some tests
Look at competitors
```

---

# Knowledge Base

A knowledge base is the collection of information your knowledge agent can search and reference. Think of it as your agent's memory.

## How Knowledge Retrieval Works (RAG)

```
User asks: "What's our refund policy?"
        ↓
Agent converts question to a search query
        ↓
Searches knowledge base for relevant content
        ↓
Finds: "Refund Policy.pdf" - page 2, section 3
        ↓
AI reads the relevant section
        ↓
Generates answer using that specific information
        ↓
Responds: "According to our refund policy, customers can..."
```

## Supported Knowledge Sources

| Source Type | What It's For | Processing Time |
|-------------|---------------|-----------------|
| Files | PDFs, Word docs, text files | 10-30 seconds |
| URLs | Web pages, articles, documentation | 15-45 seconds |
| YouTube | Video transcripts | 20-60 seconds |
| Google Docs | Workspace documents | 10-30 seconds |
| Google Sheets | Spreadsheet data | 10-30 seconds |
| Twitter/X | Tweets and threads | 15-45 seconds |
| LinkedIn | Profiles and posts | 20-60 seconds |

## Knowledge Base Best Practices

**Quality Over Quantity:**
- Curate high-quality, relevant sources
- Remove boilerplate/duplicate content
- Think "What do users actually need to know?"

**Keep Content Fresh:**
- Review quarterly for accuracy
- Update when things change
- Remove outdated info

**Structure Matters:**
- Well-organized with clear headings
- Use bullet points and lists
- Include examples and specifics

**Name Files Descriptively:**
```
Good: "[POLICY] Refund and Return Policy.pdf"
Bad: "Document1.pdf"
```

---

# Tools & Integration

This is where knowledge agents become truly powerful. While knowledge lets your agent understand and answer questions, tools let it actually do things.

## Three Types of Tools

| Tool Type | What It Does | Best For |
|-----------|--------------|----------|
| **Workflow Agents** | Call your existing Agent.AI workflow agents | Custom automations you've built |
| **MCP Servers** | Connect custom tools via Model Context Protocol | Advanced/developer capabilities |
| **Composio Integrations** | Take actions in 100+ external apps | Slack, Gmail, HubSpot, etc. |

## Adding Workflow Agents as Tools

1. Navigate to your knowledge agent builder
2. Click the "Action Agents" tab
3. Check the box next to each workflow you want to enable
4. Click "Save Action Agents Selection"

**Important:** Just enabling a workflow doesn't mean your knowledge agent will use it. Guide the AI through system instructions:

```
You are a marketing assistant with access to several workflows:

- Use the "Competitor Research" workflow when users ask about competitors
- Use the "Content Generator" workflow to create marketing content
- Use the "Social Media Poster" workflow to schedule or publish posts

When a user asks you to research competitors:
1. Call the Competitor Research workflow with the company names
2. Analyze the results
3. Present findings in bullet points
4. Ask if they want you to create content based on the research
```

## Composio Integrations

100+ pre-built integrations including:
- **Communication:** Slack, Gmail, Discord
- **CRM & Sales:** HubSpot, Salesforce, Pipedrive
- **Productivity:** Google Drive, Notion, Asana

---

# Conversations & Sharing

## Conversation Features

- **History** - All messages saved and searchable
- **Auto-generated titles** - AI creates descriptive names
- **Shareable links** - Can be shared publicly
- **Forking** - Others can copy and continue from any point

## Sharing Best Practices

**Do:**
- Review the conversation before sharing
- Share conversations that demonstrate value
- Use as examples in documentation

**Don't:**
- Share sensitive information (emails, passwords, API keys)
- Share conversations with errors if showcasing capabilities
- Assume shared links are private (they're public)

---

# Best Practices

## Prompt Engineering for Knowledge Agents

### Write for AI, Not Humans

**Don't:**
```
You're really good at helping people and should try your best
to be helpful and nice when they ask you things.
```

**Do:**
```
You are a research assistant. When users ask questions:
1. Search your knowledge base first
2. If information isn't found, use the Web Research tool
3. Cite sources in your responses
4. Ask clarifying questions for ambiguous requests
```

### Be Specific About Tool Usage

**Vague (Bad):**
```
You have access to several tools to help users.
```

**Specific (Good):**
```
Tools available:
- "Company Research" workflow: Use when users ask about specific companies
  Input: Company name
  Output: Company data, funding, employee count

- "LinkedIn Enrichment" workflow: Use after Company Research to get people
  Input: Company name from previous research
  Output: Key decision-makers and their profiles

Workflow order: Research → Enrich → Save to CRM
Always get user approval before saving to HubSpot.
```

### Use Examples in System Instructions

```
Present research findings in this format:

## [Company Name]
- Industry: [industry]
- Size: [employee count]
- Funding: [total raised]

**Key People:**
- [Name] - [Title]

**Recent News:**
- [News item 1]

Sources: [List sources used]
```

### Define Boundaries Clearly

```
Do NOT:
- Make up information if you don't know something
- Claim certainty when data is uncertain
- Send emails without showing user the draft first
- Create CRM records without confirming details

If asked to do something outside your capabilities:
"I'm specialized in [your domain]. For [their request],
I recommend [alternative or human handoff]."
```

## Tool Orchestration

### Start with 1-2 Tools, Scale Gradually

**Phase 1:** Single tool - Test it works reliably
**Phase 2:** Add complementary tool - Test they work together
**Phase 3:** Add output tool - Complete workflow end-to-end

### Design Tool Chains

**Research Chain:**
```
Input → Search → Enrich → Analyze → Output
```

**Sales Chain:**
```
Identify → Research → Qualify → Enrich → Save
```

### Add Confirmation Gates

```
System instructions:
"After using Company Research and Enrichment workflows,
show the user:

'I've found [N] prospects:
[List with key details]

Should I create these contacts in HubSpot?'

Only proceed if user explicitly confirms."
```

### Handle Tool Failures Gracefully

```
"If a tool fails:
1. Explain what happened in plain language
2. Offer alternative approaches
3. Ask user what they'd prefer

Example:
'The LinkedIn Enrichment tool isn't responding (likely API rate limit).
I can:
- Continue with the data we have
- Use an alternative enrichment source
- Try again in a few minutes
What works best?'"
```

---

# Quick Reference Card

## Knowledge Agent Setup

1. Create Knowledge Agent in builder
2. Configure: System Instructions, Welcome Message, Sample Questions
3. Train: Upload files, URLs, YouTube videos
4. Tools: Enable workflow agents in Action Agents tab
5. Test: Use chat interface to verify

## Configuration Checklist

- [ ] Clear role and identity in system instructions
- [ ] Capabilities listed explicitly
- [ ] Tool usage rules defined
- [ ] Boundaries and limitations set
- [ ] Welcome message sets expectations
- [ ] Sample questions are specific and actionable
- [ ] Prompt hint guides user input
- [ ] Knowledge base is curated and organized

---

*Documentation compiled from Agent.AI official docs. Last updated: January 2026*
