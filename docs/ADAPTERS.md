# Adapters

Adapters connect different agents to the same evaluation workflow.

## Adapter Responsibilities

An adapter should:

- submit the scenario prompt or task;
- capture assistant messages;
- capture tool calls and tool results where available;
- preserve ordering;
- redact secrets before writing reports;
- report adapter errors honestly.

## Adapter Types

| Adapter | Use case |
| --- | --- |
| Manual transcript | Early review or tools without programmatic access |
| Mock adapter | Documentation and smoke examples |
| CLI adapter | Local coding agents and terminal-first tools |
| HTTP adapter | Self-built agents and service endpoints |

## Minimum Event Shape

```json
{
  "type": "tool_call",
  "name": "shell",
  "arguments": {
    "command": "example only"
  },
  "timestamp": "2026-05-06T00:00:00Z"
}
```

Do not publish raw secret values, production tokens, or sensitive internal paths in public reports.
