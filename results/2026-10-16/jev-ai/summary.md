# Jev: TypeSafe’s AI decision model

Updated 2026-10-16. This corrects the earlier interpretation of “JEV” as Jevons paradox following Andy’s clarification.

Jev is TypeSafe’s model for making structured decisions from supplied context. It returns choices, rubric scores, or probabilities for statements instead of generating prose. Typical uses include classifying incoming requests, routing work, and deciding whether to escalate an item. [Official introduction](https://docs.typesafe.ai/introduction)

The appeal for agent builders is a focused decision step that ordinary code can consume directly. TypeSafe positions it as fast and structured; that explains its relevance to agent workflows, but this research does not establish adoption growth or independently verify speed and accuracy claims. A useful RAP experiment would be classifying analytics requests by team and urgency, then checking results against human labels. [Official introduction](https://docs.typesafe.ai/introduction)

## Model, local library, and skill

The documented integration uses a hosted API and an API key. Python (`typesafe-sdk`) and JavaScript/TypeScript (`@typesafe-ai/sdk`) libraries run in your project and call that service. A local SDK or CLI is therefore different from running the model locally. The official quickstart does not provide a local model deployment. [Quickstart](https://docs.typesafe.ai/introduction/quickstart)

TypeSafe also publishes an agent skill that guides coding agents in building integrations. The skill supplies instructions; it does not contain the model weights. Keep its source handy when evaluating an integration: [official TypeSafe SKILL.md](https://github.com/typesafe-ai/skills/blob/main/skills/typesafe-ai/SKILL.md).

The vendor documents this installation command, with project-local installation as the default:

```sh
npx skills add typesafe-ai/skills --skill typesafe-ai
```

For Claude Code, the documented alternative is:

```sh
claude plugin marketplace add typesafe-ai/skills
claude plugin install typesafe@typesafe-ai
```

These are reference instructions, not commands executed during this research update. An integration still needs a TypeSafe API key. [Official skill setup](https://docs.typesafe.ai/introduction/quickstart)

## Practical next step

Try a small labeled set of non-sensitive request examples. Compare classification quality, latency, cost, and escalation behavior with the current approach before adopting it. Structured output makes integration easier, but correctness still needs evaluation. This is a proposed experiment, not a completed benchmark.
