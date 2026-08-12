# NEXUS — Learning: Phase 1 Document Foundation

## What We Learned

1. A shared Document Foundation should provide common concepts without forcing every business document into the same lifecycle.
2. `status` is a shared concept, while status values and transitions are Document-specific.
3. Technical identity, operational scope, issuance metadata, and cancellation metadata are different concerns and should not be conflated.
4. Document References are business relationships, not merely foreign keys: they require a relationship type and immutable traceability.
5. User activity and Business History are different concepts. NEXUS uses Spatie Activity Log for user activity and keeps business history specific to the relevant Domain.
6. Attachments are infrastructure-backed through Spatie Media Library; business rules determine cardinality and mandatory/optional/conditional requirements.
7. Financial Documents need persisted totals, but financial relationships and payment behavior remain Document-specific.
8. Payment Entries are first-class parts of Financial Documents with independent technical identities, while their lifecycle remains controlled by the parent Document.
9. Product master data should be referenced rather than duplicated generically on every Document Line; logical deletion preserves historical Product relationships.
10. Explicit persisted flags such as `is_editable`, `is_removable`, and `is_hidden` belong to the shared model, while their mutation rules remain Document/Entity-specific.

## Core Principle

> **Foundations define common vocabulary and invariants; Documents define their own business behavior.**

## Reused Knowledge

This Foundation deliberately reuses the decisions already discovered in Phase 0.2 instead of rediscovering Branch, Warehouse, Product, Inventory, Permission, Return, Transfer, and Stock Adjustment behavior.
