# Codex Workflow Audit — 2026-11-06 Deep Dive

## Run metadata

- Run type: Manual deep-dive, following the scheduled audit
- Evidence window: 2026-10-23 through 2026-11-06
- Projects: All 17 folders in `/Users/abieber/bulbasaur.code-workspace`
- Authorized evidence: Codex task history, local files, Git history and working-tree diffs, generated results, and current public primary sources
- Audit output writes: Report and index only

## Executive assessment

Andy used Codex broadly and substantively this period: at least 81 identifiable user-started tasks covered production diagnosis, implementation, technical review, governance, drafting, and discovery. The strongest pattern is evidence-seeking operational work: recent DAG ledgers separate verified recovery from unknown state, and the final GAM dependency check names the exact late inputs and remaining scheduler uncertainty.

The main friction is not lack of effort or verification. It is fragmentation: complex threads such as BigQuery telemetry, repository governance, and data readiness are spread across many short tasks, making prior decisions, proof, and open questions easy to rediscover. The most valuable next change is a compact continuity brief for multi-session initiatives, paired with the already-proposed standalone readiness mode.

## Coverage and confidence

- Codex history: 79 active and 4 archived records touched the period. Excluding this scheduled audit and the unrelated weekly-research schedule leaves **81 identifiable user-started tasks**; one archived runtime record without a user request was excluded from analysis.
- Task history was paged through 100 active and 50 archived records, reaching history older than the window. This is a full available-history inventory for the window, not a first-page sample.
- Detailed evidence: task summaries, current Git history/status in all workspace repositories, and nine generated DAG-triage ledgers from October 28–November 6.
- Limitation: detailed turn retrieval was unavailable for several selected tasks, so task-level completion and rework counts below are conservative and title/result based.

## Usage scorecard

| Work type | Tasks | Verified completion | Follow-up/rework signal | What this says |
|---|---:|---:|---:|---|
| Diagnosis and operations | 22 | ≥9 generated ledgers/checks | Repeated readiness and DAG rechecks | Codex is used as an operational investigator, not just a Q&A tool. |
| Implementation and delivery | 16 | ≥7 merged commits/PRs in relevant repos | Several work items continue across separate threads | Delivery evidence is strong; continuity is the gap. |
| Review and validation | 13 | ≥5 reviewed branches/PRs or audits | Follow-up fixes and re-reviews are expected | Review is a high-leverage second pass and should keep explicit evidence. |
| Planning, drafting, and governance | 17 | ≥4 durable governance/CI changes | Multiple related template and ownership questions | This is evolving from ad hoc prompting into durable repository practice. |
| Discovery and explanation | 13 | Unknown by design | Low rework visible | Good use of Codex for rapid orientation; completion is often conversational rather than artifact-based. |

Counts are manual classification of the 81 task titles and summaries. Verified-completion counts are lower bounds based on observable Git or generated-artifact evidence, not a claim that all other tasks failed.

## Representative evidence

