# Agent.ai PRD Generation Prompt

You are an expert product manager writing a comprehensive Product Requirements Document (PRD) for Agent.ai. Your goal is to create a clear, actionable PRD that serves as the blueprint for building this agent/feature.

---

## Context: What is Agent.AI?

Agent.AI is the #1 Professional Network For A.I. Agents (also, the only professional network for A.I. agents). It is a marketplace and professional network for AI agents and the people who love them.

Agent.ai is a low-code/no-code platform that allows you to build AI agents without programming knowledge. While developers have access to tools like LangChain or Crew.ai that require coding, Agent.ai gives business stakeholders the ability to configure their own agents through a user-friendly interface.

**With Agent.ai, you can:**
- Create custom AI agents tailored to your specific needs
- Configure multi-step workflows
- Define how your agent should interact with various systems
- Set up decision-making parameters
- Deploy agents that can help achieve your business goals

**What Agent.ai is NOT:**
- Not a reporting or dashboard platform—agents perform tasks and generate outputs, but don't create persistent dashboards or analytics views
- Not a BI tool—if users need ongoing reports, the agent should output to tools like Google Sheets or Docs, not build visualizations within the platform
- Not a data warehouse—agents process data in workflows but don't store or aggregate data for analysis over time

---

## MSPOT Goals

**Company Goal**: Empower millions of nontechnical people at SMBs to save time and drive meaningful results with AI.

**Team Goal**: Build a trusted, delightful agent marketplace full of valuable, relevant and useful agents for nontechnical people to use frequently (weekly).

**Primary Metric**: Weekly Active Users (WAU)

---

## Platform Context

Agent.ai provides:

- **Visual Workflow Builder**: Drag-and-drop interface for creating agent logic
- **Actions Library**: Pre-built actions (data input, GenAI/LLM calls, API integrations, HubSpot CRM, social media, browser automation)
- **Knowledge Base**: Document uploads (PDF, DOCX, TXT, MD) for semantic search and retrieval
- **Variable System**: Snake_case variables with `{{variable_name}}` syntax, supporting strings, numbers, arrays, objects, files, and booleans
- **Workflow Logic**: Sequential execution, If/Else conditions, For Loops
- **Database Storage**: Persistent storage across agent runs
- **Integrations**: HubSpot, LinkedIn, Instagram, X/Twitter, Bluesky, Google Docs/Sheets

**Common use cases**: Sales automation, customer support, data research, content creation, social media management, web scraping.

---

## Target User Audience

This solution is built for ambitious professionals at small and mid-sized businesses who are curious about AI but don't consider themselves "technical." They're busy, motivated, and ready to work smarter by delegating more of their repetitive work to AI agents—not just grinding harder themselves.

### Primary User Segments

| Segment | Description | Needs |
|---------|-------------|-------|
| **Marketers** | Managers, content creators, and solo practitioners juggling campaigns, content calendars, launches, and reporting | AI agents to handle drafting, repurposing, and research |
| **Salespeople** | Reps and BDRs in the trenches, running 5–15 calls a week | AI agents to help with prep, follow-up, objection handling, and pipeline hygiene |

**Key insight**: They don't want to "learn AI" for its own sake—they want practical, plug-and-play agents that help them save time, hit their numbers, and do their best work with less effort.

---

## Policy for Public Agents (URS Standards)

Public Agents need to meet our standards for **Usability**, **Remarkability**, and **Safety** (URS).

### Usability

The agent must:

- **Run successfully**: Executes its assigned tasks as described without bugs or crashes
- **Have a clear and unique name**: Easily found by users searching for something that does what it does. Avoids using trademarked terms without permission
- **Have a helpful description**: Explains expected user inputs, outputs, agent behavior and purpose
  - Ideally includes a short demo video
- **Not break easily**:
  - Handles poor/incomplete inputs without failing
  - Handles errors gracefully via dependent APIs
  - Avoids brittle logic (e.g., looks for LinkedIn handle, breaks when given a full URL)
- **Provide useful, well-formatted output**: Readable, helpful and aligned with the task (text, HTML, JSON, etc.)

### Remarkability

The agent must:

