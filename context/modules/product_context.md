# Product Module Context

---

## Purpose

Manage the product catalog, including product data, availability, and retrieval.

---

## Non-Goals

- Order processing
- Pricing rules beyond base price display
- User personalization

---

## Public API / Contracts

- Retrieve product by ID
- List/search products with filters

---

## Core Invariants

- Product IDs are immutable.
- Out-of-stock products must not appear in purchasable listings.
- Product data is read-only outside this module.

---

## Data Model

- productId (string, UUID)
- name (string)
- description (string)
- price (decimal)
- availabilityStatus (enum)

---

## Failure Modes

- Missing product → return explicit “not found”
- Downstream dependency failure → fail fast with clear error

---

## Test Expectations

- Product retrieval
- Search/filter correctness
- Availability edge cases

---

## Changelog

### 2026-02-02

- Initial product module context created.
