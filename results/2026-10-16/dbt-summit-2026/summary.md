# What came out of dbt Summit 2026

The big theme was a unified, AI-oriented data stack after the Fivetran/dbt combination: faster transformation, state-aware execution, agent-facing context, and code-defined BI.

| Announcement | Status | Why it matters for RAP |
| --- | --- | --- |
| **dbt v2** | GA | Rust-based successor to Fusion; BigQuery adapter GA. Evaluate migration timing and package compatibility. |
| **dbt State** | GA | Selectively builds/skips/clones/defers based on changes and freshness rules; potential cost and orchestration simplification. |
| **Lake Compute** | Private Beta | Per-model DuckDB/Iceberg compute option; likely lower near-term relevance if RAP remains BigQuery-centric. |
| **dbt Wizard / Explore** | Public Preview | Agentic analytics-engineering workflows and business-user data exploration; assess governance before production use. |
| **dbt Charts** | Public Beta | Dashboards-as-code, YAML/versioned alongside models; relevant for durable metric artifacts. |
| **dbt MCP Server** | GA | Potential controlled interface for agents to access dbt context and tools. |
| **Fivetran Context Layer** | Private Beta | Directionally relevant to governed agent context; early-stage evaluation only. |

dbt Labs says dbt v2 is GA, with BigQuery among the GA adapters. It also says dbt State is GA and can reduce warehouse compute by identifying unchanged work, while Lake Compute is private beta and Wizard/Charts remain preview/beta. [Official Summit announcement](https://www.getdbt.com/blog/dbt-summit-2026-product-announcements)

## Suggested RAP follow-up order

1. Inventory current dbt version, adapters, packages, and CI assumptions; create a dbt v2 compatibility spike.
2. Test dbt State in a non-production BigQuery target with before/after job-cost telemetry.
3. Evaluate Charts only for a dashboard that benefits from semantic/version-controlled ownership.
4. Treat Wizard, MCP, and Context Layer as governed experiments: read-only first, scoped project context, no production write permissions until evaluated.