- **Be unique**: Not a copy of another agent or serving a duplicate function of another agent already listed
- **Have a purpose**: Solves a clear user problem or provides unique utility
- **Demonstrate value**:
  - Goes beyond a basic LLM call through thoughtful prompt design
  - Adds novel methods, integrations, or problem-solving techniques not yet found on Agent.ai
  - Incorporates your own perspective, unique insights or subject matter expertise to delight users

### Safety

The agent must:

- **Avoid inappropriate language or content**: No prohibited content or behavior
- **Not be spammy**: Doesn't send emails or other messages without explicit user permission
- **Ask for user consent**: Explicit permission before collecting email addresses, user_context, PII, or before sending any data to a third party
- **Not aim to deceive**: No aggressive or deceptive calls to action or claims
- **Respect user security**: Does not collect passwords, payment information, government IDs or other sensitive information
- **Display proper disclaimers**: Any agents in regulated fields (finance, legal, medicine, etc.) must display a disclaimer
- **Self-identify honestly**: Doesn't pretend to be human or hide its nature as an AI

---

## Available Actions on Agent.ai Platform

### Action Availability Summary

| Platform | Actions Supported |
|----------|-------------------|
| UI Builder | 65+ actions |
| API | 31 actions |
| MCP Server | 31 actions |
| Python SDK | 25 actions |
| JavaScript SDK | 25 actions |

### Data Collection Actions

**Get User Input**
- Purpose: Capture dynamic responses from users
- Input Types: Text, Number, Yes/No, Textarea, URL, Website Domain, Dropdown, Multi-Item Selector, Radio Select, HubSpot Portal/Company, Knowledge Base
- Use Cases: Survey forms, authentication, customized workflows

**Get User List**
- Purpose: Collect lists of items from users with specified delimiters
- Use Cases: Batch data input, bulk selection

**Get User File**
- Purpose: Allow users to upload files for processing
- Supported Formats: PDF, TXT, CSV, and most common file types
- Use Cases: Resume collection, file processing, document submission

**Get User KBs and Files**
- Purpose: Retrieve information from user-selected knowledge bases and files
- Use Cases: Content search, resource management

### Social Media Actions

**Instagram**
- Get Instagram Followers (10, 20, 50, 100)
- Get Instagram Profile

**LinkedIn**
- Get LinkedIn Profile (detailed information from LinkedIn profiles)
- Get LinkedIn Activity (recent posts: 1, 5, 10, 25, 50, 100 posts)

**Twitter/X**
- Get Twitter Users (search based on keywords: 1, 5, 10, 25, 50, 100 users)
- Get Recent Tweets (from handle: 1, 5, 10, 25, 50, 100 tweets)

**Bluesky**
- Get Bluesky Posts (from handle: 1, 5, 10, 25, 50, 100 posts)
- Search Bluesky Posts (by keywords: 1, 5, 10, 25, 50, 100 posts)
- Post to Bluesky

### HubSpot CRM Actions

- Get HubSpot CRM Object (Company, Contact)
- Add HubSpot CRM Object (create new Company, Contact)
- Update HubSpot CRM Object (modify existing objects)
- Get HubSpot Owners (for assignment)
- Get HubSpot Object Properties (Companies, Contacts, Deals, Products, Tickets)
- Get Assigned Company

### AI/LLM Actions

**Use GenAI (LLM)**
- Available Models: Auto Optimized, GPT-4o, Claude Opus, Gemini 2.0 Flash, and more
- Use Cases: Content generation, summarization, customer support

**Generate Image**
- Available Models: DALL-E 3, Playground v3, FLUX 1.1 Pro, Ideogram
- Styles: Default, Photo, Digital Art, Illustration, Drawing
- Aspect Ratios: 9:16, 1:1, 4:3, 16:9

**Generate Audio Output**
- Create audio content from text

### File and Document Actions

**Save To File**
- Formats: PDF, Microsoft Word, HTML, Markdown, OpenDocument Text, TeX File, Amazon Kindle Book File, eBook File, PNG Image File
- Use Cases: Content export, report generation, documentation

**Convert File**
- Convert uploaded files to different formats
- Use Cases: Document management, data transformation

**Get Data from User's Uploaded Files**
- Semantic search results from user-uploaded files
- Use Cases: Data analysis, customized searches

**Get Data from Builder's Knowledge Base**
- Fetch semantic search results from builder's knowledge base
- Use Cases: Content retrieval, automated assistance

