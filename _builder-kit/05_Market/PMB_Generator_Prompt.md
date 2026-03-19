# PMB Generation Prompt

> **SETUP REQUIRED:** Replace every `{{ placeholder }}` in this file with your own company, team of agents, brand, and audience details before using this prompt. Once customized, paste this into your AI assistant (along with the three inputs) to generate a complete Product Marketing Brief.

You are an expert product marketer creating a comprehensive Product Marketing Brief (PMB) for an agent. Your goal is to create a detailed, actionable PMB that gives the marketing team everything they need to position, launch, and promote this agent.

---

## Context: What is {{ COMPANY_NAME }}?

{{ COMPANY_DESCRIPTION }}

*(Replace with a 2–3 paragraph description of your company. Include:*
*- What it is and what it does*
*- Who it's built for*
*- What makes it different*
*- What it is NOT (important for scoping agent capabilities correctly))*

---

## Goals

**Company Goal:** {{ COMPANY_GOAL }}

*(Example: "Empower millions of nontechnical people at SMBs to save time and drive meaningful results with AI.")*

**Team Goal:** {{ TEAM_GOAL }}

*(Example: "Build a trusted, delightful agent marketplace full of valuable, relevant and useful agents for nontechnical people to use frequently.")*

**Primary Metric:** {{ PRIMARY_METRIC }}

*(Example: "Weekly Active Users (WAU)")*

---

## Brand Voice

{{ BRAND_NAME }}'s voice is {{ VOICE_CORE_DESCRIPTORS }}.

*(Paste your full voice guidelines here, or reference `_builder-kit/04_Polish/Brand_Voice.md`)*

**Apply this voice to ALL user-facing copy in the PMB:**
- Descriptions and one-liners should sound like a smart friend explaining something, not a product page
- Pain points should be visceral and emotionally honest, not corporate bullet points
- Video scripts and social hooks should sound natural, not scripted
- Use contractions (you'll, don't, here's, that's)
- Be specific over generic — real examples beat vague claims every time

---

## Target User Audience

This solution is built for {{ TARGET_USER_DESCRIPTION }}.

*(Example: "ambitious professionals at small and mid-sized businesses who are curious about AI but don't consider themselves 'technical.' They're busy, motivated, and ready to work smarter.")*

### Primary User Segments

| Segment | Description | Needs |
|---------|-------------|-------|
| **{{ PERSONA_1_NAME }}** | {{ PERSONA_1_PMB_DESCRIPTION }} | {{ PERSONA_1_PMB_NEEDS }} |
| **{{ PERSONA_2_NAME }}** | {{ PERSONA_2_PMB_DESCRIPTION }} | {{ PERSONA_2_PMB_NEEDS }} |

*(Add or remove rows as needed. Fill from your `_builder-kit/01_Ideate/Personas.md`.)*

**Key insight:** {{ AUDIENCE_KEY_INSIGHT }}

*(Example: "They don't want to 'learn AI' for its own sake — they want practical, plug-and-play agents that help them save time, hit their numbers, and do their best work with less effort.")*

---

## Marketing Frameworks to Apply

### Hell Island / Heaven Island
Position the transformation the agent provides. This is the emotional core of the PMB:
- **Hell Island:** The painful current state BEFORE the agent. Be brutally specific about the pain — not just "it takes too long" but describe the frustration, the wasted time, the anxiety, the missed opportunities. Make it visceral.
- **Heaven Island:** The dream end result AFTER using the agent. Paint the aspirational vision — not just "save time" but describe the confidence, the relief, the results they'll achieve.
- **The Bridge:** How the agent transports them from Hell Island to Heaven Island, in one sentence.

### Current Workarounds
This is ROI ammunition. Identify what people do today instead of using this agent and quantify the cost:
- **The Manual Process:** Step-by-step description of their current approach, including tools used and time per step
- **Time Investment:** Total time per instance, frequency, annual time cost
- **Pain Points in the Workaround:** Tedious/repetitive, error-prone, tool switching, context switching, scalability issues, quality inconsistency, knowledge dependency
- **Hidden Costs:** Labor cost, error correction, opportunity cost, team bottlenecks, training burden
- **Workaround Fatigue Indicators:** Real quotes that sound like what frustrated users would say

### Before/After Scenarios
Concrete comparison of the user's world before and after the agent, plus a narrative transformation story with a specific person, a real scenario, and a meaningful outcome.

---

## Input for PMB Generation

You will receive three inputs to generate the PMB:

**Input 1: Agent/Feature Description**
```
{{agent_info}}
```
This contains the high-level description of what the agent/feature does, what problem it solves, and who it's for.

**Input 2: Agent PRD (Product Requirements Document)**
```
{{agent_prd}}
```
This contains the detailed product requirements including user stories, requirements, technical considerations, UX/UI flow, and agent configuration.

**Input 3: Agent JSON Configuration**
```
{{agent_json}}
```
This contains the technical details of the agent's workflow, including:
- Actions used
- Variables and data flow
- Control flow logic (If/Else, For Loops)
- Integrations and API calls
- Input requirements
- Output format

Use these inputs together to populate every section of the PMB. The PRD provides the strategic context. The JSON provides the behind-the-scenes technical capabilities. The agent description provides the positioning anchor.

---

## PMB Structure to Follow

Generate a complete PMB with these sections, matching the structure in `_builder-kit/05_Market/PMB_Template.md` EXACTLY.

---

## Output Instructions

1. Generate a complete PMB following the EXACT structure in `PMB_Template.md` — every section, every subsection, in order
2. Be specific and detailed — each section should have substantial, usable content. Avoid placeholders or generic filler.
3. Use {{ PLATFORM_NAME }} terminology for agents, actions, and workflows
4. Extract behind-the-scenes capabilities from the agent JSON — name specific actions, models used, and data flows
5. Make the Hell Island / Heaven Island section emotionally compelling — this is the heart of the PMB
6. Current Workarounds should be detailed enough to calculate ROI — include time estimates, tool names, and dollar costs
7. Write the Transformation Story as a realistic narrative with a named character, not a generic description
8. Video script should be timed and specific enough that someone could film it
9. Social media hooks should be ready to post, not templates
10. SEO keywords should be realistic estimates, not made-up numbers
11. Use {{ BRAND_NAME }} brand voice throughout — {{ VOICE_CORE_DESCRIPTORS }}
12. Primary metric is always {{ PRIMARY_METRIC }}
13. Prioritize the end-user experience in all messaging — focus on the person running the agent, not the person who built it
14. Use proper markdown formatting with clear headers (# for h1, ## for h2, ### for h3) and consistent structure

Generate the PMB now.
