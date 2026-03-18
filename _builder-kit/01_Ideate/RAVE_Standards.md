# Quality Standards Framework

> **SETUP REQUIRED:** This file defines your quality bar for agents. Replace every `{{ placeholder }}` with your own content. The RAVE framework structure is ready to use — customize the audience language, scoring thresholds, and examples to match your context. See `CUSTOMIZE.md` for guidance.

---

## Two Tiers of Quality

| Standard | Purpose | Question |
|----------|---------|----------|
| **{{ BASELINE_STANDARD_NAME }}** | Baseline quality | Does it work? Is it safe? Is it unique? |
| **{{ PREMIUM_STANDARD_NAME }}** | Premium designation | Does it *delight* and drive retention? |

All public agents must pass `{{ BASELINE_STANDARD_NAME }}`. Premium agents must also pass `{{ PREMIUM_STANDARD_NAME }}`.

*Tip: You can keep "URS" and "RAVE" as your standard names, or rename them to match your organization's language.*

---

## The RAVE Framework

RAVE is the quality bar for **Premium** agents — agents that are **#GoodToGo** for your target users.

Premium agents must deliver consistent value to {{ TARGET_USER_DESCRIPTION }} who use them as part of their regular workflow.

*(Example: "nontechnical SMB professionals who use them as part of their daily workflow")*

### R — Relevant

The agent must solve a real problem for your target users with clear, immediate value.

| Criterion | What It Means |
|-----------|---------------|
| **Clear ROI** | Time saved, quality improved, or confidence gained |
| **Immediately understandable** | Your target user gets the purpose in 5 seconds |
| **Minimal setup** | Useful results without configuration or training |
| **Low input, high value** | First run delivers value without asking for too much |

**Pass Example:** {{ RELEVANT_PASS_EXAMPLE }}
*(Example: "Meeting Prep" — user enters a meeting link, gets a briefing in 2 minutes.)*

**Fail Example:** {{ RELEVANT_FAIL_EXAMPLE }}
*(Example: "Universal Data Processor" — unclear purpose, requires configuration to be useful.)*

---

### A — Actionable

The agent must deliver unique value with every run and solve recurring friction.

| Criterion | What It Means |
|-----------|---------------|
| **Unique value every run** | Not a one-and-done tool |
| **Recurring friction** | Solves a daily or weekly need, not occasional |
| **Drives next action** | Output tells the user what to do next |

**Pass Example:** {{ ACTIONABLE_PASS_EXAMPLE }}
*(Example: "Daily Sales Digest" — run every morning, tells you which deals need attention today.)*

**Fail Example:** {{ ACTIONABLE_FAIL_EXAMPLE }}
*(Example: "Company Name Generator" — useful once, not recurring value.)*

---

### V — Validated

The agent must perform as promised with consistent, reliable outputs. This is about **platform capability + builder craftsmanship** — can you do this "pretty good" across the 80% case, not just the perfect demo?

| Criterion | What It Means |
|-----------|---------------|
| **Performs as promised** | Works across typical use cases, not just demos |
| **Handles typical variations** | Clean input, messy input, edge cases — can you deliver reliably? |
| **Proven reliability** | Consistent quality, not hit-or-miss |
| **Trusted source** | {{ TRUSTED_SOURCE_DESCRIPTION }} |
| **Positive signals** | Reviews, re-use patterns, user sentiment |

*(Example trusted source: "Built by verified platform partners or validated community builders")*

**The Variations Test:** Before building, map out the typical variations of the use case:
- The typical case (clean input) — Can you handle it? ✓
- The messy case (poor quality input) — Can you handle it? ✓ / ⚠️
- The edge case (unusual scenarios) — Can you handle it? ⚠️ / ✗
- The complex case (high volume/complexity) — Can you handle it? ⚠️ / ✗

If most are green → V is achievable. If too many are red → narrow scope or reconsider.

**Pass Example:** {{ VALIDATED_PASS_EXAMPLE }}
*(Example: Agent tested with 50+ real users across typical variations, 4.5+ star rating, consistent output quality.)*

**Fail Example:** {{ VALIDATED_FAIL_EXAMPLE }}
*(Example: Works in demo but breaks with real-world edge cases.)*

---

### E — Evergreen

The agent must fit into existing workflows without requiring new habits.

