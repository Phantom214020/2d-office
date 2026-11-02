# Architecture

This describes the private build. File names may change before the code is published.

## The pieces

| piece | job |
|---|---|
| hook | A small Node script registered as an async Claude Code hook. It never blocks Claude and always exits 0. |
| local server | Node, no dependencies. Serves the office page, takes events from the hook and streams them to the window over Server-Sent Events. Binds to localhost only. |
| office window | A canvas app in a small Edge or Chrome app window. It draws the office and runs the simulation. |

## Event flow

```
Claude Code event
  -> hook (event type, tool name, trimmed detail)
  -> local server on 127.0.0.1
  -> SSE stream
  -> office window: jobs system assigns work, workers act it out
```

## Claude events and what they look like

| Claude event | in the office |
|---|---|
| UserPromptSubmit | the receptionist calls it in, the manager reads it and walks it to the owner |
| PreToolUse / PostToolUse | the owner of that tool works at their desk, thought bubble shows the action |
| subagent start | another specialist is assigned. Two or more at once call a huddle |
| big prompt | a team meeting in the conference room first |
| Notification | the manager shows a question mark and "Need your answer" |
| Stop | the specialist hands the answer to the manager, an "Answer delivered" toast appears |

## Who owns what (default roles)

| role | owns |
|---|---|
| manager | takes every request first |
| engineer | code: shell, edits, tests, builds |
| researcher and writer | web search, browsing, docs, design |
| mathematician | math, finance, accounting |
| problem solver | general questions, economics |
| spreadsheet specialist | spreadsheets, CSV, formulas |
| sales lead | sales and marketing |
| analyst | stats, analytics, pricing |
| strategist | strategy, risk, review |
| planner | planning, to-do lists |
| receptionist | admin documents, invoices |
| communications | messages and communication |

The public version will let you rename these roles, change who owns what and add your own.

## Inside the window

- **Map:** floors, doors, furniture, seats and occluders measured off the office art, so desks hide the legs of people sitting behind them.
- **Navigation:** a walk grid with A* that charges extra near walls, plus a personal space rule so people do not stand on top of each other.
- **Agents:** each worker has an action queue, animation playback and held props.
- **Brain:** idle life driven by needs and personality. Chats are scripted back and forth, and a chat can end in a real action.
- **Jobs:** turns Claude events into work for the right worker.
- **Rendering:** pixel art drawn by code from pose keyframes, with a pixel font for bubbles and labels.

## Privacy

Only the event type, the tool name and a short detail (a file name, a command's description, a search query or a web host) leave Claude. File contents, subagent prompts and full URLs are never sent. Nothing leaves the machine.

## Timing

The Stop hook fires when Claude has already answered. The hand-off and toast happen at that moment. The manager's walk to the front door plays after as an epilogue.
