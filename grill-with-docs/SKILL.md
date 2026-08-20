---
name: grill-with-docs
description: Interview the user relentlessly about a plan, decision, or idea while actively building and sharpening the project's documentation hierarchy -- glossary and ADRs -- as terms and decisions crystallize. Use when the user wants to stress-test a plan against existing project documentation, resolve fuzzy terminology, cross-check claims against the actual codebase, or wants resolved decisions captured into CONTEXT.md / ADRs as they're made rather than after the fact.
---

# Grill With Docs

Interrogate a plan, decision, or idea until every branch is resolved, and write
each resolution into the project's documentation the moment it crystallizes.
This differs from a plain interview in one load-bearing way: it doesn't just
question, it **documents live**. By the end, the interview and the docs are the
same artifact.

## Operating contract

- Interview one round of questions at a time; never ask the whole tree at once.
- Update `CONTEXT.md` and write ADRs inline, during the session, not as a
  wrap-up step. A resolved term or decision gets written down before the next
  question is asked.
- Finding *facts* from the codebase or existing docs is your job, never the
  user's. Only put *decisions* to them.
- Do not touch source code. The only files this skill writes are the
  documentation hierarchy described below.

## 1. Map the design tree

Break the plan, decision, or idea into a **design tree**: every decision
branches into the decisions that hang off it.

Work the tree in **rounds**. The **frontier** is every decision whose
prerequisites are already settled -- the questions you can ask *now* without
guessing at answers you haven't heard yet. Ask the whole frontier in one round:
number each question and give your recommended answer. Then wait for the
user's answers before the next round.

Format each question like this:

```
❓ **Q1** - **<question title>**: <question body, may be multiple paragraphs,
including multiple choices>

➡️ <your recommended answer>
```

Each round the user answers reshapes the tree: settled decisions push the
frontier outward and unblock questions that depended on them. Recompute the
frontier and ask the next round. A question whose answer depends on another
question still open in this round belongs to a *later* round, not this one.

When a frontier question needs a fact from the environment (filesystem, git
history, existing docs), dispatch a sub-agent or read the file yourself; don't
ask the user for anything you could look up. Don't block the whole round on
it: a running exploration is an unsettled prerequisite, so only the questions
downstream of it wait -- ask the rest of the frontier now.

The session is done when the frontier is empty: every branch of the design
tree visited, nothing left silently assumed. Do not act on the plan itself
until the user confirms you've reached a shared understanding.

## 2. Grill against the documentation hierarchy, not just the user

Every round, cross-check the plan against what's already written down, in this
order of authority: `CLAUDE.md`/`AGENTS.md` conventions, ADRs, `CONTEXT.md`,
then the code itself. Surface contradictions as questions, not corrections:

> Your glossary defines "cancellation" as X, but you seem to mean Y here.
> Which is it?

> Your code cancels entire Orders, but you just said partial cancellation is
> possible. Which is right?

**Sharpen fuzzy language.** When the user uses a vague or overloaded term,
propose a precise canonical one and put it to them as a question rather than
silently substituting it: "You're saying 'account' -- do you mean the Customer
or the User? Those are different things."

**Stress-test with concrete scenarios.** When a domain relationship is on the
table, invent a specific edge-case scenario and ask how it resolves. This
forces precision about the boundary between concepts faster than an abstract
question does.

## 3. File structure

Most repos have a single context:

```
/
├── CONTEXT.md
├── docs/
│   └── adr/
│       ├── 0001-event-sourced-orders.md
│       └── 0002-postgres-for-write-model.md
└── src/
```

If a `CONTEXT-MAP.md` exists at the root, the repo has multiple contexts. The
map points to where each one lives:

```
/
├── CONTEXT-MAP.md
├── docs/
│   └── adr/                          ← system-wide decisions
├── src/
│   ├── ordering/
│   │   ├── CONTEXT.md
│   │   └── docs/adr/                 ← context-specific decisions
│   └── billing/
│       ├── CONTEXT.md
│       └── docs/adr/
```

Create files lazily: only when you have something to write. If no
`CONTEXT.md` exists, create one when the first term is resolved. If no
`docs/adr/` exists, create it when the first ADR is needed. When multiple
contexts exist, infer which one the current topic relates to; if unclear, ask.

## 4. Write CONTEXT.md inline

The instant a term is resolved in conversation, write it into `CONTEXT.md`.
Don't batch these up. Use [CONTEXT-FORMAT.md](references/CONTEXT-FORMAT.md).

`CONTEXT.md` is a glossary and nothing else -- totally devoid of
implementation details. Never treat it as a spec, a scratchpad, or a place to
record implementation decisions.

## 5. Offer ADRs sparingly

Only offer to create an ADR when all three are true:

1. **Hard to reverse** -- the cost of changing your mind later is meaningful.
2. **Surprising without context** -- a future reader will wonder "why did they
   do it this way?"
3. **The result of a real trade-off** -- there were genuine alternatives and
   one was picked for specific reasons.

If any of the three is missing, skip the ADR. Use
[ADR-FORMAT.md](references/ADR-FORMAT.md).

## 6. Converge

Stop when the frontier is empty. Summarize what's now written down: the
resolved glossary entries, the ADRs created, and any branch explicitly
deferred rather than answered. Ask the user to confirm the shared
understanding before treating the plan as ready to implement.
