# Agent.ai Examples

Real-world agent examples with detailed annotations. Study these to understand common patterns and best practices.

> **Authoritative source:** Always validate action types and input fields against `_builder-kit/03_Build/LLMs.txt`. These examples illustrate patterns but LLMs.txt is the source of truth for the official Agent.AI schema.

---

## Examples Overview

| Example | Complexity | Actions | Key Patterns |
|---------|------------|---------|--------------|
| [News Summarizer](01_simple_news_summarizer.md) | Simple | 4 | Input → Process → Output |
| [Sales Email Writer](02_sales_email_writer.md) | Medium | 22 | Loops, serverless, conditionals |
| [Meeting Prep](03_meeting_prep_agent.md) | Complex | 46 | Triggers, parallel, sub-agents |
| [PMB Generator](04_pmb_generator.md) | Meta | 9 | Multi-input, massive prompts, docs output |

---

## When to Study Each Example

### Start with News Summarizer if you want to:
- Understand basic agent structure
- See the simplest input → output pattern
- Learn variable naming and references

### Study Sales Email Writer if you need to:
- Process URLs from user input
- Run custom code with serverless functions
- Generate multiple variations from one input
- Handle conditional logic for optional features

### Study Meeting Prep if you need to:
- Use triggers (calendar, CRM)
- Process items in parallel
- Compose sub-agents together
- Build complex multi-step workflows

### Study PMB Generator if you need to:
- Create documentation-generating agents
- Handle large, structured prompts
- Save outputs to Google Docs
- Build "meta-agents" that work on other agents

---

## Pattern Coverage

| Pattern | News Summarizer | Sales Email | Meeting Prep | PMB Generator |
|---------|:---------------:|:-----------:|:------------:|:-------------:|
| User Input | ✓ | ✓ | ✓ | ✓ |
| LLM Generation | ✓ | ✓ | ✓ | ✓ |
| Display Output | ✓ | ✓ | ✓ | |
| For Loop | | ✓ | ✓ | |
| Parallel Loop | | | ✓ | |
| If/Else | | ✓ | ✓ | |
| Serverless Function | | ✓ | | |
| Sub-Agent | | | ✓ | |
| Web Scraping | | ✓ | | |
| Trigger | | | ✓ | |
| Google Docs Output | | | | ✓ |

---

## Complexity Levels

### Simple (1-10 actions)
Linear flow, no branching, no loops. Good for learning the basics.

```
[Input] → [Process] → [Output]
```

### Medium (10-25 actions)
Includes loops, conditionals, or serverless functions. Handles multiple steps.

```
[Input] → [Extract] → [Loop: Process Each] → [Generate] → [Output]
```

### Complex (25+ actions)
Multiple data sources, parallel processing, sub-agents, error handling.

```
[Trigger] → [Parallel: Research All] → [Combine] → [Generate] → [Output]
```

### Meta-Agents
Agents that generate documentation, analyze other agents, or create structured outputs for human workflows.

```
[Collect Agent Info] → [Process with Large Prompt] → [Save to External Tool]
```

---

## Raw JSON Files

Need the actual JSON to import or study?

```
04_Examples/json/
├── news_summarizer.json
├── sales_email_writer.json
├── meeting_prep.json
└── pmb_generator.json
```

---

## How to Read These Examples

Each annotated example includes:

1. **Overview** — What the agent does and who it's for
2. **Architecture Diagram** — Visual flow of the agent
3. **Action Breakdown** — Each action explained
4. **Key Patterns** — Techniques you can reuse
5. **Lessons Learned** — What makes this agent work well

---

## Quick Links

- [01: Simple - News Summarizer](01_simple_news_summarizer.md)
- [02: Medium - Sales Email Writer](02_sales_email_writer.md)
- [03: Complex - Meeting Prep](03_meeting_prep_agent.md)
- [04: Meta - PMB Generator](04_pmb_generator.md)
