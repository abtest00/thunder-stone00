# Notes

## Article Facts

- Published by Google Cloud on June 15, 2026.
- Authors: Mikul Bhatt, Director of Engineering at Yahoo; Bei Li, Sr. Staff Software Engineer.
- The case study says Yahoo partnered with Google Cloud to build Seller Agent, a digital media buying platform.
- The article frames the change as a shift from "systems of intelligence" to "systems of action."
- Seller Agent is described as compressing multi-week manual media buying processes into governed live campaigns executable in seconds.
- The system uses a planning supervisor agent on GKE, orchestrated with Google's Agent Development Kit.
- The supervisor decomposes buyer requests into specialist tasks:
  - inventory discovery
  - audience matching
  - forecasting
  - pricing analysis
  - package recommendation
  - governance review
  - execution
- Agents coordinate through Agent2Agent.
- Gemini Enterprise Agent Platform hosts models for embeddings, forecasting, and graph learnings.
- Buyer briefs are submitted over Ad Context Protocol.

## Dual-Graph Pattern

Knowledge graph:

- Built on Spanner Graph.
- Represents operational commercial reality.
- Includes products, placements, audiences, inventory, contracts, and governance controls.
- Policies are versioned relationships.
- Used during active campaign evaluation and execution.

Context graph:

- Built on BigQuery Graph.
- Captures decision lineage and operational traces.
- Uses BigQuery Agent Analytics plugin / SDK according to the case study.
- Includes decision points, candidate packages, scores, policy evaluations, delegations, and execution outcomes.
- Supports audit questions such as why a package was selected and which policies influenced it.

## RAPLAT Translation

Commercial ontology candidates:

- Advertiser
- Agency
- Campaign brief
- Product
- Placement
- Package
- Inventory pool
- Audience segment
- Forecast
- Price/rate card
- Contract
- Policy
- Approval
- Measurement contract
- Outcome

Useful edge types:

- `eligible_for`
- `constrained_by`
- `priced_by`
- `forecasted_by`
- `requires_approval`
- `violates_policy`
- `approved_by`
- `selected_over`
- `executed_as`
- `measured_by`
- `resulted_in`

Potential evidence events:

- Brief received
- Candidate generated
- Candidate rejected
- Forecast attached
- Score assigned
- Policy evaluated
- Human review requested
- Human approval granted
- Execution started
- Execution completed
- Delivery signal received
- Attribution signal received

## Cautions

- This is a vendor/customer case study, so claims about speed and capabilities should be treated as directional rather than independently verified benchmarks.
- The article describes the architecture at a high level. It does not provide schema details, latency numbers, cost profile, SLA, or operational failure modes.
- "Graph" is the visible architecture pattern, but the actual value depends on ontology quality, data freshness, governance ownership, and operational adoption.
- The AdCP/AAMP standards landscape remains unsettled, based on the prior research.
