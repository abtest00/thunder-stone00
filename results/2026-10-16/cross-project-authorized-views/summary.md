# Cross-project authorized views with service accounts

Yes—an application/service account can query an authorized view in one BigQuery project while the view reads source data in another. The clean pattern separates three responsibilities:

| Layer | Role |
| --- | --- |
| Source project | Owns restricted base tables and authorizes the view to read them. |
| Consumption/view project | Hosts curated authorized views and grants consumers access only to those view datasets. |
| Execution/billing project | Hosts the query job and its `bigquery.jobUser` grant; this is where the job runs and is billed. |

BigQuery’s documentation explicitly says a principal needs `roles/bigquery.dataViewer` on the authorized-view dataset and `roles/bigquery.jobUser` only on the project where the query job runs—regardless of where the view is hosted. The consumer does not need IAM access to the source dataset. [Google Cloud authorized views](https://docs.cloud.google.com/bigquery/docs/authorized-views?hl=en)

## Recommended RAP pattern

1. Maintain base tables in the owning data project.
2. Host governed views in `ddm-dataops-data-mart` (or its replacement) and authorize each view against the necessary source dataset.
3. Create a workload-specific service account in the execution project (for example, `sigma-prod-query@…`), grant it dataset-level `dataViewer` only on the view dataset, and `jobUser` only in the intended execution project.
4. Configure the client/tool to submit jobs to that execution project. Verify billing with `region-us.INFORMATION_SCHEMA.JOBS_BY_PROJECT`.
5. Manage the view authorization as code; avoid mixing legacy dataset ACL changes with IAM in an unmanaged way.

## Important constraints

- Source and authorized-view datasets must be in the same region.
- If VPC Service Controls apply, ingress/egress must allow BigQuery access to both the view and source projects even though the consumer lacks source-dataset IAM.
- View changes require care: a view’s SQL and its authorization are separate controls.

This aligns with the existing RAP migration notes, which identify `ddm-dataops-data-mart` authorized views as the curated consumption boundary and caution that the query project determines billing. Related internal context: `../abtest00/work/projects/infra-migration/iam-research.md` and `access-patterns/gcp.md`.
