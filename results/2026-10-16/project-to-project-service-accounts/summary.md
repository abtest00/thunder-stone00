# Project-to-project service accounts in GCP

A service account belongs to one “home” project but can be granted narrowly scoped access to resources in other projects. Create it where the workload runs and where its lifecycle/billing ownership belongs; grant resource access in the target projects. Do not create a duplicate account in every data project merely because it reads there.

For a RAP workload, the default pattern is:

- **Identity/execution project:** owns `raplat-<workload>-<env>` and holds `bigquery.jobUser` for jobs billed there.
- **Data projects:** grant that service-account principal only the dataset/table/view permissions it needs.
- **Orchestration/runtime:** attach or impersonate that identity using short-lived credentials, rather than distributing keys.

For governed reads, prefer source tables → authorized views in a consumption project → workload identity. This lets the account read curated interfaces without direct access to restricted source tables. [BigQuery authorized views](https://docs.cloud.google.com/bigquery/docs/authorized-views?hl=en)

## Guardrails

- Grant roles at the lowest useful resource level; Google specifically warns against broad project/folder-level ability to use or impersonate service accounts.
- Separate runtime permission from admin permission. A pipeline may run as an account without being allowed to alter its IAM policy or mint keys.
- Use names that expose owner, workload, and environment; keep a registry and periodic access review.
- If using Workload Identity Federation or service-account impersonation, scope who may impersonate each account individually.

Google’s IAM guidance explains why: a person who can impersonate a more-privileged account can inherit all of that account’s cross-project access, and project-level token-creator grants can be overly broad. [Service-account best practices](https://docs.cloud.google.com/iam/docs/best-practices-service-accounts)
