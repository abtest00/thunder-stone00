# Measuring agent context and skill effectiveness

Date researched: 2026-11-06
Inbox item: How can I measure the effectiveness of context fed to models, and the effectiveness of skills?

## Short answer

Treat context and skills as **versioned interventions**, not as ambient prompt text. For a representative set of real tasks, hold the model, tools, and task prompt fixed; compare a minimal baseline against a context or skill variant; capture the trace and artifacts; and score outcome, process, safety, and cost. The useful question is not “did the model like the context?” but “did this version improve the decisions and deliverables we care about without adding regressions or unreasonable cost?”

OpenAI’s current agent-evaluation guidance recommends starting with traces while behavior is still being debugged, then using datasets and repeatable eval runs for comparisons. A trace records model calls, tool calls, guardrails, and handoffs, so it can reveal *why* a context or skill helped or hurt. [Evaluate agent workflows](https://developers.openai.com/api/docs/guides/agent-evals)

## Evaluate context: an ablation, not a vibes test

For each task, prepare a compact record containing the user request, the authoritative source material, an expected answer or rubric, and risk labels (for example: stale-source risk, permission-sensitive, or must-escalate). Run the same task through:

| Variant | What changes | What it tells you |
|---|---|---|
| Baseline | Task prompt + required tools only | Current capability / control |
| Context candidate | Baseline plus the proposed retrieved document, graph subgraph, or instruction | Net value of that context |
| Negative control | Baseline plus plausible but irrelevant context | Whether the system is distractible |
| Degraded context | An intentionally stale, conflicting, or incomplete source | Whether provenance, uncertainty, and escalation work |

Score each run on a small task-specific rubric: **grounded correctness**, **source/citation accuracy**, **constraint and permission adherence**, **appropriate uncertainty or escalation**, **tool selection/arguments**, **latency**, and **input/output tokens or cost**. Report the delta versus baseline, failure count, and confidence interval or repeated-run range—not merely an average score. OpenAI’s guidance warns against generic metrics and recommends task-specific tests, production-shaped data, logging, and human calibration of automated scores. [Evaluation best practices](https://developers.openai.com/api/docs/guides/evaluation-best-practices)

For RAP’s graph/OKF direction, each example should include a known approved answer and source evidence. Measure whether the agent selected the right product/package, cited the governing record, surfaced caveats/effective dates, and refused or escalated when the graph is incomplete. This extends the existing proposed measures of product selection, constraint violations, citation coverage, and escalation quality in the [AdCP research](../adcp-knowledge-graph-agent/summary.md).

## Evaluate skills separately

A skill can improve a result yet still fail operationally if it does not trigger, omits a required step, or performs needless work. OpenAI’s skill-evaluation guide defines the practical loop as **prompt → captured run (trace + artifacts) → small set of checks → comparable score**. It recommends measuring outcome, process, style, and efficiency; a small 10–20-prompt set is enough to catch early regressions. [Testing Agent Skills Systematically with Evals](https://developers.openai.com/blog/eval-skills)

Build a “skill contract” for each skill:

1. **Activation cases:** explicit requests and realistic implicit requests where the skill should trigger.
2. **Non-activation cases:** adjacent work where it must *not* trigger.
3. **Definition of done:** required files, commands, citations, schema, checks, and human-approval boundaries.
4. **Artifacts and trace checks:** did the agent read the required source, invoke the expected tool only when appropriate, create the required output, and avoid prohibited actions?
5. **Quality rubric:** does a blinded reviewer—or a calibrated LLM judge—find the output accurate, complete, usable, and aligned with conventions?

Use deterministic checks first: file existence, structured-output/schema validity, expected source references, command/tool events, and no forbidden writes. Then add a small rubric-based review for qualities deterministic checks cannot see. The OpenAI guide specifically describes recording `codex exec --json` JSONL and testing structured events, then using a structured rubric for style and conventions. [Testing Agent Skills Systematically with Evals](https://developers.openai.com/blog/eval-skills)

## A low-overhead first experiment

Start with 12–15 historical, non-sensitive questions from one bounded workflow, such as revenue-product planning or weekly research. Label each with the correct sources, essential facts, expected action state, and an acceptable answer example.

1. Run the baseline twice or three times to establish ordinary variation.
2. Run the candidate context version with identical model, tools, and task wording.
3. Blindly review paired outputs against the rubric; preserve traces and artifacts.
4. Promote the context only if it improves the must-pass measures without a material safety, latency, or cost regression.
5. Turn each real failure into a new case. Version the corpus, context bundle, skill, rubric, and evaluator so a future change is comparable.

Use a binary **release gate** alongside any aggregate score: for example, zero ungrounded claims in high-risk cases, 100% required-citation coverage, no unauthorized tool calls, and at least baseline completion rate. Aggregate scores can hide a serious safety failure.

## What to track in a simple scorecard

`case_id, task_family, context_version, skill_version, model, run_id, outcome_pass, grounded_correctness_0_2, citation_pass, constraint_pass, escalation_pass, tool_path_pass, latency_s, input_tokens, output_tokens, human_score_1_5, failure_tag, trace_path`

Do not aim for a universal “context quality” number. A context bundle is good only relative to a task distribution and an explicit policy. The earlier [context-library research](../2026-10-16/codex-claude-context-library/summary.md) remains a useful design constraint: keep scope, owner, freshness, sensitivity, and retrieval path explicit, rather than loading a large unbounded library.

## Source notes

- OpenAI Docs: [Evaluate agent workflows](https://developers.openai.com/api/docs/guides/agent-evals), [Evaluation best practices](https://developers.openai.com/api/docs/guides/evaluation-best-practices), and [Testing Agent Skills Systematically with Evals](https://developers.openai.com/blog/eval-skills).
- Local prior research: `results/2026-10-09/agents-vs-skills/`, `results/2026-10-16/codex-claude-context-library/`, and `results/2026-10-30/adcp-knowledge-graph-agent/`.
