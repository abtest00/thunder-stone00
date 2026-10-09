# Agents vs. Skills

## Short Answer

Agents are the runtime actors: systems that plan, decide, call tools, use context, and carry work across steps. Skills are packaged task knowledge: reusable instructions, references, scripts, templates, and assets that an agent can discover and apply when a workflow matches.

OpenAI's agents documentation frames agents around runtime choices: Agents API for OpenAI-managed long-running Codex harness work, Agents SDK for application-controlled agent loops, and Responses API for direct model calls or custom orchestration. It also separates sessions, conversations, sandboxes, and execution environments as distinct resources. Source: [OpenAI Agents guide](https://developers.openai.com/api/docs/guides/agents).

OpenAI's skills documentation defines a skill as a directory with a `SKILL.md` manifest plus optional supporting files. Skills are modular instructions used to codify processes and conventions, and they can be loaded into hosted or local shell/container environments. Source: [OpenAI Skills guide](https://developers.openai.com/api/docs/guides/tools-skills).

## Practical Distinction

Agent:

- Owns the loop: observe, reason, act, verify, continue.
- Uses tools and state.
- May coordinate other agents.
- Needs runtime infrastructure: API session, SDK runner, Responses loop, sandbox, or app environment.
- Is responsible for applying judgment under the active instruction hierarchy.

Skill:

- Does not act by itself.
- Teaches an agent how to do a repeatable workflow.
- Can include references, scripts, templates, assets, and examples.
- Is selected by metadata first, then read in full only when relevant.
- Is best for durable process knowledge that would otherwise bloat global instructions.

## Relationship

Skills are capabilities for agents, not substitutes for agents. A useful mental model:

- Agent = worker plus runtime.
- Tool = action surface.
- Skill = playbook plus supporting materials.
- `AGENTS.md` = broad local operating context and preferences.

In practice, an agent may see a list of available skills with names, descriptions, and paths. When a skill applies, the agent reads `SKILL.md`, follows its instructions, and uses any referenced files or scripts. This keeps the initial context smaller while letting specialized workflows carry richer instructions when needed. Source: [OpenAI Skills guide](https://developers.openai.com/api/docs/guides/tools-skills).

## Why This Matters For Andy's Setup

Your `AGENTS.md` preferences are best for stable cross-task defaults: your name, role, repo conventions, PR norms, and recurring research process. Skills are better for narrow repeatable workflows such as LookML diagnostics, RAPLAT priorities, Google Docs sync, spreadsheet manipulation, or a future "Thunderstone research run" workflow.

The clean architecture is:

- Keep global preferences short and stable.
- Move workflow-specific steps into skills.
- Let skills point to deeper references instead of pasting everything into global instructions.
- Keep scripts with the skill when the workflow has repeatable mechanical steps.

## Takeaways

1. An agent performs work; a skill shapes how the agent performs a specific kind of work.
2. Skills are useful when the same workflow recurs and needs more context than a short standing instruction.
3. Tools expose capabilities; skills explain how to combine them.
4. Skills should be reviewed before use because they can affect agent behavior and may carry security risk, especially with network access or code execution. Source: [OpenAI Skills guide](https://developers.openai.com/api/docs/guides/tools-skills).
5. For your workspace, a Thunderstone research skill would be a natural next consolidation: it could encode inbox selection, output folder structure, source capture, and DONE marking.