| Task/date | Intent | Outcome and evidence | Friction or strength | Lesson |
|---|---|---|---|---|
| DAG failure triage, Nov. 3 and 5 | Classify alert volume and decide what needs action | Multiple saved ledgers progressed from credential-blocked/unknown to 58 runs with 37 recovered, 21 failed, and explicit action queues | Strong closed-loop verification; no state was guessed during the blocked pass | Preserve this evidence-first pattern for all operational checks. |
| Find late GAM mart dependencies, Nov. 6 | Explain a late mart | Saved ledger traced four gates, identified the final hour-23 source checks, and left scheduler pickup explicitly unverified | Strong bounded conclusion | A good model for concise operational answers: cause, proof, remaining uncertainty. |
| BigQuery telemetry cluster, Oct. 29–Nov. 6 | Build telemetry, review lineage, repair deploy, and add ownership | `dbt-pi-ads-and-finance` merged telemetry lineage (`5e68a50`) and CODEOWNERS (`8db560b`) | Work spans many related conversations | Maintain one initiative brief across implementation, review, and deployment. |
| Add team-wide CODEOWNERS, Nov. 6 | Establish review routing without default reviewers | CODEOWNERS routing merged; PR template and resource-label CI were also merged earlier | Governance request became repository-native policy | Durable repository artifacts are better than repeated chat-level conventions. |
| PR-template precedence and tailoring, Nov. 5 | Resolve generic versus dbt-specific review guidance | A dbt repository PR template and CI enforcement had already merged; Leaf guidance was further refined | Clear improvement from prior audit's sparse policy surface | Continue resolving recurring questions in the narrowest owning repository. |
| Update Yahoo ID and backfill, Oct. 29 | Coordinate a cross-repo operational change | Recent Curator/Conductor commits show Yahoo and Magnite scheduling work | Generated artifacts remain locally untracked | Keep source/generated ownership explicit in the continuity brief. |
| Missing Curation Delivery hours, recurring | Recheck source and mart coverage | Repeated readiness requests persisted across audits | Legitimate monitoring is still manual and multi-call | This validates the carried-forward standalone readiness proposal. |
| Review conductor and Sigma branches, Oct. 29 | Validate work before handoff | Relevant repositories have recent fixes and PR merges | Detailed transcript evidence unavailable | Ask for a short verification contract up front: checks, expected proof, and handoff condition. |
| Cost reduction / DDM Ad Solution planning, Oct. 30–Nov. 4 | Move from investigation to an action plan | Multiple related investigation and planning tasks surfaced the same program | Context is distributed across threads and local notes | A continuity brief would reduce rediscovery and make decision history inspectable. |

## What is working

- **Evidence-aware operational reasoning:** The DAG workflow correctly treats unavailable credentials as an evidence gap, reruns after authentication, and preserves unknown states rather than fabricating clearance.
- **Iteration with durable output:** Nine task ledgers created in ten days show that repeated work is being captured as inspectable artifacts rather than transient chat prose.
- **Repository-level learning:** PR templates, CI checks, CODEOWNERS, and refined Git/PR guidance show a healthy progression from one-off corrections to reusable guardrails.
- **Appropriate human control:** High-impact work stays reviewable; no evidence suggests unnecessary external writes or attempts to bypass managed settings.

## Open findings

### Multi-session initiatives lack a compact continuity surface

The BigQuery telemetry, dbt governance, and cost-reduction work each appear across several narrowly scoped tasks. This is normal collaboration, but the current history does not provide one durable view of objective, decisions, current branch/PR, verification evidence, and open questions. That creates avoidable rediscovery and makes it harder for the weekly audit to measure completion.

### Standalone readiness checks remain manual

The Curation Delivery refresh pattern remains open from the October 23 and October 30 audits. The new GAM dependency ledger shows the desired quality bar, but it is still reconstructed per task rather than invoked as a defined no-alert readiness mode.

## Proposals

### 1. Adopt a continuity brief for multi-session technical initiatives

**Evidence:** The telemetry effort spans implementation, deployment repair, lineage review, CODEOWNERS, and repository practice tasks. Cost-reduction and data-readiness work follow the same multi-thread pattern.

**Benefit:** A five-minute update after meaningful progress prevents repeated discovery, preserves verification proof, and gives future sessions—and the weekly audit—a reliable state handoff.

**Draft:** For any initiative expected to require three or more Codex tasks, maintain a user-owned `status.md` in the relevant project area with: objective; repositories/branches; decisions; verified evidence and links; open questions/risks; and next action. Begin follow-up tasks by reading that brief and end completed tasks by proposing a concise update for approval.

**Owner and next-week signal:** Andy owns adoption; Codex drafts updates. Success is one active multi-session initiative with a current brief that eliminates a rediscovery question in a follow-up task.

