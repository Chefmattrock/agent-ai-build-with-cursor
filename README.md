# Agent.ai Builder Kit for Cursor

A complete toolkit for designing, building, and marketing agents on **[Agent.ai](https://agent.ai)** — the no-code platform for building AI agents. Built to work with Cursor AI, structured around a 5-phase lifecycle.

> **What is Agent.ai?** Agent.ai is a no-code platform that lets non-technical professionals build, deploy, and share AI agents without programming knowledge. This kit assumes you're building agents on Agent.ai and using Cursor as your AI-assisted development environment.

This kit is designed to be **used as-is or customized for your own brand.** The Agent.ai platform references in `03_Build/` are fixed — that's the platform you're building on. The sections covering personas, brand voice, and quality standards contain `{{ placeholders }}` you can fill in with your own context (or leave as-is to build generic agents). See [CUSTOMIZE.md](./CUSTOMIZE.md) for the setup guide.

---

## What's In This Kit

```
_builder-kit/
├── 01_Ideate/     → Define the problem and your target user
├── 02_Document/   → Write the PRD
├── 03_Build/      → Generate the Agent.ai action workflow (JSON)
├── 04_Polish/     → Apply brand voice and refine copy
└── 05_Market/     → Create the Product Marketing Brief
```

---

## Quick Start

### 1. (Optional) Customize the kit

If you're building agents for a specific brand or audience, open [CUSTOMIZE.md](./CUSTOMIZE.md) and fill in your personas, brand voice, and quality standards. This takes 30–60 minutes and makes Cursor much more useful as a building assistant.

If you just want to start building, skip to step 2.

### 2. Open in Cursor

The `.cursorrules` file turns Cursor into an Agent.ai building assistant. Just say:

- `"Build an agent"` → Guided workflow from ideation to JSON
- `"Write a PRD"` → Generates a requirements document
- `"Design the actions"` → Outputs valid Agent.ai action JSON
- `"Create a PMB"` → Generates a marketing brief

### 3. Start a new agent project

```bash
cp -r "_builder-kit" "My-Agent-Name"
```

Rename the folder with your agent name (e.g. `Meeting-Prep-Agent`). Your outputs go in that folder:
- `PRD.md` — Requirements document
- `actions.json` — Agent.ai action workflow
- `PMB.md` — Marketing brief

---

## The 5-Phase Lifecycle

```
┌─────────┐    ┌──────────┐    ┌─────────┐    ┌────────┐    ┌────────┐
│ IDEATE  │ -> │ DOCUMENT │ -> │  BUILD  │ -> │ POLISH │ -> │ MARKET │
└─────────┘    └──────────┘    └─────────┘    └────────┘    └────────┘
     │              │               │              │             │
Define the     Create PRD      Generate      Apply voice    Create PMB
problem &      & name the      Agent.ai      & refine       for go-to-
target user    agent           action JSON   copy           market
```

### Phase 1: Ideate
Define the problem and identify your target user. Validate the idea against the RAVE quality framework before building.

### Phase 2: Document
Create a Product Requirements Document (PRD) that captures requirements, user stories, and the agent's name and description.

### Phase 3: Build
Generate the Agent.ai action workflow — a JSON array of actions that chains together inputs, LLM calls, integrations, and outputs. Uses the Agent.ai action schema.

### Phase 4: Polish
Apply your brand voice to all user-facing copy — input descriptions, output headings, error messages, and LLM prompts.

### Phase 5: Market
Create a Product Marketing Brief (PMB) with positioning, content hooks, and launch materials.

---

## About Agent.ai

Agent.ai is a no-code platform for building and deploying AI agents. Agents on Agent.ai are configured as JSON workflows made up of **actions** — discrete steps that can call LLMs, scrape URLs, search the web, run code, send emails, and more.

**With Agent.ai you can:**
- Create custom agents tailored to specific workflows
- Configure multi-step action sequences
- Integrate with tools like HubSpot, Google Workspace, and more
- Deploy agents that non-technical users can run in one click

**Agent.ai is not:**
- A reporting or dashboard platform (use Google Sheets for persistent outputs)
- A data warehouse (agents process data in workflows, they don't store it)
- A coding environment (no-code by design)

The `03_Build/` docs and examples in this kit are specific to Agent.ai's action schema. See `_builder-kit/03_Build/Workflow_Agent_Reference.md` for the full reference.

---

## Setup Checklist

> The files below contain `{{ placeholders }}` for brand- and audience-specific content. Fill these in to get the most out of Cursor's assistance. Everything else works out of the box.

| # | File | What to Add | Status |
|---|------|-------------|--------|
| 1 | `_builder-kit/01_Ideate/Personas.md` | Your ICP and 2–3 target personas with full profiles | ☐ |
| 2 | `_builder-kit/01_Ideate/RAVE_Standards.md` | Your audience description, quality threshold, and persona examples | ☐ |
| 3 | `_builder-kit/04_Polish/Brand_Voice.md` | Your brand name, voice descriptors, and do/don't examples | ☐ |
| 4 | `_builder-kit/04_Polish/Naming_Guidelines.md` | Example agent names from your catalog | ☐ |
| 5 | `_builder-kit/04_Polish/Writing_Style_Guide.md` | Your voice attributes and before/after copy examples | ☐ |
| 6 | `_builder-kit/05_Market/PMB_Generator_Prompt.md` | Your company goals, primary metric, and persona details | ☐ |
| 7 | `_builder-kit/01_Ideate/Discovery_Call_Script.md` | Your persona names (quick find-and-replace) | ☐ |

See [CUSTOMIZE.md](./CUSTOMIZE.md) for detailed instructions on each file.

---

## When to Use Each Document

| I want to... | Use this |
|--------------|----------|
| **IDEATE** | |
| Understand my target personas | `01_Ideate/Personas.md` |
| Check the agent quality bar (RAVE) | `01_Ideate/RAVE_Standards.md` |
| Run a discovery call to scope an agent | `01_Ideate/Discovery_Call_Script.md` |
| **DOCUMENT** | |
| Document requirements before building | `02_Document/PRD_Template.md` |
| Generate a PRD with AI assistance | `02_Document/PRD_Generator_Prompt.md` |
| **BUILD** | |
| Build a workflow agent on Agent.ai | `03_Build/Workflow_Agent_Reference.md` |
| Build a knowledge/RAG agent on Agent.ai | `03_Build/Knowledge_Agent_Reference.md` |
| See real-world Agent.ai examples | `03_Build/examples/` |
| **POLISH** | |
| Apply brand voice and tone | `04_Polish/Writing_Style_Guide.md` |
| Name my agent properly | `04_Polish/Naming_Guidelines.md` |
| Review brand voice principles | `04_Polish/Brand_Voice.md` |
| **MARKET** | |
| Create marketing materials post-build | `05_Market/PMB_Template.md` |
| Generate a PMB with AI assistance | `05_Market/PMB_Generator_Prompt.md` |

---

## Quality Standards

### Baseline (Required for all Agent.ai agents)

All public agents should meet standards for **Usability**, **Remarkability**, and **Safety**:

| U — Usability | R — Remarkability | S — Safety |
|---------------|-------------------|------------|
| Runs without bugs | Unique, not a duplicate | No inappropriate content |
| Clear, searchable name | Solves real problem | Not spammy |
| Helpful description | Beyond basic LLM call | Asks consent for PII |
| Handles poor inputs | Novel methods/insights | Self-identifies as AI |

### RAVE (Premium designation)

Premium agents must also meet **RAVE** standards — the bar for agents that are **#GoodToGo**:

| R — Relevant | A — Actionable | V — Validated | E — Evergreen |
|--------------|----------------|---------------|---------------|
| Clear ROI | Unique value every run | Performs as promised | Fits existing workflow |
| Immediately understandable | Daily/weekly need | Consistent quality | No new habits required |
| Minimal setup | Drives next action | Tested with real users | Trigger/integration ready |

See `_builder-kit/01_Ideate/RAVE_Standards.md` for the full framework and scoring guide.

---

## Need Help?

- **Examples:** Start with `03_Build/examples/` to see real Agent.ai action patterns
- **Voice:** Read `04_Polish/Writing_Style_Guide.md` to nail the copy
- **Quality:** Check `01_Ideate/RAVE_Standards.md` for the bar to hit
- **Setup:** Work through `CUSTOMIZE.md` before your first build

Pull up a chair. Let's build something great on Agent.ai.
