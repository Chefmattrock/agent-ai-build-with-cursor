# Writing Style Guide

> **SETUP REQUIRED:** This file defines the writing style for all agent copy. Replace every `{{ placeholder }}` with your own brand's voice and examples. See `CUSTOMIZE.md` for guidance. The copy template patterns and structure are ready to use as-is.

{{ BRAND_NAME }}'s voice is **{{ VOICE_CORE_DESCRIPTORS }}** — {{ VOICE_ONE_LINER }}.

*(Example: "warm, clear, and quietly confident — the voice of a friendly expert who wants you to feel capable")*

---

## Voice Profile

The tone is {{ VOICE_TONE_DESCRIPTORS }}. We speak like {{ VOICE_SPEAKER_DESCRIPTION }}.

*(Example: "conversational, curious, and lightly witty — never snarky, never salesy, never corporate. We speak like someone who's delighted by what AI can do, realistic about where it falls short, and always rooting for the person on the other end of the screen.")*

**The vibe:** "{{ VOICE_SIGNATURE_PHRASE }}"

*(Example: "Pull up a chair. Let's figure this out together.")*

---

## Quick Reference: Do's and Don'ts

| Attribute | Do | Don't |
|-----------|----|-------|
| **{{ VOICE_ATTR_1 }}** | {{ VOICE_DO_1 }} | {{ VOICE_DONT_1 }} |
| **{{ VOICE_ATTR_2 }}** | {{ VOICE_DO_2 }} | {{ VOICE_DONT_2 }} |
| **{{ VOICE_ATTR_3 }}** | {{ VOICE_DO_3 }} | {{ VOICE_DONT_3 }} |
| **{{ VOICE_ATTR_4 }}** | {{ VOICE_DO_4 }} | {{ VOICE_DONT_4 }} |
| **Concise** | Keep sentences clean and fluid | Add filler words (very, really, basically) |
| **Human** | "What are you working on today?" | "Please specify your input parameters." |
| **Optimistic** | "Here's how to make this work." | "This might not work because..." |

