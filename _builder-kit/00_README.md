# Agent Builder Starter Kit

Welcome to the Agent Builder Starter Kit — your complete guide to designing, building, and marketing AI agents.

> **New here?** Start with [CUSTOMIZE.md](../CUSTOMIZE.md) in the root folder to fill in your personas, brand voice, and quality standards before you build your first agent.

---

## How to Use This Template

This folder is a reusable template. To start a new agent project:

### 1. Duplicate the folder
```bash
cp -r "_builder-kit" "My-Agent-Name"
```

### 2. Rename with your agent
Use a clear name like `Meeting-Prep-Agent` or `Sales-Email-Writer`.

### 3. Open in Cursor
The `.cursorrules` file will automatically guide you through building.

### 4. Start building
Switch to **Agent mode** and say:
> "Build an agent that [your idea here]"

### 5. Your outputs go in the project folder
- `PRD.md` — Your requirements document
- `actions.json` — Your agent's action workflow
- `PMB.md` — Your marketing brief

The template docs stay as reference.

---

## The Agent Lifecycle

Building great agents follows a 5-phase lifecycle:

```
┌─────────┐    ┌──────────┐    ┌─────────┐    ┌────────┐    ┌────────┐
│ IDEATE  │ -> │ DOCUMENT │ -> │  BUILD  │ -> │ POLISH │ -> │ MARKET │
└─────────┘    └──────────┘    └─────────┘    └────────┘    └────────┘
     │              │               │              │             │
Define the     Create PRD      Generate      Apply voice    Create PMB
problem &      & name the      action        & refine       for go-to-
target user    agent           workflows     copy           market
```

### Phase 1: IDEATE
Define the problem you're solving and identify your target user. Who needs this? What pain are you relieving?

### Phase 2: DOCUMENT
Create a Product Requirements Document (PRD) that captures requirements, user stories, and the agent's name and description.

### Phase 3: BUILD
Generate the action workflow using the Actions Reference. Chain together inputs, AI calls, integrations, and outputs.

### Phase 4: POLISH
Apply your brand voice to all user-facing copy. Make it warm, clear, and human.

### Phase 5: MARKET
Create a Product Marketing Brief (PMB) and profile page content to prepare launch materials.

---

## Quick Start Guide

### Starting a New Agent

1. **Read your Writing Style Guide** to understand your brand's voice
2. **Fill out the PRD Template** to document your agent's purpose and requirements
3. **Use the Naming Guidelines** to create a clear, searchable name
4. **Reference the Build docs** to design your workflow
5. **Study the Examples** to see patterns in action
6. **Create a PMB** when ready to launch

### Building from an Existing Idea

If you already have a concept:
1. Start with `02_Document/PRD_Template.md` to structure your thinking
2. Jump to `03_Build/` for action references
3. Check `03_Build/examples/` for similar patterns

---

## When to Use Each Document

| I want to... | Use this |
|--------------|----------|
| **IDEATE** | |
| Understand my target personas | `01_Ideate/Personas.md` |
| Check my quality bar | `01_Ideate/RAVE_Standards.md` |
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

## File Structure

```
_builder-kit/
├── 00_README.md                          <- You are here
│
├── 01_Ideate/                            # Define problem & user
│   ├── Personas.md                       # Target user profiles {{ REQUIRES SETUP }}
│   ├── RAVE_Standards.md                 # Quality bar for agents {{ REQUIRES SETUP }}
│   └── Discovery_Call_Script.md          # Scoping call guide
│
├── 02_Document/                          # Create PRD
│   ├── PRD_Template.md                   # Requirements template
│   ├── PRD_Generator.md                  # PRD generation guide
│   └── PRD_Generator_Prompt.md           # AI prompt for PRD creation
│
├── 03_Build/                             # Generate workflows
│   ├── Workflow_Agent_Reference.md       # Action-based agent guide
│   ├── Knowledge_Agent_Reference.md      # RAG/knowledge agent guide
│   └── examples/                         # Real-world patterns
│       ├── 01_simple_news_summarizer/
│       ├── 02_sales_email_writer/
│       ├── 03_meeting_prep_agent/
│       └── 04_pmb_generator/
│
├── 04_Polish/                            # Apply voice & refine
│   ├── Writing_Style_Guide.md            # Voice and copy templates {{ REQUIRES SETUP }}
│   ├── Naming_Guidelines.md              # Agent naming rules {{ REQUIRES SETUP }}
│   └── Brand_Voice.md                    # Brand voice principles {{ REQUIRES SETUP }}
│
└── 05_Market/                            # Go-to-market
    ├── PMB_Template.md                   # Marketing brief template
    └── PMB_Generator_Prompt.md           # AI prompt for PMB creation {{ REQUIRES SETUP }}
```

---

## Quality Standards

### Baseline

All public agents should meet standards for **Usability**, **Remarkability**, and **Safety**.

### RAVE (Premium)

Premium agents must also meet **RAVE** standards — agents that are **#GoodToGo**:

| R — Relevant | A — Actionable | V — Validated | E — Evergreen |
|--------------|----------------|---------------|---------------|
| Clear ROI | Unique value every run | Performs as promised | Fits existing workflow |
| Immediately understandable | Daily/weekly need | Consistent quality | No new habits required |
| Minimal setup | Drives next action | Tested with real users | Trigger/integration ready |

See `01_Ideate/RAVE_Standards.md` for the full framework and checklist.

---

## Using with Cursor AI

This folder includes a `.cursorrules` file that turns Cursor into an agent-building assistant.

**Just say:**
- `"Build an agent"` → Guided workflow from ideation to JSON
- `"Write a PRD"` → Generates requirements document
- `"Design the actions"` → Outputs valid action JSON
- `"Create a PMB"` → Generates marketing brief

Cursor will automatically reference the documentation and guide you through the 5-phase lifecycle.

---

## Need Help?

- **Examples:** Start with `03_Build/examples/` to see patterns in action
- **Voice:** Read `04_Polish/Writing_Style_Guide.md` to nail the tone
- **Quality:** Check `01_Ideate/RAVE_Standards.md` for the bar to hit
- **Setup:** Work through `../CUSTOMIZE.md` before your first build

Pull up a chair. Let's build something great together.
