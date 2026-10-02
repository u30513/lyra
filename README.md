# Lyra

**An enterprise operations hub with a chat interface.**

A team works from a single screen. Someone writes what they need done in plain
language, and the application carries it out by coordinating the tools the team
already uses: Jira, Slack, Outlook, Confluence, GitHub and others.

> Public write-up. The implementation is private.

---

## What it is, concretely

A web and desktop application with an enterprise look and feel, presenting a
chat interface or command bar as the single point of entry. Behind that
interface it connects to the company's existing ecosystem through integrations,
interprets the user's intent using integrated AI engines, and executes the
corresponding actions in the relevant tools.

It is delivered turnkey: pre-configured, contextualised and refined to fit the
client by implementation engineers, so that it is accurate from the first day
of use rather than after months of the customer tuning it themselves.

## What it is not

Positioning matters here, because every term in this space is overloaded.

- **Not an AI company.** No in-house models are developed or trained.
- **Not a communication tool, a task manager, a wiki or a mail client.**
- **Not a replacement for anything.** None of the tools the company already
  runs are displaced.

## The exact role

Lyra is the **administration and execution layer that sits above** those tools.
It integrates third-party AI engines to interpret the user's instructions, and
connects to the enterprise tools' APIs to carry out the resulting actions.

The AI is an internal component of the product, not the product itself. That
distinction drives the architecture: a language model is used for
understanding, never granted authority to act on its own.

---

## How it works

A single instruction can span several systems at once:

> 💬 *"Prepare next week's sprint with the priority tasks from the backlog,
> tell the team in the project's Slack channel, and schedule the planning
> meeting for Monday at 10:00."*

What the application does behind that one sentence:

1. **Interprets the intent** using integrated AI engines.
2. **Consults the company's persistent operational context** - teams, active
   projects, internal rules and conventions, all configured in advance.
3. **Selects the most appropriate AI engine for each microtask**, weighing
   capability against cost.
4. **Generates a structured execution plan and shows it to the user** before
   anything happens.
5. **Asks for human confirmation** on critical or write actions.
6. **Executes the actions** in the target tools through managed connectors.
7. **Records a full audit trail** of the process for the IT team.

Steps 4, 5 and 7 are the ones that make this deployable inside an
organisation. Nothing is written to a company system without a plan the user
has seen and, where it matters, explicitly approved - and everything that
happened remains reconstructable afterwards.

---

## Status

In development. The deterministic execution engine and the natural-language
understanding layer are built and under test; the configuration tooling and
managed connectors to the enterprise tools are the current focus.
