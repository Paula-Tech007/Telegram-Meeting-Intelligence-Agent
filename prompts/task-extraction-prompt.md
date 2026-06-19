# Task Extraction Prompt

Analyze the meeting content and extract only actionable tasks.

For each task, identify:

- Task description
- Owner
- Deadline
- Priority
- Status
- Dependency or blocker, when present

Return valid JSON only:

```json
{
  "action_items": [
    {
      "task": "",
      "owner": "",
      "deadline": "",
      "priority": "medium",
      "status": "open",
      "dependency": ""
    }
  ]
}
```

Rules:

- Do not invent owners.
- Do not invent dates.
- Use `high`, `medium`, or `low` for priority.
- Use `open` for new tasks.
- If there are no tasks, return an empty `action_items` array.
