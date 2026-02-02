# Orders Module Context

---

## Purpose

Handle order lifecycle from creation through completion or cancellation.

---

## Public API / Contracts

- Create order
- Retrieve order
- Update order status

---

## Core Invariants

- An order must belong to exactly one user or guest session.
- Order status transitions are strictly controlled.
- Orders are immutable after completion.

---

## Order State Machine

- Pending
- Confirmed
- Paid
- Shipped
- Completed
- Cancelled

Invalid transitions must be rejected.

---

## Failure Modes

- Payment failure → order remains Pending
- Inventory failure → order creation fails atomically

---

## Test Expectations

- Valid and invalid state transitions
- Guest vs authenticated orders

---

## Changelog

### 2026-02-02

- Defined initial order lifecycle and invariants.
