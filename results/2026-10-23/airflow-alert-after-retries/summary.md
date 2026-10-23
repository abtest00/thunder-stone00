# Alert only after Airflow retries are exhausted

Use `retries=2` to produce **three total attempts** (the first attempt plus two retries), and attach the pager/Slack callback as `on_failure_callback`, not `on_retry_callback`. `on_retry_callback` fires whenever a task moves to retry; `on_failure_callback` fires only when the task/DAG reaches failure after retry policy has been applied. [Airflow callbacks](https://airflow.apache.org/docs/apache-airflow/stable/administration-and-deployment/logging-monitoring/callbacks.html) · [Airflow task retries](https://airflow.apache.org/docs/apache-airflow/stable/concepts/tasks.html)

```python
default_args = {
    "retries": 2,  # attempt 1 + retry 1 + retry 2 = 3 total attempts
    "retry_delay": timedelta(minutes=10),
    "on_failure_callback": slack_fail_alert,
    # do not set on_retry_callback for paging alerts
}
```

For a DAG-level alert, set the DAG’s `on_failure_callback` and avoid simultaneous task-level callbacks unless the alerting helper deliberately suppresses duplicates. The local Conductor implementation already contains `slack_fail_alert`, `slack_dag_fail_alert`, and logic to suppress task-level spam when a DAG aggregates failures (`../conductor/conductor/core/alerting.py`).

## Recommended alert policy

- **Attempt 1–2 failures:** logs/metrics only; optionally a low-noise retry notice in a non-paging channel.
- **Final failure:** send one actionable alert with DAG, task, run, attempt count, owner, and log link.
- **Permanent/non-retryable errors:** fail immediately using a retry policy or exception classification; alert once.

Airflow’s newer retry policies can classify exceptions: `RETRY` remains capped by `retries`, while `FAIL` bypasses remaining retries. This is preferable to retrying authentication/configuration errors three times. [Airflow retry policies](https://airflow.apache.org/docs/apache-airflow/stable/concepts/tasks.html)
