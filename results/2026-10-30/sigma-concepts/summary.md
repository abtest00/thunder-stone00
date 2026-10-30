# Sigma structure: connections, workspaces, data models, workbooks, and reports

Sigma organizes work around **connections**, **documents**, and **workspaces**. A connection points to a data platform; workspaces organize access/content; documents include workbooks, reports, and data models. [Sigma fundamentals](https://quickstarts.sigmacomputing.com/guide/fundamentals_1_getting_around_v3/index.html)

| Concept | Role | Use it when |
| --- | --- | --- |
| Connection | Credentialed link to BigQuery/Snowflake/etc. | An admin sets governed data-platform access. |
| Workspace | Content/access boundary | A team needs shared discovery, permissioning, and organization. |
| Data model | Reusable governed semantic layer | Multiple workbooks need the same sources, joins, metrics, descriptions, or row/column rules. |
| Workbook | Interactive analysis/dashboard/app canvas | A user explores data, builds pages/elements, controls, and visualizations. |
| Report | Distributable formatted document | A polished, presentation-like output is needed. |

Data models are the important shift: Sigma says they centralize reusable data sources, relationships, and metrics without modifying raw data; other workbooks and data models can use them as sources. Legacy datasets are deprecated—new/edited dataset behavior ended in 2026, and they can no longer be used as a data source after September 15, 2026. [Sigma data-model documentation](https://help.sigmacomputing.com/docs/create-and-manage-data-models)

## A useful operating pattern

`BigQuery curated marts → Sigma connection → governed data model → many workbooks → reports/distribution`

Keep joins and metrics in the data model when they must be consistent/reused. Keep workbook calculations local when they are exploratory or specific to one decision. Promote repeated workbook logic into the data model only after its grain, ownership, and definition are stable.

For RAP, the clearest first semantic surface is a data model over curated marts with approved metrics, descriptions, default time handling, and tested relationships. Workbooks should be the consumption layer—not the place where every team independently redefines revenue.
