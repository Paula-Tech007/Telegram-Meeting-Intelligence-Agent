# n8n Workflows

Esta pasta contem os arquivos JSON importaveis no n8n.

## Workflow Principal

Importe este arquivo no n8n:

[`telegram-meeting-intelligence-agent.json`](telegram-meeting-intelligence-agent.json)

Ele contem o fluxo principal:

```text
Telegram Trigger
-> Normalize Input
-> Validate Message
-> Route Message Type
-> AI Meeting Analyzer
-> Format Telegram Response
-> Send Telegram Response
```

## Workflow Complementar

[`telegram-meeting-reminder-engine.json`](telegram-meeting-reminder-engine.json)

Este arquivo e uma base de roadmap para lembretes de pendencias. Ele nao e obrigatorio para testar a primeira versao.

## Como Importar

1. Abra o n8n.
2. Clique em **Workflows**.
3. Clique em **Import from File**.
4. Selecione `telegram-meeting-intelligence-agent.json`.
5. Depois da importacao, abra os nodes com credenciais.
6. Selecione manualmente:
   - Credencial `Telegram API`
   - Credencial `OpenAI API`
7. Salve e ative o workflow.

## Seguranca

Os JSONs usam apenas placeholders de credenciais do n8n. Eles nao contem token real do Telegram, API key real da OpenAI, chat ID real ou URLs privadas.
