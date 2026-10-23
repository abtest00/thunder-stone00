# Tracing Sigma dashboards to BigQuery jobs

**Short answer:** BigQuery supports job labels, but Sigma’s public documentation does not promise that it passes a workbook/dashboard identifier as a BigQuery job label. Treat that as unverified until tested in the actual connection. Sigma does provide per-session workbook/data-model Query History, including generated SQL, element name, and a Sigma request ID; BigQuery exposes query principal, job labels, query text, bytes billed, and slot usage. [Sigma Query History](https://help.sigmacomputing.com/docs/examine-workbook-queries) · [BigQuery job labels](https://docs.cloud.google.com/bigquery/docs/viewing-labels)

## What to test

1. Open one known Sigma workbook and refresh one distinct element.
2. In Sigma, capture its Query History: workbook URL, element name, timestamp, generated SQL, and request ID.
3. In the BigQuery execution project, inspect `region-us.INFORMATION_SCHEMA.JOBS_BY_PROJECT` over that minute for the Sigma service-account principal, query text, and `labels`.
4. Compare repeat runs from two different workbooks. If labels are absent or identical, they cannot provide workbook-level attribution.

```sql
SELECT creation_time, job_id, user_email, labels, total_bytes_billed, query
FROM `EXECUTION_PROJECT`.`region-us`.INFORMATION_SCHEMA.JOBS_BY_PROJECT
WHERE creation_time >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY)
  AND statement_type = 'SELECT'
ORDER BY creation_time DESC;
```

BigQuery labels must be supplied when the job is submitted; they cannot be added after a job is running or complete. They are included in billing data. [Google Cloud job submission](https://docs.cloud.google.com/bigquery/docs/running-jobs?hl=en)

## Recommendation

Use a two-layer approach: (1) Sigma Query History for human/support tracing to a workbook element, and (2) BigQuery job telemetry for cost/trend attribution. If Sigma does not emit a document identifier in labels or SQL comments, ask Sigma Support whether the connection supports a query tag, then retain a mapping of Sigma request IDs and job IDs for sampled investigations. Do not infer a dashboard from query text alone—Sigma optimizes and can cache/generated SQL differently.
