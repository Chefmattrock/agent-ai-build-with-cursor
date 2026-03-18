# Agent Naming & Description Guidelines

> **SETUP REQUIRED:** Replace every `{{ placeholder }}` with your own examples and platform-specific conventions. See `CUSTOMIZE.md` for guidance. The core principles and structure are ready to use as-is.

This guide covers how to name your agent and write a compelling description that helps users find and understand what it does.

---

## Core Naming Principles

### 1. Clarity Over Cleverness
The name should instantly communicate what the agent does. Avoid puns, wordplay, or brand-y names that sacrifice clarity.

### 2. Outcome-First Orientation
Lead with the primary outcome or domain. Users scan for what they need — put the most important keyword first.

### 3. Avoid Technical Language
Your users are non-technical. Skip jargon, acronyms, and insider terms.

### 4. Searchability and Discovery
Think about what users would type when searching. Make your name match their mental model.

### 5. Consistency Across Platform
Follow {{ PLATFORM_NAME }} patterns so your agent fits naturally alongside others.

*(Replace `{{ PLATFORM_NAME }}` with your platform's name, e.g. "Agent.ai", "your marketplace", etc.)*

---

## The Naming Formula

```
[Primary Outcome or Domain] + [Task or Role]
```

### Examples

| Name | Why It Works |
|------|--------------|
| {{ NAMING_EXAMPLE_1 }} | {{ NAMING_EXAMPLE_1_WHY }} |
| {{ NAMING_EXAMPLE_2 }} | {{ NAMING_EXAMPLE_2_WHY }} |
| {{ NAMING_EXAMPLE_3 }} | {{ NAMING_EXAMPLE_3_WHY }} |
| {{ NAMING_EXAMPLE_4 }} | {{ NAMING_EXAMPLE_4_WHY }} |
| {{ NAMING_EXAMPLE_5 }} | {{ NAMING_EXAMPLE_5_WHY }} |

*(Fill these in with real examples from your agent catalog or target domain. Generic reference examples: "Meeting Prep", "Lead Scoring", "SEO Audit", "Sales Email Writer")*

### Optional Qualifiers

You can add specificity when needed:

| Qualifier Type | Example |
|---------------|---------|
| Audience | "B2B Lead Scorer" |
| Integration | "HubSpot Contact Enricher" |
| Versioning | "Meeting Prep v2" (internal only) |

---

## Names to Avoid

| Pattern | Example | Why It Fails |
|---------|---------|--------------|
| Filler words | "AI Smart Lead Scorer" | "AI" and "Smart" add no value |
| Vague terms | "Business Helper" | Too generic to be useful |
| Technical jargon | "NLP Entity Extractor" | Users don't know what this means |
| Clever wordplay | "The Lead Whisperer" | Unclear what it does |
| Long compound | "Automated Sales Prospecting Research and Outreach Tool" | Not scannable |

---

## Naming Checklist

Before finalizing your name, confirm:

- [ ] Is it instantly clear what this agent does?
- [ ] Is the most important keyword first?
- [ ] Would a non-technical user understand it?
- [ ] Is it short (2–4 words)?
- [ ] Is it scannable in a list?
- [ ] Would users search for these words?
- [ ] Does it avoid filler words (AI, Smart, Auto, Magic)?
- [ ] Is it free of trademarked terms?

---

## Description Guidelines

### Lead with Value

Start with the benefit, not the mechanics. Tell users what they'll get, then explain how.

**Bad:** "This agent uses GPT-4 to analyze meeting notes and extract action items."

**Good:** "Never miss a follow-up again. This agent turns messy meeting notes into a clean list of action items — who's doing what, and by when."

### Keep It Short

Aim for 1–2 sentences + optional bullets. Users skim.

**Structure:**
```
[1-sentence value promise]

[1-sentence summary of how it helps]

- [Key capability or feature]
- [Time saved or outcome]
- [What makes it unique]
```

### Use Everyday Language

Write like you're explaining to a smart friend who doesn't work in tech.

| Instead of... | Say... |
|---------------|--------|
| "Leverages NLP capabilities" | "Reads and understands your notes" |
| "Integrates with your CRM" | "Pulls in your contacts from {{ EXAMPLE_CRM }}" |
| "Generates actionable insights" | "Tells you what to do next" |

*(Replace `{{ EXAMPLE_CRM }}` with a CRM your users actually use, e.g. HubSpot, Salesforce)*

### Be Specific, Not Vague

Concrete details build trust. Vague claims feel like marketing fluff.

| Vague | Specific |
|-------|----------|
| "Saves you time" | "Prep for meetings in 2 minutes instead of 20" |
| "Improves your emails" | "Write sales emails that match your voice and actually get replies" |
| "Helps with research" | "Get company size, funding, and recent news before your call" |

### Describe Outputs, Not Internals

Users care about what they receive, not how it's made.

| Internal focus | Output focus |
|----------------|--------------|
| "Uses semantic search to query knowledge bases" | "Finds the right info from your uploaded docs" |
| "Runs parallel API calls for efficiency" | "Gets you answers fast — usually under 30 seconds" |

---

## Description Checklist

Before publishing, confirm:

- [ ] Does it lead with value (benefit first)?
- [ ] Is it 1–2 sentences + optional bullets?
- [ ] Does it use everyday language?
- [ ] Is it specific, not vague?
- [ ] Does it describe outputs, not internals?
- [ ] Does it explain expected inputs?
- [ ] Would a non-technical user understand it?

---

## Before/After Examples

### Example 1: {{ NAMING_BEFORE_AFTER_1_NAME }}

**Before:**
> "{{ NAMING_BEFORE_1 }}"

**After:**
> "{{ NAMING_AFTER_1 }}"

*(Fill in with a real example from your domain)*

---

### Example 2: {{ NAMING_BEFORE_AFTER_2_NAME }}

**Before:**
> "{{ NAMING_BEFORE_2 }}"

**After:**
> "{{ NAMING_AFTER_2 }}"

---

## Style Rules

### Always lowercase "agent" in copy
- ✓ "This agent helps you..."
- ✗ "This Agent helps you..."

### Skip filler words
These add no value: AI, Smart, Auto, Magic, Intelligent, Advanced, Ultimate, Pro

### Use active, confident phrasing
- ✓ "Prep for meetings in 2 minutes"
- ✗ "Can help you potentially prepare for meetings"

### Match your brand voice
See `04_Polish/Writing_Style_Guide.md` for full details.

---

## Quick Reference

| Element | Pattern | Example |
|---------|---------|---------|
| **Name** | [Outcome/Domain] + [Task/Role] | {{ QUICK_REF_NAME_EXAMPLE }} |
| **Description line 1** | Value promise | {{ QUICK_REF_DESC_LINE_1 }} |
| **Description line 2** | How it helps | {{ QUICK_REF_DESC_LINE_2 }} |
| **Optional bullets** | Key capabilities | {{ QUICK_REF_BULLETS }} |
