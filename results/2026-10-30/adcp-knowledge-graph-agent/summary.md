# AdCP and the role of a knowledge/context graph

AdCP (Advertising Context Protocol) is an open standard for agent-driven advertising automation. Its negotiation layer covers discovery, planning, commercial setup, creative preparation, audience activation, governance, and reporting; it uses MCP/A2A for planning-time tasks and a separate low-latency serve-time profile. [AdCP repository](https://github.com/adcontextprotocol/adcp) · [AgenticAdvertising.org](https://www.adcontextprotocol.org/)

## Why a graph matters

AdCP gives agents a shared **protocol**; it does not supply an individual publisher’s or buyer’s business truth. A knowledge/context graph provides the context that makes protocol calls safe and useful:

`advertiser objective → product/package → eligible inventory → audience/geo constraints → price/terms → creative rules → measurement plan → privacy/approval policy → owner → evidence`

That graph needs provenance, effective dates, access policy, confidence/status, and links to authoritative sources. It should retrieve the small relevant subgraph for each decision, rather than pasting an entire rate card or product playbook into the prompt.

## Practical RAP architecture

1. **Publish governed context:** OKF/Knowledge Catalog records describe revenue products, availability, measurement, caveats, owners, and approved usage.
2. **Model decision relationships:** connect product capabilities, inventory, audiences, terms, measurement definitions, restrictions, and approval paths. Start with one product family.
3. **Put an agent in the middle:** retrieve graph context; explain/cite it; form an AdCP planning request only when required constraints are satisfied.
4. **Keep actions gated:** discovery may be read-only; proposals require human approval; buy/activate actions require policy/authorization checks and auditable tool calls.
5. **Evaluate outcomes:** correct product selection, constraint violations, unsupported claims, citation coverage, escalation quality, and conversion/measurement results.

The core value is not “a graph because AI”: it is making product promises, data definitions, and governance constraints explicit enough that an agent can explain its recommendation and decline an unsafe request. This also fits the existing OKF direction—context and safe-use guidance first, not an attempt to make the OKF repository the permanent semantic layer.

## First proof of concept

Choose one sales-planning question, e.g. “Which approved PMP package fits this buyer’s reach/measurement constraints?” Make the agent return the candidate package, eligibility explanation, known caveats, owner, source links, and a clear `needs approval` state. Do not begin with autonomous transaction execution.
