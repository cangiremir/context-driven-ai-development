# User Authentication Context

---

## Purpose

Manage user identity, authentication, and authorization.

---

## Public API / Contracts

- User registration
- Login (password and OAuth)
- Token issuance and refresh

---

## Core Invariants

- Passwords are never stored in plaintext.
- Tokens have explicit expiration.
- Authorization checks are enforced at every boundary.

---

## Security Constraints

- Account lock after repeated failed attempts
- JWT expiration ≤ 15 minutes
- Refresh tokens are revocable

---

## Data Model

- userId (UUID)
- email
- hashedPassword
- roles
- wishlistItems (array of product IDs)

---

## Test Expectations

- Login success/failure
- Token expiration
- Authorization enforcement

---

## Changelog

### 2026-02-02

- Added wishlistItems field to user profile.
