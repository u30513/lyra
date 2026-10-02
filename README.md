# Lyra

**The thesis.** A company defines its own business process once - as a
structured process definition - and from that point on, any employee can
run it reliably through plain natural language, no matter how specific that
process is to the company. If that holds, there's a product underneath it.
Everything else is secondary to proving it.

> This repository is the public write-up. The implementation is private.

## Why this, and why this way

Most "AI agent" tools let a language model decide what action to take and
then just... execute it. That's fast to build and fundamentally unreliable:
the same request can resolve two different ways on two different days, and
nobody can audit why. Lyra is built on the opposite assumption - **the LLM
is only ever allowed to understand, never to act.** Intent recognition and
slot-filling happen in the language layer; every actual decision about what
runs, in what order, under what conditions, is made by a deterministic
engine that has no model in its execution path at all. The process
definition is the contract between the two, and it's the one artifact that
isn't allowed to drift.

The reason this matters: a process that works for one company's onboarding
flow is rarely identical to another's, even when the shape of the
conversation is the same. The interesting engineering problem isn't "can an
LLM understand a request" - that's mostly solved. It's whether the same
natural-language interface can sit on top of arbitrarily different
per-tenant configurations without the reliability degrading as the
configuration space grows. That's the question the MVP is built to answer,
not assume.

## Architecture, at a glance

- **A deterministic workflow engine**, with zero runtime dependencies,
  that owns every state transition. It only executes from a validated
  "ready" state - there's no code path where a model-generated action
  reaches it directly.
- **An LLM-backed understanding layer** that does exactly one job per
  message: identify intent and fill in the slots the process needs, with
  structured output and a deterministic template for the response. It
  cannot call an action itself.
- **A process-definition schema** as the central contract - the one thing
  a Process Builder, the understanding layer, and the engine all read from,
  so a schema change is a decision that has to be justified, not a drive-by
  edit.

## Where it stands

The engine and the chat/understanding layer are built and tested (unit
tests plus a phrase-based evaluation harness targeting ≥95% reliability,
the number the MVP lives or dies by). What's next is a minimal Process
Builder - the editor that lets a company author its own process definition
without touching code - followed by real connectors (Composio and
third-party APIs) behind the engine's action-execution port.
