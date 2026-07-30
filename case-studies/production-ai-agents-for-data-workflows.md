# Building Production AI Agents for Complex B2B Data Workflows

A sanitized case study on turning high-variance, data-heavy operations into reliable AI-assisted products.

## Summary

Production AI is not just an LLM call wrapped in a user interface.

The real engineering challenge is combining deterministic validation, retrieval, specialized reasoning, observability, and human review into a system that remains predictable when the data is incomplete, inconsistent, or ambiguous.

I designed and shipped AI-assisted workflows around this principle. The resulting systems process large B2B datasets, automate repetitive analysis, preserve review paths for uncertain decisions, and produce structured outputs that downstream products can trust.

## The problem

B2B operational data rarely arrives clean.

Common issues include:

- Inconsistent schemas and file formats
- Missing, duplicated, or contradictory records
- Large datasets that do not fit safely into a single model context
- External providers with different identifiers and data contracts
- Decisions that mix strict business rules with contextual judgment
- Low-confidence cases that should not become silent database writes
- Workflows that need to be inspected, retried, and improved over time

A monolithic prompt can appear effective in a demo while failing unpredictably under these conditions.

The goal was to build an operational system, not a magic trick.

## System design

The workflow is designed as a staged pipeline:

```text
Ingestion
   ↓
Deterministic validation and normalization
   ↓
Retrieval and candidate generation
   ↓
Specialized AI agents
   ↓
Confidence and policy gates
   ↓
Automatic action or human review
   ↓
Structured outputs, traces, and eval feedback
```

Each stage has a narrow responsibility, explicit inputs and outputs, and its own failure behavior.

### Deterministic validation

Rules-based checks handle decisions that should be repeatable and auditable:

- Schema and required-field validation
- Email and domain normalization
- Duplicate detection
- Database lookups and exact matches
- Business-rule enforcement
- Candidate-set validation
- Output-contract validation

This reduces the number of decisions delegated to an LLM and prevents probabilistic reasoning from replacing straightforward logic.

### Retrieval before reasoning

Agents receive relevant records, candidate matches, historical context, and policy information before making a recommendation.

Retrieval is bounded and task-specific. Large datasets are processed in batches, while the model receives only the context needed for the current decision.

### Specialized agents

Instead of one agent attempting to solve the entire workflow, focused agents handle narrow responsibilities such as:

- Record classification
- Entity and company resolution
- Data-quality analysis
- Candidate comparison
- Enrichment review
- Readiness and policy checks

A coordinating layer controls sequencing, optional steps, retries, and final output assembly.

### Confidence gates and human review

Not every result should be applied automatically.

High-confidence decisions that satisfy deterministic policy checks can continue through the workflow. Conflicting signals, weak candidates, or ambiguous model outputs are converted into reviewable proposals.

This keeps humans in control of consequential changes without forcing them to inspect every routine case.

### Structured outputs and contracts

Agent outputs use explicit schemas rather than free-form text.

Identifiers are checked against candidate sets, proposed actions are validated, and downstream systems receive stable payloads containing decisions, reasons, confidence signals, and supporting metadata.

## Reliability and observability

The system treats production reliability as part of the AI architecture:

- Retry-safe and resumable processing
- Bounded concurrency for model calls
- Per-step traces and structured run metadata
- Prompt and workflow versioning
- Error isolation so one record does not fail an entire batch
- Configurable and skippable workflow stages
- Evaluation datasets for regression testing
- Operator-visible warnings when a signal or dependency degrades
- Review queues for low-confidence proposals

Observability is used both for debugging and for measuring whether a workflow is improving over time.

## Selected production outcomes

### List-hygiene workflow

A production AI-assisted workflow turns raw lead files into validated, campaign-ready segments while recording per-run telemetry and detailed reports.

Current production telemetry:

- **96 completed runs**
- **94 runs with detailed reports**
- **293.6K rows processed**
- **150.6K usable leads produced**
- **55.1 hours saved** compared with estimated manual cleanup
- **1.1× measured efficiency lift** based on estimated manual hours versus pipeline runtime

Runs vary in size and configuration, so aggregate time saved is measured from each run's own report rather than extrapolated from a single benchmark.

### Database-quality system

A coordinated 12-agent system scans more than 2.8 million records across multiple quality dimensions.

The workflow:

- Reduced tracked data-quality issues by approximately 96%
- Improved the internal database-health score from 78% to above 95%
- Preserved review paths for ambiguous or potentially destructive changes
- Produced structured reports that operators could inspect before approval

### Large-scale entity resolution

For a backlog of approximately 62,000 contacts without a confirmed company relationship, I designed a hybrid resolver combining:

- Exact domain and URL signals
- Database co-occurrence analysis
- Fuzzy name matching
- An optional LLM candidate picker
- Confidence thresholds and review proposals

Deterministic matches remain deterministic. Conflicting or low-confidence signals are deferred instead of being forced into an answer.

## Engineering principles

### Use AI where ambiguity exists

LLMs are valuable when context and judgment matter. They are unnecessary for exact matching, validation, or deterministic policy enforcement.

### Prefer reviewable proposals over silent automation

When the system is uncertain, it should explain the uncertainty and ask for review rather than fabricate confidence.

### Design for partial failure

External APIs, database queries, and model calls will occasionally fail. A production workflow should degrade visibly, isolate the failure, and preserve retryability.

### Treat evals as product infrastructure

Evaluations are not a research exercise added after launch. They protect behavior as prompts, models, business rules, and data distributions change.

### Optimize the full workflow

Model quality is only one part of the system. Operator time, review effort, processing cost, latency, traceability, and recovery behavior all affect whether the product creates leverage.

## What this reflects

This is the kind of AI engineering I focus on:

- Decomposing complex business processes into reliable components
- Combining deterministic systems with model reasoning
- Building human review into the product
- Measuring behavior instead of trusting demos
- Shipping the surrounding platform, not just the prompt

AI agents become valuable when they stop being magic tricks and start becoming dependable operational leverage.

## Work with me

I help teams productionize AI workflows, modernize data-heavy platforms, and turn internal operations into reliable software.

[Tell me what you are building](mailto:espiritosanto.gabriel@gmail.com?subject=Consulting%20inquiry&body=Company%3A%0AWhat%20are%20you%20trying%20to%20build%20or%20improve%3F%0ACurrent%20bottleneck%3A%0ATimeline%3A) or [connect with me on LinkedIn](https://www.linkedin.com/in/gabesanto).

## More case studies

- [From manual operations to an AI-powered B2B platform](./manual-operations-to-ai-powered-b2b-platform.md)
- [Making a critical workflow 21× faster while reducing cloud costs](./workflow-performance-and-cloud-cost-optimization.md)
