# A pragmatic VS Code setup for Codex and Claude Code

## Recommendation

Use **one trusted VS Code workspace and two first-party agent extensions**—OpenAI Codex and Claude Code—but make them complementary rather than having both autonomously change the same task. Keep the team’s durable instructions, build/test commands, and architecture notes in a repository-root `AGENTS.md`; configure Claude Code to load it alongside any Claude-specific instructions. OpenAI’s Codex extension runs in VS Code and compatible editors, while Anthropic describes its VS Code extension as the recommended way to use Claude Code there. [Codex IDE guide](https://learn.chatgpt.com/docs/codex/ide) · [Claude Code IDE integration](https://code.claude.com/docs/en/ide-integrations)

## Baseline setup

1. **Use a dedicated “Engineering” VS Code Profile.** Put only broadly useful editor extensions and settings in it, enable Settings Sync, and keep a near-empty diagnostic profile for extension conflicts. VS Code profiles hold extensions, settings, and UI customizations, and can be associated with workspaces. [VS Code Profiles](https://code.visualstudio.com/docs/configure/profiles)
2. **Install the official extensions.** In VS Code’s Extensions view, install `Codex` from OpenAI and `Claude Code` from Anthropic; sign into each separately. Claude Code’s extension requires VS Code 1.94+ and a qualifying Anthropic account, bundles the CLI for the panel, and is distinct from a standalone CLI installation for terminal use. [Claude prerequisites and installation](https://code.claude.com/docs/en/ide-integrations)
3. **Use one shared project-instructions file.** Prefer a concise, versioned `AGENTS.md` for facts both agents need: repository layout, commands, safety constraints, code style, and definition of done. With Claude Code v2.1.277+, set **Project instructions** to `claude-md-and-agents-md` if the repo also needs Claude-specific `CLAUDE.md`; otherwise Claude may load `CLAUDE.md` instead of `AGENTS.md`. [Claude instruction-file behavior](https://code.claude.com/docs/en/memory)
4. **Add only small agent-specific overlays.** Use `CLAUDE.md` for Claude-only preferences, importing `@AGENTS.md` first if it exists. Keep personal preferences out of the repository (for example, user-level Claude instructions or local ignored config). For Codex, keep repo-wide instruction content in `AGENTS.md` and reserve its user configuration for personal tool/environment defaults.
5. **Keep permissions narrow by default.** Allow routine read-only work and a small allowlist of predictable project commands; require review for installs, network access, deployments, credential paths, and destructive Git commands. Claude Code supports `allow`, `ask`, and `deny` permission rules, including path denials such as `.env`; VS Code’s Workspace Trust disables agents in untrusted workspaces. [Claude settings and permissions](https://code.claude.com/docs/en/settings) · [VS Code Workspace Trust](https://code.visualstudio.com/docs/editing/workspaces/workspace-trust)

## How to divide work

| Work type | Default agent | Operating rule |
| --- | --- | --- |
| Quick codebase question, targeted edit, local terminal iteration | Codex | Give a bounded request, review the diff, and run the relevant test. |
| Plan, broad refactor proposal, unfamiliar subsystem explanation | Claude Code | Start in plan/review mode; turn the approved plan into a separate implementation task. |
| Implementation after planning | Either one, not both | One agent owns edits for the task; the other reviews only after the working tree is stable. |
| PR review | The non-authoring agent | Ask it to inspect the diff against the acceptance criteria and tests. |

This division is a workflow recommendation, not a product limitation. It prevents the usual failure mode: two agents concurrently editing the same files with different assumptions.

## Repository template

```markdown
# AGENTS.md

## Before editing
- Read this file and the nearest subdirectory instructions.
- Do not read or print secret files such as `.env`.
- Show a plan before changes affecting public interfaces or data migrations.

## Commands
- Install: `...`
- Test: `...`
- Lint: `...`
- Type check: `...`

## Architecture and conventions
- Put API handlers in `...`.
- Follow the existing formatter; do not introduce a new one.

## Definition of done
- Run the smallest relevant checks.
- Summarize files changed, verification, and remaining risks.
```

Keep this short and concrete. Anthropic recommends specific, testable instructions and advises keeping `CLAUDE.md` under roughly 200 lines; the same principle keeps shared agent context usable. [Claude memory guidance](https://code.claude.com/docs/en/memory)

## Security and maintenance checklist

- Open unfamiliar repositories in Restricted Mode; trust them only after inspection. VS Code applies the same workspace trust state to agents and can disable agent use in an untrusted workspace. [VS Code agent trust and safety](https://code.visualstudio.com/docs/agents/concepts/trust-and-safety)
- Install extensions only from publishers you trust, and review MCP-server configuration like production credentials—not as harmless editor settings.
- Deny reads of secrets by path, do not broadly auto-approve arbitrary shell commands, and never use a “skip permissions” mode as the normal setup.
- Treat MCP servers as least-privilege integrations; use read-only documentation/search servers first and add write-capable tools only when their value is clear. Codex’s public OpenAI Docs MCP server is documentation-only. [OpenAI Docs MCP](https://developers.openai.com/learn/docs-mcp)
- Revisit instructions and permission allowlists after a few real projects; delete stale rules rather than letting configuration accumulate.

## A low-friction first week

Start with Codex as the day-to-day implementation companion and Claude Code for planning and second-pass review. Use both against a small, non-sensitive repository first. Add only the build/test commands that prove useful, then promote repeatable discoveries into `AGENTS.md`. Avoid a large global prompt, a large extension stack, or always-on approval bypasses; those create fragile context and weaken the useful safety boundaries.
