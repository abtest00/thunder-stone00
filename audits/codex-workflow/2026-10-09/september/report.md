# Codex Workflow Audit — September 2026

## Run metadata

- Run date: 2026-10-09
- Run type: Manual; reconstructed from original Codex session history on 2026-10-26
- Evidence window: 2026-09-01 through 2026-09-30
- Projects: Entire Bulbasaur workspace plus the `abtest00` Obsidian vault
- Authorized evidence: Git history, local files, dotfiles, notes, targeted diffs, and results

## Executive summary

September showed repeated multi-repository data-workflow corrections. Validation
often revealed missing orchestration, date-window, source-shape, or downstream
steps after the first implementation. Existing playbooks already captured much of
the correct process, making them strong candidates for durable Codex guidance.

## Scope and coverage

Andy-authored activity was concentrated in `curator`, `dataops-dbt-bigquery`,
`ddm_pd_ffp`, `dbt-data-lake`, `conductor`, `leaf-stone00`, and `moon-stone00`.
The audit used commit clusters and targeted workflow notes rather than reading
every file and diff in full.

## Proposals

### 1. Create a Curator-to-Airflow migration skill

**Evidence:** Amazon Publisher and Celtra work required follow-up fixes for
success-marker gating, count validation, megacron scheduling, recursive copy
behavior, task order, fan-in references, and dbt source/model wiring. The local
`curator-to-airflow-migration-framework.md` already documented the repository
order and validation chain.

**Benefit:** A skill could prevent omitted cross-repository steps in a
high-blast-radius workflow and require verification before PR completion.

**Draft:** Create `curator-airflow-migration`. Require the relevant migration
framework and duck-check notes; identify affected repositories and merge order;
verify integration identity, partitions, perspectives, dependencies, generated
DAG configuration, dev DAG appearance, download, sync/add-partition, fan-in, dbt
run/test, and duck status. Keep cloud writes and PR publication behind approval.

**Approval status:** Proposed. The broader cross-repository need reappeared in
the 2026-10-23 audit and informed the later `data-integration-change` proposal.

### 2. Add lightweight data-workflow verification to AGENTS.md

**Evidence:** September fixes frequently concerned runtime verification rather
than syntax: source comparison windows, date defaults, blank bidder mappings,
correct lake sources, partition freshness, and confusion between governed views
and physical tables. Project notes also contained open questions about whether
dbt tests were actually scheduled in production rather than merely defined.

**Benefit:** A small global reminder would prompt end-to-end verification whenever
Codex changes dbt, Curator, Conductor, Airflow, or data-product context.

**Draft:** Identify the production surface, physical table/view, partition field,
and orchestration owner; verify source readiness before downstream reruns; verify
tests are actually scheduled; check physical partitions; and list checks performed
and not performed.

**Approval status:** Proposed; later guidance in specialized skills addresses
parts of this need, but no global rule was approved by this audit.

### 3. Consider a read-only data-workflow health review

**Evidence:** The Index Exchange investigation repeatedly required lineage
mapping, choke-point identification, raw-source checks, rerun ordering, and a
decision not to rerun raw ingestion when source data was already present.

**Benefit:** A read-only review could assemble failed DAGs, source presence,
partition freshness, likely rerun layer, and unresolved checks without performing
operational mutations.

**Draft:** Produce failed or stale workflows, likely choke points, source-data
presence, suggested rerun layers, checks performed, checks omitted, and open
questions. Do not react in Slack, edit Jira or Confluence, write cloud config, or
rerun jobs without approval.

**Approval status:** Deferred pending a chosen schedule and authorized sources.
The later `dag-failure-triage` skill now owns much of this workflow.

## Limitations

This report preserves the findings from the original session; it does not rerun
September queries against the repositories' current state.

No audited project files or external systems were changed during this audit.

