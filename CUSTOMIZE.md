# Customize This Kit

This kit is templatized. Before you build your first agent, you need to fill in your own brand, personas, and quality standards. This takes **30–60 minutes** and you only do it once.

Every file that needs customization contains `{{ double curly brace placeholders }}` like this:

```
{{ BRAND_NAME }}
{{ PERSONA_1_NAME }}
{{ VOICE_CORE_DESCRIPTORS }}
```

Work through the steps below in order. Each step tells you exactly what to fill in and why it matters.

---

## Step 1 — Define Your Personas

**File:** `_builder-kit/01_Ideate/Personas.md`

**Time:** 20–30 minutes

**Why it matters:** Every agent you build should be designed for a specific person with a specific pain. Without defined personas, your agents will be generic. With them, Cursor can help you make design decisions automatically.

**What to fill in:**

1. **ICP (Ideal Customer Profile)** — The broad profile of your target customer. Company size, funding model, maturity, AI adoption level.

2. **3 Personas** — Each persona needs:
   - A name (e.g. "Marketing Meg", or "Sarah the Coordinator" — whatever resonates)
   - Role and company size
   - A one-line description that captures their essence
   - Their responsibilities, jobs-to-be-done, and trigger events
   - What they actually want (emotional, not functional)
   - What it's really costing them (make this human — describe the real-life impact)
   - Agent ideas specific to their pain

3. **UX questions** — For each persona, list 3–4 questions to ask when designing agents for them (e.g. "Can this run in under 2 minutes?")

4. **Quick Reference table** — Fill in the bottom summary table with key facts per persona.

**Tip:** If you already have customer personas from sales or marketing, start there. The structure here is more detailed than most persona docs — use it to go deeper.

---

## Step 2 — Set Your Quality Bar

**File:** `_builder-kit/01_Ideate/RAVE_Standards.md`

**Time:** 10–15 minutes

**Why it matters:** The RAVE framework (Relevant, Actionable, Validated, Evergreen) gives you and Cursor a shared quality standard. Without it, "is this agent good enough?" is a gut feeling. With it, it's a checklist.

**What to fill in:**

1. **Standard names** — You can keep "URS" and "RAVE", or rename them to match your org's language (e.g. "Basic" and "Premium").

2. **Target user description** — Who is the RAVE bar designed for? (e.g. "nontechnical SMB professionals", "enterprise IT teams", "independent creators")

3. **Pass/Fail examples** — For each of the 4 criteria (R, A, V, E), add one pass example and one fail example from your domain.

4. **Trusted source description** — What makes a builder "trusted" in your context? (e.g. "verified platform partners", "builders with 100+ runs", "internal team only")

5. **Tech stack** — What tools do your users commonly use? (for the Evergreen criterion)

6. **Scoring threshold** — Default is 12/16. Adjust if you want a stricter or looser bar.

7. **Persona examples** — For each persona, add a sample Premium agent with a one-line RAVE justification for each criterion.

8. **#GoodToGo question** — Replace the placeholder with a description of your target user.

---

## Step 3 — Define Your Brand Voice

**File:** `_builder-kit/04_Polish/Brand_Voice.md`

**Time:** 15–20 minutes

**Why it matters:** Every agent produces user-facing copy — input descriptions, output headings, error messages, LLM prompts. Without a defined voice, that copy will be cold, generic, or inconsistent. This file is the source of truth Cursor references when polishing your agents.

**What to fill in:**

1. **Brand name** — Replace `{{ BRAND_NAME }}` throughout.

2. **Voice core descriptors** — 3–5 adjectives that define your tone (e.g. "warm, clear, and quietly confident").

3. **Voice one-liner** — A short phrase capturing the feeling (e.g. "the voice of a friendly expert who wants you to feel capable").

4. **Voice tone descriptors** — How the voice *feels* in practice (e.g. "conversational, curious, and lightly witty").

5. **Signature phrase** — A memorable sentence that captures the brand vibe (e.g. "Pull up a chair. Let's figure this out together.").

6. **5 core voice attributes** — Name and describe each (e.g. "Warm and Human", "Genuinely Helpful", "Expert but Approachable"). Include what to do, what to avoid, and a vibe/mindset/belief for each.

7. **Brand examples** — Write 2 short examples: how you talk about yourselves, and how you talk about your product.

8. **Do/Don't table** — 4 rows of contrasting examples showing your voice vs. what to avoid.

9. **Words we use / avoid** — Lists of specific language choices.

---

## Step 4 — Set Your Naming Conventions

**File:** `_builder-kit/04_Polish/Naming_Guidelines.md`

**Time:** 10 minutes

**Why it matters:** Agent names are the first thing users see. Good names drive discoverability and set expectations. Cursor will reference this file when suggesting names during the Build phase.

