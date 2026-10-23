# Testing Sigma with a semantic layer

Sigma’s reusable **Data Models** are its native semantic-layer surface: they centralize reusable data sources, relationships, and metrics without changing raw data. Sigma documents that models improve governed self-service and that semantic descriptions, relationships, default timelines, and metrics improve Assistant/MCP accuracy. [Sigma data models](https://help.sigmacomputing.com/docs/get-started-with-data-modeling) · [Sigma modeling best practices](https://help.sigmacomputing.com/docs/data-modeling-best-practices)

## Recommended RAP pilot

Choose one decision domain—not a company-wide metric program—such as campaign delivery/pacing or advertising revenue. Publish a curated mart as the base data source, then define:

- canonical dimensions and grain;
- 5–10 owner-approved metrics with descriptions and default time behavior;
- relationships only where keys and join cardinality are understood;
- access rules separating broad analysis from sensitive fields;
- three representative workbooks and ten acceptance questions.

Measure: whether users obtain the approved metric without bespoke SQL, number of metric-definition disputes, query cost/latency, join errors, and Assistant/MCP answer quality with citations to the data model.

This sequencing matches existing RAP guidance: contract-shaped metadata, tests, stable curated marts, and ownership create the “spine” for a thin semantic layer; expose staging to broad users only as an exception. Related local reference: `../abtest00/work/projects/data-contracts/data-contracts-validation.md`.

## Scope guardrail

Do not attempt to make Sigma a replacement for dbt contracts, curated marts, or a cross-company semantic standard. First prove that a bounded Sigma data model reduces rework and creates trustworthy self-service; then decide whether its definitions should be synchronized with dbt/Looker or managed elsewhere.
