# Research notes

## Prior related research

- Searched inbox history and `results/` for Codex, Claude, VS Code, and Visual Studio references.
- No prior result addressed this setup question directly.
- Related conceptual result: `results/2026-10-09/agents-vs-skills/`.

## Evidence used

- OpenAI’s current Codex IDE documentation identifies VS Code and compatible editors as extension-based clients.
- Anthropic’s current VS Code guide calls the extension the recommended way to use Claude Code in VS Code; it bundles the panel CLI.
- Anthropic’s memory documentation now supports direct `AGENTS.md` loading in recent Claude Code versions, but default behavior favors `CLAUDE.md` when one is present. This is the key interoperability detail for a shared instruction file.
- VS Code’s trust model applies to agents and workspace-defined MCP configuration, so it is a meaningful control boundary—not an optional cosmetic preference.

## Judgment calls

- Recommended no “automatic routing” between agents. A human-owned task boundary and single edit owner is more predictable than parallel autonomous edits.
- Recommended a shared `AGENTS.md` plus an optional Claude overlay, rather than duplicating broad instructions in `AGENTS.md` and `CLAUDE.md`.
- Did not recommend a specific third-party extension bundle: it changes frequently and a minimal profile is safer and easier to diagnose.
