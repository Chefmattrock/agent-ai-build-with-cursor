# Example 2: Sales Email Writer

**Complexity:** Medium (22 actions)
**Patterns:** User input, loops, serverless functions, conditionals, multi-variation output

---

## Overview

This agent generates personalized sales emails based on user input. It extracts URLs from prospect intelligence, scrapes and summarizes that content, then generates three email variations tailored to the user's tone and style.

**Target User:** Sales reps and BDRs who want to write personalized outreach.

**Time Saved:** ~20 minutes per email vs. manual research and drafting.

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              INPUT COLLECTION                                    │
├─────────────────────────────────────────────────────────────────────────────────┤
│  [Email Type] -> [Tone] -> [Prospect Intel] -> [Email Length] -> [Specific Ask] │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      v
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              URL EXTRACTION & SCRAPING                           │
├─────────────────────────────────────────────────────────────────────────────────┤
│  [Extract URLs] -> [For Each URL] -> [Scrape] -> [Summarize] -> [Collect]       │
│      (LLM)           (loop)         (serverless)    (LLM)      (add_to_list)    │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      v
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              CONDITIONAL LINKEDIN                                │
├─────────────────────────────────────────────────────────────────────────────────┤
│  [If LinkedIn URL] -> [Get Profile] -> [End If]                                 │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      v
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              EMAIL GENERATION                                    │
├─────────────────────────────────────────────────────────────────────────────────┤
│  [Generate 3 Email Variations] -> [Display Output]                              │
│      (massive prompt with all context)                                          │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

## Action Breakdown

### Phase 1: Input Collection (Actions 0-4)

| # | Action | Type | Variable Created |
|---|--------|------|------------------|
| 0 | Email Type | `get_user_input` | `email_type` |
| 1 | Tone | `get_user_input` | `tone` |
| 2 | Prospect Intel | `get_user_input` | `prospect_intel` |
| 3 | Email Length | `get_user_input` | `email_length` |
| 4 | Specific Ask | `get_user_input` | `specific_ask` |

**Key Design Choice:** Each input is separate, not combined into a form. This allows clearer descriptions and better flow.

**Example Input Description:**
> "What do you know about them? (LinkedIn profiles, CRM notes — anything helps)"

---

### Phase 2: URL Extraction & Scraping (Actions 5-11)

#### Action 5: Extract URLs from Prospect Intel
```json
{
  "type": "invoke_llm",
  "inputs": [
    { "name": "llm_engine", "value": "gpt-5-nano" },
    { "name": "instructions", "value": "Extract any URLs from the following text and return them as a JSON array of strings. If no URLs found, return []. Text: {{prospect_intel}}" },
    { "name": "output_variable_name", "value": "extracted_urls" }
  ]
}
```

#### Action 6-7: Initialize and Loop
```json
{ "type": "set_variable", "inputs": [{ "name": "variable_name", "value": "url_summaries" }, { "name": "value", "value": "[]" }] }

{ "type": "for_condition", "inputs": [{ "name": "list_variable", "value": "extracted_urls" }, { "name": "item_variable", "value": "current_url" }] }
```

#### Action 8: Serverless Web Scraper
This is the key custom code piece. It uses Python to scrape web content:

```json
{
  "type": "serverless_function",
  "inputs": [
    { "name": "language", "value": "python" },
    { "name": "code", "value": "import requests\nfrom bs4 import BeautifulSoup\n\nurl = '{{current_url}}'\nresponse = requests.get(url, timeout=10)\nsoup = BeautifulSoup(response.content, 'html.parser')\n\n# Extract text content\nfor script in soup(['script', 'style']):\n    script.decompose()\ntext = soup.get_text(separator=' ', strip=True)\n\n# Limit to first 5000 chars\nresult = text[:5000]" },
    { "name": "output_variable_name", "value": "scraped_content" }
  ]
}
```

**Why Serverless?** The built-in `grab_web_text` action works for most cases, but serverless gives you full control over parsing logic.

#### Actions 9-11: Summarize and Collect
- LLM summarizes each page's content
- `add_to_list` appends to `url_summaries`
- `end_condition` closes the loop

---

### Phase 3: Conditional LinkedIn (Actions 12-15)

```json
{ "type": "if_condition", "inputs": [{ "name": "query", "value": "'linkedin.com' in '{{prospect_intel}}'" }] }
{ "type": "get_linkedin_profile", "inputs": [...] }
{ "type": "end_condition" }
```

**Pattern:** Check if LinkedIn URL exists before calling the LinkedIn API. Avoids errors on empty input.

---

### Phase 4: Email Generation (Actions 16-21)

#### The Massive Prompt

The email generation prompt includes:
- User's LinkedIn profile (from `user_linkedin_profile` variable)
- User's writing style (from `user_writing_style` variable)
- All context gathered (prospect intel, URL summaries, LinkedIn data)
- Email type-specific guidelines
- Tone mapping
- Length constraints

**Prompt Structure:**
```
## CONTEXT
[User profile, writing style]

## PROSPECT INTELLIGENCE
[prospect_intel]
[url_summaries]
[linkedin_data if available]

## EMAIL REQUIREMENTS
- Type: {{email_type}}
- Tone: {{tone}}
- Length: {{email_length}}
- Specific Ask: {{specific_ask}}

## EMAIL TYPE GUIDELINES
[Detailed instructions for each email type]

## OUTPUT FORMAT
Generate exactly 3 variations...
```

---

## Key Patterns

### 1. URL Extraction → Loop → Scrape
A powerful pattern for processing unknown URLs from user input:
```
[Extract URLs with LLM] → [For Each] → [Scrape/Process] → [Collect Results]
```

### 2. Serverless for Custom Logic
When built-in actions aren't enough, serverless functions let you run any code:
- Web scraping with BeautifulSoup
- Data transformation
- Complex calculations
- API calls with custom authentication

### 3. Conditional API Calls
Wrap expensive or conditional operations in if/else:
```
[If condition] → [API Call] → [End If]
```
Prevents errors and saves API calls.

### 4. Multi-Variation Output
Instead of generating one email, generate three variations. Gives users options without running the agent multiple times.

### 5. User Context Variables
The agent uses pre-defined user context:
- `user_linkedin_profile` — User's LinkedIn data
- `user_writing_style` — Saved writing style preferences

This personalization happens automatically for returning users.

---

## Lessons Learned

1. **Break inputs apart:** Separate questions get better answers than one giant form.
2. **Summarize before using:** Don't pass raw scraped content to the final LLM. Summarize first.
3. **Use nano models for extraction:** Simple tasks (URL extraction, ID parsing) work fine with smaller models.
4. **Conditional calls prevent errors:** Always check before calling APIs that might fail on empty input.
5. **Three variations > one variation:** Users appreciate options.

---

## When to Use This Pattern

- Content generation with external research
- Multi-step data gathering
- Personalized output based on user context
- Any workflow needing custom code logic

---

## Full JSON

See `json/sales_email_writer.json` for the complete action array.
