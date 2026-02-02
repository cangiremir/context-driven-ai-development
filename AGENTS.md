# AGENTS.md — Global Rules for Humans and AI Agents

This file defines **global constraints and expectations** for all work performed in this repository by humans or AI agents.

If there is a conflict between code and context, **context wins** until explicitly updated.

---

## Core Principles

- Humans own intent, correctness, and accountability.
- AI agents are collaborators, not authorities.
- Context is normative; code is an executable artifact.
- Decisions must be durable and reviewable.

---

## Non-Negotiable Rules

### 1. Human in the Loop

- No AI-generated code is merged without human review.
- Architectural, security, and data-model changes require explicit approval.

### 2. Context Discipline

- Any durable decision MUST be recorded in:
  - a module context file, or
  - an ADR (for cross-cutting concerns).
- Context updates are reviewed like code changes.

### 3. Prefer Invariants Over Implementation

- Context defines **what must be true**, not **how it is implemented**.
- Avoid copying code snippets into context unless illustrative.

### 4. Security First

- Default to least privilege.
- Never store secrets, credentials, or sensitive data in code or context.
- Follow security constraints defined in module contexts.

### 5. Tests Are Mandatory

- New behavior requires tests.
- Bug fixes require regression tests.

---

## Definition of Done

A change is “done” only if:

- Code is implemented
- Tests pass
- Relevant context files are updated
- Changelog entries are added where applicable
