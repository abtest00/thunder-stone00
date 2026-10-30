# Saving Codex and Claude conversations outside the tools

Use **explicit exports plus a curated decision log**, not automatic blind syncing of every transcript. Full conversations often contain secrets, customer data, noisy tool output, and dead ends; durable project knowledge should be a reviewed artifact.

## Practical workflow

1. Create a private archive directory outside both tools, such as a private Git repository or encrypted cloud folder, organized by `YYYY-MM/topic/`.
2. At material milestones, export the full transcript and save a short human-reviewed `decision.md` containing outcome, decisions, files/links, next steps, and sensitivity.
3. Store long-lived operating guidance in repository `AGENTS.md`/docs, not in chat archives or local memories.
4. Exclude secrets and sensitive work content from any repo that is not explicitly approved for them; use a private encrypted store for raw transcripts.

Codex supports `/export session.md` to save the complete conversation as Markdown; it also keeps local transcripts by default, but those are local state—not a shared knowledge system. [Official OpenAI documentation](https://learn.chatgpt.com/docs/developer-commands) · [Codex history persistence](https://learn.chatgpt.com/docs/config-file/config-advanced)

Claude Code supports `/export` for a full conversation file, and Claude app/desktop supports an account data export through **Settings → Privacy → Export data**. [Claude Code FAQ](https://support.claude.com/en/articles/14554922-claude-code-user-faq) · [Claude data export](https://support.claude.com/en/articles/9450526-export-your-claude-data)

## Suggested cadence

- **Per meaningful session:** export if it produced a decision, complex plan, or reusable investigation.
- **Weekly:** review exports and promote only durable decisions into the relevant project docs/Thunder research results.
- **Monthly:** verify private archive access and prune duplicate exports according to retention policy.

This gets the “outside the tools” safety benefit without turning every chat into unreviewed, searchable organizational context.
