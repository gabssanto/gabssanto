# From Manual Operations to an AI-Powered B2B Platform

A sanitized case study on turning spreadsheet-heavy operations into a production product platform while supporting company growth.

## Summary

I joined an early-stage B2B company as its sole engineer and technical lead.

The business had strong operational knowledge and customer demand, but much of the execution still depended on spreadsheets, manual coordination, disconnected scripts, and service-heavy workflows.

My role was not limited to implementing features. I owned the technical transformation end to end: product architecture, backend and frontend systems, AI workflows, cloud infrastructure, integrations, security, QA, and delivery.

The resulting platform helped support growth from approximately **5 customers when I joined to 53 cumulative customers served**, without first building a traditional engineering organization.

## The starting point

The company had already validated a real customer problem. The next challenge was making delivery repeatable.

Operational knowledge existed across people, spreadsheets, scripts, and provider dashboards. This created several constraints:

- Important workflows required manual coordination
- Customer delivery was difficult to standardize
- Internal knowledge was not encoded into reusable product behavior
- Data moved between tools without consistent contracts
- Long-running tasks were difficult to observe and recover
- Product improvements competed with daily operational work
- Scaling service delivery risked requiring proportional headcount growth

The goal was to preserve the team's domain expertise while turning repeatable parts of the operation into software.

## Transformation strategy

The platform evolved incrementally rather than through a single rewrite.

```text
Manual operations and spreadsheets
                ↓
Structured internal workflows
                ↓
Shared data and service contracts
                ↓
AI-assisted automation and review
                ↓
Customer-facing product capabilities
```

Each stage reduced operational dependence while keeping the business usable during the transition.

### Productize workflows, not screenshots

The first step was understanding how operators actually completed the work:

- Which decisions were deterministic?
- Which steps required contextual judgment?
- Where did data enter and leave the process?
- Which exceptions were common enough to design for?
- Which outputs did customers and operators need to trust?

The software was designed around those decisions and state transitions rather than around a visual copy of the existing spreadsheets.

### Introduce service boundaries deliberately

Different workloads had different runtime and scaling needs.

The platform grew into a multi-service architecture using:

- Rails for core product and business workflows
- Python for AI, data processing, and automation
- Go for focused backend services
- Next.js and React for product interfaces
- PostgreSQL as the shared operational data foundation
- Google Cloud, Cloud Run, and Cloud SQL for production infrastructure

Services were separated when ownership, runtime behavior, or deployment needs justified the boundary—not simply to maximize the number of technologies.

### Keep operators in control

Automation was designed to support operational judgment rather than hide it.

The platform introduced:

- Structured reports and review queues
- Human approval for ambiguous or consequential changes
- Confidence and policy gates
- Retryable background processing
- Operator-visible status and failure information
- Customer-scoped controls and permissions

This allowed more work to be automated without turning the system into an opaque black box.

### Build reusable product capabilities

Internal workflows gradually became platform features:

- AI-assisted data hygiene and enrichment
- Database-quality analysis
- Customer and campaign configuration
- Multi-provider integrations
- Deliverability and operational automation
- A Unified Inbox with categorization and reply workflows
- Customer-facing interfaces backed by the same operational systems

The important shift was from one-off execution to reusable product behavior.

## Technical leadership

As the sole engineer, I worked across both strategy and implementation:

- Converted founder and operator knowledge into a technical roadmap
- Chose where to buy, integrate, automate, or build
- Designed architecture and data contracts
- Implemented backend, frontend, AI, and infrastructure changes
- Established testing, observability, security, and release practices
- Supported customer-facing execution and production incidents
- Balanced immediate operational needs with long-term platform integrity

This required optimizing for leverage rather than building every possible abstraction upfront.

## Selected outcomes

The platform and automation work helped support:

- Growth from approximately **5 customers at join to 53 cumulative customers served**
- **5× operational growth** without proportional engineering headcount
- More than **900 customer meetings in 2025**
- A **21× reduction** in a core processing workflow
- A **40% reduction** in cloud operating costs
- Production AI workflows operating across hundreds of thousands of rows
- A 12-agent data-quality system scanning more than 2.8 million records

These results came from product, operational, and commercial work across the company. My contribution was building and owning the technical systems that made the growth supportable.

## What I learned

### Start with operational reality

The best architecture starts with how work is actually performed, including exceptions and failure cases.

### Productization is a sequence

Moving from services to software does not require freezing the business for a complete rewrite. Each reusable workflow can become a product boundary incrementally.

### Technical leverage matters more than system count

A small team benefits from strong defaults, observable workflows, and carefully chosen service boundaries more than from architectural complexity.

### AI needs surrounding product infrastructure

The model is only one component. Review interfaces, data contracts, retries, evals, observability, and operator control determine whether an AI workflow is useful in production.

### Senior ownership includes business context

Architecture decisions improve when the engineer understands customer delivery, operational constraints, and the company's current stage—not only the codebase.

## Work with me

I help early-stage B2B companies turn manual operations into reliable software and production AI systems.

[Tell me what you are building](mailto:espiritosanto.gabriel@gmail.com?subject=Consulting%20inquiry&body=Company%3A%0AWhat%20are%20you%20trying%20to%20build%20or%20improve%3F%0ACurrent%20bottleneck%3A%0ATimeline%3A) or [connect with me on LinkedIn](https://www.linkedin.com/in/gabesanto).

## More case studies

- [Building production AI agents for complex B2B data workflows](./production-ai-agents-for-data-workflows.md)
- [Making a critical workflow 21× faster while reducing cloud costs](./workflow-performance-and-cloud-cost-optimization.md)