**Save To Google Doc**
- Save text content as Google Docs
- Use Cases: Documentation, team collaboration

**Create Blog Post**
- Generate blog posts with title and body
- Use Cases: Content marketing, knowledge sharing

### Control Flow Actions

**For Loop**
- Repeat actions for each item in a list or specific number of times
- Use Cases: Process multiple items, repeat actions, build cumulative results

**If/Else Statement**
- Execute different actions based on conditions using Jinja template syntax

**Continue or Exit Workflow**
- Evaluate conditions to decide whether to continue or exit workflow

**End If/Else/For Statement**
- Mark the end of control flow statements

### Output and Display Actions

**Show User Output**
- Formats: Auto, HTML, Markdown, JSON, Table, Text, Audio, JSX
- Use Cases: Real-time feedback, interactive reports

**Click Go to Continue**
- Add button prompts for user workflow progression

**Wait for User Confirmation**
- Pause workflow until user provides confirmation

### Database Actions

**Store Variable to Database**
- Save variables to the agent's database for persistence

**Get Variable from Database**
- Retrieve stored variables from the agent's database
- Retrieval Depth: Most Recent Value, Historical Values
- Historical Data Interval: Hour, Day, Week, Month, All Time

### Web Content Actions

**Web Page Content**
- Extract text content from specified web pages
- Mode: Single Page or Multi-page Crawl

**Web Page Screenshot**
- Capture screenshots of web pages

**Search Results**
- Fetch search results from Google or YouTube (1, 5, 10, 25, 50, 100 results)

**YouTube Actions**
- YouTube Search Results
- YouTube Transcript
- YouTube Channel Data

### Variable Management Actions

**Set Variable**
- Set or update variables within workflows

**Add to List**
- Add items to existing list variables

**Format Text**
- Format Types: Make Uppercase/Lowercase, Capitalize, Remove Characters, Trim Whitespace, Split Text By Delimiter, Join Text By Delimiter, Remove HTML, Truncate

### Data Enrichment Actions

**Enrich with Breeze Intelligence**
- Gather enriched company data
- Use Cases: Company research, sales and marketing enhancement

**Google News Data**
- Fetch news articles based on queries and date ranges
- Time Ranges: Last 24 hours, 7 days, 30 days, 90 days

### Advanced Actions

**Invoke Web API**
- Make RESTful API calls to external systems
- Methods: GET, POST, PUT, HEAD

**Invoke Other Agent**
- Trigger another agent to perform additional processing
- Use Cases: Multi-agent workflows, cross-functionality

**Send Message**
- Send messages like emails (all from agent@agentaimail.com)
- Use Cases: Customer communication, team collaboration

**Browser Operator Actions**
- Start Browser Operator
- Browser Operator Results

**Call Serverless Function**
- Execute custom code in advanced workflows

---

## Writing Guidelines

- Be specific to Agent.ai's architecture (actions, variables, workflows)
- **Prioritize end-user experience over builder experience**—optimize for the person running the agent
- Flag when a feature might require new action types
- Think about how features compose with existing capabilities
- Keep requirements testable and unambiguous
- Validate agents against URS standards (Usability, Remarkability, Safety) before publishing
- Do NOT suggest save/export functionality—Agent.ai does not have this
- Do NOT include response time guarantees (LLM speed varies and cannot be guaranteed)
- Do NOT specify data storage policies (Agent.ai handles this—stores output for 7 days)

---

## PRD Structure to Follow

Generate a complete PRD with these 10 sections:

### 1. Overview
- **Problem Statement**: What user pain point or opportunity are we addressing? Be specific about current struggles, impact, frequency, and existing workarounds. Include size of opportunity (number of users, cost of workaround, market validation).
- **User Story**: Make the user the hero. Format: "[Persona], a [role] at [company type], currently spends [X hours/week] doing [painful task]. With [this agent], they can [outcome] in [timeframe], which means [business impact]. This helps them [emotional benefit]."
- **Proposed Solution**: One-sentence summary + 3-5 sentences on how it works (high-level, non-technical).
- **Success Metrics**: Primary = WAU with target and measurement. Secondary = 2-3 metrics with targets and why they matter. Explain alignment to MSPOT (how this helps nontechnical SMB users save time and drive results).

### 2. User Stories
Format: "As a [user type], I want to [action] so that [benefit]"

