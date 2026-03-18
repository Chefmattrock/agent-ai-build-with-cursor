# Example 4: PMB Generator (Meta-Agent)

**Complexity:** Meta (9 actions)
**Patterns:** Multi-input collection, massive prompt engineering, Google Docs output, meta-agent pattern

---

## Overview

This is a "meta-agent" — an agent that generates documentation for other agents. After you've built an agent and written its PRD, this agent creates a Product Marketing Brief (PMB) to help you market it.

**Target User:** Agent builders who need to create go-to-market materials.

**Time Saved:** ~2-3 hours of marketing copywriting per agent.

---

## What Makes This a Meta-Agent?

Unlike typical agents that solve end-user problems, meta-agents operate on other agents:

| Typical Agent | Meta-Agent |
|---------------|------------|
| Helps end users do tasks | Helps builders document/improve agents |
| Takes user data as input | Takes agent info, PRD, or JSON as input |
| Outputs content for users | Outputs documentation or marketing materials |

**Examples of Meta-Agents:**
- PMB Generator (this one)
- PRD Generator
- Agent JSON Validator
- Agent Performance Analyzer

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              INPUT COLLECTION                                    │
├─────────────────────────────────────────────────────────────────────────────────┤
│  [Agent Info] -> [Agent PRD] -> [Agent JSON]                                    │
│   (textarea)      (textarea)     (textarea)                                     │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      v
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              PMB GENERATION                                      │
├─────────────────────────────────────────────────────────────────────────────────┤
│  [Massive LLM Prompt with All Context + Marketing Frameworks]                   │
│   - Hell Island / Heaven Island positioning                                     │
│   - Current workarounds analysis                                                │
│   - Video structure templates                                                   │
│   - AEO optimization                                                            │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      v
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              OUTPUT                                              │
├─────────────────────────────────────────────────────────────────────────────────┤
│  [Format as Markdown] -> [Save to Google Doc]                                   │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

## Action Breakdown

### Phase 1: Input Collection (Actions 0-2)

#### Action 0: Agent Information
```json
{
  "type": "get_user_input",
  "inputs": [
    { "name": "input_type", "value": "textarea" },
    { "name": "input_description", "value": "Describe what your agent does, who it's for, and the problem it solves:" },
    { "name": "input_name", "value": "agent_info" }
  ]
}
```

#### Action 1: Agent PRD
```json
{
  "type": "get_user_input",
  "inputs": [
    { "name": "input_type", "value": "textarea" },
    { "name": "input_description", "value": "Paste the agent's PRD (Product Requirements Document):" },
    { "name": "input_name", "value": "agent_prd" }
  ]
}
```

#### Action 2: Agent JSON
```json
{
  "type": "get_user_input",
  "inputs": [
    { "name": "input_type", "value": "textarea" },
    { "name": "input_description", "value": "Paste the agent's JSON configuration:" },
    { "name": "input_name", "value": "agent_json" }
  ]
}
```

**Why Three Inputs?**
- **Agent Info:** High-level understanding for messaging
- **Agent PRD:** Requirements and user stories for pain points
- **Agent JSON:** Technical capabilities for feature descriptions

---

### Phase 2: PMB Generation (Actions 3-5)

This is where the magic happens. A single, massive LLM call with:
- All three inputs
- Agent.ai brand voice guidelines
- Marketing frameworks
- Output structure requirements

#### The Massive Prompt (Abbreviated)

