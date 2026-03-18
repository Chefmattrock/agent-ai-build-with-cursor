# Example 3: Meeting Prep Agent

**Complexity:** Complex (46 actions)
**Patterns:** Triggers, parallel execution, sub-agent composition, conditional fallback, JSON intermediates

---

## Overview

This agent creates comprehensive meeting preparation briefs. It syncs with Google Calendar, researches all attendees and their companies, and generates a structured HTML email briefing.

**Target User:** Sales reps and account managers preparing for prospect meetings.

**Time Saved:** ~30-45 minutes per meeting vs. manual research.

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                           TRIGGER OR MANUAL INPUT                                │
├─────────────────────────────────────────────────────────────────────────────────┤
│  [Calendar Trigger] ──┬── trigger_data exists ──> [Use Trigger Data]            │
│                       │                                                          │
│                       └── no trigger_data ──────> [Manual: Select Meeting]       │
│                                                    [Enrich Calendar Event]       │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      v
┌─────────────────────────────────────────────────────────────────────────────────┐
│                           PARALLEL: INITIAL PROCESSING                           │
├─────────────────────────────────────────────────────────────────────────────────┤
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐               │
│  │ Generate Subject │  │ Process Event    │  │ Separate         │               │
│  │ Line             │  │ Data (JSON)      │  │ Attendees        │               │
│  └──────────────────┘  └──────────────────┘  └──────────────────┘               │
│           ↓                    ↓                      ↓                          │
│   results_subject_line   processed_gcal_event   external_attendees               │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      v
┌─────────────────────────────────────────────────────────────────────────────────┐
│                           PARALLEL: COMPANY RESEARCH                             │
├─────────────────────────────────────────────────────────────────────────────────┤
│  [Invoke Company Intel Agent] × N companies                                      │
│  [Invoke Person Intel Agent] × N external attendees                             │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      v
┌─────────────────────────────────────────────────────────────────────────────────┐
│                           SYNTHESIS & OUTPUT                                     │
├─────────────────────────────────────────────────────────────────────────────────┤
│  [Combine All Intelligence] -> [Generate Brief] -> [Format HTML Email]          │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

## Action Breakdown

### Phase 1: Trigger or Manual Input (Actions 0-6)

#### Action 0: Google Calendar Trigger
```json
{
  "type": "GOOGLECALENDAR_GOOGLE_CALENDAR_EVENT_SYNC_TRIGGER",
  "label": "Calendar Event Sync",
  "inputs": [
    { "name": "runAs", "value": "user" },
    { "name": "calendarId", "value": "primary" },
    { "name": "maxResults", "value": 10 },
    { "name": "output_variable_name", "value": "trigger_data" }
  ]
}
```

**How Triggers Work:**
- Agent can be triggered automatically when calendar events are created/updated
- `trigger_data` contains the event details
- When run manually, `trigger_data` is empty (`{}`)

#### Actions 1-6: Fallback for Manual Runs
```json
{ "type": "if_condition", "inputs": [{ "name": "query", "value": "{{trigger_data}} == \"{}\"" }] }
{ "type": "get_calendar_events_list", ... }  // Get next 30 events
{ "type": "get_user_input", ... }  // User selects meeting
{ "type": "invoke_llm", ... }  // Extract event ID
{ "type": "enrich_calendar_event", ... }  // Get full event data
{ "type": "end_condition" }
```

**Pattern: Trigger with Manual Fallback**
This allows the agent to work both ways:
- Automatically via calendar sync
- Manually when user runs it themselves

---

### Phase 2: Initial Parallel Processing (Actions 7-12)

```json
{ "type": "parallel_condition", "label": "Parallel: Initial Processing" }
```

Three LLM calls run simultaneously:

| Branch | Purpose | Output Variable |
|--------|---------|-----------------|
| 1 | Generate email subject line | `results_subject_line` |
| 2 | Parse calendar event to JSON | `processed_gcal_event` |
| 3 | Separate internal/external attendees | `external_attendees` |

```json
{ "type": "end_condition", "label": "End Parallel" }
```

**Why Parallel?** These three tasks are independent. Running them in parallel cuts processing time by ~60%.

---

### Phase 3: Research Phase (Actions 13-30)