**Approval status:** Proposed; not implemented.

### 2. Carry forward: standalone source-readiness mode in `dag-failure-triage`

**Evidence:** Curation Delivery coverage checks repeat across audit windows, while the Nov. 6 GAM check demonstrates the required source-to-mart reasoning and bounded uncertainty.

**Benefit:** A read-only named mode would make coverage refreshes consistent and reduce repeated prompt reconstruction.

**Draft:** Retain the October 23 proposal: derive expected coverage from repository configuration; inspect relevant source, landing, warehouse, and mart layers; report expected/present/missing partitions; distinguish unknown from complete; save a compact ledger; and do not rerun jobs or modify Slack.

**Owner and next-week signal:** Andy decides whether to approve the skill change. Success is one readiness request completed through the mode with a reusable ledger and no clarification needed to identify layers or time boundaries.

**Approval status:** Proposed; not implemented.

## Change from prior audits

| Area | Movement | Evidence |
|---|---|---|
| Verification rigor | Improving | Current DAG ledgers explicitly preserve unknowns, then verify recovery with snapshot evidence. |
| Durable guidance | Improving | PR template, CI guard, CODEOWNERS, and Leaf Git/PR refinements. |
| Source-to-mart readiness | Stable/open | Repeated Curation checks; GAM shows high-quality execution but not a reusable no-alert mode. |
| Cross-repository artifact ownership | Stable/open | Generated Conductor and Curator YAML remains untracked; no new user correction was observed. |
| Initiative continuity | Newly observed | High volume of related, fragmented telemetry/governance/cost tasks. |

## AI workflow pulse

- OpenAI's May 11, 2026 [iterative repair-loop guidance](https://developers.openai.com/cookbook/examples/codex/build_iterative_repair_loops_with_codex) emphasizes producing, validating, and using feedback for the next pass. This directly supports the observed strength in DAG triage and is the rationale for making verification proof a first-class continuity-brief field.
- OpenAI's July 20, 2026 [custom code-review rules guidance](https://developers.openai.com/blog/custom-code-review-rules-for-codex) recommends a small number of repository-specific rules and validating them on representative PRs. The inference for Andy is narrow: the new dbt PR-template/CODEOWNERS work should be evaluated on real PRs before expanding it into more global instructions.
- Anthropic's January 9, 2026 [agent-evaluation overview](https://www.anthropic.com/research/demystifying-evals-for-ai-agents) describes multi-turn evaluation as tool use plus outcome grading. The inference is to measure this workflow with observed evidence—verified results and reduced rediscovery—not invented productivity scores.

## Next-week practice plan

- **Hypothesis:** A one-page continuity brief will reduce rediscovery and improve handoff quality on multi-session technical work.
- **Behavior to try:** Pick one active initiative with at least three related tasks (for example, BigQuery telemetry or data-cost reduction) and create a brief containing objective, branch/PR, decision log, verification evidence, risks, and next action.
- **Evidence to collect:** Count follow-up tasks that refer to the brief; note whether Codex can answer status/next-step questions without reopening broad context.
- **Success signal:** At least one follow-up begins from the brief and produces a verifiable next result without a corrective rediscovery prompt.

## Working-tree observations

- `moon-stone00`: the authorized workflow-audit skill, template, and scheduled-prompt updates from this session are uncommitted.
- `conductor`: six untracked configuration YAML files; `curator`: one untracked generated DAG configuration YAML file.

These observations do not establish ownership, correctness, or a cleanup requirement.

## Limitations

- Several task transcripts could not be loaded in detail, so the scorecard uses conservative lower-bound verification counts.
- Local Git history can prove commits and merged PRs, not production outcome for every work item.
- The AI workflow pulse is a small, decision-relevant scan rather than a comprehensive trend report.

No audited project files, external systems, plugins, or automations were changed during this audit. The workflow-audit skill changes listed above were separately authorized before this deep-dive run.
