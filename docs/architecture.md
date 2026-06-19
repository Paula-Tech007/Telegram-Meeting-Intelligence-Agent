# Architecture

## Overview

The Telegram Meeting Intelligence Agent is an n8n automation that receives meeting information through Telegram, sends valid text content to an AI model, extracts structured meeting intelligence, and returns a formatted response to the same chat.

The first version is intentionally lightweight:

- Telegram is the input and output channel.
- n8n orchestrates validation, routing, AI request, formatting, and error handling.
- OpenAI is called through a credentialed HTTP Request node.
- PostgreSQL is prepared for future persistence, but it is not required for v1.
- Audio is detected and converted into a transcription-ready payload, with transcription left as a roadmap module.

## Logical Flow

```text
Telegram Trigger
  -> Normalize Input
  -> Validate Message
  -> Route Message Type
      -> Command Response
      -> Text Meeting Analysis
      -> Audio Transcription Placeholder
      -> Invalid Content Response
  -> Send Telegram Response
```

## Main Workflow Sections

| Section | Responsibility |
|---|---|
| Input | Receives Telegram updates and extracts chat/message metadata. |
| Validation | Rejects empty, too-short, unsupported, or unknown content. |
| Routing | Separates commands, text meeting content, audio, and fallback cases. |
| AI Analysis | Sends meeting text to OpenAI and expects strict JSON output. |
| Formatting | Escapes dynamic values and renders an HTML message for Telegram. |
| Error Handling | Returns a friendly message when the AI request fails. |

## Data Contract

The AI analysis returns this structured object:

```json
{
  "meeting_summary": "",
  "decisions": [],
  "action_items": [
    {
      "task": "",
      "owner": "",
      "deadline": "",
      "priority": "",
      "status": "open"
    }
  ],
  "pending_items": [],
  "risks": [],
  "next_steps": [],
  "ai_observations": ""
}
```

## Security Boundary

Secrets are not stored in workflow JSON. The workflow references n8n credentials only:

- Telegram credential type: `telegramApi`
- OpenAI credential type: `openAiApi`

All tokens and API keys must be configured manually in n8n credentials or local environment files that are not committed.

## Future Persistence

The `/database/schema.sql` file prepares tables for:

- Meetings
- Tasks
- Decisions
- Risks

The current workflow does not write to the database. This keeps the initial portfolio project easy to import and test.
