# System Architecture Context

This document describes the **high-level architecture and boundaries** of the system.

---

## Purpose

- Define system boundaries and responsibilities
- Clarify module ownership
- Prevent architectural drift

---

## Architecture Overview

- Modular, domain-oriented design
- Clear separation of concerns
- Modules communicate via explicit contracts (APIs/events)

---

## Core Modules

- Product
- Orders / Checkout
- Payments
- User Authentication & Identity

Each module has its own context file under `/context/modules/`.

---

## Cross-Cutting Concerns

- Authentication and authorization
- Logging and observability
- Error handling and retries
- Security and compliance

Cross-cutting decisions are documented as ADRs.

---

## Architectural Invariants

- Modules do not directly access each other’s data stores.
- All external integrations are isolated behind adapters.
- Public APIs are versioned and documented.
