# Codex Workflow Audit — 2026-10-23

## Run metadata

- Run type: Manual
- Evidence window: 2026-10-09 through 2026-10-23
- Projects: All 17 folders in `/Users/abieber/bulbasaur.code-workspace`
- Authorized evidence: Codex task history, instructions, skills, Git history,
  working-tree status and diffs, and generated results
- Audit output writes: None during the original run; report reconstructed and
  indexed on 2026-10-26

## Executive summary

The audit reviewed 85 user-started Codex sessions. Two prominent correction
patterns had already become durable guidance: legacy Atlassian routing and the
DAG-triage rules for evidence, rate limits, Slack links, reaction semantics, and
ledgers. The remaining opportunities were a shared-system preview gate,
standalone source-readiness coverage, and cross-repository integration ownership.

## Already addressed

- Repeated corrections to avoid the legacy Atlassian connector are now covered
  by the global AGENTS.md rule that requires the current connection exclusively.
- Earlier DAG-triage problems—including guessed results during rate limits,
  malformed Slack links, and inconsistent ledgers—are now addressed in the
  current `dag-failure-triage` skill. Recent run directories consistently contain
  ledgers and reports.

No plugin change was recommended because the approved current connectors covered
the observed needs.

## Proposals

### 1. Add a shared-system preview gate to AGENTS.md

**Evidence:** Multiple tasks explicitly requested drafting Jira work before
submission, and Andy positively identified preview-before-publish behavior as the
preferred Confluence workflow. Google Docs had an approval rule, but shared-system
writes did not have an equivalent global rule.

**Benefit:** Makes preview and verification the durable default across Jira,
Confluence, Slack, Drive, and similar systems.

**Draft:** Default shared systems to read-only inspection. Before creating,
updating, publishing, or sending, show the exact draft and targets and wait for
approval. After an approved write, read it back and report its link and
verification.

**Approval status:** Proposed; not implemented.

### 2. Add standalone source-readiness mode to `dag-failure-triage`

**Evidence:** Fourteen tasks concerned PubMatic, Magnite, or Amazon Publisher
completeness/readiness. Several source-layer answers required follow-ups asking
whether the missing hours reached marts or had been backfilled.

**Benefit:** A single request could trace source, landing, ingestion, warehouse,
and mart coverage without stopping after the first layer.

**Draft:** When no Slack alert is involved, derive expected coverage from code and
configuration, check each applicable layer, report expected/present/missing
partitions, distinguish unknown from complete, and save a compact coverage ledger.
Remain read-only and do not rerun jobs or modify Slack.

**Approval status:** Proposed; not implemented.

### 3. Create a cross-repository data-integration skill

**Evidence:** Six recent tasks spanned Curator, Conductor, Airflow, and dbt. One
PubMatic workflow needed a later realization that Conductor required an update.
A Celtra request began in Conductor before identifying
`curator/taskmaster/specs.yaml` as the canonical source whose generated
configuration Conductor consumes.

**Benefit:** Establishes ownership and verification across the integration
lifecycle before editing a generated artifact, choosing PR boundaries, or omitting
a downstream step.

**Draft:** Create `data-integration-change`. Map source API/storage, Curator
specification, generated configuration, Conductor, Airflow, warehouse landing,
and dbt marts; identify canonical versus generated artifacts; propose repository
and PR boundaries; separate schema, scheduling, and modeling work; and verify
generation, compile/lint, DAG visibility, source landing, ingestion, and marts.

**Approval status:** Proposed; not implemented.

## Working-tree observations

At audit time, four repositories had uncommitted state: four untracked Conductor
YAML files, one untracked Curator YAML file, one modified dataops dbt model, and a
`.DS_Store` in Looker. The audit made no ownership or cleanup assumptions.

## Change from prior audits

The strongest change was that several earlier correction patterns had already
been incorporated into source-controlled skills and global routing rules. The
audit therefore avoided recommending duplicate fixes.

## Decisions and follow-up

- Andy chose a split architecture on 2026-10-26: Moon owns the reusable audit
  skill and canonical schedule prompt; Thunder owns dated reports and decisions.
- The `codex-workflow-audit` skill and this report history were created on
  2026-10-26.
- The intended recurring schedule remains Friday at 3:00 PM America/Detroit.
  It was not enabled because automation-management tools were unavailable in the
  managed chat where creation was attempted.
- The three workflow-improvement proposals above remain unapproved.

## Limitations

The audit included an inclusive October 9–23 evidence window and reported it as
the requested 14-day lookback. Future runs should calculate the exact preceding
14-day boundary at runtime and record it explicitly.

No audited project files, external systems, plugins, skills, or automations were
changed during the original audit.
