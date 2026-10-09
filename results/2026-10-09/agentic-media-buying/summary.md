# Agentic Media Buying

## Short Answer

Agentic media buying is the shift from human-operated campaign setup and optimization toward AI agents that interpret briefs, discover inventory or audiences, propose plans, negotiate or create buys, execute within constraints, and optimize against outcomes. The 2026 market signal is that this has moved beyond demos: PubMatic reports production campaigns, IAB Tech Lab is standardizing agentic advertising workflows through AAMP, and publisher-side systems such as Hearst's AURA IQ are using agentic planning to turn RFPs and first-party data into media recommendations.

## Hearst Signal

The relevant Hearst thread appears to be AURA IQ and related Optable work, not a generic "AI media buying" announcement. Optable describes Hearst and Optable collaborating to organize and taxonomize engagement across Hearst websites so advertiser goals can map to targetable audiences. In that account, Jessica Hogue, Hearst's chief data officer for consumer media, says RFP analysis and custom audience creation have historically been slow and manual, and the new agentic planner removes handoffs. Source: [Optable newsroom](https://www.optable.co/newsroom).

The core product pattern is seller-side intelligence:

- Read an RFP or campaign goal.
- Use first-party behavioral, editorial, and engagement data.
- Generate richer audience recommendations than keyword-only human workflows.
- Compress planning time from hours to minutes.
- Make the publisher better prepared for buyer agents asking structured questions.

This matters because it pushes planning intelligence closer to the publisher. If agencies or brands increasingly use buyer agents, publishers need seller agents or agent-readable planning systems that can answer with inventory, audiences, constraints, pricing, and measurement logic.

## Market Map

Protocol layer:

- IAB Tech Lab's AAMP initiative is an umbrella for bringing agentic AI into advertising workflows. Its examples include buyer and seller agent SDKs, media-plan creation from a brief, seller negotiation, transaction confirmation, and pushing to Google Ad Manager. Source: [IAB Tech Lab AAMP](https://iabtechlab.com/standards/aamp-agentic-advertising-management-protocols/).
- AdCP is a separate open protocol from AgenticAdvertising.org. It describes standardized agent collaboration across product discovery, media buying, creative generation, audience activation, and brand governance, and explicitly says AdCP and OpenRTB operate at different layers. Source: [AdCP FAQ](https://github.com/adcontextprotocol/adcp/blob/main/docs/faq.mdx).

Execution/platform layer:

- PubMatic launched AgenticOS for agent-to-agent advertising. Its launch release says an early December 2025 campaign used natural-language input through Claude, with AgenticOS recommending tactics, executing the buy, and optimizing in real time within predefined parameters. Source: [PubMatic AgenticOS launch](https://pubmaticinc.gcs-web.com/news-releases/news-release-details/pubmatic-launches-agenticos-operating-system-agent-agent).
- PubMatic's Q2 2026 results say AgenticOS had run more than 80 fully autonomous end-to-end campaigns globally, up from more than 30 the prior quarter, and had transacted more than 4,000 AI-powered deals. Source: [PubMatic Q2 2026 results](https://pubmaticinc.gcs-web.com/news-releases/news-release-details/pubmatic-announces-second-quarter-2026-financial-results).

Publisher/seller layer:

- Hearst's AURA IQ / Optable story is less about a buyer agent spending money autonomously and more about using agentic planning to respond to RFPs, build better audiences, and prepare for interoperable buyer-seller agent workflows. Source: [Optable newsroom](https://www.optable.co/newsroom).

## Implications For Revenue Analytics Platform

Agentic media buying increases the value of machine-readable commercial truth. The platform advantage will likely come from clean product catalogs, audience definitions, inventory availability, forecast confidence, pricing rules, measurement metadata, and guardrail-ready approval/audit trails.

Likely RAPLAT-adjacent opportunities:

1. Product and audience catalog quality: agents need structured, current, queryable definitions.
2. Forecasting and availability APIs: buyer/seller agents will need fast answers about reach, inventory, pacing, and constraints.
3. Measurement contracts: outcomes, attribution windows, deduping, and incrementality claims need standardized fields.
4. Governance and auditability: autonomous execution needs approvals, limits, and logs.
5. Semantic RFP intake: parse goals, verticals, audiences, KPIs, budget, dates, geography, brand safety, and creative constraints into a normalized planning object.

## Takeaways

- "Agentic" in this space is not just campaign optimization; it is the full workflow wrapper around planning, discovery, negotiation, activation, measurement, and governance.
- Hearst's public signal is especially relevant because it uses publisher first-party data and RFP planning, which is close to revenue analytics and sales enablement.
- Standards are unsettled: IAB Tech Lab AAMP and AdCP are adjacent but separately governed. That creates near-term integration ambiguity.
- Production claims exist, especially from PubMatic, but they should be read carefully as vendor-reported case evidence.
- For RAPLAT, the best strategic bet is probably not to build a fully autonomous buyer, but to make commercial data agent-ready: canonical, governed, explainable, and accessible through APIs or MCP-like interfaces.

