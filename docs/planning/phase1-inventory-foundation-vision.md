# NEXUS — Vision

## Purpose

NEXUS is a business management system for a single company operating through branches, warehouses, cash registers/POS, customers, suppliers, inventory, sales, purchases, returns, transfers, wallets, and related financial operations.

The system is being designed domain-first: business rules are discovered and explicitly documented before implementation.

## Core Design Principle

NEXUS separates:

- business transactions/documents;
- inventory effects;
- current inventory state;
- financial/accounting concerns.

For inventory, the current quantity is represented by `Current Stock`.

## Inventory Foundation Principle

`Current Stock` is the Source of Truth for the current inventory quantity.

There is exactly one `Current Stock` record for each:

`Product + Warehouse`

Historical inventory effects are represented by immutable `Stock Movement` records.

## Current Phase

Phase 1 — Inventory Foundation / Domain Boundaries.

The current focus is defining the boundary and relationship between:

`Inventory Document → Stock Movement → Current Stock`

No previously settled business rule is reopened by this document.