| Criterion | What It Means |
|-----------|---------------|
| **Fits existing workflow** | Integrates with tools your users already use |
| **Supports current habits** | Doesn't require users to change how they work |
| **Trigger-ready** | Can be automated or integrated with existing tools |
| **Tech stack compatible** | Works with {{ USER_TECH_STACK }} |

*(Example: "common tools like Google Workspace, HubSpot, Slack")*

**Pass Example:** {{ EVERGREEN_PASS_EXAMPLE }}
*(Example: "Meeting Prep" triggered automatically when a calendar event is created.)*

**Fail Example:** {{ EVERGREEN_FAIL_EXAMPLE }}
*(Example: Requires user to remember to run it manually every time.)*

---

## RAVE Checklist

Use this checklist before designating an agent as Premium.

### Relevant
- [ ] Clear ROI: time saved, quality improved, or confidence gained
- [ ] Purpose immediately understandable by your target user
- [ ] Minimal setup — useful results without configuration
- [ ] Low input, high value output on first run

### Actionable
- [ ] Delivers unique value with every run (not one-and-done)
- [ ] Solves recurring friction (daily/weekly need)
- [ ] Output drives the user's next action

### Validated
- [ ] Performs as promised across typical use cases (the 80% case, not just demos)
- [ ] Typical variations assessed: can you handle clean, messy, and edge cases?
- [ ] Tested with real users or representative scenarios
- [ ] Quality outputs are consistent, not hit-or-miss
- [ ] Built by {{ TRUSTED_SOURCE_SHORT }}

### Evergreen
- [ ] Fits into existing workflow
- [ ] Supports current habits, doesn't require new ones
- [ ] Can be triggered automatically or integrates with existing tools
- [ ] Works with your users' common tech stack

---

## RAVE Scoring

For each criterion, score 0–2:

| Score | Meaning |
|-------|---------|
| 0 | Fails criterion |
| 1 | Partially meets criterion |
| 2 | Fully meets criterion |

**Premium threshold:** {{ PREMIUM_SCORE_THRESHOLD }} out of 16 total points, with no 0s.

*(Default: 12+ out of 16)*

---

## Examples by Persona

### {{ PERSONA_1_NAME }} — Premium Agent

**"{{ PERSONA_1_EXAMPLE_AGENT }}"**
- **Relevant:** {{ PERSONA_1_RELEVANT_EXAMPLE }} ✓
- **Actionable:** {{ PERSONA_1_ACTIONABLE_EXAMPLE }} ✓
- **Validated:** {{ PERSONA_1_VALIDATED_EXAMPLE }} ✓
- **Evergreen:** {{ PERSONA_1_EVERGREEN_EXAMPLE }} ✓

### {{ PERSONA_2_NAME }} — Premium Agent

**"{{ PERSONA_2_EXAMPLE_AGENT }}"**
- **Relevant:** {{ PERSONA_2_RELEVANT_EXAMPLE }} ✓
- **Actionable:** {{ PERSONA_2_ACTIONABLE_EXAMPLE }} ✓
- **Validated:** {{ PERSONA_2_VALIDATED_EXAMPLE }} ✓
- **Evergreen:** {{ PERSONA_2_EVERGREEN_EXAMPLE }} ✓

### {{ PERSONA_3_NAME }} — Premium Agent

**"{{ PERSONA_3_EXAMPLE_AGENT }}"**
- **Relevant:** {{ PERSONA_3_RELEVANT_EXAMPLE }} ✓
- **Actionable:** {{ PERSONA_3_ACTIONABLE_EXAMPLE }} ✓
- **Validated:** {{ PERSONA_3_VALIDATED_EXAMPLE }} ✓
- **Evergreen:** {{ PERSONA_3_EVERGREEN_EXAMPLE }} ✓

---

## The #GoodToGo Question

Before marking an agent as Premium, ask yourself:

> *"Would I bet my reputation on recommending this agent to {{ GOODTOGO_USER_DESCRIPTION }}?"*

*(Example: "a nontechnical SMB user who's skeptical of AI")*

If the answer is yes — it's #GoodToGo.

If there's hesitation — it needs more work.

---

## Quick Reference

| Letter | Criterion | Key Question |
|--------|-----------|--------------|
| **R** | Relevant | Is the value obvious and immediate? |
| **A** | Actionable | Will they use it every week? |
| **V** | Validated | Can we do this "pretty good" across the 80% case? |
| **E** | Evergreen | Does it fit their existing workflow? |
