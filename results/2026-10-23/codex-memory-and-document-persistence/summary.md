# Codex memory and durable document persistence

Codex can save **local memories automatically**, but it does not automatically turn a working chat into a curated, repository-owned documentation set in the way a deliberate project workflow can. Use local memories for helpful recall; use `AGENTS.md` and checked-in Markdown for guidance or knowledge that must persist and be reviewable. [OpenAI Docs: Memories](https://learn.chatgpt.com/docs/customization/memories) · [OpenAI Docs: AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)

## Turn on memory

In the ChatGPT desktop app, go to **Settings → Personalization → Enable Codex memories**. In an individual chat, use `/memories` to choose whether it can consume existing memories and contribute future ones. Codex generates memories in the background after a chat is idle; it may skip the pass for short/active chats or low rate-limit headroom. [OpenAI Docs: Memories](https://learn.chatgpt.com/docs/customization/memories)

## For periodic durable docs, use an explicit workflow

1. Keep repeatable repo rules in a short root `AGENTS.md`, with scoped files in subdirectories.
2. Ask Codex to write a dated decision/research note at a clear milestone; review it like any other change.
3. Use `/export session.md` when you need the full conversation saved as Markdown, rather than relying on memory extraction.
4. Create scheduled tasks only for a recurring, explicit outcome (for example, a weekly research pass); do not use schedules merely to force generic chat summarization.

Codex’s local memories live under `~/.codex/memories/` and should be treated as generated local state, not the source of truth. OpenAI’s documentation recommends keeping required team guidance in `AGENTS.md` or checked-in documentation. [OpenAI Docs: Memories](https://learn.chatgpt.com/docs/customization/memories)

## Best fit for Andy’s library

Keep the current Thunder workflow for research results and use explicit repository docs for plans, decisions, and runbooks. Enable Codex memories for continuity across chats, but avoid copying all memories into source control automatically; promote only reviewed, durable learning.
