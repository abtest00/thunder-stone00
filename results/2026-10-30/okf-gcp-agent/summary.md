# Using the RAP OKF bundle with a GCP agent

The OKF bundle is already in the right place for a controlled agent experiment: **17 validated Markdown records are published as custom `okf-bundle` entries in Google Cloud Knowledge Catalog**, but all are still marked `draft`. The recommended first path is not a new deployed agent—it is a read-only Sigma or local agent connected to the managed Knowledge Catalog MCP endpoint. [Google Knowledge Catalog remote MCP](https://docs.cloud.google.com/knowledge-catalog/docs/use-remote-mcp)

## What the pieces do

- **OKF bundle:** authored source of truth for business context, safe-use guidance, joins, caveats, ownership, and support routing.
- **Knowledge Catalog:** indexed/governed publication and discovery surface for those records and native BigQuery assets.
- **MCP server:** the managed bridge that lets an agent search/retrieve catalog context at `https://dataplex.googleapis.com/mcp`.
- **Agent:** retrieves that context, makes uncertainty visible, and answers bounded questions; it should not treat draft records as certified truth.

## Lowest-risk path

1. Keep editing and validating in `context-pi-ads-and-finance`; publish through the repeatable OKF → validate → review → publish → verify workflow.
2. Use a dedicated read-only agent identity with `roles/mcp.toolUser` and the narrowest catalog read permissions that pass testing. Google explicitly recommends separate identities for agents and supports the `dataplex.readonly` OAuth scope. [Google documentation](https://docs.cloud.google.com/knowledge-catalog/docs/use-remote-mcp)
3. Connect a local MCP-capable client or a Sigma agent to the discovery endpoint. Validate search/retrieval against `okf_demo` only.
4. Test a small answer set: product selection, grain, required filters, join guidance, freshness, and “what should I do when the rule is absent?”
5. Require citations to the catalog record and a visible `draft` warning. Do not grant warehouse write tools in this phase.

The local architecture plan already recommends this direct connector route and treats the Google ADK discovery agent as a local evaluation harness/fallback—not the first production deployment. Related plan: `../abtest00/work/projects/new-infra/knowledge-catalog-and-sigma-agent-plan.md`.
