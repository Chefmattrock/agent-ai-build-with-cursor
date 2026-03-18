# Example 1: Tech News Summarizer

**Complexity:** Simple (4 actions)
**Pattern:** Input → Fetch → Process → Output

---

## Overview

This agent asks for a technology topic, fetches the latest news from the last 24 hours, and uses an LLM to generate a concise summary.

**Target User:** Anyone who wants a quick daily digest on a tech topic.

**Time Saved:** ~15 minutes of manual research and reading.

---

## Architecture Diagram

```
┌──────────────┐    ┌─────────────────┐    ┌──────────────┐    ┌────────────────┐
│  Get Topic   │ -> │  Fetch News     │ -> │  Summarize   │ -> │  Display       │
│  (user input)│    │  (Google News)  │    │  (LLM)       │    │  (formatted)   │
└──────────────┘    └─────────────────┘    └──────────────┘    └────────────────┘
     ↓                     ↓                      ↓                    ↓
  news_topic         raw_news_data          news_summary         Final output
```

---

## Action Breakdown

### Action 1: Get Topic (order: 0)
**Type:** `get_user_input`

Captures the topic the user wants news about.

```json
{
  "type": "get_user_input",
  "label": "Get Topic",
  "order": 0,
  "inputs": [
    { "name": "input_type", "value": "text" },
    { "name": "input_description", "value": "Enter a tech topic to summarize (e.g., 'Artificial Intelligence', 'Cybersecurity'):" },
    { "name": "required", "value": true },
    { "name": "input_name", "value": "news_topic" }
  ]
}
```

**Output Variable:** `news_topic`

**Voice Note:** The description is friendly and includes examples to guide the user.

---

### Action 2: Fetch Recent News (order: 1)
**Type:** `get_google_news`

Fetches news articles matching the topic from the last 24 hours.

```json
{
  "type": "get_google_news",
  "label": "Fetch Recent News",
  "order": 1,
  "inputs": [
    { "name": "query", "value": "{{news_topic}}" },
    { "name": "date_range", "value": "24h" },
    { "name": "output_variable_name", "value": "raw_news_data" }
  ]
}
```

**Input Variable:** `{{news_topic}}` — References the user's input from Action 1

**Output Variable:** `raw_news_data` — Contains the fetched articles

---

### Action 3: Summarize News (order: 2)
**Type:** `invoke_llm`

Uses GPT-4o-mini to analyze the news and create a structured summary.

```json
{
  "type": "invoke_llm",
  "label": "Summarize News",
  "order": 2,
  "inputs": [
    { "name": "llm_engine", "value": "gpt-5-mini" },
    { "name": "instructions", "value": "You are a tech news editor. Analyze the following news data about '{{news_topic}}' and create a concise summary.\n\nRequirements:\n1. Identify the top 3 most important stories.\n2. For each story, provide a headline and a 2-sentence summary.\n3. Add a 'Key Takeaway' section at the bottom synthesizing the general sentiment.\n\nNews Data:\n{{raw_news_data}}" },
    { "name": "output_variable_name", "value": "news_summary" }
  ]
}
```

**Input Variables:** `{{news_topic}}`, `{{raw_news_data}}`

**Output Variable:** `news_summary`

**Prompt Breakdown:**
- Sets clear role ("tech news editor")
- Provides structured requirements (numbered list)
- Includes both input variables for context
- Asks for specific output format

---

### Action 4: Display Summary (order: 3)
**Type:** `output_formatter`

Shows the final summary to the user with a dynamic heading.

```json
{
  "type": "output_formatter",
  "label": "Display Summary",
  "order": 3,
  "inputs": [
    { "name": "heading", "value": "Daily Tech Digest: {{news_topic}}" },
    { "name": "output_formatted", "value": "{{news_summary}}" },
    { "name": "format", "value": "markdown" }
  ]
}
```

**Input Variables:** `{{news_topic}}`, `{{news_summary}}`

**Note:** The heading includes the topic for personalization.

---

## Key Patterns

### 1. Linear Flow
This agent follows the simplest pattern: Input → Process → Output. No branching, no loops.

### 2. Variable Chaining
Each action's output becomes the next action's input:
- `news_topic` → used by Google News and LLM
- `raw_news_data` → used by LLM
- `news_summary` → used by output

### 3. Good Prompt Engineering
The LLM prompt is structured with:
- Clear role assignment
- Numbered requirements
- Specific output format
- All necessary context included

---

## Lessons Learned

1. **Start simple:** This 4-action pattern covers many use cases.
2. **Include examples in input descriptions:** Helps users understand what to enter.
3. **Use smaller models for simple tasks:** `gpt-5-mini` is enough for summarization.
4. **Dynamic headings:** Including `{{news_topic}}` in the output makes it personal.

---

## When to Use This Pattern

- Single-input agents
- Content summarization
- Data fetching + processing
- Quick information lookups

---

## Full JSON

See `json/news_summarizer.json` for the complete action array.
