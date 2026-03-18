# Agent Discovery Call Script

Use this script to scope an agent with a stakeholder, client, or team member. The goal is to validate the idea against RAVE before building.

**Time:** 20-30 minutes  
**Output:** Enough context to write a PRD — and confidence it will pass RAVE

---

## Before the Call

- [ ] Review `_builder-kit/01_Ideate/Personas.md` — know your target personas
- [ ] Review `_builder-kit/01_Ideate/RAVE_Standards.md` — know the four criteria
- [ ] Have this script open
- [ ] Be ready to take notes

---

## RAVE at a Glance

| Letter | Criterion | Key Question |
|--------|-----------|--------------|
| **R** | Relevant | Is the value obvious and immediate? |
| **A** | Actionable | Will they use it every week? Does it drive their next action? |
| **V** | Validated | Can we prove it works with real scenarios? |
| **E** | Evergreen | Does it fit their existing workflow? |

**Your job on this call:** Gather enough to confidently check all four boxes — or identify which one will fail.

---

## Opening (2 min)

> "Thanks for taking the time. My goal today is to understand the problem you're trying to solve so we can design an agent that actually helps — and gets used, not abandoned. I'll ask a bunch of questions. Some might seem obvious, but they help me build something that works for real people, not just in demos."

> "Let's start broad and get specific. Sound good?"

---

## Part 1: The Person (5 min)

*Goal: Identify the persona and understand their world.*

### Who is this for?

> "Tell me about the person who would use this agent. What's their role?"

*Listen for: Marketing coordinator? Operations manager? Sales rep?*

> "What size company are they at? How many people on their team?"

> "How technical are they? Would they describe themselves as 'good with technology' or more like 'I just need it to work'?"

### Persona check (internal — don't ask out loud):
- [ ] Sounds like **{{ PERSONA_1_NAME }}** — {{ PERSONA_1_SHORT_DESCRIPTION }}
- [ ] Sounds like **{{ PERSONA_2_NAME }}** — {{ PERSONA_2_SHORT_DESCRIPTION }}
- [ ] Sounds like **{{ PERSONA_3_NAME }}** — {{ PERSONA_3_SHORT_DESCRIPTION }}

### Their day-to-day:

> "Walk me through a typical day for this person. What are they juggling?"

> "When do they feel most overwhelmed? What makes a bad day bad?"

---

## Part 2: Relevant — Is the Value Obvious? (5 min)

*Goal: Confirm the agent solves a real problem with clear, immediate value.*

### The problem:

> "What specific task or pain point are we trying to help with?"

> "If I described this agent in one sentence to them, would they instantly get why it matters?"

*Listen for: Can they articulate the problem clearly? If they struggle, the purpose isn't obvious enough.*

### The ROI:

> "What would they get out of this? Time saved? Better quality? More confidence?"

> "How much time does this take them right now? What's that costing them?"

*Listen for: Concrete numbers. "A few hours" is better than "it's frustrating."*

### The setup:

> "How much are they willing to put in to get value out? If we asked for 5 inputs, would they bail?"

> "What's the minimum we could ask for and still be useful?"

*Listen for: Low input tolerance = good. High setup requirement = RAVE risk.*

### ✅ RAVE Checkpoint — Relevant:
- [ ] Clear ROI (time, quality, or confidence)
- [ ] Purpose obvious in 5 seconds
- [ ] Minimal setup required
- [ ] Low input → high value on first run

**⚠️ Red flag:** If they can't articulate the ROI, or the setup is complex — Relevant may fail.

---

## Part 3: Actionable — Will They Keep Using It? (5 min)

*Goal: Confirm this solves recurring friction and drives their next action.*

### Frequency:

> "How often does this come up? Daily? Weekly? A few times a month?"

> "Is this something they do every [day/week], or more like once in a while?"

*Listen for: Daily or weekly = strong. Monthly or occasional = RAVE risk.*

### The next action:

> "Once they have the output, what would they DO with it?"

> "Would they copy-paste it? Send it? Make a decision based on it?"

*Listen for: Clear next step. If they'd just "look at it" — not actionable enough.*

### Recurring value:

> "Would they use this again tomorrow? Next week? Why?"

> "What would make them come back vs. forget about it?"

*Listen for: Habit potential. One-and-done tools fail Actionable.*

