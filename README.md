# Context-Driven AI Development (Source Context + Prompt History)

This repository demonstrates a workflow in which **AI agents build and maintain software using curated source context and prompt history**, with humans firmly in the loop for review, verification, and governance.

The model is simple:

> **An AI agent is like a developer with anterograde amnesia.**  
> It can reason and write code, but it doesn’t reliably “remember” your system unless you give it durable memory.

In this paradigm, durable project memory lives in two first-class artifacts:

- **Source context** — versioned documentation that defines requirements, contracts, constraints, architecture, and invariants.
- **Prompt history** — the evolving dialogue that captures rationale, corrections, and decisions, which is continuously distilled back into source context.

This approach is inspired by the Medium article  
👉 **[AI Agents, Source Context, and Prompt History: A New Software Development Paradigm](https://medium.com/@cangiremir/ai-agents-source-context-and-prompt-history-a-new-software-developmenst-paradigm-56347b568733)** (5-minute read).

The article argues that modern software development is shifting from traditional **code-centric workflows** toward **knowledge-centric workflows**, where:

- Natural language and structured context are first-class artifacts.
- AI agents generate and modify code under explicit human guidance.
- Long-term project memory is preserved in versioned documents rather than ephemeral chat logs.

Together, these ideas frame a development model where intent and constraints are durable, AI agents are productive collaborators, and humans remain responsible for correctness, security, and system evolution.


## Core concepts

### Source context
Curated Markdown documents that act like a project “constitution”:
- requirements and constraints
- architectural boundaries
- module contracts and invariants
- security and operational rules
- test expectations

**Context is normative**: it states what must be true.  
It should not be a dump of implementation details.

### Prompt history
Prompt history is useful working memory, but it becomes durable only when distilled.

> Conversation is the transcript. Context is the minutes.

This repo encourages: **conversation → decision capture → context update**.

### The four-layer stack
1. **Code** — executable artifact  
2. **Source context** — normative spec (“what must be true”)  
3. **Prompt history** — rationale & corrections (“why we chose this”)  
4. **Agent** — translates (2)+(3) into (1), under review

---

## Repository structure
``` bash
/AGENTS.md
/context/
  architecture.md
  modules/
    product_context.md
    orders_context.md
    payment_context.md
    user_auth_context.md
/decisions/
  ADR-0001-context-as-constitution.md
/prompts/
  implement_feature.md
  write_tests.md
  update_context.md
```


### What each folder is for
- **AGENTS.md**: global rules and guardrails for humans + agents
- **context/**: canonical “source context” docs
- **decisions/**: optional ADRs for cross-cutting choices
- **prompts/**: reusable prompt macros for common workflows

---

## How to work in this repo (human + agent loop)

### 1) Plan
- Open an issue describing desired behavior and constraints.
- Agent proposes:
  - affected modules / files
  - API changes
  - data model changes
  - risks (security, migration, performance)
  - test plan
  - context updates needed

### 2) Review (human checkpoint)
- Confirm architecture boundaries
- Confirm security/privacy requirements
- Confirm operational constraints (retries, idempotency, logging)
- Confirm “definition of done”

### 3) Implement
- Agent writes code following:
  - `AGENTS.md` global rules
  - relevant module contexts
  - ADRs (if applicable)

### 4) Verify
- Run tests / lint / static analysis
- Human reviews code + tests
- Agent fixes issues

### 5) Update context
- Agent updates the module context file(s) touched:
  - invariants/contracts
  - workflows/state machine changes
  - edge cases discovered
  - test expectations
  - **dated changelog entry**
- Human reviews context changes too

---

## Context file template (recommended)

Every module context should follow this shape:

- **Purpose / Non-goals**
- **Public API / Contracts** (endpoints/events/schemas)
- **Core invariants** (“must always hold”)
- **Data model** (field meaning; avoid schema dumps)
- **Workflows / State machines**
- **Security & privacy constraints**
- **Operational constraints** (latency, retries, idempotency)
- **Failure modes & recovery**
- **Observability** (logs/metrics/traces)
- **Test expectations** (golden paths + edge cases)
- **Changelog** (dated, human-readable)

---

## Context governance rules

- **Decision capture:** any durable decision must be recorded in a module context or ADR.
- **Supersede, don’t delete:** mark old decisions as superseded with a date and replacement.
- **Review required:** context changes are reviewed like code changes.
- **Prefer invariants over implementation:** context states constraints/contracts, not exact code structure.

---

## Retrieval strategy (what to load for a task)

When an agent starts work, it should load:

1. `AGENTS.md` (always)
2. Relevant module context(s)
3. Adjacent interface contexts (anything you call, anything that calls you)
4. Most recent changelog entries (e.g., last 30–90 days)

If context window is tight, prioritize:
- invariants + contracts
- security rules
- recent changes

---

## Safety note: context is an attack surface

Context strongly steers agent behavior. Incorrect or malicious context can lead to insecure or noncompliant code.

Treat context like code:
- review it
- version it
- validate it when possible

**Recommended checks (optional):**
- CI validation that endpoints listed in context match OpenAPI
- schema checks for fields referenced in context
- grep-based checks for deprecated APIs mentioned in context
- security linters enforcing constraints from `AGENTS.md`

---

## Getting started

1. Create/complete `AGENTS.md`
2. Fill out `/context/architecture.md` (system map + boundaries)
3. Create a context file per major module in `/context/modules/`
4. Add at least one ADR for a cross-cutting decision (optional but helpful)
5. Add prompt macros in `/prompts/` for repeatable agent workflows

---

