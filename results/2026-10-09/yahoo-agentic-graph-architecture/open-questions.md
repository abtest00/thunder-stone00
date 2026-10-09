# Open Questions

- What are the minimum commercial entities and relationships RAPLAT would need to expose for a useful seller-agent knowledge graph?
- Which policies are currently buried in application logic, sales process, spreadsheets, or human judgment and would need to become policy-as-data?
- Where should decision traces live: BigQuery tables, graph-shaped BigQuery views, event logs, or a dedicated lineage/audit model?
- What is the first bounded workflow that could benefit from this architecture without requiring autonomous execution, for example RFP intake, package recommendation, or policy review?
- How should human approvals be modeled so they are reusable by agents, sales users, finance users, legal/compliance users, and auditors?
- Which identifiers are stable enough today to connect briefs, products, audiences, forecasts, contracts, proposals, campaigns, and outcomes?
- How should AdCP and IAB Tech Lab AAMP be monitored so RAPLAT does not overfit to the wrong protocol layer too early?