### ✅ RAVE Checkpoint — Actionable:
- [ ] Daily or weekly use case
- [ ] Output drives a clear next action
- [ ] Not a one-and-done tool
- [ ] Solves recurring friction

**⚠️ Red flag:** "Once a quarter" or "it depends" — Actionable will fail. Push to find recurring friction.

---

## Part 4: Validated — Can We Do This Well? (5 min)

*Goal: Confirm we can deliver this reliably across typical use cases — not just the perfect demo scenario.*

### Real-world test:

> "If we built this, how would we know it's working?"

> "Could you give me a real example we could test it with?"

*Listen for: Concrete scenarios, not hypotheticals.*

### Quality bar:

> "What would 'good enough' output look like? What would make it unacceptable?"

> "If the output wasn't perfect, would they edit it or throw it out?"

*Listen for: Tolerance for imperfection. Perfectionism = risk.*

### Typical variations (the V confidence check):

> "What does this look like in the real world? Walk me through different versions of this."

> "Sometimes the input is clean, sometimes it's messy — what are the variations?"

> "Are there edge cases that would break this? Languages, formats, complexity?"

*This is where you assess: Can your platform handle the 80% case — or just the perfect demo?*

**Map the variations:**

| Variation | Can We Handle It? |
|-----------|-------------------|
| The typical case | ✓ / ⚠️ / ✗ |
| The messy case | ✓ / ⚠️ / ✗ |
| The edge case | ✓ / ⚠️ / ✗ |
| The complex case | ✓ / ⚠️ / ✗ |

*If most are green → V passes. If too many are yellow/red → narrow the scope or reconsider.*

### ✅ RAVE Checkpoint — Validated:
- [ ] We have real scenarios to test with
- [ ] We know what "good" looks like
- [ ] User would edit imperfect output (not abandon)
- [ ] Quality can be consistent, not hit-or-miss
- [ ] **Your platform can handle the typical variations reliably (the 80% case)**

**⚠️ Red flag:** Can't provide a real example, expects perfection, or too many variations are outside our capabilities — Validated is at risk.

---

## Part 5: Evergreen — Does It Fit Their Life? (5 min)

*Goal: Confirm this fits existing workflows and doesn't require new habits.*

### Current tools:

> "What tools do they already use every day? CRM? Calendar? Email? Slack?"

> "Where does this task live today? What app are they in when they do it?"

*Listen for: Integration opportunities. Meeting them where they are.*

### Triggers:

> "Could this run automatically? Like, triggered by a calendar event or new lead?"

> "Or would they have to remember to run it?"

*Listen for: Auto-trigger potential = strong Evergreen. Manual-only = risk.*

### New habits:

> "Would using this require them to change how they work? Or does it slot into what they already do?"

> "Would their team need training?"

*Listen for: "It fits right in" = good. "We'd need to train people" = Evergreen fails.*

### ✅ RAVE Checkpoint — Evergreen:
- [ ] Integrates with tools they already use
- [ ] Can be triggered automatically (or easily remembered)
- [ ] No new habits required
- [ ] Works on mobile if they're mobile-first

**⚠️ Red flag:** "We'd need to train people" or "they'd have to remember" — Evergreen is at risk.

---

## Part 6: Constraints & Priority (2 min)

*Goal: Define scope and identify the #1 thing.*

### Guardrails:

> "Anything this agent should *not* do? Any guardrails?"

> "What would make this feel creepy or overreaching?"

### Priority:

> "If we could only solve one part of this problem, what's the most important piece?"

> "What would make this a win even if we didn't do everything?"

---

## Closing (2 min)

> "This is really helpful. Let me play back what I heard..."

*Summarize in this format:*

> "[Persona] spends [X time] doing [task] because [workaround]. This causes [pain/consequence], which costs them [human cost]. With this agent, they could [outcome] in [timeframe], which would mean [benefit]. The key is [most important thing]."

> "Did I get that right? Anything I missed?"

---

## After the Call: Scoping Canvas

*Capture the essence of the agent in this format — one row per element.*

