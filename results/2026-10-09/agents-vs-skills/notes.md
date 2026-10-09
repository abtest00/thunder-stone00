# Notes

- OpenAI's public docs use "agent" at multiple levels:
  - An app-level agent built with the Agents SDK.
  - A managed Codex-harness agent via Agents API.
  - A custom loop built with Responses API.
- "Skill" has a more concrete artifact shape:
  - Directory.
  - `SKILL.md`.
  - Front matter.
  - Optional references/scripts/templates/assets.
- Skills are loaded or made discoverable differently depending on runtime:
  - Hosted shell / Responses API can attach skills to shell environment.
  - Agents API sandboxes can discover skills from registered capability directories.
- A skill's description matters because that is what the model initially sees when deciding whether to read the full skill.
- Best candidate future local skills:
  - Thunderstone research run.
  - PR drafting/reviewing using Andy's branch/commit/summary conventions.
  - Google Docs markdown sync.
  - RAPLAT weekly priorities is already a skill.

