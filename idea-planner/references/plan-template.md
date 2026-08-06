# Idea Plan Output Template

Adapt sections to the idea. Keep the executive portion concise and make detailed
tasks independently executable.

## 1. Verdict

- Decision: Proceed | Proceed as experiment | Proceed as learning/portfolio |
  Pivot | Stop
- Confidence: High | Medium | Low
- Reason: one short paragraph
- Strongest evidence:
- Largest uncertainty:
- Next decision:

## 2. Refined idea

- Primary user:
- Painful job/current alternative:
- Proposed outcome and mechanism:
- Intended outcome: business | internal | learning | portfolio | open source
- Success measure:
- Constraints and assumptions:

## 3. Business-case review

Summarize each rubric dimension as `strong`, `uncertain`, or `weak`. Include the
cheapest validation for every important uncertainty and explicitly state reasons
not to build.

## 4. Duplication and improvement landscape

State search date, sources, and queries.

| Project/product | Type | Overlap | Evidence/signals | Gap or lesson | Reuse/license note |
|---|---|---|---|---|---|

Conclude whether duplication validates demand, removes the need to build, or
suggests a narrower differentiator. Label incomplete research clearly.

## 5. Technology-stack decision

| Layer/need | Supplied choice and constraint | Fit | Decision | Trade-off/mitigation |
|---|---|---|---|---|

Separate `must use`, `prefer/reuse`, `want to learn`, and `open` technologies.
Call out any technology included mainly for learning rather than product need.
For current price, license, quota, or support claims, cite an official source and
access date. When live verification is unavailable, use budget ceilings and
unknown placeholders instead of remembered vendor prices.

## 6. Scope and critical components

### MVP in scope

- Primary journey:
- Capabilities:
- Acceptance criteria:

### Explicitly out of scope

-

### Component sweep

| Component | MVP-critical | Production-critical | Decision/owner |
|---|---|---|---|

### Validation checkpoint

Ask the user to confirm the scope and verdict before detailed planning unless a
one-shot plan was requested.

## 7. Architecture

Describe the smallest coherent system. Include a compact flow or component
diagram only when it materially clarifies relationships. Cover data ownership,
trust boundaries, integrations, and failure paths.

## 8. Implementation roadmap

### Phase 0 — Validate

- Hypothesis:
- Cheapest test:
- Evidence threshold:
- Stop/pivot condition:

### Phase 1 — Proof of concept

- Deliverable:
- Ordered tasks:
- Tests/acceptance:
- Risks/dependencies:
- Decision gate:

### Phase 2 — MVP

- Deliverable:
- Ordered tasks:
- Tests/acceptance:
- Risks/dependencies:
- Decision gate:

### Phase 3 — Production hardening, if justified

- Security/privacy:
- Reliability/observability:
- Performance/cost:
- Operations/support:
- Release/migration:

## 9. Tool and MCP map

| Job | Recommended available tool | Why | Access/approval needed | Optional fallback |
|---|---|---|---|---|

Consider repository/code search, browser research, design, database, deployment,
analytics, observability, project tracking, and communications only when
relevant. Distinguish installed/callable tools from optional suggestions.

## 10. Immediate next actions

List the next user decision and the first one to three executable actions. Do not
begin costly implementation before the key validation gate is satisfied.
