# Architecture Learning Lenses

Use these lenses to choose the next high-value branch. Select only those that
can change the design. Favor the causal question over the named pattern.

## Goals and constraints

- What user or business outcome makes this system worth changing?
- Which constraint is hard now, and which is only a forecast?
- What observable result defines success?

Overengineering smell: selecting architecture styles before naming the outcome
and constraints they serve.

## Boundaries and ownership

- Which capabilities change for different reasons?
- Who owns each rule and piece of data?
- Where must consistency be enforced?
- Can a module boundary provide the needed isolation before a network boundary?

Overengineering smell: splitting services around nouns, teams, or fashionable
patterns without independent scaling, ownership, security, or release needs.

## Data and consistency

- What is the source of truth for each important fact?
- Which invariants must hold, and across what boundary?
- What consistency, retention, migration, and recovery behavior is required?
- What is the simplest data model that makes invalid states difficult?

Overengineering smell: multiple databases, event copies, or synchronization
paths without a concrete need that outweighs reconciliation cost.

## Interfaces and coupling

- What contract must remain stable, for whom, and for how long?
- Which coupling is inherent to the domain and which is accidental?
- How will versioning, retries, idempotency, and partial failure work when the
  interface crosses a process boundary?

Overengineering smell: interfaces and abstraction layers that hide no volatile
decision, enforce no policy, and have only one real implementation.

## Workload and performance

- What are the measured or credibly forecast volume, latency, burst, and growth?
- Where is the current bottleneck, and how is it known?
- Can indexing, batching, bounded concurrency, or vertical scaling meet the
  requirement before introducing distribution?

Overengineering smell: caches, sharding, streaming, or autoscaling without a
budget, measurement, invalidation model, or load threshold.

## Failure and reliability

- Which failures matter to users, and what recovery time or data loss is
  acceptable?
- Which dependency failures can be retried, degraded, queued, or surfaced?
- Who detects and repairs each failure mode?

Overengineering smell: high-availability machinery whose own failure modes and
operator burden exceed the risk it mitigates.

## Security and privacy

- What are the trust boundaries, assets, actors, and abuse paths?
- Where are authentication, authorization, validation, encryption, audit, and
  deletion enforced?
- What data can be avoided, minimized, or isolated?

Overengineering smell: security products added without a threat or control
objective. Underengineering smell: postponing known access-control, privacy, or
compliance requirements as future hardening.

## Operations and delivery

- How will the team deploy, observe, debug, roll back, migrate, and support it?
- Does the team have the skills and time to own every introduced component?
- What is the smallest useful set of logs, metrics, traces, alerts, and runbooks?

Overengineering smell: adopting more operational surfaces than the team can
reliably understand and maintain.

## Change and reversibility

- Which decisions are expensive to reverse and therefore deserve attention now?
- Which decisions can wait for evidence behind a stable seam?
- What concrete event should trigger the next architectural investment?

Overengineering smell: paying permanent complexity costs today to make every
imagined future change cheap.

## Testing and validation

- Which assumption has the highest combination of uncertainty and consequence?
- What prototype, load test, failure drill, threat model, or user test can
  resolve it cheaply?
- Which architecture properties need automated enforcement?

Overengineering smell: building the complete architecture to learn whether its
premise was correct.
