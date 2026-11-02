# Phantom Office

**A 2D pixel office that replaces the "waiting for an answer" spinner in Claude Code.**

Status: work in progress. A private build runs today. This repo holds the plan and the design while the open source version gets ready. No code has been published here yet.

## The idea

You paste a prompt into Claude and then you wait. You see a spinner and a line of text, and that is it.

Phantom Office turns that wait into something you can watch. When you send a prompt, a separate window opens with a small pixel office inside it. Ten or more little workers live there. Each one is a subagent with its own specialty. The office acts out the real work Claude is doing, as it happens.

- A math question goes to the mathematician. He walks to his desk, opens his laptop and gets to work.
- A coding task goes to the engineer. Her thought bubble shows the command Claude is running, like "Running: npm test".
- Everyone who is not on the job carries on with their day. They play pool, hit the gym, grab a coffee, nap on the sofa and chat with each other.

## A bigger job

Say the prompt is "research this topic and then write a book on it."

1. The manager takes the brief at the front desk.
2. The team meets in the conference room and talks it over in speech bubbles, like real people, to decide how to split the work.
3. The researcher and the writer go back to their laptops and do their parts. They message each other in text bubbles as they go.
4. A banner at the top of the screen shows when the answer is coming.
5. When the answer is ready, the worker hands it to the manager, and the office brings you back to the Claude tab you were on so you can read it.

## What works today (private build)

These parts run on my machine and are tested. They are not published yet.

- A live window that opens by itself when a prompt is sent, wired to Claude Code through hooks.
- 13 hand-drawn characters with their own walks, idles, sleeping poses and signature moves, plus 5 office pets.
- A full floor plan with desks, a conference room, cafe, gym, nap room, washrooms and a pool table with real eight-ball physics.
- Routing from Claude events to workers: each tool call pulls in the worker who owns that kind of tool. Two or more subagents at once call a huddle in the conference room.
- Idle life driven by needs and personalities, with 176 scripted conversations where each line answers the last.
- Privacy: the hook sends only the event type, the tool name and a short trimmed detail to localhost. File contents, subagent prompts and full URLs never leave Claude.
- A test suite of 383 checks covering every animation frame, every walkable seat, a simulated 25 minute work day and the live event stream.

## What is still to come

See [ROADMAP.md](ROADMAP.md). The short version:

- Open source release with a clean install.
- Custom workers. Right now the cast is my friends, who agreed to be in it for personal use. The public version will let you build your own team: names, looks, outfits and specialties.
- True one worker per subagent, so the office mirrors Claude's subagents one to one.
- Planning meetings that show the real plan, and a live "answer in" banner.
- Jump back to the Claude tab when the answer lands.

## How it works

See [docs/architecture.md](docs/architecture.md) for the pieces and how a Claude event becomes an action in the office.

## Who is building it

John (Phantom214020). Feedback and ideas are welcome in Issues.
