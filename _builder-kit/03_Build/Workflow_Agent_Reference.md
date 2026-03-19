# Workflow Agent Reference

> Documentation for building Workflow Agents (Mini-Agents) on Agent.AI

> **Authoritative source:** When generating or validating agent JSON, always follow `_builder-kit/03_Build/LLMs.txt` first. It contains the official Agent.AI action schema directly from the platform. The reference below provides context and examples, but LLMs.txt is the source of truth for action types, input fields, and valid values.

---

## Table of Contents

1. [Overview](#overview)
2. [Action Structure](#action-structure)
3. [Variable Rules](#variable-rules)
4. [Available Actions Reference](#available-actions-reference)
   - [Inputs & Data Retrieval](#inputs--data-retrieval)
   - [AI & Content Generation](#ai--content-generation)
   - [HubSpot CRM & Automation](#hubspot-crm--automation)
   - [Workflow & Logic](#workflow--logic)
   - [Outputs](#outputs)
   - [Social Media & Online Presence](#social-media--online-presence)
   - [Business & Financial Data](#business--financial-data)
   - [Integration Intelligence](#integration-intelligence)
5. [Runtime Variables](#runtime-variables)
6. [Example Workflows](#example-workflows)
7. [Best Practices](#best-practices)
8. [Validation Checklist](#validation-checklist)

---

# Overview

Workflow agents are deterministic, step-by-step automations defined in JSON. They follow exact sequences and are called by knowledge agents as tools.

| Aspect | Workflow Agent |
|--------|----------------|
| **Interface** | Step-by-step workflow |
| **How it works** | Deterministic, predictable |
| **Best for** | Automation + tasks |
| **Execution** | Follows exact steps |
| **User interaction** | Input → Run → Output |
| **When to use** | Repeatable processes |

---

# Action Structure

Every action MUST follow this exact structure:

```json
{
  "id": "<uuid>",
  "type": "<action_type>",
  "label": "<human_readable_label>",
  "order": <sequential_integer_starting_from_0>,
  "inputs": [
    {
      "name": "<input_name>",
      "value": "<input_value>",
      "type": "<input_type>",
      "required": <boolean>
    }
  ]
}
```

---

# Variable Rules

## Variable Naming
- Must match regex: `^[a-zA-Z][a-zA-Z0-9_]*$`
- Must start with a letter (a-z, A-Z)
- Can only contain letters, numbers, and underscores
- NO spaces, dashes, or special characters

**Good:** `user_email`, `newsData`, `search_results_1`
**Bad:** `user-email`, `1data`, `my result`

## Variable References
- Use Jinja template syntax: `{{ variable_name }}`
- Variables must be defined BEFORE they are referenced
- Actions execute sequentially - order matters!

## Action IDs
- Generate unique UUIDs for each action
- Format: `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`

## Order Field
- Sequential integers starting from 0
- Each action's order must be unique

---

# Available Actions Reference

## Inputs & Data Retrieval

### Get User Input
Capture user input with options like text, numbers, URLs, and dropdowns.
```json
{
  "type": "get_user_input",
  "inputs": [
    {"name": "input_type", "value": "text", "type": "dropdown", "required": true},
    {"name": "input_description", "value": "<description>", "type": "text", "required": true},
    {"name": "default_value", "value": "<default>", "type": "text", "required": false},
    {"name": "required", "value": true, "type": "checkbox", "required": false},
    {"name": "input_name", "value": "user_input", "type": "text", "required": true}
  ]
}
```

### Get User List
Capture a list of items from a textarea and split on a delimiter.
```json
{
  "type": "get_user_list",
  "inputs": [
    {"name": "input_description", "value": "<description>", "type": "text", "required": true},
    {"name": "delimiter", "value": "<delimiter>", "type": "text", "required": false},
    {"name": "required", "value": true, "type": "checkbox", "required": false},
    {"name": "input_name", "value": "user_input", "type": "text", "required": true}
  ]
}
```

### Get User File
Allow users to upload files for processing.
```json
{
  "type": "get_user_files",
  "inputs": [
    {"name": "input_description", "value": "Upload your File(s)", "type": "text", "required": true},
    {"name": "required", "value": true, "type": "checkbox", "required": false},
    {"name": "input_name", "value": "assistant_files", "type": "text", "required": true},
    {"name": "in_session_files_only", "value": true, "type": "checkbox", "required": false}
  ]
}
```

### Wait for User Confirmation
Pause until the user confirms.
```json
{
  "type": "wait_for_confirmation",
  "inputs": [
    {"name": "user_message", "value": "<message>", "type": "text", "required": false}
  ]
}
```

### Web Page Content
Extract text from a web page or crawl multiple pages.
```json
{
  "type": "grab_web_text",
  "inputs": [
    {"name": "url", "value": "<url>", "type": "text", "required": true},
    {"name": "mode", "value": "scrape", "type": "dropdown", "required": false},
    {"name": "output_variable_name", "value": "crawled_pages", "type": "text", "required": true}
  ]
}
```

### Web Page Screenshot
Capture a visual screenshot of a web page.
```json
{
  "type": "grab_web_screenshot",
  "inputs": [
    {"name": "url", "value": "<url>", "type": "text", "required": true},
    {"name": "ttl_for_screenshot", "value": "86400", "type": "dropdown", "required": false},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": true}
  ]
}
```

### YouTube Transcript
Fetch the transcript of a YouTube video.
```json
{
  "type": "get_youtube_transcript",
  "inputs": [
    {"name": "url", "value": "<url>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "transcription", "type": "text", "required": true}
  ]
}
```

### YouTube Channel Data
Retrieve detailed information about a YouTube channel.
```json
{
  "type": "get_youtube_channel",
  "inputs": [
    {"name": "url", "value": "<url>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "channel_data", "type": "text", "required": true}
  ]
}
```

### Google News Data
Fetch news articles based on queries and date ranges.
```json
{
  "type": "get_google_news",
  "inputs": [
    {"name": "query", "value": "<query>", "type": "text", "required": true},
    {"name": "date_range", "value": "24h", "type": "dropdown", "required": true},
    {"name": "output_variable_name", "value": "news_data", "type": "text", "required": true}
  ]
}
```
Date range options: `24h`, `7d`, `30d`

### Search Results
Fetch search results from Google, YouTube, or YouTube channels.
```json
{
  "type": "get_search_results",
  "inputs": [
    {"name": "search_engine", "value": "google", "type": "dropdown", "required": true},
    {"name": "query", "value": "<query>", "type": "text", "required": true},
    {"name": "num_posts", "value": 1, "type": "dropdown", "required": true},
    {"name": "output_variable_name", "value": "search_results", "type": "text", "required": true}
  ]
}
```

### Save Agent Memory
Save notes, context, or insights to the agent's persistent memory.
```json
{
  "type": "save_to_agent_kb",
  "inputs": [
    {"name": "text_content", "value": "<content>", "type": "textarea", "required": true},
    {"name": "metadata", "value": "<metadata>", "type": "text", "required": false},
    {"name": "suggested_keywords", "value": "<keywords>", "type": "text", "required": false},
    {"name": "output_variable_name", "value": "saved_memory", "type": "text", "required": true}
  ]
}
```

### Look Up Agent Memories
Search agent's memories with AI-powered semantic search.
```json
{
  "type": "query_agent_kb",
  "inputs": [
    {"name": "query", "value": "<query>", "type": "textarea", "required": true},
    {"name": "agent_id_override", "value": "<agent_id>", "type": "text", "required": false},
    {"name": "include_citations", "value": true, "type": "checkbox", "required": false},
    {"name": "output_variable_name", "value": "recalled_memories", "type": "text", "required": true}
  ]
}
```

### List Agent Memories
List all saved memories with topics, keywords, and previews.
```json
{
  "type": "list_agent_memories",
  "inputs": [
    {"name": "agent_id_override", "value": "<agent_id>", "type": "text", "required": false},
    {"name": "keyword_filter", "value": "<filter>", "type": "text", "required": false},
    {"name": "limit", "value": "50", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "agent_memories", "type": "text", "required": true}
  ]
}
```

---

## AI & Content Generation

### Generate Image
Create images using AI models.
```json
{
  "type": "generate_image",
  "inputs": [
    {"name": "model", "value": "DALL-E 3", "type": "dropdown", "required": true},
    {"name": "model_style", "value": "digital art", "type": "dropdown", "required": true},
    {"name": "model_aspect_ratio", "value": "9:16", "type": "dropdown", "required": true},
    {"name": "model_prompt", "value": "<prompt>", "type": "textarea", "required": true},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": false}
  ]
}
```

### Process Video
Analyzes YouTube videos into transcripts, analysis, or additional videos.
```json
{
  "type": "process_video",
  "inputs": [
    {"name": "video_type", "value": "YouTube URL", "type": "dropdown", "required": true},
    {"name": "video_url", "value": "<url>", "type": "text", "required": true},
    {"name": "model_prompt", "value": "<prompt>", "type": "textarea", "required": true},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": false}
  ]
}
```

### Generate Audio Output
Convert text to speech using AI.
```json
{
  "type": "output_audio",
  "inputs": [
    {"name": "text_to_speech", "value": "<text>", "type": "text", "required": false},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": false}
  ]
}
```

### Generate Content (Invoke LLM)
Invoke a language model to generate text based on instructions.
```json
{
  "type": "invoke_llm",
  "inputs": [
    {"name": "llm_engine", "value": "gpt-5-mini", "type": "dropdown", "required": true},
    {"name": "instructions", "value": "<instructions>", "type": "textarea", "required": true},
    {"name": "knowledge_bases", "value": "<kb_ids>", "type": "multi-select-checkbox", "required": false},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": false}
  ]
}
```
LLM options: `gpt-5`, `gpt-5-mini`

### Convert File
Convert uploaded files to different formats.
```json
{
  "type": "convert_file",
  "inputs": [
    {"name": "input_files", "value": "{{assistant_files}}", "type": "text", "required": true},
    {"name": "show_all_conversion_options", "value": "true", "type": "checkbox", "required": true},
    {"name": "convert_to_extension", "value": "<extension>", "type": "text", "required": false},
    {"name": "output_variable_name", "value": "converted_files", "type": "text", "required": true}
  ]
}
```

---

## HubSpot CRM & Automation

### Search HubSpot Objects
```json
{
  "type": "hubspot.v2.search_objects",
  "inputs": [
    {"name": "object_type", "value": "contacts", "type": "dropdown", "required": true},
    {"name": "filters", "value": "<filters>", "type": "properties", "required": false},
    {"name": "properties", "value": "<properties>", "type": "properties", "required": false},
    {"name": "associations", "value": "<associations>", "type": "associations", "required": false},
    {"name": "output_variable_name", "value": "search_results", "type": "text", "required": false},
    {"name": "output_sort", "value": "<sort_field>", "type": "dropdown", "required": false},
    {"name": "output_sort_dir", "value": "ASCENDING", "type": "dropdown", "required": false},
    {"name": "output_limit", "value": "100", "type": "text", "required": false}
  ]
}
```
Object types: `contacts`, `companies`, `deals`, `tickets`

### Create HubSpot Object
```json
{
  "type": "hubspot.v2.create_object",
  "inputs": [
    {"name": "object_type", "value": "<type>", "type": "hubspot_object_type", "required": true},
    {"name": "properties", "value": "<properties>", "type": "properties", "required": true},
    {"name": "associations", "value": "<associations>", "type": "associations", "required": false},
    {"name": "output_variable_name", "value": "created_object", "type": "text", "required": true}
  ]
}
```

### Update HubSpot Object
```json
{
  "type": "hubspot.v2.update_object",
  "inputs": [
    {"name": "object_type", "value": "<type>", "type": "hubspot_object_type", "required": true},
    {"name": "identification_method", "value": "HubSpot ID", "type": "dropdown", "required": true},
    {"name": "identifier_value", "value": "<id>", "type": "text", "required": true},
    {"name": "properties", "value": "<properties>", "type": "properties", "required": true},
    {"name": "output_variable_name", "value": "updated_object", "type": "text", "required": true}
  ]
}
```

### Look up HubSpot Object
```json
{
  "type": "hubspot.v2.lookup_object",
  "inputs": [
    {"name": "object_type", "value": "<type>", "type": "hubspot_object_type", "required": true},
    {"name": "object_id", "value": "{{contact_id}}", "type": "text", "required": true},
    {"name": "properties", "value": "<properties>", "type": "properties", "required": false},
    {"name": "output_variable_name", "value": "retrieved_object", "type": "text", "required": true}
  ]
}
```

### Create HubSpot Engagement
```json
{
  "type": "hubspot.v2.create_engagement",
  "inputs": [
    {"name": "object_type", "value": "note", "type": "dropdown", "required": true},
    {"name": "content_body", "value": "<content>", "type": "textarea", "required": true},
    {"name": "title_subject", "value": "<title>", "type": "text", "required": false},
    {"name": "duration", "value": "<duration>", "type": "text", "required": false},
    {"name": "status", "value": "COMPLETED", "type": "dropdown", "required": false},
    {"name": "priority", "value": "HIGH", "type": "dropdown", "required": false},
    {"name": "properties", "value": "<properties>", "type": "properties", "required": false},
    {"name": "associations", "value": "<associations>", "type": "associations", "required": false}
  ]
}
```
Engagement types: `note`, `call`, `email`, `meeting`, `task`

### Get HubSpot Engagements
```json
{
  "type": "hubspot.v2.get_engagements",
  "inputs": [
    {"name": "object_type", "value": "note", "type": "dropdown", "required": true},
    {"name": "source_object_id", "value": "{{contact_id}}", "type": "text", "required": true},
    {"name": "engagement_types", "value": ["notes", "calls", "emails", "meetings", "tasks"], "type": "checkboxes", "required": false},
    {"name": "properties", "value": "<properties>", "type": "properties", "required": false},
    {"name": "start_date", "value": "<start>", "type": "text", "required": false},
    {"name": "end_date", "value": "<end>", "type": "text", "required": false},
    {"name": "output_variable_name", "value": "engagement_history", "type": "text", "required": true},
    {"name": "result_limit", "value": "100", "type": "text", "required": false}
  ]
}
```

### Create HubSpot Timeline Event
```json
{
  "type": "hubspot.v2.create_timeline_event",
  "inputs": [
    {"name": "target_object_type", "value": "company", "type": "dropdown", "required": true},
    {"name": "target_object_id", "value": "{{company_id}}", "type": "text", "required": true},
    {"name": "event_type", "value": "deployment_completed", "type": "text", "required": true},
    {"name": "event_title", "value": "Production Deployment Completed", "type": "text", "required": true},
    {"name": "event_description", "value": "<description>", "type": "textarea", "required": false},
    {"name": "event_properties", "value": "<properties>", "type": "textarea", "required": false},
    {"name": "event_timestamp", "value": "<timestamp>", "type": "text", "required": false},
    {"name": "output_variable_name", "value": "timeline_event", "type": "text", "required": true}
  ]
}
```

### Get HubSpot Timeline Events
```json
{
  "type": "hubspot.v2.get_timeline_events",
  "inputs": [
    {"name": "source_object_type", "value": "company", "type": "dropdown", "required": true},
    {"name": "source_object_id", "value": "{{company_id}}", "type": "text", "required": true},
    {"name": "event_type_filter", "value": "<filter>", "type": "text", "required": false},
    {"name": "properties", "value": "<properties>", "type": "properties", "required": false},
    {"name": "start_date", "value": "<start>", "type": "text", "required": false},
    {"name": "end_date", "value": "<end>", "type": "text", "required": false},
    {"name": "result_limit", "value": "100", "type": "text", "required": false},
    {"name": "output_variable_name", "value": "timeline_events", "type": "text", "required": true}
  ]
}
```

---

## Workflow & Logic

### Invoke Other Agent
Trigger another agent for additional processing.
```json
{
  "type": "invoke_agent",
  "inputs": [
    {"name": "module", "value": "<agent_id>", "type": "text", "required": true},
    {"name": "params", "value": "<params>", "type": "keyvalues", "required": false},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": true}
  ]
}
```

### Call Serverless Function
Execute serverless code directly within workflows.
```json
{
  "type": "serverless_function",
  "inputs": [
    {"name": "language", "value": "python", "type": "dropdown", "required": true},
    {"name": "serverless_code", "value": "<code>", "type": "textarea", "required": true},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": true}
  ]
}
```

### Invoke Web API
Make a RESTful API call to external endpoints.
```json
{
  "type": "rest_call",
  "inputs": [
    {"name": "url", "value": "<url>", "type": "text", "required": true},
    {"name": "method", "value": "POST", "type": "dropdown", "required": true},
    {"name": "format", "value": "JSON", "type": "dropdown", "required": true},
    {"name": "headers", "value": "<headers>", "type": "text", "required": false},
    {"name": "body", "value": "<body>", "type": "text", "required": false},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": true}
  ]
}
```

### Store Variable to Database
Store and track variables in the agent's database.
```json
{
  "type": "store_variable_to_database",
  "inputs": [
    {"name": "variable", "value": "<variable>", "type": "text", "required": true},
    {"name": "output_variable", "value": "tracked_value_name", "type": "text", "required": true}
  ]
}
```

### Get Variable from Database
Retrieve variables from the agent's database.
```json
{
  "type": "get_variable_from_database",
  "inputs": [
    {"name": "variable", "value": "<variable>", "type": "text", "required": true},
    {"name": "variable_retrieval_depth", "value": "most_recent_value", "type": "dropdown", "required": true},
    {"name": "agent_db_historical_values", "value": "daily", "type": "dropdown", "required": false},
    {"name": "agent_db_variable_retrieval_count", "value": "<count>", "type": "text", "required": false},
    {"name": "output_variable", "value": "tracked_values", "type": "text", "required": true}
  ]
}
```

### Set Variable
Set or update variables within the workflow.
```json
{
  "type": "set_variable",
  "inputs": [
    {"name": "variable_name", "value": "<name>", "type": "text", "required": true},
    {"name": "variable_value", "value": "<value>", "type": "textarea", "required": true}
  ]
}
```

### Add to List
Add output to a list variable.
```json
{
  "type": "add_to_list",
  "inputs": [
    {"name": "input_text", "value": "<text>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "list_variable", "type": "text", "required": true}
  ]
}
```

### Continue or Exit Workflow
Evaluate conditional logic to continue or exit.
```json
{
  "type": "check_condition",
  "inputs": [
    {"name": "query", "value": "<condition>", "type": "textarea", "required": true}
  ]
}
```

### If/Else Statement
Evaluate conditional logic for branching.
```json
{
  "type": "if_condition",
  "inputs": [
    {"name": "else", "value": false, "type": "checkbox", "required": false},
    {"name": "query", "value": "<condition>", "type": "textarea", "required": false}
  ]
}
```

### For Loop
Iterate over a list a fixed number of times.
```json
{
  "type": "for_condition",
  "inputs": [
    {"name": "loop_count", "value": "<count>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "loop_variable", "type": "text", "required": true},
    {"name": "variable_name", "value": "for_loop_index", "type": "text", "required": true}
  ]
}
```

### Parallel For Loop
Execute iterations concurrently.
```json
{
  "type": "parallel_for_condition",
  "inputs": [
    {"name": "loop_count", "value": "<count>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "loop_variable", "type": "text", "required": true},
    {"name": "variable_name", "value": "parallel_for_index", "type": "text", "required": true}
  ]
}
```

### While Loop
Iterate until a condition is met.
```json
{
  "type": "while_condition",
  "inputs": [
    {"name": "variable", "value": "<variable>", "type": "text", "required": true},
    {"name": "operator", "value": "equals", "type": "dropdown", "required": true},
    {"name": "value", "value": "<value>", "type": "text", "required": false},
    {"name": "output_variable_name", "value": "while_loop_index", "type": "text", "required": true}
  ]
}
```

### End If/Else/For Statement
Mark the end of a conditional or loop.
```json
{
  "type": "end_condition",
  "inputs": []
}
```

### Parallel Block (Start)
Execute following steps in parallel.
```json
{
  "type": "parallel_condition",
  "inputs": [
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": false}
  ]
}
```

### Parallel Block (End)
End of parallel execution block.
```json
{
  "type": "end_parallel_condition",
  "inputs": []
}
```

---

## Outputs

### Show User Output
Format and display results to users.
```json
{
  "type": "output_formatter",
  "inputs": [
    {"name": "heading", "value": "Output", "type": "text", "required": false},
    {"name": "output_formatted", "value": "<output>", "type": "textarea", "required": true},
    {"name": "format", "value": "auto", "type": "dropdown", "required": true}
  ]
}
```
Format options: `auto`, `markdown`, `html`, `json`, `table`

### Send Message
Send a message (email) to a recipient.
```json
{
  "type": "send_message",
  "inputs": [
    {"name": "type", "value": "email", "type": "dropdown", "required": true},
    {"name": "to", "value": "current_user", "type": "dropdown", "required": true},
    {"name": "email_addresses", "value": "<emails>", "type": "textarea", "required": false},
    {"name": "subject", "value": "<subject>", "type": "text", "required": false},
    {"name": "output_formatted", "value": "<body>", "type": "textarea", "required": true}
  ]
}
```

### Save To Google Doc
Save text content as a Google Doc.
```json
{
  "type": "create_google_drive_document",
  "inputs": [
    {"name": "title", "value": "<title>", "type": "text", "required": true},
    {"name": "body", "value": "<body>", "type": "textarea", "required": true}
  ]
}
```

### Save To File
Save text content as a downloadable file.
```json
{
  "type": "create_file",
  "inputs": [
    {"name": "file_type", "value": "pdf", "type": "dropdown", "required": true},
    {"name": "body", "value": "<body>", "type": "textarea", "required": true},
    {"name": "output_variable_name", "value": "saved_file", "type": "text", "required": true}
  ]
}
```

### Save To Google Sheet
Save content as a Google Sheet.
```json
{
  "type": "create_google_drive_sheet",
  "inputs": [
    {"name": "title", "value": "<title>", "type": "text", "required": true},
    {"name": "body", "value": "<body>", "type": "textarea", "required": true}
  ]
}
```

### Format Text
Change casing, remove characters, split text, etc.
```json
{
  "type": "format_text",
  "inputs": [
    {"name": "format_type", "value": "text", "type": "dropdown", "required": true},
    {"name": "delimiter", "value": "<delimiter>", "type": "text", "required": false},
    {"name": "input_text", "value": "<text>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": true}
  ]
}
```

### Post to Bluesky
Create a new post on Bluesky.
```json
{
  "type": "post_to_bluesky",
  "inputs": [
    {"name": "username", "value": "<username>", "type": "text", "required": true},
    {"name": "password", "value": "<password>", "type": "text", "required": true},
    {"name": "content", "value": "<content>", "type": "textarea", "required": true},
    {"name": "output_variable_name", "value": "post_result", "type": "text", "required": true}
  ]
}
```

---

## Social Media & Online Presence

### Get Twitter Users
Search and retrieve Twitter user profiles.
```json
{
  "type": "get_twitter_users",
  "inputs": [
    {"name": "keywords", "value": "<keywords>", "type": "text", "required": true},
    {"name": "num_users", "value": 1, "type": "dropdown", "required": true},
    {"name": "output_variable_name", "value": "twitter_users", "type": "text", "required": true}
  ]
}
```

### Recent Tweets
Fetch recent tweets from a Twitter handle.
```json
{
  "type": "get_recent_tweets",
  "inputs": [
    {"name": "profile_handle", "value": "<handle>", "type": "text", "required": true},
    {"name": "recent_tweets_count", "value": "20", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": true}
  ]
}
```

### Find LinkedIn Profile
Find someone's LinkedIn profile from a query.
```json
{
  "type": "find_linkedin_profile",
  "inputs": [
    {"name": "query", "value": "<query>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "linkedin_profile_slug", "type": "text", "required": true}
  ]
}
```

### Get LinkedIn Profile Details
Retrieve detailed information from a LinkedIn profile.
```json
{
  "type": "get_linkedin_profile",
  "inputs": [
    {"name": "profile_handle", "value": "<handle>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": true}
  ]
}
```

### Get LinkedIn Activity
Fetch recent LinkedIn posts from specified profiles.
```json
{
  "type": "get_linkedin_activity",
  "inputs": [
    {"name": "profile_urls", "value": "<urls>", "type": "textarea", "required": true},
    {"name": "num_posts", "value": 25, "type": "dropdown", "required": true},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": true}
  ]
}
```

### Search LinkedIn People
Search for LinkedIn profiles by name.
```json
{
  "type": "search_linkedin_people",
  "inputs": [
    {"name": "first_name", "value": "<first>", "type": "text", "required": true},
    {"name": "last_name", "value": "<last>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "linkedin_search_results", "type": "text", "required": true}
  ]
}
```

### Get LinkedIn Company Profile
Retrieve company page information.
```json
{
  "type": "get_linkedin_company_profile",
  "inputs": [
    {"name": "company_url", "value": "<url>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "company_profile", "type": "text", "required": true}
  ]
}
```

### Get LinkedIn Company Posts
Retrieve recent company posts.
```json
{
  "type": "get_linkedin_company_posts",
  "inputs": [
    {"name": "company_url", "value": "<url>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "company_posts", "type": "text", "required": true}
  ]
}
```

### Get LinkedIn Job Posting
Retrieve job posting details.
```json
{
  "type": "get_linkedin_job_posting",
  "inputs": [
    {"name": "job_url", "value": "<url>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "job_posting", "type": "text", "required": true}
  ]
}
```

### Search LinkedIn Jobs
Search for job postings.
```json
{
  "type": "search_linkedin_jobs",
  "inputs": [
    {"name": "keyword", "value": "<keyword>", "type": "text", "required": true},
    {"name": "location", "value": "<location>", "type": "text", "required": false},
    {"name": "country", "value": "<country>", "type": "text", "required": false},
    {"name": "job_type", "value": "<type>", "type": "dropdown", "required": false},
    {"name": "experience_level", "value": "<level>", "type": "dropdown", "required": false},
    {"name": "remote", "value": "<remote>", "type": "dropdown", "required": false},
    {"name": "time_range", "value": "<range>", "type": "dropdown", "required": false},
    {"name": "output_variable_name", "value": "job_search_results", "type": "text", "required": true}
  ]
}
```

### Get LinkedIn Posts
Retrieve posts by their direct URLs.
```json
{
  "type": "get_linkedin_posts",
  "inputs": [
    {"name": "post_urls", "value": "<urls>", "type": "textarea", "required": true},
    {"name": "output_variable_name", "value": "linkedin_posts", "type": "text", "required": true}
  ]
}
```

### Get Instagram Profile
Get Instagram profile info.
```json
{
  "type": "get_instagram_profile",
  "inputs": [
    {"name": "username", "value": "<username>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "instagram_profile", "type": "text", "required": true}
  ]
}
```

### Get Instagram Followers
Get top followers for an Instagram account.
```json
{
  "type": "get_instagram_followers",
  "inputs": [
    {"name": "username", "value": "<username>", "type": "text", "required": true},
    {"name": "limit", "value": "20", "type": "dropdown", "required": true},
    {"name": "output_variable_name", "value": "instagram_followers", "type": "text", "required": true}
  ]
}
```

### Bluesky Posts
Fetch recent posts from a Bluesky user.
```json
{
  "type": "get_bluesky_posts",
  "inputs": [
    {"name": "handle", "value": "<handle>", "type": "text", "required": true},
    {"name": "num_posts", "value": 25, "type": "dropdown", "required": true},
    {"name": "output_variable_name", "value": "bluesky_posts", "type": "text", "required": true}
  ]
}
```

---

## Business & Financial Data

### Enrich Company Data with Breeze Intelligence
```json
{
  "type": "get_company_object",
  "inputs": [
    {"name": "domain", "value": "<domain>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": true}
  ]
}
```

### Enrich User Data with Breeze Intelligence
```json
{
  "type": "get_person_object",
  "inputs": [
    {"name": "email", "value": "<email>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": true}
  ]
}
```

### Company Earnings Info
```json
{
  "type": "company_financial_info",
  "inputs": [
    {"name": "company", "value": "<company>", "type": "text", "required": true},
    {"name": "quarter", "value": "<quarter>", "type": "text", "required": true},
    {"name": "year", "value": "<year>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "company_earnings_report", "type": "text", "required": true}
  ]
}
```

### Company Financial Profile
```json
{
  "type": "company_financial_profile",
  "inputs": [
    {"name": "company", "value": "<company>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "company_financial_profile", "type": "text", "required": true}
  ]
}
```

### Domain Info
```json
{
  "type": "domain_info",
  "inputs": [
    {"name": "domain", "value": "<domain>", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "domain_info", "type": "text", "required": true}
  ]
}
```

### Get Data from Builder's Knowledge Base
```json
{
  "type": "get_data_from_builder_knowledge_base",
  "inputs": [
    {"name": "query", "value": "{{user_input}}", "type": "text", "required": true},
    {"name": "builder_knowledge_bases_list", "value": "<kb_list>", "type": "dropdown", "required": true},
    {"name": "max_documents_count", "value": "10", "type": "text", "required": true},
    {"name": "score_cutoff", "value": "0.2", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "knowledge_base_results", "type": "text", "required": true}
  ]
}
```

### Get Data from User's Uploaded Files
```json
{
  "type": "get_data_from_user_uploaded_files",
  "inputs": [
    {"name": "query", "value": "{{user_input}}", "type": "text", "required": true},
    {"name": "assistant_files", "value": "{{assistant_files}}", "type": "text", "required": true},
    {"name": "max_documents_count", "value": "10", "type": "text", "required": true},
    {"name": "score_cutoff", "value": "0.2", "type": "text", "required": true},
    {"name": "output_variable_name", "value": "knowledge_base_results", "type": "text", "required": true}
  ]
}
```

---

## Integration Intelligence

### Contact Enrichment & Relationship Synthesis
```json
{
  "type": "comprehensive_contact_intelligence",
  "inputs": [
    {"name": "email_provider", "value": "gmail", "type": "dropdown", "required": true},
    {"name": "email_list", "value": "<emails>", "type": "textarea", "required": false},
    {"name": "name_company_list", "value": "<name_company_pairs>", "type": "textarea", "required": false},
    {"name": "analyze_relationships", "value": true, "type": "checkbox", "required": false},
    {"name": "enrich_linkedin", "value": true, "type": "checkbox", "required": false},
    {"name": "enrich_company", "value": true, "type": "checkbox", "required": false},
    {"name": "output_variable_name", "value": "final_attendee_analysis", "type": "text", "required": true}
  ]
}
```

### Analyze Contact Email History & Insights
```json
{
  "type": "fetch_relevant_gmail_threads",
  "inputs": [
    {"name": "email_provider", "value": "gmail", "type": "dropdown", "required": true},
    {"name": "contact_email", "value": "<email>", "type": "text", "required": false},
    {"name": "meeting_topic", "value": "<topic>", "type": "text", "required": false},
    {"name": "date_range_days", "value": "90", "type": "dropdown", "required": true},
    {"name": "max_results", "value": "10", "type": "text", "required": true},
    {"name": "analysis_type", "value": "none", "type": "dropdown", "required": true},
    {"name": "output_variable_name", "value": "topic_relevant_gmail_threads", "type": "text", "required": true}
  ]
}
```

### Enrich Calendar Event
```json
{
  "type": "enrich_calendar_event",
  "inputs": [
    {"name": "calendar_provider", "value": "googlecalendar", "type": "dropdown", "required": true},
    {"name": "event_id", "value": "<event_id>", "type": "text", "required": true},
    {"name": "calendar_id", "value": "<calendar_id>", "type": "text", "required": false},
    {"name": "include_attendees", "value": true, "type": "checkbox", "required": false},
    {"name": "include_description", "value": true, "type": "checkbox", "required": false},
    {"name": "include_transcript", "value": true, "type": "checkbox", "required": false},
    {"name": "include_ai_insights", "value": true, "type": "checkbox", "required": false},
    {"name": "scrape_context_documents", "value": true, "type": "checkbox", "required": false}
  ]
}
```

### Get Calendar Events List
```json
{
  "type": "get_calendar_events_list",
  "inputs": [
    {"name": "calendar_provider", "value": "all", "type": "dropdown", "required": true},
    {"name": "event_filter", "value": "future", "type": "dropdown", "required": true},
    {"name": "max_events", "value": "30", "type": "text", "required": true},
    {"name": "primary_calendar_only", "value": true, "type": "checkbox", "required": true},
    {"name": "output_format", "value": "json", "type": "dropdown", "required": true},
    {"name": "output_variable_name", "value": "<output_variable>", "type": "text", "required": true}
  ]
}
```

---

# Runtime Variables

These variables are automatically available at runtime:

## User Context
| Variable | Description |
|----------|-------------|
| `user_token` | Unique token identifying the current user |
| `user_email` | Email address of the current user (if available) |
| `user_name` | Display name of the current user (if available) |
| `user_id` | Internal user ID |

## Session & Run
| Variable | Description |
|----------|-------------|
| `run_id` | Unique identifier for the current agent run |
| `agent_id` | The ID of the agent being executed |
| `agent_name` | The name of the current agent |
| `session_id` | The current session identifier |

## Date & Time
| Variable | Description |
|----------|-------------|
| `current_date` | Current date in YYYY-MM-DD format |
| `current_time` | Current time in HH:MM:SS format |
| `current_datetime` | Current date and time combined |
| `timestamp` | Unix timestamp of the current moment |
| `timezone` | The user's timezone (if available) |

## HubSpot Context (when connected)
| Variable | Description |
|----------|-------------|
| `hubspot_portal_id` | The connected HubSpot portal ID |
| `hubspot_user_id` | The HubSpot user ID |
| `hubspot_access_token` | OAuth access token for HubSpot API calls |

## Files (when uploaded)
| Variable | Description |
|----------|-------------|
| `assistant_files` | Array of files uploaded by the user |
| `file_urls` | Array of URLs for uploaded files |
| `file_names` | Array of names for uploaded files |

## Example Usage

In action inputs:
```
Hello {{ user_name }}, welcome to this agent run (ID: {{ run_id }}).
Today's date is {{ current_date }}.
```

In conditionals:
```
{{ hubspot_portal_id }} is not None
{{ user_email }} contains "@company.com"
```

---

# Example Workflows

## Example 1: Tech News Summarizer

```json
[
  {
    "id": "11111111-e29b-41d4-a716-446655440000",
    "type": "get_user_input",
    "label": "Get Topic",
    "order": 0,
    "inputs": [
      {"name": "input_type", "value": "text", "type": "dropdown", "required": true},
      {"name": "input_description", "value": "Enter a tech topic to summarize:", "type": "text", "required": true},
      {"name": "required", "value": true, "type": "checkbox", "required": false},
      {"name": "input_name", "value": "news_topic", "type": "text", "required": true}
    ]
  },
  {
    "id": "22222222-e29b-41d4-a716-446655440000",
    "type": "get_google_news",
    "label": "Fetch Recent News",
    "order": 1,
    "inputs": [
      {"name": "query", "value": "{{news_topic}}", "type": "text", "required": true},
      {"name": "date_range", "value": "24h", "type": "dropdown", "required": true},
      {"name": "output_variable_name", "value": "raw_news_data", "type": "text", "required": true}
    ]
  },
  {
    "id": "33333333-e29b-41d4-a716-446655440000",
    "type": "invoke_llm",
    "label": "Summarize News",
    "order": 2,
    "inputs": [
      {"name": "llm_engine", "value": "gpt-5-mini", "type": "dropdown", "required": true},
      {"name": "instructions", "value": "Analyze the following news about '{{news_topic}}' and create a concise summary with top 3 stories.\n\nNews Data:\n{{raw_news_data}}", "type": "textarea", "required": true},
      {"name": "output_variable_name", "value": "news_summary", "type": "text", "required": false}
    ]
  },
  {
    "id": "44444444-e29b-41d4-a716-446655440000",
    "type": "output_formatter",
    "label": "Display Summary",
    "order": 3,
    "inputs": [
      {"name": "heading", "value": "Daily Tech Digest: {{news_topic}}", "type": "text", "required": false},
      {"name": "output_formatted", "value": "{{news_summary}}", "type": "textarea", "required": true},
      {"name": "format", "value": "markdown", "type": "dropdown", "required": true}
    ]
  }
]
```

## Example 2: HubSpot Sales Prep with Conditional Logic

```json
[
  {
    "id": "12345678-1234-1234-1234-123456789abc",
    "type": "get_user_input",
    "label": "Enter Contact Email",
    "order": 0,
    "inputs": [
      {"name": "input_type", "value": "text", "type": "dropdown", "required": true},
      {"name": "input_description", "value": "Enter the email of the prospect:", "type": "text", "required": true},
      {"name": "required", "value": true, "type": "checkbox", "required": false},
      {"name": "input_name", "value": "target_email", "type": "text", "required": true}
    ]
  },
  {
    "id": "87654321-4321-4321-4321-cba987654321",
    "type": "hubspot.v2.search_objects",
    "label": "Search HubSpot Contact",
    "order": 1,
    "inputs": [
      {"name": "object_type", "value": "contacts", "type": "dropdown", "required": true},
      {"name": "filters", "value": [{"propertyName": "email", "operator": "EQ", "value": "{{target_email}}"}], "type": "properties"},
      {"name": "properties", "value": ["firstname", "lastname", "jobtitle", "company"], "type": "properties"},
      {"name": "output_variable_name", "value": "hs_search_results", "type": "text"}
    ]
  },
  {
    "id": "99887766-5544-3322-1100-aabbccddeeff",
    "type": "if_condition",
    "label": "Check if Contact Exists",
    "order": 2,
    "inputs": [
      {"name": "query", "value": "{{hs_search_results.total}} > 0", "type": "textarea"}
    ]
  },
  {
    "id": "11223344-5566-7788-9900-112233445566",
    "type": "set_variable",
    "label": "Set Contact ID",
    "order": 3,
    "inputs": [
      {"name": "variable_name", "value": "contact_id", "type": "text", "required": true},
      {"name": "variable_value", "value": "{{hs_search_results.results[0].id}}", "type": "textarea", "required": true}
    ]
  },
  {
    "id": "55667788-9900-1122-3344-556677889900",
    "type": "hubspot.v2.get_engagements",
    "label": "Get Recent Emails",
    "order": 4,
    "inputs": [
      {"name": "source_object_type", "value": "contacts", "type": "dropdown", "required": true},
      {"name": "source_object_id", "value": "{{contact_id}}", "type": "text", "required": true},
      {"name": "engagement_types", "value": ["emails", "notes"], "type": "checkboxes"},
      {"name": "result_limit", "value": "10", "type": "text"},
      {"name": "output_variable_name", "value": "engagements", "type": "text", "required": true}
    ]
  },
  {
    "id": "aabbccdd-eeff-0011-2233-445566778899",
    "type": "invoke_llm",
    "label": "Generate Meeting Brief",
    "order": 5,
    "inputs": [
      {"name": "llm_engine", "value": "gpt-5", "type": "dropdown", "required": true},
      {"name": "instructions", "value": "Review HubSpot engagements for {{target_email}}.\n\nGenerate a Pre-Meeting Briefing:\n1. Summary of last 3 interactions\n2. Detected sentiment\n3. Three suggested talking points\n\nEngagements:\n{{engagements}}", "type": "textarea", "required": true},
      {"name": "output_variable_name", "value": "briefing_doc", "type": "text", "required": false}
    ]
  },
  {
    "id": "ffeeddcc-bbaa-9988-7766-554433221100",
    "type": "if_condition",
    "label": "Else (Contact Not Found)",
    "order": 6,
    "inputs": [
      {"name": "else", "value": true, "type": "checkbox", "required": false}
    ]
  },
  {
    "id": "00112233-4455-6677-8899-aabbccddeeff",
    "type": "set_variable",
    "label": "Set Not Found Message",
    "order": 7,
    "inputs": [
      {"name": "variable_name", "value": "briefing_doc", "type": "text", "required": true},
      {"name": "variable_value", "value": "### Contact Not Found\nNo contact found with email {{target_email}}.", "type": "textarea", "required": true}
    ]
  },
  {
    "id": "8899aabb-ccdd-eeff-0011-223344556677",
    "type": "end_condition",
    "label": "End Conditional",
    "order": 8,
    "inputs": []
  },
  {
    "id": "77665544-3322-1100-ffee-ddccbbaa9988",
    "type": "output_formatter",
    "label": "Display Result",
    "order": 9,
    "inputs": [
      {"name": "heading", "value": "Agent Results", "type": "text", "required": false},
      {"name": "output_formatted", "value": "{{briefing_doc}}", "type": "textarea", "required": true},
      {"name": "format", "value": "markdown", "type": "dropdown", "required": true}
    ]
  }
]
```

---

# Best Practices

## Testing Strategies

### 3-Phase Testing Approach

**Phase 1: Unit Testing (Individual Capabilities)**
```
Test each tool separately:
- "Use Company Research to research Microsoft"
- "Use LinkedIn Enrichment for TechCorp"
- "Create a test contact in HubSpot"
```

**Phase 2: Integration Testing (Tool Combinations)**
```
Test tool chains:
- "Research Company X and add to HubSpot"
- "Analyze data and save to Google Sheets"
```

**Phase 3: User Acceptance Testing (Real Scenarios)**
```
Test like a real user:
- Ask vague questions
- Change mind mid-conversation
- Request edge cases
- Try to break it
```

### Build a Test Suite

```
BASIC FUNCTIONALITY
✓ Agent responds to greetings
✓ Sample questions all work
✓ Knowledge retrieval works
✓ Tool calling works

KNOWLEDGE TESTS
✓ "What do you know about [topic from knowledge]?"
✓ "Explain [concept from documentation]"

TOOL TESTS (for each tool)
✓ "[Simple tool request]"
✓ "[Complex tool request with multiple parameters]"
✓ "[Error scenario - invalid input]"

INTEGRATION TESTS
✓ "[Request requiring 2 tools]"
✓ "[Request requiring 3+ tools in sequence]"
✓ "[Request requiring approval gates]"

EDGE CASES
✓ Very long conversation (10+ turns)
✓ Ambiguous request
✓ Request outside capabilities
✓ Tool failure during workflow
✓ User says "no" to confirmation
```

---

# Validation Checklist

Before deploying your workflow agent JSON, verify:

## Structure
- [ ] Each action has: id, type, label, order, inputs
- [ ] All IDs are unique UUIDs
- [ ] Order is sequential starting from 0

## Variables
- [ ] Variable names match `^[a-zA-Z][a-zA-Z0-9_]*$`
- [ ] Variables are defined before being referenced
- [ ] Variable references use `{{ variable_name }}` syntax

## Action Types
- [ ] Each `type` matches an available action type exactly
- [ ] All required inputs are included
- [ ] Dropdown values match valid options

## Control Flow
- [ ] Every `if_condition` or `for_condition` has matching `end_condition`
- [ ] Else statements have `"else": true` and empty query

## Labels
- [ ] Each action has a descriptive, human-readable label

---

# Quick Reference Card

## Workflow Agent Setup

1. Create Workflow Agent in builder
2. Add actions with proper JSON structure
3. Define variables with valid names
4. Chain actions with variable references
5. Add control flow (if/else, loops) as needed
6. End with output formatter

## Common Patterns

**Input → Process → Output:**
```
get_user_input → invoke_llm → output_formatter
```

**Research → Enrich → Save:**
```
get_company_object → get_linkedin_profile → hubspot.v2.create_object
```

**Conditional with Fallback:**
```
if_condition → [success path] → else → [fallback path] → end_condition
```

---

*Documentation compiled from Agent.AI official docs. Last updated: January 2026*
