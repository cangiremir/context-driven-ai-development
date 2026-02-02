# ADR-0001: Context as Constitution

## Status

Accepted

## Context

AI agents require durable, explicit memory to operate safely and effectively across sessions.

## Decision

Source context documents are treated as the **normative source of truth** for the system.

## Consequences

- Context changes are reviewed like code.
- Durable decisions must be recorded.
- Prompt history is distilled into context.

## Rationale

This reduces ambiguity, improves onboarding, and enables AI agents to work reliably.

## Date

2026-02-02
