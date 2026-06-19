# Security

## Security Goals

This repository is designed for public GitHub portfolio use. It must never contain real credentials, tokens, private URLs, chat IDs, personal data, or corporate data.

## What Must Never Be Committed

- Telegram bot token
- OpenAI API key
- Real Telegram chat ID
- n8n encryption key
- n8n credential export with secret values
- Private URLs
- Real meeting notes
- Personal or corporate data
- Production screenshots with visible tokens or API keys

## Credential Handling

Use the n8n credential system:

| Service | n8n Credential Type |
|---|---|
| Telegram | `telegramApi` |
| OpenAI | `openAiApi` |

The workflow JSON contains placeholder credential references only. After import, select the credential manually in the n8n UI.

## Environment Variables

Use `.env.example` only as a template. Local `.env` files are ignored by Git.

```env
TELEGRAM_BOT_TOKEN=your_telegram_bot_token_here
OPENAI_API_KEY=your_openai_api_key_here
TELEGRAM_CHAT_ID=your_chat_id_here
```

## Screenshot Policy

Before adding screenshots:

1. Blur or remove API keys.
2. Blur or remove bot tokens.
3. Blur or remove chat IDs.
4. Use fictitious meeting data.
5. Do not show private URLs.
6. Do not expose internal hostnames.
7. Prefer masked credentials screens.

## Runtime Data

Meeting notes sent to the workflow are runtime data. If you adapt this for production:

- Define retention rules.
- Minimize storage.
- Avoid logging raw meeting content unless required.
- Consider encryption at rest for persisted data.
- Add access control around executions and database records.

## Recommended Production Hardening

- Configure an n8n workflow-level error workflow.
- Use separate credentials for development and production.
- Rotate credentials periodically.
- Limit Telegram bot usage to authorized chats.
- Add persistence only after a retention policy is defined.
- Add monitoring for OpenAI and Telegram failures.