#### Company Intelligence (Parallel Loop)
```json
{
  "type": "parallel_condition",
  "inputs": [
    { "name": "list_variable", "value": "external_companies" },
    { "name": "item_variable", "value": "company" },
    { "name": "max_parallel", "value": "5" }
  ]
}
```

For each external company, invokes a specialized sub-agent:

```json
{
  "type": "invoke_agent",
  "inputs": [
    { "name": "agent_id", "value": "company-intelligence-agent" },
    { "name": "input_data", "value": "{{company}}" },
    { "name": "output_variable_name", "value": "company_intel_{{company}}" }
  ]
}
```

#### Person Intelligence (Parallel Loop)
Same pattern for attendees:
```json
{
  "type": "parallel_condition",
  "inputs": [
    { "name": "list_variable", "value": "external_attendees" },
    { "name": "item_variable", "value": "attendee" }
  ]
}
{ "type": "invoke_agent", "inputs": [{ "name": "agent_id", "value": "person-intelligence-agent" }] }
```

**Sub-Agent Composition:**
- `company-intelligence-agent`: Researches companies (news, funding, leadership)
- `person-intelligence-agent`: Researches individuals (LinkedIn, recent posts)

This modular approach means you can improve sub-agents independently.

---

### Phase 4: Synthesis & Output (Actions 31-46)

#### Combine All Intelligence
```json
{
  "type": "invoke_llm",
  "inputs": [
    { "name": "llm_engine", "value": "gpt-5" },
    { "name": "instructions", "value": "Synthesize all research into a meeting brief...\n\nEvent: {{processed_gcal_event}}\nCompany Intel: {{all_company_intel}}\nPerson Intel: {{all_person_intel}}" }
  ]
}
```

#### Generate HTML Email
The final output is a formatted HTML email:

```json
{
  "type": "invoke_llm",
  "inputs": [
    { "name": "instructions", "value": "Convert this meeting brief JSON to a beautiful HTML email...\n\nUse this structure:\n- Header with meeting title and time\n- Quick Facts section (bullet points)\n- Company Overview (collapsible sections)\n- Attendee Profiles (cards with photos)\n- Suggested Talking Points\n- Recent News (if available)\n\nOutput valid HTML only." }
  ]
}
```

---

## Key Patterns

### 1. Trigger with Manual Fallback
```
[Trigger] -> [If no trigger data] -> [Manual input flow] -> [End If]
```
Allows agents to work both automatically and on-demand.

### 2. Parallel Execution
```
[Parallel Start] -> [Task A] | [Task B] | [Task C] -> [Parallel End]
```
Independent tasks run simultaneously, cutting total time significantly.

### 3. Sub-Agent Composition
```
[Invoke Agent] -> Use output -> [Invoke Another Agent]
```
Build specialized agents and compose them into complex workflows.

### 4. JSON Intermediate Format
Process calendar data into structured JSON first, then use it:
```
[Raw Event] -> [Parse to JSON] -> [Use structured data in subsequent prompts]
```
Makes prompts cleaner and outputs more reliable.

### 5. Parallel For Loops
```
[Parallel For Each item in list] -> [Process item] -> [End]
```
Process multiple items (attendees, companies) simultaneously.

---

## Lessons Learned

1. **Parallel cuts time dramatically:** A 10-minute sequential agent becomes 3 minutes parallel.

2. **Sub-agents enable modularity:** Update company research once, all agents benefit.

3. **JSON intermediates are reliable:** Raw data → structured JSON → final output produces consistent results.

4. **Triggers need fallbacks:** Not all users will set up triggers. Always provide a manual path.

5. **Limit parallel concurrency:** `max_parallel: 5` prevents rate limiting and timeouts.

6. **HTML email outputs are powerful:** Users can copy/paste into Gmail directly.

---

## Performance Notes

| Metric | Sequential (estimated) | Parallel (actual) |
|--------|------------------------|-------------------|
| 3 companies, 5 attendees | ~8-10 min | ~3 min |
| API calls | Same | Same |
| User wait time | Long | Acceptable |

---

## When to Use This Pattern

- Multi-source research agents
- Workflow with independent sub-tasks
- Agents triggered by external events
- Complex data synthesis
- Email or document generation

---

## Full JSON

See `json/meeting_prep.json` for the complete action array.
