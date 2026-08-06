# Idea Evaluation Rubric

Use this rubric to structure judgment, not to manufacture numeric certainty.
Rate each dimension `strong`, `uncertain`, or `weak`, cite the evidence, and name
the cheapest way to resolve uncertainty.

## Business coherence

| Dimension | Strong signal | Warning signal |
|---|---|---|
| User | Specific reachable persona | “Everyone” or multiple unrelated personas |
| Problem | Frequent, costly, urgent, or mandated job | Mild inconvenience or technology-first premise |
| Alternative | Known workaround with visible cost | No evidence users try to solve it |
| Outcome | Observable time, money, risk, quality, or access gain | Vague convenience or novelty |
| Adoption | Fits an existing workflow or has a credible change path | Requires several parties to change at once |
| Distribution | Plausible route to initial users | “Build it and they will come” |
| Value exchange | Credible payment, sponsorship, internal savings, or learning value | No beneficiary willing to fund or maintain it |
| Timing | New constraint, capability, regulation, behavior, or cost shift | No reason to switch now |
| Advantage | Better niche, workflow, data, integration, trust, cost, or distribution | Only “uses AI/blockchain/latest framework” |
| Feasibility | Critical inputs and skills are obtainable within constraints | Depends on unavailable data, rights, or integrations |

## Critical-component sweep

Check only applicable items, but explain every omitted critical item:

- user discovery and acquisition;
- onboarding, identity, roles, and permissions;
- primary workflow and failure/recovery path;
- data sources, ownership, consent, retention, deletion, and quality;
- external APIs, quotas, reliability, and fallback behavior;
- payments, billing, entitlement, or internal chargeback;
- abuse prevention, secrets, auditability, and threat model;
- privacy, accessibility, compliance, and jurisdiction;
- support, moderation, content policy, and dispute handling;
- analytics, success measures, experiment design, and feedback;
- deployment, observability, backup, recovery, and ongoing ownership;
- migration/import/export and exit path;
- licensing and lawful reuse of code, content, models, and datasets.

Distinguish `MVP-critical`, `production-critical`, and `not applicable`. Do not
inflate the MVP with production-hardening work when a manual or reversible test
can answer the main hypothesis.

## Sanity tests

Ask:

1. What costly behavior occurs today without this product?
2. Why would the target user switch from the current alternative?
3. Can the core value be tested manually or with a thin prototype?
4. What observation would cause the user to stop or pivot?
5. Is the proposed buyer also the beneficiary? If not, what aligns them?
6. Does seasonality, frequency, geography, regulation, or timing undermine the
   case—such as selling a low-need product in the wrong season?
7. Is the difficult part software, data access, behavior change, distribution,
   trust, or operations?
8. Would a service, workflow change, spreadsheet, existing product, or plugin
   solve the problem more cheaply?

## Verdict guidance

- Choose `Proceed` only when the problem, user, validation path, and feasible
  differentiator are coherent.
- Choose `Proceed as experiment` when a cheap test can resolve the largest
  uncertainty.
- Choose `Proceed as learning/portfolio` when the build has explicit learning or
  evidence value despite weak commercial demand.
- Choose `Pivot` when evidence favors a nearby persona, problem, scope, or
  delivery model.
- Choose `Stop` when critical dependencies are unavailable or the value path is
  implausible under the constraints.
