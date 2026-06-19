# Telegram Response Template

Use this template after the AI returns structured JSON.

Telegram parse mode recommended: `HTML`.

```html
<b>Resumo da Reuniao</b>

<b>Resumo executivo:</b>
{{meeting_summary}}

<b>Decisoes:</b>
1. {{decision}}

<b>Acoes identificadas:</b>
1. <b>Responsavel:</b> {{owner}}
   <b>Tarefa:</b> {{task}}
   <b>Prazo:</b> {{deadline}}
   <b>Prioridade:</b> {{priority}}

<b>Pendencias:</b>
1. {{pending_item}}

<b>Riscos:</b>
1. {{risk}}

<b>Proximos passos:</b>
1. {{next_step}}

<b>Observacoes da IA:</b>
{{ai_observations}}
```

Security note:

- Escape HTML before sending dynamic values to Telegram.
- Never include tokens, API keys, raw credential objects, or private URLs in the final message.
