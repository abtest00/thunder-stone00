# Yahoo Agentic Graph Architecture

## Short Answer

Yahoo's Google Cloud case study is useful because it moves "agentic media buying" from product language into architecture. The core pattern is a dual-graph system: a knowledge graph for operational truth and a context graph for decision lineage. In that design, agents do not just ask an LLM what to do; they traverse governed commercial data, evaluate policies, execute approved actions, and preserve the reasoning trail as structured evidence.

The important RAPLAT readout is that agentic revenue systems need two different data products:

- An operating graph that represents products, placements, audience segments, inventory, contracts, pricing rules, consent rules, brand-safety rules, and approval thresholds.
- An evidence graph that records briefs, candidate packages, scores, policy evaluations, handoffs, approvals, rejected alternatives, execution events, and outcomes.

That split is a strong blueprint for making commercial data agent-ready without pretending the model itself is the source of truth.

## What Yahoo Built

Yahoo built Seller Agent as a multi-agent media buying platform on Google Cloud. Buyer requests enter through a planning supervisor agent running on GKE and orchestrated with Google's Agent Development Kit. The supervisor decomposes the request into specialist tasks such as inventory discovery, audience matching, forecasting, pricing analysis, package recommendation, governance review, and execution. Agents coordinate through Agent2Agent, while Gemini Enterprise Agent Platform supports embeddings, forecasting, and graph learnings. Source: [Google Cloud Yahoo case study](https://cloud.google.com/blog/products/databases/graph-technologies-underpin-yahoo-system-of-action).

The architecture is anchored by two graph systems:

- Knowledge graph: built on Spanner Graph, used for live operational decisions. It models advertising products, placements, audience segments, inventory, contracts, and governance controls. Policies are represented as versioned relationships, so the agent can evaluate commercial eligibility and compliance in the same traversal.
- Context graph: built on BigQuery Graph, used for audit and learning. It captures every decision point, candidate package, score, policy evaluation, delegation, and execution outcome as connected evidence.

Google describes Spanner Graph as combining graph database capabilities with Spanner's scale, availability, and consistency, with an ISO GQL-compatible interface and interoperability between relational and graph models. Source: [Spanner Graph overview](https://docs.cloud.google.com/spanner/docs/graph/overview).

BigQuery Graph is positioned for large-scale graph analysis using BigQuery. It lets teams create node and edge tables from existing tables or views and use GQL to find relationships that would be awkward to express in standard SQL alone. Source: [BigQuery Graph overview](https://docs.cloud.google.com/bigquery/docs/graph-overview?hl=en).

## Why This Matters

The article's strongest idea is that "trust" is not a UX layer or a prompt instruction. It is data architecture. A media buying agent can only act safely if the facts it depends on are deterministic, current, policy-aware, and inspectable.

This is especially relevant for premium advertising because campaign planning mixes several kinds of truth:

- Commercial truth: products, packages, pricing, inventory, guarantees, contractual constraints.
- Audience truth: segment definitions, reach, overlap, taxonomy, sensitivity, consent.
- Operational truth: availability, activation path, approvals, handoffs, execution status.
- Measurement truth: KPIs, attribution windows, delivery outcomes, forecast confidence.
- Governance truth: policies, thresholds, consent requirements, brand safety, regulatory controls.

The dual-graph pattern says these truths should be queryable before action and traceable after action.

## Relationship To Prior Agentic Media Buying Research

This should be treated as an extension of the prior research in `results/2026-10-09/agentic-media-buying/`.

The prior research established that agentic media buying is moving from demos to early production signals, including PubMatic AgenticOS, IAB Tech Lab AAMP, AdCP, and Hearst/Optable publisher-side planning. This Yahoo article adds the missing architectural layer: how a seller-side agent can ground, govern, execute, and explain decisions.

AdCP matters here because Yahoo's flow starts from a buyer agent submitting a campaign brief over Ad Context Protocol. AgenticAdvertising.org describes AdCP as an open protocol for agents to discover, plan, buy, sell, and measure media across channels. Source: [AgenticAdvertising.org](https://adcontextprotocol.org/).

## RAPLAT Implications

For Revenue Analytics Platform, the likely strategic opportunity is not "build an autonomous media buyer." It is to make the commercial substrate agent-ready.

High-value platform bets:

1. Canonical commercial ontology: products, placements, packages, audiences, supply, demand, contracts, governance rules, and measurements need stable IDs and typed relationships.
2. Policy-as-data: approval thresholds, consent rules, category exclusions, brand safety, discounting limits, and contractual obligations should be represented as governed data, not hidden in application code.
3. Forecast and availability services: agents will need machine-readable answers about reach, pacing, sell-through, inventory risk, confidence intervals, and alternatives.
4. Decision trace capture: every automated recommendation should preserve the brief, candidates considered, scores, policies applied, rejected alternatives, approvals, and outcome signals.
5. Outcome feedback loops: delivery and attribution data should join back to the decisions that caused them, creating supervised learning data for future planning.
6. Human review design: automatic approval should be bounded by explicit thresholds, with escalations captured as first-class events.

## Practical Architecture Pattern

A RAPLAT-aligned version of the Yahoo pattern could look like this:

1. Normalize the brief: parse RFP/campaign goals into structured fields for audience, budget, geography, dates, KPIs, exclusions, guarantees, and measurement needs.
2. Retrieve candidates: use a product/audience/inventory graph to find eligible packages and alternatives.
3. Score candidates: attach reach, forecast, margin, performance history, confidence, and operational feasibility.
4. Apply governance: traverse policy relationships for consent, category, contractual, regulatory, and approval checks.
5. Recommend or execute: create a proposal, route for human approval, or execute under policy thresholds.
6. Record the trace: write every candidate, score, policy, approval, delegation, and outcome to an evidence graph.
7. Learn from outcomes: connect delivery and measurement signals back to the original decision path.

## Key Takeaways

- The architecture separates "acting" from "remembering": Spanner Graph supports operational decisions, while BigQuery Graph supports audit, analysis, and learning.
- The moat is not the model. It is the proprietary graph of commercial operations and the governed history of past decisions.
- Agentic buying makes data quality visible. Ambiguous product definitions, stale audience metadata, buried policies, and inconsistent measurement contracts become blockers to automation.
- For RAPLAT, graph thinking is less about buying a graph database and more about modeling commercial relationships explicitly enough for agents, humans, and auditors to share the same truth.
