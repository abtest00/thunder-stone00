# Traceable GCP service-account costs

Create service accounts by **workload and environment**, not by person or generic team: for example `raplat-dbt-prod`, `raplat-composer-prod`, and `raplat-sigma-prod`. Give each a clearly named execution project, dataset-level access, an owner, a purpose, and a review date. This makes BigQuery workload attribution practical without granting excessive privileges.

BigQuery’s `INFORMATION_SCHEMA.JOBS` includes `user_email` (which can be a service account), `project_id`, job labels, bytes billed, and slot milliseconds; it retains 180 days of history. Use it as the operational attribution source, joined to a service-account registry and billing export. [Google Cloud JOBS reference](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs?hl=en)

## Minimal operating model

1. **One account per production workload/environment.** No shared human-owned accounts.
2. **One explicit execution project per spend boundary.** Give `bigquery.jobUser` only there; this makes job-level project attribution meaningful.
3. **A small registry** in source control: account email, workload, owner team, execution project, data domains, run surface, environment, approver, expiry/review date.
4. **Job labels where the client permits them** (`workload`, `team`, `environment`, `cost_center`, `pipeline`). Treat them as supplemental—not a substitute for distinct identities.
5. **Monthly review:** new principals, unusual bytes/slot use, accounts with no jobs, keys, over-broad roles, and unowned accounts.

Avoid key files where possible. Google recommends temporary/attached credentials or federation over service-account keys, individual management of service-account access, and least privilege; impersonation or key creation can become privilege escalation. [Google Cloud service-account best practices](https://docs.cloud.google.com/iam/docs/best-practices-service-accounts)

This directly supports RAP’s stated need for clean access boundaries and billing visibility, and follows the local observation that Sigma jobs are attributed to the project selected for its BigQuery connection. Related internal context: `../abtest00/work/projects/sigma-governance/service-accounts.md`.