**What to fill in:**

1. **Platform name** — Replace `{{ PLATFORM_NAME }}` (e.g. "Agent.ai", "your marketplace").

2. **Naming examples table** — Fill in 5 real or representative agent names from your catalog with a one-line explanation of why each works.

3. **Example CRM** — Replace `{{ EXAMPLE_CRM }}` with a tool your users actually use (e.g. HubSpot, Salesforce).

4. **Before/after examples** — Two examples of bad → good agent descriptions from your domain.

5. **Quick reference row** — Fill in the example name, description lines, and bullet points at the bottom.

---

## Step 5 — Fill In the Writing Style Guide

**File:** `_builder-kit/04_Polish/Writing_Style_Guide.md`

**Time:** 10–15 minutes

**Why it matters:** This is the operational version of the brand voice — focused on the specific copy patterns used inside agents (input descriptions, output headings, error messages, LLM prompts). Cursor reads this file when generating or reviewing copy.

**What to fill in:**

1. **Brand name, voice descriptors, signature phrase** — Same as Step 3 (keep consistent).

2. **Do/Don't table** — 4–5 rows with attribute names and contrasting examples.

3. **Core voice attributes** — Same as Step 3 (the 5 named attributes with bullets).

4. **Before/After examples** — Fill in 4 examples:
   - Input description: bad → good
   - Output heading: bad → good
   - Error message: bad → good
   - LLM output: bad → good

5. **In-context examples** — One example each for: agent descriptions, user prompts, output formatting.

6. **LLM voice description and tone** — How you'd describe your voice to an LLM in a prompt.

---

## Step 6 — Customize the PMB Generator Prompt

**File:** `_builder-kit/05_Market/PMB_Generator_Prompt.md`

**Time:** 15–20 minutes

**Why it matters:** This is the AI prompt that generates your Product Marketing Brief. It needs your platform context, brand voice, and persona details to produce relevant output — without them, it generates generic copy.

**What to fill in:**

1. **Platform name and description** — Replace `{{ PLATFORM_NAME }}` and `{{ PLATFORM_DESCRIPTION }}`. Write 2–3 paragraphs describing your platform, who it's for, what makes it different, and what it is NOT.

2. **Goals** — Your company goal, team goal, and primary success metric.

3. **Brand voice** — Paste your voice summary or reference your Brand Voice file.

4. **Target user description** — 1–2 sentences describing who the agents are built for.

5. **Persona segments table** — 2–3 rows from your Personas file, condensed to: name, description, needs.

6. **Audience key insight** — One sentence capturing what these users really want (not "to use AI" but the underlying goal).

7. **Output instructions** — Update instruction #11 to reference your brand name and voice descriptors. Update #12 to reference your primary metric.

---

## Step 7 — Update the Discovery Call Script (Quick)

**File:** `_builder-kit/01_Ideate/Discovery_Call_Script.md`

**Time:** 5 minutes

**Why it matters:** The discovery call script has three persona checkboxes that need your persona names. Everything else is generic.

**What to fill in:**

Find and replace the three placeholders near line 55:
```
{{ PERSONA_1_NAME }} — {{ PERSONA_1_SHORT_DESCRIPTION }}
{{ PERSONA_2_NAME }} — {{ PERSONA_2_SHORT_DESCRIPTION }}
{{ PERSONA_3_NAME }} — {{ PERSONA_3_SHORT_DESCRIPTION }}
```

Also update the RAVE scorecard row near the bottom:
```
{{ PERSONA_1_NAME }} / {{ PERSONA_2_NAME }} / {{ PERSONA_3_NAME }}
```

And update the `{{ GOODTOGO_USER_DESCRIPTION }}` placeholder with your target user description.

---

## After Setup: Verify Everything

Run through this checklist once you've completed all 7 steps:

- [ ] `Personas.md` — No `{{ placeholders }}` remaining; all 3 personas have complete profiles
- [ ] `RAVE_Standards.md` — Quality bar is defined; pass/fail examples are from your domain
- [ ] `Brand_Voice.md` — Brand name filled in; voice attributes and examples are yours
- [ ] `Naming_Guidelines.md` — Platform name filled in; examples are from your catalog
- [ ] `Writing_Style_Guide.md` — Consistent with Brand_Voice.md; all before/after examples filled
- [ ] `PMB_Generator_Prompt.md` — Platform description, goals, and personas filled in
- [ ] `Discovery_Call_Script.md` — Persona names updated in checkboxes and scorecard

---

## You're Ready to Build

Open Cursor, navigate to this folder, and say:

> "Build an agent that [your idea here]"

Cursor will guide you through all 5 phases using your customized documentation.

**Good luck. Pull up a chair.**