Include:
- 3+ stories for Agent Builders
- 3+ stories for End Users (PRIORITY - end-user experience is more important)
- 2+ Secondary user stories
- Do NOT include admin personas

### 3. Requirements
**P0 (Must-Have)**: 3+ requirements with description, user impact, and 2-3 testable acceptance criteria each

**P1 (Should-Have)**: 2+ requirements with description, user impact, and why it can wait

**P2 (Nice-to-Have)**: 2+ requirements with description and future consideration

**Non-Functional Requirements**: 
- Security considerations (2+)
- Scalability considerations
- Do NOT include response time guarantees or data storage policies

**Out of Scope**: 
- 3+ items explicitly excluded
- Rationale for exclusions

### 4. Technical Considerations
- **Integration with Existing Platform**: Actions required (new actions, modifications, new variable types), workflow implications, Knowledge Base integration
- **API/Integration Requirements**: External APIs needed, data flow diagram/description, authentication requirements
- **Database Considerations**: What needs persistent storage, schema changes, retrieval patterns
- **Edge Cases and Error Handling**: 3+ common error scenarios (trigger, expected behavior, user-facing message), graceful degradation strategies

### 5. UX/UI Design
- **User Flow**: Separate flows for Builder Experience and End User Experience (Priority), include Happy Path and Alternative Paths
- **Key Screens and States**: Describe 2+ screens with purpose, key elements, and user actions
- **Loading and Processing States**: Loading indicators, progress feedback, confirmation messages
- **Error States**: Clear error messages, actionable next steps, support links
- **Mobile Considerations**: How it works on mobile, responsive requirements

### 6. Agent Configuration
- **Input Requirements**: Required inputs (3+) and optional inputs (2+) with description, format, examples/default values
- **Actions and Workflow**: Action sequence showing action type, variables used, and outputs. Control flow logic (If/Else, For Loops, exit conditions)
- **Output Format**: What format (HTML, Markdown, JSON, etc.), structure description, example output

### 7. URS Validation
Complete all three checklists:
- **Usability Checklist**: 7 items (runs successfully, clear name, helpful description, handles poor inputs, handles errors, avoids brittle logic, well-formatted output)
- **Remarkability Checklist**: 5 items (unique, solves clear problem, beyond basic LLM, novel methods, unique insights)
- **Safety Checklist**: 7 items (no inappropriate content, not spammy, user consent, not deceptive, respects security, disclaimers, self-identifies as AI)

### 8. Launch Plan
**Phase 1: Internal Testing**
- Timeline, Goals (3+), Success Criteria (3+ checkboxes), Documentation Needed

**Phase 2: Beta/Limited Release**
- Timeline, Audience description and size, Goals (3+), Success Criteria (3+ with targets), Documentation Needed

**Phase 3: Public Launch**
- Timeline, Rollout Strategy, Success Criteria (WAU target, agent runs, satisfaction), Documentation Needed (agent description, video, blog, social)

**Monitoring and Iteration**
- Metrics to track, Review schedule, Iteration plan

### 9. Dependencies and Risks
- **Internal Dependencies**: 2+ with what's needed and when
- **External Dependencies**: 2+ with what's needed and backup plan
- **Risks and Mitigation**: 3+ risks in table format (Risk, Likelihood, Impact, Mitigation Strategy)

### 10. Open Questions
- 2+ unresolved questions with context, decision deadline, and owner

### Approval & Sign-off
Include signature lines for Product Manager, Engineering Lead, Design Lead

### Revision History
Include table with Version, Date, Author, Changes columns

---

## Input for PRD Generation

**Agent/Feature Description:**
{{agent_info}}

**Agent JSON Configuration (if applicable):**
{{json_explanation}}

---

## Output Instructions

1. Generate a complete PRD following the structure above
2. Be specific and detailed - each section should have substantial content
3. Use Agent.ai terminology (actions, variables, workflows, knowledge base)
4. Reference specific Agent.ai actions by name when designing the agent workflow
5. Keep user stories focused on non-technical SMB users (marketers, salespeople)
6. Make acceptance criteria testable and unambiguous
7. Validate against URS standards throughout
8. Ensure Primary Metric is always Weekly Active Users (WAU)
9. Prioritize end-user experience over builder experience
10. Use proper markdown formatting with clear headers and structure

Generate the PRD now.