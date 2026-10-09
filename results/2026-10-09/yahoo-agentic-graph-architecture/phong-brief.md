# Brief: Agentic Media Buying and Yahoo's Graph Architecture

## Summary

Agentic media buying appears to be moving from concept to early production. The market is forming around buyer and seller agents that can exchange structured campaign briefs, discover inventory and audiences, recommend packages, evaluate policy constraints, initiate governed transactions, and measure outcomes. This is not primarily about replacing ad serving. It is about automating and governing the commercial workflow around planning, buying, selling, activation, measurement, and optimization.

The most important implication for RAPLAT is that agentic buying will make machine-readable commercial truth more valuable. The strategic opportunity is less "build a fully autonomous media buyer" and more "make our product, audience, inventory, pricing, policy, forecasting, and measurement data agent-ready."

## What Is Changing

Several public signals suggest the category is becoming real:

- IAB Tech Lab is developing AAMP, an agentic advertising standards effort covering buyer and seller agent SDKs, media plan creation from a brief, seller negotiation, transaction confirmation, and downstream activation workflows. Source: [IAB Tech Lab AAMP](https://iabtechlab.com/standards/aamp-agentic-advertising-management-protocols/).
- AdCP is an open protocol for agent-to-agent advertising workflows. It is positioned as a collaboration layer for product discovery, planning, buying, selling, and measurement, distinct from real-time bidding and ad serving protocols such as OpenRTB. It's a spec, not a product. Source: [AdCP FAQ](https://github.com/adcontextprotocol/adcp/blob/main/docs/faq.mdx).
- PubMatic reports production use of AgenticOS, including autonomous campaigns and AI-powered deals. These are vendor-reported claims, but they are a meaningful market signal. Source: [PubMatic Q2 2026 results](https://pubmaticinc.gcs-web.com/news-releases/news-release-details/pubmatic-announces-second-quarter-2026-financial-results).
- Hearst and Optable show a publisher-side version of the pattern: using first-party data and agentic planning to interpret RFPs, build custom audiences, and respond faster with better recommendations. Source: [Optable newsroom](https://www.optable.co/newsroom/optables-new-agent-aims-to-ease-the-ad-planning-load-for-publishers).

## How To Think About AdCP

https://github.com/adcontextprotocol/adcp/blob/main/README.md 
https://docs.adcontextprotocol.org/dist/docs/3.2.3/intro 

AdCP should be understood as a common protocol for agentic media buying. It allows buyer-side and seller-side agents to exchange structured campaign and RFP context, discover products or inventory, evaluate fit, and collaborate on planning and transaction workflows.

AdCP is not primarily an impression-level ad-serving or auction protocol. It operates at the agent workflow layer, closer to the business conversation: intake, planning, package discovery, recommendation, governance, media-buy creation, audience activation, reporting, and measurement coordination. In classic programmatic delivery, a publisher's AdCP agent might accept a media-buy task and then use OpenRTB or another delivery system internally to execute impression-level serving.

There is an important nuance for AI-native sponsored experiences: AdCP can participate more directly in how sponsored content is surfaced, governed, and attributed inside AI assistants or conversational platforms. In that context, "serving the ad" may look less like rendering a banner through an ad server and more like generating or presenting a clearly labeled sponsored recommendation from structured brand and product data. In practical terms, AdCP gives agents a shared language for work that today often happens across RFPs, spreadsheets, email, sales planning tools, ad platforms, and manual follow-up.

## Why Yahoo Matters

Yahoo's Seller Agent case study is useful because it adds an architecture pattern behind the market language. Yahoo describes a seller-side multi-agent system where a buyer agent can submit a structured campaign brief over AdCP, after which a planning supervisor coordinates specialist agents for discovery, forecasting, pricing, governance, recommendation, and execution. Source: [Google Cloud Yahoo case study](https://cloud.google.com/blog/products/databases/graph-technologies-underpin-yahoo-system-of-action).

The core pattern is a dual-graph architecture:

- Knowledge graph: the operating truth. This models products, placements, audiences, inventory, contracts, pricing, and governance controls. The agent uses it to determine what is eligible, available, compliant, priced correctly, or requires approval.
- Context graph: the evidence trail. This records the brief, candidate packages, scores, policy evaluations, handoffs, approvals, rejected alternatives, execution events, and outcomes. The purpose is auditability, learning, and explainability.

The lesson is that trust is not just a prompt or a UX feature. For agentic commercial systems, trust has to be built into the data architecture. The agent needs governed facts before it acts and a structured trace after it acts.

## How Yahoo Surfaces and Orchestrates the Agents

One useful detail in the Yahoo case study is that Seller Agent appears to be surfaced as an agent-accessible commercial workflow, not simply as a human-facing chatbot. A buyer agent submits a structured campaign brief over AdCP, including audience, budget, geography, and business objective. That request enters Yahoo's Seller Agent through a planning supervisor agent running on Google Kubernetes Engine and orchestrated with Google's Agent Development Kit.

The supervisor then decomposes the request into specialist tasks: inventory discovery, audience matching, forecasting, pricing analysis, package recommendation, governance review, and execution. Those specialist agents coordinate through Agent2Agent, which suggests a modular workflow rather than one monolithic agent.

The execution pattern is important: the knowledge graph grounds the recommendation in eligible inventory, audience definitions, contractual availability, historical performance, pricing, and governing policies. Forecasting models score the opportunities, while a governance agent evaluates consent, brand safety, and regulatory constraints. If the recommendation falls within defined policy thresholds, it can be automatically approved and activated; otherwise, it is escalated for human review.

In parallel, the context graph records the full decision trail: every candidate considered, score assigned, policy applied, governance decision, approval, execution event, and eventual outcome signal. This makes the workflow explainable after the fact and creates training data for future recommendations.

The public case study does not provide much detail on the actual user interface, such as whether Yahoo exposes this through an advertiser portal, sales planning UI, chatbot, or internal operations tool. The stronger public signal is architectural: the agent is surfaced through structured protocol intake, coordinated through a supervisor/specialist-agent pattern, grounded in commercial data, bounded by policy thresholds, and audited through a graph-shaped evidence trail.

## RAPLAT Implications

For RAPLAT, the likely value is in becoming the agent-ready commercial substrate. That could mean investing in:

1. Canonical commercial ontology: stable IDs and typed relationships for products, placements, packages, audiences, inventory, advertisers, contracts, campaigns, forecasts, measurement definitions, and outcomes.
2. Policy-as-data: approval thresholds, consent rules, category exclusions, brand-safety rules, discounting limits, and contractual obligations represented as governed data rather than buried in code, spreadsheets, or process memory.
3. Forecast and availability services: machine-readable answers about reach, pacing, sell-through, inventory risk, confidence intervals, and alternative recommendations.
4. Semantic RFP intake: normalized extraction of audience, budget, geography, dates, KPIs, exclusions, guarantees, brand safety, creative requirements, and measurement needs.
5. Decision trace capture: durable logging of candidates considered, scores assigned, policies applied, alternatives rejected, human approvals, execution events, and outcome signals.
6. Feedback loops: connecting delivery and measurement outcomes back to the original recommendation path, creating supervised learning data for future planning.

## Practical Framing

A bounded RAPLAT-aligned workflow could look like this:

1. Parse an RFP or campaign brief into a normalized planning object.
2. Retrieve eligible products, audiences, packages, and inventory using explicit commercial relationships.
3. Attach forecasts, price guidance, margin expectations, feasibility signals, and confidence bands.
4. Apply policy checks for consent, category, contract, brand safety, pricing, and approval rules.
5. Produce a recommendation or proposal with supporting evidence.
6. Route exceptions or high-risk decisions for human review.
7. Record the full decision trace so the recommendation can be audited and improved.

This probably doesn't require autonomous execution as a first step. The first useful product could be decision support: faster RFP response, better package recommendation, clearer policy review, or more explainable sales planning.

## Bottom Line

Agentic media buying is best understood as an emerging automation layer around the commercial workflow of advertising. The winners will not just have better models; they will have better structured commercial truth, better governance, and better decision lineage. Yahoo's implementation is a useful proof point because it shows how a seller-side agent can be grounded in a knowledge graph and audited through a context graph. For RAPLAT, this points toward a concrete platform strategy: make our commercial data canonical, governed, explainable, and accessible enough for agents and humans to use the same truth.
