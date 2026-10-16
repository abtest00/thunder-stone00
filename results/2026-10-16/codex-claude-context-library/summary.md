# Codex/Claude setup: how the current context library compares

The current setup is already ahead of a generic “single global prompt” approach: it has a shared workspace, repository-level `AGENTS.md` guidance, an explicit research repository, and domain-specific reference material. The next improvement is not more context—it is **clearer scope, ownership, and retrieval paths**.

## Current strengths

- `bulbasaur.code-workspace` establishes a deliberate multi-repository working set.
- `abtest00` holds human-facing organizational and work context; `thunder-stone00` separates durable research capture/results.
- Global instructions route specialized work (Jira, Slack, Confluence, research) to specific reference folders instead of placing everything in one file.
- The earlier [Codex/Claude VS Code setup research](../2026-10-09/codex-claude-vscode/summary.md) correctly recommends a shared durable instructions layer plus narrow agent-specific overlays.

## Gaps to close

1. **Make the instruction hierarchy explicit.** Add a short root `AGENTS.md` in each active repo that points to more specific instructions only when needed. Avoid relying on parent-folder discovery that may vary by tool.
2. **Classify the library.** Give each context source an owner, audience, sensitivity, freshness date, and “source of truth / reference / archive” status.
3. **Create a context index.** A one-page map of the most useful projects, decision logs, architecture docs, and commands is higher value than duplicating those contents in agent prompts.
4. **Use path-scoped rules.** Keep data-platform, dbt, and personal-workflow instructions separate so an agent working on one does not consume irrelevant context from another.
5. **Establish a maintenance loop.** After recurring corrections, promote stable rules into the appropriate repo instruction; delete obsolete guidance. Research findings belong in Thunder, not indiscriminately in agent files.

Claude Code can load `AGENTS.md` directly in recent versions, but its default behavior can prefer `CLAUDE.md` when both exist; configure it to load both when a Claude-specific overlay is needed. [Anthropic’s instruction-file guide](https://code.claude.com/docs/en/memory) Codex uses its own `AGENTS.md` conventions, so shared repo guidance remains the right interoperability baseline. [Codex IDE guide](https://learn.chatgpt.com/docs/codex/ide)

## Ideal target

`workspace index → repo AGENTS.md → path-specific rules → source-of-truth documents → tools/skills`.

Each layer should answer one kind of question. The agent should be able to find context deterministically, while sensitive or stale material is neither automatically loaded nor treated as authoritative.
