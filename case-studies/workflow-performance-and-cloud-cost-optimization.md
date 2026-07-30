# Making a Critical Workflow 21× Faster While Reducing Cloud Costs

A sanitized case study on performance engineering, workflow redesign, and infrastructure modernization.

## Summary

Two related modernization workstreams addressed different forms of operational drag:

- A critical processing workflow took approximately **42,000 seconds**, or **11.7 hours**, to complete
- The cloud environment carried avoidable cost and operational complexity

After profiling the workflow and redesigning its execution model, runtime fell to approximately **2,000 seconds**, or **33 minutes**—a **21× improvement**.

Infrastructure modernization reduced cloud operating costs by approximately **40%** while preserving the networking and production controls the platform required.

## The problem

The workflow had grown organically alongside the business.

At production scale, several patterns became expensive:

- Repeated work across stages
- Sequential execution where bounded concurrency was safe
- External calls and data access without sufficient reuse
- Long-running jobs with limited progress visibility
- Failure behavior that made partial retries expensive
- Infrastructure sized or organized around earlier workload assumptions

The right solution was not to rewrite everything in a faster language. It was to understand where time and money were actually being spent.

## Measurement first

Optimization began by establishing an end-to-end baseline.

```text
Total runtime
   ├── Data access
   ├── External provider latency
   ├── CPU-bound processing
   ├── Repeated calculations
   ├── Queue and scheduling delays
   └── Serialization and persistence
```

The workflow was measured as a system rather than as isolated functions.

This made it possible to distinguish:

- Work that could be removed
- Work that could be cached or reused
- Work that could run concurrently
- Work that needed a better query or data contract
- Work that needed asynchronous orchestration
- Work that was inherently dependent on an external provider

## Workflow redesign

### Remove unnecessary work

The highest-leverage optimization is often not faster execution—it is avoiding execution entirely.

Repeated reads, calculations, provider calls, and transformations were identified and removed or reused where correctness allowed.

### Introduce bounded concurrency

Independent units of work were allowed to run concurrently with explicit limits.

Concurrency was bounded to protect:

- Database connections
- External provider rate limits
- Memory usage
- Queue throughput
- Downstream services

The goal was predictable throughput, not maximum parallelism.

### Make processing resumable

Long-running work was divided into stages with explicit state.

This enabled:

- Retrying only failed units
- Preserving completed work
- Reporting progress to operators
- Isolating malformed records
- Recovering from external failures without restarting the full workflow

### Improve data access

Queries and data movement were reviewed alongside application code.

Depending on the stage, improvements included:

- Better filtering and pagination
- Reducing repeated database access
- Reusing stable intermediate results
- Moving expensive work outside request-response paths
- Writing results in controlled batches

### Preserve correctness

Performance improvements were verified against expected outputs.

Faster processing was not considered successful if it changed business behavior, skipped review gates, or made failure recovery less reliable.

## Infrastructure modernization

The cloud work focused on matching infrastructure to the real production workload.

Areas reviewed included:

- Service deployment boundaries
- Runtime sizing and scaling behavior
- Database and networking costs
- Static egress and production connectivity requirements
- Security controls and public exposure
- Observability and operational ownership

The resulting architecture used Google Cloud, Cloud Run, Cloud SQL, production networking, and controlled egress while reducing avoidable cost.

## Results

### Workflow performance

- **Before:** approximately 42,000 seconds / 11.7 hours
- **After:** approximately 2,000 seconds / 33 minutes
- **Improvement:** approximately 21× faster

### Cloud operations

- Approximately **40% lower cloud operating costs**
- Production networking and security requirements preserved
- Clearer service boundaries and deployment ownership
- Better visibility into runtime and failure behavior

The runtime and cost improvements came from separate but complementary changes. Both followed the same principle: measure the complete system, then remove unnecessary work and complexity.

## What I learned

### Profile before choosing a solution

The slowest-looking code is not always the dominant bottleneck. End-to-end measurements prevent teams from optimizing the wrong layer.

### Optimize for recovery as well as speed

A fast job that must restart from zero after one failure is not operationally efficient.

### Concurrency needs policy

Parallelism without limits simply moves the bottleneck into the database, provider, or queue.

### Infrastructure cost is an architecture signal

Cloud bills often reveal duplicated workloads, poor boundaries, unnecessary data movement, or services that no longer match current usage.

### Preserve product behavior

Performance engineering should make the same trusted workflow faster—not silently change its semantics.

## Work with me

I help teams diagnose slow critical workflows, modernize backend platforms, and reduce cloud costs without sacrificing reliability.

[Tell me what you are trying to improve](mailto:espiritosanto.gabriel@gmail.com?subject=Consulting%20inquiry&body=Company%3A%0AWhat%20are%20you%20trying%20to%20build%20or%20improve%3F%0ACurrent%20bottleneck%3A%0ATimeline%3A) or [connect with me on LinkedIn](https://www.linkedin.com/in/gabesanto).

## More case studies

- [Building production AI agents for complex B2B data workflows](./production-ai-agents-for-data-workflows.md)
- [From manual operations to an AI-powered B2B platform](./manual-operations-to-ai-powered-b2b-platform.md)
