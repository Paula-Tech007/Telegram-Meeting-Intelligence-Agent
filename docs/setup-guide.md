# Setup Guide

## Requirements

- n8n Cloud or self-hosted n8n
- Telegram account
- Telegram bot created with BotFather
- OpenAI API key
- Optional: PostgreSQL for future persistence

## 1. Clone or Download

```bash
git clone https://github.com/Paula-Tech007/Telegram-Meeting-Intelligence-Agent.git
cd telegram-meeting-intelligence-agent
```

## 2. Prepare Environment File

```bash
cp .env.example .env
```

Fill only your local `.env`. Do not commit it.

## 3. Configure Telegram Bot

1. Open Telegram and search for `@BotFather`.
2. Run `/newbot`.
3. Choose a bot name and username.
4. Copy the generated token.
5. In n8n, create a credential of type `Telegram API`.
6. Paste the bot token into the credential inside n8n.
7. Do not paste the token into workflow nodes, README files, examples, or JSON exports.

## 4. Configure OpenAI

1. Create or use an OpenAI API key.
2. In n8n, create a credential of type `OpenAI API`.
3. Paste the API key into the credential field.
4. Keep the key out of workflow JSON and documentation files.

## 5. Import Workflow

1. Open n8n.
2. Go to **Workflows**.
3. Click **Import from File**.
4. Select `workflows/telegram-meeting-intelligence-agent.json`.
5. Open each credentialed node and select the correct credential:
   - `01 - Telegram Trigger`
   - `06 - AI Meeting Analyzer`
   - Telegram send nodes
6. Save the workflow.
7. Activate the workflow.

## 6. Test

Send a meeting note to the bot with at least a few sentences, decisions, tasks, owners, or pending items.

Example:

```text
Reuniao de alinhamento do projeto. Foi decidido que a primeira versao sera entregue no n8n. O Lider Tecnico ficara responsavel por importar o workflow ate sexta-feira. Ainda falta validar politica de retencao.
```

Expected result:

- Executive summary
- Decisions
- Action items
- Pending items
- Risks
- Next steps
- AI observations

## 7. Optional Reminder Engine

The file `workflows/telegram-meeting-reminder-engine.json` is a companion workflow prepared for future reminders. It needs a target chat ID through an n8n variable or manual configuration before activation.

## Troubleshooting

| Problem | Likely Cause | Fix |
|---|---|---|
| Bot does not receive messages | Workflow inactive or Telegram credential missing | Activate workflow and reselect credential. |
| OpenAI request fails | OpenAI credential not selected or API key invalid | Recreate/reselect OpenAI credential. |
| Telegram response fails | Chat not available to bot | Start a chat with the bot and send `/start`. |
| Audio returns placeholder | Transcription is not enabled in v1 | Add Telegram file download + transcription step. |
