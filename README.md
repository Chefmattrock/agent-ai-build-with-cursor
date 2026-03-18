# Agent Builder Kit

A complete toolkit for designing, building, and marketing AI agents — structured around a 5-phase lifecycle and built to work with Cursor AI.

This kit is **templatized for external builders.** Before you can use it effectively, you'll need to fill in your own personas, brand voice, quality standards, and naming conventions. See [CUSTOMIZE.md](./CUSTOMIZE.md) for the step-by-step setup guide.

---

## What's In This Kit

```
_builder-kit/
├── 01_Ideate/     → Define the problem and your target user
├── 02_Document/   → Write the PRD
├── 03_Build/      → Generate the agent workflow (JSON)
├── 04_Polish/     → Apply brand voice and refine copy
└── 05_Market/     → Create the Product Marketing Brief
```

---

## Quick Start

### 1. Customize the kit (do this first)

Open [CUSTOMIZE.md](./CUSTOMIZE.md) and work through the setup checklist. This takes 30–60 minutes and unlocks everything else.

### 2. Open in Cursor

The `.cursorrules` file turns Cursor into an agent-building assistant. Once you've completed setup, just say:

- `"Build an agent"` → Guided workflow from ideation to JSON
- `"Write a PRD"` → Generates a requirements document
- `"Design the actions"` → Outputs valid action JSON
- `"Create a PMB"` → Generates a marketing brief

### 3. Start a new agent project

```bash
cp -r "_builder-kit" "My-Agent-Name"
```

Rename the folder with your agent name (e.g. `Meeting-Prep-Agent`). Your outputs go in that folder:
- `PRD.md` — Requirements document
- `actions.json` — Agent workflow
- `PMB.md` — Marketing brief

---

## The 5-Phase Lifecycle

```
┌─────────┐    ┌──────────┐    ┌─────────┐    ┌────────┐    ┌────────┐
│ IDEATE  │ -> │ DOCUMENT │ -> │  BUILD  │ -> │ POLISH │ -> │ MARKET │
└─────────┘    └──────────┘    └─────────┘    └────────┘    └────────┘
     │              │               │              │             │
Define the     Create PRD      Generate      Apply voice    Create PMB
problem &      & name the      action        & refine       for go-to-
target user    agent           workflows     copy           market
```

### Phase 1: Ideate
Define the problem and identify your target user. Validate the idea against your quality framework before building.

### Phase 2: Document
Create a Product Requirements Document (PRD) that captures requirements, user stories, and the agent's name and description.

### Phase 3: Build
Generate the action workflow using the Actions Reference. Chain together inputs, AI calls, integrations, and outputs.

### Phase 4: Polish
Apply your brand voice to all user-facing copy. Make it warm, clear, and human.

### Phase 5: Market
Create a Product Marketing Brief (PMB) to prepare launch materials.

---

## Setup Checklist

> These files contain `{{ placeholders }}` that must be filled in before the kit is fully functional. Complete them in order.

| # | File | What to Add | Status |
|---|------|-------------|--------|
| 1 | `_builder-kit/01_Ideate/Personas.md` | Your ICP, 2–3 target personas with full profiles | ☐ |
| 2 | `_builder-kit/01_Ideate/RAVE_Standards.md` | Your audience description, quality threshold, persona examples | ☐ |
| 3 | `_builder-kit/04_Polish/Brand_Voice.md` | Your brand name, voice descriptors, signature phrase, do/don't examples | ☐ |
| 4 | `_builder-kit/04_Polish/Naming_Guidelines.md` | Your platform name, example agent names from your catalog | ☐ |
| 5 | `_builder-kit/04_Polish/Writing_Style_Guide.md` | Your brand name, voice attributes, before/after copy examples | ☐ |
| 6 | `_builder-kit/05_Market/PMB_Generator_Prompt.md` | Your platform description, company goals, primary metric, persona details | ☐ |
| 7 | `_builder-kit/01_Ideate/Discovery_Call_Script.md` | Your persona names (3 short find-and-replace) | ☐ |

See [CUSTOMIZE.md](./CUSTOMIZE.md) for detailed instructions on each file.

---

## When to Use Each Document

| I want to... | Use this |
|--------------|----------|
| **IDEATE** | |
| Understand my target personas | `01_Ideate/Personas.md` |
| Check agent quality bar | `01_Ideate/RAVE_Standards.md` |
| Run a discovery call to scope an agent | `01_Ideate/Discovery_Call_Script.md` |
| **DOCUMENT** | |
| Document requirements before building | `02_Document/PRD_Template.md` |
| Generate a PRD with AI assistance | `02_Document/PRD_Generator_Prompt.md` |
| **BUILD** | |
| Build a workflow agent | `03_Build/Workflow_Agent_Reference.md` |
| Build a knowledge/RAG agent | `03_Build/Knowledge_Agent_Reference.md` |
| See real-world examples | `03_Build/examples/` |
| **POLISH** | |
| Understand my brand voice and tone | `04_Polish/Writing_Style_Guide.md` |
| Name my agent properly | `04_Polish/Naming_Guidelines.md` |
| Review brand voice principles | `04_Polish/Brand_Voice.md` |
| **MARKET** | |
| Create marketing materials post-build | `05_Market/PMB_Template.md` |
| Generate a PMB with AI assistance | `05_Market/PMB_Generator_Prompt.md` |

---

## Quality Standards

### Baseline (Required for all agents)

All public agents should meet standards for **Usability**, **Remarkability**, and **Safety**:

| U — Usability | R — Remarkability | S — Safety |
|---------------|-------------------|------------|
| Runs without bugs | Unique, not a duplicate | No inappropriate content |
| Clear, searchable name | Solves real problem | Not spammy |
| Helpful description | Beyond basic LLM call | Asks consent for PII |
| Handles poor inputs | Novel methods/insights | Self-identifies as AI |

### RAVE (Premium designation)

Premium agents must also meet **RAVE** standards:

| R — Relevant | A — Actionable | V — Validated | E — Evergreen |
|--------------|----------------|---------------|---------------|
| Clear ROI | Unique value every run | Performs as promised | Fits existing workflow |
| Immediately understandable | Daily/weekly need | Consistent quality | No new habits required |
| Minimal setup | Drives next action | Tested with real users | Trigger/integration ready |

See `_builder-kit/01_Ideate/RAVE_Standards.md` for the full framework.

---

## Need Help?

- **Examples:** Start with `03_Build/examples/` to see patterns in action
- **Voice:** Read `04_Polish/Writing_Style_Guide.md` to nail the tone
- **Quality:** Check `01_Ideate/RAVE_Standards.md` for the bar to hit
- **Setup:** Work through `CUSTOMIZE.md` before your first build

Pull up a chair. Let's build something great together.