*(Fill in your own Do/Don't examples. Generic examples are provided for Concise, Human, Optimistic.)*

---

## Core Voice Attributes

### 1. {{ VOICE_ATTRIBUTE_1_NAME }}
{{ VOICE_ATTRIBUTE_1_BULLETS }}

*(Example: "Warm and Human — Talk to people, not personas. Write like a one-to-one conversation. Use approachable, everyday language. Make readers feel welcomed, not talked at.")*

### 2. {{ VOICE_ATTRIBUTE_2_NAME }}
{{ VOICE_ATTRIBUTE_2_BULLETS }}

### 3. {{ VOICE_ATTRIBUTE_3_NAME }}
{{ VOICE_ATTRIBUTE_3_BULLETS }}

### 4. {{ VOICE_ATTRIBUTE_4_NAME }}
{{ VOICE_ATTRIBUTE_4_BULLETS }}

### 5. Thoughtful and Precise
- Choose words with intention
- Keep sentences clean and fluid
- Vary rhythm to keep writing lively
- Skip filler; keep the warmth
- **Belief:** Concise doesn't mean cold.

---

## Copy Templates

Use these patterns when writing user-facing copy in your agents.

### Input Descriptions

**Pattern:** `[Action verb] + [what] + [optional: why/benefit]`

| Good | Why It Works |
|------|--------------|
| "Enter the email of the prospect you're meeting with:" | Specific, action-oriented |
| "Paste the URL you want to analyze:" | Clear about what's needed |
| "What do you know about them? (Any context helps)" | Inviting, reduces pressure |
| "How long should this be? (Shorter usually wins.)" | Adds helpful guidance |
| "Any specific asks? (Tell us what matters.)" | Encourages detail without demanding it |

| Bad | Why It Fails |
|-----|--------------|
| "Input your query string:" | Technical jargon |
| "Enter data:" | Vague and cold |
| "Provide the necessary information:" | Corporate and unhelpful |

### Output Headings

**Pattern:** `[Your/The] + [Result Type] + [optional: context variable]`

| Good | Why It Works |
|------|--------------|
| "Your {{ output_type }}: {{ context_variable }}" | Personal, includes context |
| "Here's what we found:" | Conversational |
| "{{ agent_name }} Results" | Clear and direct |

| Bad | Why It Fails |
|-----|--------------|
| "Output" | Generic, tells nothing |
| "Results" | Vague |
| "Generated Content" | Cold, technical |

### Error Messages

**Pattern:** `[What happened] + [What to do next]`

| Good | Why It Works |
|------|--------------|
| "We couldn't reach that URL. Double-check the link and try again?" | Friendly, actionable |
| "Looks like the file didn't upload. Give it another shot?" | Human, encouraging |
| "No results found for that input. Try a different format?" | Explains problem + solution |

| Bad | Why It Fails |
|-----|--------------|
| "Error: Invalid input" | Unhelpful, blaming |
| "Process failed" | No guidance |
| "Exception occurred" | Technical, scary |

### LLM Instruction Tone

When writing prompts for LLM actions, match your brand voice in the output instructions.

**Pattern:** Include voice direction in your prompt

```
## VOICE GUIDELINES

Write like a {{ VOICE_LLM_DESCRIPTION }}. The tone is {{ VOICE_LLM_TONE }}.

*(Example: "friendly expert briefing a colleague. The tone is warm, clear, curious, and human.")*

DO:
- Use contractions (you'll, don't, here's, it's)
- Write conversationally, one-to-one
- Explain the why, not just the what
- Be specific with facts and details
- Stay grounded but optimistic

DON'T:
- Corporate jargon (synergy, leverage, circle back, align)
- Buzzwords (revolutionary, game-changing, cutting-edge)
- Sarcasm or silliness
- Condescension or talking down
- Filler words (very, really, quite, just, actually)
```

---

## Before/After Examples

### Input Description

**Before:** "Enter text to process"

**After:** "{{ STYLE_BEFORE_AFTER_INPUT_AFTER }}"

*(Example: "What are you working on today? (Paste your notes, transcript, or rough draft)")*

---

### Output Heading

**Before:** "LLM Output"

**After:** "{{ STYLE_BEFORE_AFTER_OUTPUT_AFTER }}"

*(Example: "Your Email Drafts — Ready to Send")*

---

### Error Message

**Before:** "Error: Contact not found in database"

**After:** "{{ STYLE_BEFORE_AFTER_ERROR_AFTER }}"

*(Example: "We couldn't find that contact. Check the email address or add them first?")*

---

### LLM Output

**Before:** "The analysis indicates that the subject demonstrates positive growth indicators."

**After:** "{{ STYLE_BEFORE_AFTER_LLM_AFTER }}"

*(Example: "Good news — this company is growing fast. They just raised a $30M Series B and are hiring across sales.")*

---

## Applying Voice by Context

### In Agent Descriptions
Write like you're explaining to a colleague what this agent does and why they'd use it.

> "{{ VOICE_IN_CONTEXT_DESCRIPTION }}"

*(Example: "Walk into every meeting ready. This agent turns your notes, agenda, and past conversations into a clean briefing you can skim in seconds.")*

### In User Prompts
Be specific about what you need, but warm about how you ask.

> "{{ VOICE_IN_CONTEXT_PROMPT }}"

*(Example: "What's your tone? (Friendly? Formal? Or use your saved writing style.)")*

### In Output Formatting
Make results scannable and human-readable.

> "{{ VOICE_IN_CONTEXT_OUTPUT }}"

*(Example: "Here's your meeting brief. The key points are up top — scroll down for the full breakdown.")*

---

## Key Takeaway

{{ BRAND_NAME }}'s voice is {{ VOICE_SUMMARY }}.

**{{ VOICE_CLOSING_BELIEF }}**

*(Example: "The most joyful companies build the most joyful products — and we try to bring that joy into every sentence.")*