```
You are a product marketing expert creating a PMB for an Agent.ai agent.

## BRAND VOICE
[Agent.ai voice guidelines - warm, clear, helpful, human]

## INPUTS
Agent Description: {{agent_info}}
Agent PRD: {{agent_prd}}
Agent JSON: {{agent_json}}

## MARKETING FRAMEWORKS

### Hell Island / Heaven Island
- Hell Island: The painful current state before the agent
- Heaven Island: The transformed state after using the agent
- The Bridge: How the agent creates the transformation

### Current Workarounds
Identify what people do today instead:
- Manual process (time cost, error rate)
- Hire someone (money cost, quality issues)
- Use inferior tools (limitations, frustrations)
- Skip it entirely (consequences, missed opportunities)

### Video Structure
- Hook (0-5s): Pattern interrupt or curiosity gap
- Bumper (5-10s): What they'll learn/see
- Content (10-60s): Demo the transformation

### AEO (Answer Engine Optimization)
- Questions the agent answers
- Natural language queries
- How to show up in AI search results

## OUTPUT STRUCTURE
Generate a complete PMB with:
1. Core Product Info
2. Positioning (Hell → Heaven)
3. Technical Context
4. Marketing Ammunition
5. Content Hooks
6. SEO/AEO Strategy
```

---

### Phase 3: Output (Actions 6-8)

#### Action 6: Format as Markdown
```json
{
  "type": "invoke_llm",
  "inputs": [
    { "name": "instructions", "value": "Format the following PMB content as clean markdown with proper headers, bullet points, and tables:\n\n{{pmb_content}}" },
    { "name": "output_variable_name", "value": "formatted_pmb" }
  ]
}
```

#### Action 7: Save to Google Doc
```json
{
  "type": "save_to_google_doc",
  "inputs": [
    { "name": "title", "value": "PMB: {{agent_name}}" },
    { "name": "content", "value": "{{formatted_pmb}}" },
    { "name": "folder_id", "value": "" }  // Creates in root
  ]
}
```

**Why Google Docs?**
- Easy to share with team
- Editable after generation
- Integrates with existing workflows
- Professional format

---

## Key Patterns

### 1. Meta-Agent Pattern
Agents that work ON other agents, taking agent artifacts as input:
```
[Agent Info] + [Agent PRD] + [Agent JSON] → [Documentation/Analysis]
```

### 2. Massive Prompt Engineering
When you need complex, structured output, pack everything into one powerful prompt:
- All context and inputs
- Frameworks and guidelines
- Clear output structure
- Examples of good output

### 3. Multi-Input Collection
Gather multiple pieces of information separately:
```
[Input 1] -> [Input 2] -> [Input 3] -> [Process All Together]
```

### 4. Document Output
Save structured content to external tools:
```
[Generate Content] -> [Format] -> [Save to Google Docs/Sheets]
```

---

## Marketing Frameworks Explained

### Hell Island / Heaven Island

| Hell Island | The Bridge | Heaven Island |
|-------------|------------|---------------|
| What's painful now | How agent helps | What's possible after |
| 2 hours of research | Automated intelligence | 2 minute briefing |
| Missed context | CRM + LinkedIn + News | Complete picture |
| Stressed, unprepared | Confidence | Ready, informed |

### Current Workarounds ROI

| Workaround | Cost | Downside |
|------------|------|----------|
| Manual research | 2 hours × $50/hr = $100 | Inconsistent quality |
| Hire VA | $20/hr + training time | Not always available |
| Skip it | $0 | Lost deals from poor prep |

### Video Hook Patterns

| Pattern | Example |
|---------|---------|
| Provocative question | "What if you never walked into a meeting blind again?" |
| Bold claim | "I prep for meetings in 2 minutes. Here's how." |
| Pain amplification | "Stop wasting 30 minutes researching before every call." |

---

## Lessons Learned

1. **Meta-agents are powerful:** Once built, they accelerate your whole agent workflow.

2. **Massive prompts work:** With enough context and structure, one LLM call can produce comprehensive output.

3. **External doc output is practical:** Users can edit, share, and iterate on Google Docs.

4. **Marketing frameworks are reusable:** Hell Island/Heaven Island works for any agent.

5. **Take technical input, produce human output:** The PMB translates JSON into messaging.

---

## When to Use This Pattern

- Documentation generation
- Marketing content creation
- Agent analysis or validation
- Any "meta" workflow on agents themselves

---

## Full JSON

See `json/pmb_generator.json` for the complete action array.
