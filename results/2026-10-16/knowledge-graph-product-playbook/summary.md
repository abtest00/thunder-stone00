# Turning a product playbook into a knowledge graph

A product playbook becomes more useful as a graph when it stops being a single document and becomes a **governed set of entities, relationships, evidence, and decisions**. Start with one revenue/product use case—such as “which audience and measurement approach should support this advertiser objective?”—instead of attempting an enterprise-wide ontology.

## Recommended graph shape

`Product → Capability → Use case → Customer segment → KPI → Measurement method → Data asset → Owner → Decision → Evidence → Constraint`

Add a source URL/path, owner, effective date, confidence, sensitivity, and review cadence to every decision-grade node. Graphs add connected context; knowledge graphs add meaning; context graphs focus that meaning on what matters for a particular task or agent. [Neo4j’s comparison](https://neo4j.com/blog/agentic-ai/context-graph-vs-knowledge-graph/) is a useful concise framing.

For RAP, an MVP could model ad products, eligible inventory, targeting/measurement capabilities, standard packages, policy constraints, source-of-truth dashboards, and the people who own each. A user or agent could then ask: “What premium-display package fits a retail advertiser seeking incremental reach, what evidence supports it, and who must approve exceptions?” The response should traverse approved relationships and cite the underlying playbook material—not improvise policy.

## Build in four iterations

1. **Normalize the playbook.** Split durable facts from narrative; identify canonical IDs and owners. Do not embed every paragraph first.
2. **Publish a small schema.** Define each entity, allowed relationships, source systems, access rules, and freshness SLA. Treat metrics and definitions as first-class nodes.
3. **Ingest with provenance.** Keep original documents and link every extracted assertion back to its source, section, and review date. Entity resolution and relationship creation should be reviewable.
4. **Serve bounded questions.** Start with search, recommendation, and agent-context retrieval. Evaluate correct entities, citations, permission adherence, freshness, and decision outcomes before adding automated actions.

Google’s current enterprise Knowledge Graph documentation illustrates practical fundamentals: linking people, content, and interactions improves entity recognition and contextual retrieval; it also applies ACL checks so users see only authorized entities. [Google Cloud documentation](https://docs.cloud.google.com/gemini/enterprise/docs/use-knowledge-graph-search?hl=en)

## Avoid two traps

- A graph is not a replacement for a controlled source of truth: stale content, unclear ownership, and access errors simply become more connected.
- Do not begin with a graph database purchase. The first deliverable is a tested semantic contract and a narrow question set with measurable quality.

## Suggested next step

Select one existing product playbook and inventory 20–40 entities plus their source links. Run three real seller/analyst questions against it, then decide whether a graph layer improves outcomes beyond well-structured documents and conventional retrieval.