| Element | Question | Answer | RAVE |
|---------|----------|--------|------|
| **Trigger** | When does the need arise? | _After [event], when they need to [action]..._ | E |
| **Task** | What are they trying to do? | _Convert [input] into [output] that [purpose]..._ | A |
| **Desired Outcome** | What does success look like? | _A [deliverable] ready to [use] in [timeframe]..._ | R |
| **Current Workaround** | How do they handle it today? | _Manually [process], taking [time], often [failure mode]..._ | R (ROI) |
| **Typical Variations** | What does this look like in the real world? | _Clean case: ✓ / Messy case: ⚠️ / Edge case: ✗_ | V |

**Example filled in:**

| Element | Answer |
|---------|--------|
| **Trigger** | After completing a client call, when they need to document what happened |
| **Task** | Convert raw meeting notes into a structured summary with decisions and action items |
| **Outcome** | A clean summary ready to send or log in CRM within minutes |
| **Workaround** | Manually reviewing notes, typing up summaries, 15-30 min per meeting or skipped |
| **Variations** | Clean notes: ✓ / Messy bullets: ✓ / Audio transcript: ✓ / 2-hour dump: ⚠️ |

---

## RAVE Scorecard

### Capture the key facts:

| Question | Answer |
|----------|--------|
| **Persona** | {{ PERSONA_1_NAME }} / {{ PERSONA_2_NAME }} / {{ PERSONA_3_NAME }} |
| **Role & company size** | |
| **Task to automate** | |
| **Frequency** | Daily / Weekly / Occasional |
| **Current time cost** | |
| **Human cost** | |
| **Current workaround** | |
| **Desired output** | |
| **Next action after output** | |
| **Key integration** | |
| **Trigger type** | Auto / Manual |
| **Must-have constraint** | |

### RAVE Validation:

| Criterion | Pass? | Notes |
|-----------|-------|-------|
| **R — Relevant** | ☐ Yes ☐ No ☐ Maybe | Clear ROI? Purpose obvious? Low input? |
| **A — Actionable** | ☐ Yes ☐ No ☐ Maybe | Daily/weekly? Drives next action? |
| **V — Validated** | ☐ Yes ☐ No ☐ Maybe | Real test scenario? Know what good looks like? |
| **E — Evergreen** | ☐ Yes ☐ No ☐ Maybe | Fits workflow? Auto-trigger? No new habits? |

### The Verdict:

- [ ] **All four pass** → Proceed to PRD. This is #GoodToGo material.
- [ ] **One or two "Maybe"** → Proceed with caution. Address the gaps in the PRD.
- [ ] **Any "No"** → Pause. Either pivot the scope or have a follow-up conversation.

### Next step:

> "I'll draft a one-pager / PRD and send it over for your review. Then we can build."

---

## Red Flags by RAVE Criterion

| Red Flag | RAVE Risk |
|----------|-----------|
| "It would be nice to have..." | **R** — Not a real pain |
| Can't articulate the ROI | **R** — Value not obvious |
| "Requires some configuration" | **R** — Setup too complex |
| "Once a quarter" | **A** — Not recurring |
| "They'd just look at it" | **A** — Doesn't drive action |
| "It depends on the situation" | **A** — Scope too broad |
| Can't give a real example | **V** — Can't validate |
| "It needs to be perfect" | **V** — Unrealistic quality bar |
| Too many edge cases / variations | **V** — Can't deliver reliably |
| "Every case is different" | **V** — Platform can't handle the 80% |
| "We'd need to train people" | **E** — Requires new habits |
| "They'd have to remember to run it" | **E** — No trigger, won't stick |

---

## Quick Reference: The 11 Must-Ask Questions

| # | Question | RAVE |
|---|----------|------|
| 1 | What's the ROI? Time saved? Quality? Confidence? | R |
| 2 | Would they get the purpose in 5 seconds? | R |
| 3 | What's the minimum input needed? | R |
| 4 | How often does this come up? Daily? Weekly? | A |
| 5 | What would they DO with the output? | A |
| 6 | Would they use it again tomorrow? | A |
| 7 | Give me a real example to test with. | V |
| 8 | What does "good enough" look like? | V |
| 9 | What are the typical variations? Can we handle the 80% case? | V |
| 10 | What tools do they already use? | E |
| 11 | Could this trigger automatically? | E |

---

## The #GoodToGo Question

Before recommending you proceed:

> *"Would I bet my reputation on recommending this agent to {{ GOODTOGO_USER_DESCRIPTION }}?"*

If yes → Build it.  
If no → Find out why and fix it first.
