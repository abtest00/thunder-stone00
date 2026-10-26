# Connecting to Sigma MCP

Sigma MCP lets Codex/other assistants search Sigma documents and data sources, query data, analyze it, and build workbooks using the user’s existing Sigma permissions. The intended setup is OAuth over HTTP. [Sigma MCP server guide](https://help.sigmacomputing.com/docs/use-sigma-mcp-server)

## Prerequisites

- A Sigma account type with **Use Sigma MCP with OAuth** enabled.
- The usual Sigma permissions for each intended action; MCP does not bypass workbook/data permissions.
- Your organization-specific MCP URL from **Sigma → Profile → Integrations → Connect Sigma to AI tools**.

## Connect it to Codex

```bash
codex mcp add sigma --url 'https://api.sigmacomputing.com/mcp/v2'
```

Complete the OAuth authorization prompt, then verify the configured server with `codex mcp list`. Sigma’s docs specify HTTP transport and OAuth authentication; use the exact organization URL, not a guessed shared endpoint. [Sigma setup details](https://help.sigmacomputing.com/docs/use-sigma-mcp-server)

Start read-only: search for a known workbook, describe a data source, and run a small approved query. Only then enable workbook creation/editing for profiles that need it. The MCP approach is appropriate for natural-language analysis and workbook building, while administration or data-model creation requires the REST API/CLI and should have tighter controls. [Sigma connection choices](https://help.sigmacomputing.com/docs/interact-with-ai-tools)

Internal governance material already proposes Sigma MCP with OAuth even for read-only profiles: `../abtest00/work/projects/sigma-governance/account-types/read-only.md`.
